
### Introduction

One possible way of thinking of this is to used the ID auto incrementer. This cannot be used because the system might be scalable and trying to pull multiple id's at the same time by multiple system can cause race condition and the DB's aren't that fast as they need to be when we're trying to generate Unique ID's for distributed systems. 

So for any good system design there are [4 steps](Chapter 3 - Designing a System) that needs to be followed. 

1. Understand the problems and establish design scope: Asking questions mentioned in [[Step 1 Generic questions]], or framing the questions more suitable to the system design at hand. Some question that can be asked when designing a Unique ID system are:
	1. What are the characteristics of the unique id? -> ID must be unique and sortable
	2. For each new transaction / record are we incrementing the value by 1? -> IDs incremented by time not necessarily only increments by 1. IDs created in the evening are larger than those created on the same day.
	3. Do IDs only contain numerical values? -> Yes
	4. What is the ID length requirement? -> 64bits.
	5. What is the scare of the system? The system should generate 10000 records / second. 
2. Propose high level 
