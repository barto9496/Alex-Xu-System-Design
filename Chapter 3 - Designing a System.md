## 4 Step Process for effective system design interview 


Every system design is different. A great system design is open minded and there is no one size fits all solution. However there are steps and common ground to cover in every system design interview.

### Step 1: Understand the problem and establish design scope 

Never answer or design a question without knowing all the details. Ex:
**Teacher**: Why did the tiger roar? 
**Jimmy**: Because the tiger was hungry!
**Teacher**: Correct Jimmy! 

Never be jimmy know the full scope of the question even though you are answering correctly to the interviewer. There are no extram / bonus points for answering the question early. Hence, **'NEVER BE JIMMY'** when designing a system. 

When you ask question the interviewer either answers the question or allows you to assume the details for the questions. But any assumptions you make, not them down on the paper or the whiteboard. 

Some standard question to ask when designing the systems: 

1. How many users are going to be using the system?
2. What all features are we going to build? 
3. What is the current tech stack that can be utilized to simplify the design.
4. How fast does the company plan to scale up? In 3 months, 6months, and a year? 

If you're asked to design a news feed system. Some standard question to be asked are: 

1. How many users are going to be using the system? -> **10 million Daily users (DAU) **
2.  Is this a mobile app / web app or both? -> **Both**
3. What features are we building? **News articles are presented based on the users' friends interaction**
4. How are we sorting the news articles? 
	1. Is it based on chronological order? 
	2. Is it possible for the user to update the order? 
	3. Are we enabling reordering on our side based on the users' friends news articles? 
5. Does it containing any media in it? **Yes the articles have images, videos and other media files**


### Step 2: Propose an initial design and get a buy in
In this step we propose a design with the Interviewer and get a
- Come up with an initial blueprint for the design. Ask for feedback. Treat your interviewer as a teammate and work together. Many good interviewers love to talk and get involved.
- Draw box diagrams with key components on the whiteboard or paper. This might include clients (mobile/web), APIs, web servers, data stores, cache, CDN, message queue, etc.
- Do back-of-the-envelope calculations to evaluate if your blueprint fits the scale constraints. Think out loud. Communicate with your interviewer if back-of-the-envelope is necessary before diving into it.

If possible go through a few concrete cases, If will help you design some good use case for the design and you might be able to come up on a certain edge cases for the system.

Always communicate with your interviewer
Let us design the news feed system now to demonstrate the high level design. Here we're not actually required to 