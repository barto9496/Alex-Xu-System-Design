## Introduction

Sometimes you're asked to estimate the system capacity or performance requirements using back of the envelope solution. To estimate this you will need a combination of thought experiments and common performance numbers to get a good feel for which design will meet your requirements.

### Back of the envelope solution
Back of the envelop solution can be estimated using three properties
1. Power of 2
2. Latency number every programmer should know 
3. Availability numbers


### Power of 2
When designing a system the capacity of the system can be enormous to calculate this approximation you will need understand the power of 2. So, an ascii character such as 'A' takes a byte of space which is 8 bits ('00000000'). 


### Latency Numbers
Latency numbers define the time for an action performed by the system under consideration 

Some common time frames are: 
1. 1ms - 10<sup>-3</sup>
2. 1µs - 10<sup>-6</sup>
3. 1ns - 10<sup>-9</sup>

Some considerations: 
- Memory is fast but the disk is slow.
- Avoid disk seeks if possible.
- Simple compression algorithms are fast.
- Compress data before sending it over the internet if possible.
- Data centers are usually in different regions, and it takes time to send 	data between them.


## Availability Numbers:

High availability is the availability of the system to be continously operation for longer period of time. High availability is measured as %. If the system is available for 100% of the time, it has 0 down time. Most systems rely between 99% - 100%

## Service Level Agreement
A service level agreent is an agreement between you and the customer of the time when your system will be online. Big tech companies have their SLA's around 99.9% 

#### Calculation of 9s:

1. 99% - This means the system is up for 99% of the time which mean 1% of 365 days it is not available which translates to 3.65days/year
2. 99.9%(3 nines): This system uptime is 99.9% of the time. Down time can be calculated using the formula:
$$ Downtime  =1 - (\frac{99.9}{100}) \times 360 \times 24 \times 60 \times 60 = 31536s/yr $$

We can similarly calculate other values for each time length of weeks, days and months per year.

#### Twitter System capacity estimation(Query Per Second(QPS) and storage requirements)

Assumptions:
-  300 million monthly active users.
-  50% of users use Twitter daily.
-  Users post 2 tweets per day on average. 
-  10% of tweets contain media.
-  Data is stored for 5 years.


Calculations:

$$ DAU = 300 \times (\frac{50}{100}) = 150$$
So twitter has 150 million users daily
