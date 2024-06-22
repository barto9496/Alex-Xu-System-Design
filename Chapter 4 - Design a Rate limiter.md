The design steps are based on : [[Chapter 3 - Designing a System]]

In n/w system, a rate limiter is used to control the rate of traffic sent by a client or a service. In the HTTp world, a rate limiter limits the no of client requests to be sent over a specific period. If the API request count exceeds the threshold defined by the rate limiter all the excess call are blocked here are a few examples.

- A user can write no more than 2 posts per second
- You can create a maximum of 10 accounts per day from the same IP address.
- You can claim rewards no more than 5 times per week from the same device
  
  
  In this chapter you are asked to design a rate limiter. Before starting the design , we first look at the benefits of using an API rate limiter
  1. **Prevent resource starvation** caused by Denial of Service(DoS) attack. Almost all APIs published by large tech companies enfoce some form of rate limiting. For ex: Twitter limits the no of tweets to 300 per 3 hours. Google docs PAIs have the following default limit: 300 per user per 60 seconds for read requests. A rate limiter prevents DoS attacks either intentional or unintentional, by blocking the excess calls. 
  2. **Reduce Costs**: Rate. limit excess requests means fewer servers and allocating more resources to high priority APIs. Rate limiting is extremely important for companies that use paid third party APIs. For exampls, you are charged on a per-call basis for the following external APIs: check credit, make a payment, retrieve health records, etc. Limiting the number of calls is essential to reduce costs. 
  3. Prevent server. from being overloaded. To reduce server load a rate limited is used to filter out excess requests cause by. bots or users' misbehavior.
- ### Step 1 - Understand the problem and establis design scope
  
  Rate limiting can be implemented using different algorithms each with its pros and cons. The interactions between an interviewer and a candidate help to clarify the type of rate limiters we are tyring to build.
  
  Candidate: What kind of rate limiter are we going to design? Is it client side rate limiter or server side rate limiter? 
  Interviewer: Great question. We focus on the server-side API rate limiter
  
  
  Candidate: Does the rate limiter throttle API requests based on what properties? Is it he user id, or any other unique identifier.
  Interviewer: The rater limiter should be flexible enough to different set of throttle rules.
  
  
  Candidate: What is the scale of the system? Is it build for a start up or a big tech company? 
  Interviewer: The rate limiter should be able to handle large amount of incoming requests. So, basically a big tech company. 
  
  Candidate: Will the product work in a distributed env? 
  Interviewer: Yes! 
  
  Candidate: Is the rate limiter a separate service or should it be implemented in the application code.
  Interviewer: It is a design scope and you can choose how to do it. **Write down your assumptions here**
  
  Candidate: Do we need to inform users who are thresholded? 
  Interviewer: Yes
- ## Step 2: Propose a high level design and get a buy in
  
  To keep things simple use a basic client and server model for communication.
- #### Where to put the rate limiter? 
  Intuitively, you can implement a rate limiter at either the client or the server side.
- Client-side implementation. Generally speaking, client is an unreliable place to enforce rate limiting because client requests can be easily forged by malicious actors. Moreover, we might not have control over the client implementation.
- Server side implementation. With server side implementation we can have a rate limiter in the server. 
- There is another way of implementing a rate limiter as a middleware layer. 

Let's say you send a request to the server which has a rate limiter and it allows 2 requests/s but you send 3 the first 2 requests are routed to the API server, and the third one returns a code of 429. 429 is a HTTP status code for too many requests. 


Cloud micro services have become widely popular and rate limiting is usually implemented within a component called API gateway. API gateway is a fully managed service that supports rate limiting, SSL termination, authentication, IP whitelisting servicing static content, etc. For now, we only need to know that the API gateway is a middleware that supports rate limiting.

While designing a rate limiter, an important question to ask ourselves is where should the rate limiter be implemented, on the server-side or in a API gateway? There is no absolute answer. It depends on your company's current tech stack, engineering resources priorities goals, etc. Here a few general guidelines: 


- Evaluate your current tech stack, such as programming language, cache service, etc. Make sure your current programming languages is efficient to implement rate limiting on the server-side
- Identify the rate limiting algorithm that fits your business needs. When you implement everything on server side you have full control of the algorithm. However, your choice might be limited if you use a third party gateway.
- If you have already used a micro service architecture and included an API gateway in the design to perform authentications, IP whitelisting, etc., you may add a rate limiter to the API gateway.

### Algorithm for rate limiting
Rate limiting can be implemented using different algorithms, and each of them has distinct pros and cons. But the most used algorithms to develop API rate limiter are
1. Token Bucket
2. Leaking bucket
3. Fixed window counter
4. Sliding window log
5. Sliding window counter


#### Token Bucket Algorithm
The token bucket algorithm is widely used for rate limiting. It is simple well understood and commonly used by internet companies. Both Amazon and Stripe use this algorithm to throttle their API requests. 

The token bucket algorithm work as follows:
- A token bucket is a container that has pre-defined capacity. Tokens are put in the bucket at preset rates periodically. Once the bucket is full, no more tokens are added. Lets the token capacity is at 4. The re filler puts 2 tokens into the bucket every  . Once the bucket is full, extra tokens will overflow.


So when a request is sent the request checks if there is a token in the bucket if one is present then the request goes through. If not then the HTTP code 429 is returned. 