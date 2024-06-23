Race condition is a process when extracting data and updating them from two different process causes the data to be mismanaged. As you can see in the below image. 


![[Screenshot 2024-06-22 at 14.19.38.png]]


Say for request 1 the counter reads the value at time = minute 1 past an hour and checks and update the counter to 4 after almost 45 seconds

Also request 2 the counter reads the value at time = minute 1 and second 30 past the hour.
since the counter hasn't update to 5 the counter still picks up 4. The simultaneous extraction and updation of the process without the other being completed causes race condition. 
