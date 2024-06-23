

## Introduction

When a system needs to be horizontally scaled(meaning you need to add more servers or nodes). To route the traffic equally to all the servers. Consistent hashing is a commonly used techniqu to achieve this goal. But first, let us take an in-depth look at the problem


### Rehashing problem

If you have n cache servers a common way to balance the load is to use the following hash method: 

$$
serverIndex = hash(key) \mod N
$$

Where N is the number of cache servers. 

Let us use an example to illustrate how it works. As shown in the table below. we have 4 servers and 8 string keys with their hashes. 



| key  | hash     | hash % 4 |
| ---- | -------- | -------- |
| key0 | 18358617 | 1        |
| key1 | 2614384  | 0        |
| key2 | 18131146 | 2        |
| key3 | 35863496 | 0        |

To fetch the server where a key is stored, we perform the modular operation 

$$
f(key(n)) \mod 4 = server
$$



This works well when the size of the server is fixed and not varying. For instance if one of the  server (server 1) goes down we have 3 servers left. In this case we would have to re route / change the keys and the values in the server as the modular functions rearranges the hashes with their keys in different servers. 

Once the server goes down, remaining servers try to get the data from the server that is down. ([[Race Condition]]) is something to keep in mind. 

In this case most keys are rearranged not just the ones in server one, since the modular operation changes the value in the servers. So consistent


### Consistent hashing

Consistent hashing is a special kind of hashing such when a hash table is re-sized and consistent hashing is used only k/n keys need to be remapped on average, where k is the number of keys and n is the number of slots. IN contrast, in most traditional hash tables, a change in the number of array slots causes nearly all keys to be remapped. 



### Hash space and Hash ring

Now we understand the definition of consistent hashing, let us find out how it works. Assume SHA-1 is used as the hash function f, and the ouptut range of the hash function is: x0, x1, x2, x3 ..., xn. In cryptography, SHA-1's hash space goes from to 0 to 2^160-1 and all the other hash values fall in the middle of 0 to 2^160-1. By connecting both ends of a hash space(which is a linear space value in this case). We get a circle of x0 and xn beside each other in a circle. 


### Hash Servers
Unlike the same hash function f, we map servers based on server IP or name onto the ring. Figure below shows that 4 servers are mapped to the hash ring 


![[Screenshot 2024-06-22 at 21.08.44.png]]


### Hash keys
One thing worth mentioning is that hash function used here is different from the one in "The rehashing problem" and there is no modular operation. As shown in the figure below cache keys (k0,k1, k2, and k3) are hashed on to the hash ring

![[Screenshot 2024-06-22 at 21.10.20.png]]


### Add a server 

Using the logic describe above, adding a new server will only require redistribution of a fraction of keys.

IN the figure after a new server 4 is added, only k0 needs to redistributed. k1,k2, and k3 remain on the same servers. Let us take a close look at the logic. Before the server 4 is added, key0 is stored on server 0. Now, key0 will be stored on server 4 because server 4 is the first server it encounters by going clockwise from key-'s position on the ring. The other keys are not redistributed based on consistent hashing algorithm. 

### Two possible problems with Consistent hashing

1. The space between two servers. i.e., considering that a server (s1) is removed from the hash space circle. The distance between the servers s0 and s2 is higher than the space between s2 and s3.
2. There is no guarantee of uniformity for distribution of keys for the server. 


This problem is solved by usage of virtual nodes. 


