# VPS
Virtual Private Server hosting, aka VPS hosting, is a website hosting environment that allows for resources such as RAM and CPU to be dedicated to your account. This is achieved by virtualizing a dedicated server and splitting the resources amongst the users on that server.

Users are guranteed the resources on their VPS web hosting account. This means that your account will always be allocated the set amount of RAM, CPU and Disk Space you've chosen regardless of what other users on the server are doing. This allows for greater stability and performance of your website. You also do not share the Operating System with any other users, providing better security for your website files. VPSes shre the underlying physical hardware with other VPSes, the performance may be slow.

# Scalability
## What is scalability
The scalability of an application can be measured by the number of requests it can effectively support simultaneously. The point at which an application no longer handle additional requests effectively is the limit of its scalability. This limit is reached when a critical hardware resource runs out, requiring different or more machines. Scaling these resources can include any combination of adjustments to CPU and pysical memory, hard dis, and/or the network bandwidth.

## Horizontal Scaling and Vertical Scaling
Horizontal scaling means scaling by adding more machines to your pool of resources. Horizontal scaling is aslo called "scaling out". Vertical scaling referes to scaling by adding more power (e.g., CPU, RAM) to an existing machine. Vertical scaling is also called "Scaling up".

One fundamental differences between the two is that horizontal scaling requires breaking a sequential piece of logic into smaller pieces so that they can be executed in parallel across multiple machines. In many aspects, vertical scaling is easier because the logical doesn't need to change. We just run the same programs on higher-spec machines. However, there are many other factors should be considered when determining the appropriate scaling approach.

![scaling](https://github.com/idanhuang/Learning_Note/blob/main/img/scaling.jpg)

|         | Horizontal Scaling           | Vertical Scaling  |
| ------------- |:--------------------| :--------------------|
| Database      | Each node only contains part of the data | Data resides on a single node and scaling is done through multi-core. i.e., spreading the load between the CPU and RAM resources of that machine |
| Downtime      | less or no downtime      |   Vertical scaling is limited to the capacity of one machine, scaling involves downtime |
| Concurrency | It involves distributing jobs across machines over the network. Several patterns associated with this model: Master/Worker*, Tuple Spaces, Blackboard, MapReduce.     |    Actor model: concurrent programming on multi-core machines is often performed via multi-threading and in-process message passing.|
| Message passing |In distributed computing, the lack of a shared address space makes data sharing more complex. It also makes the process of sharing, passing or updating data more costly since you have to pass copies of the data.|In a multi-threaded scenario, you can assume the existence of a shared address space, so data sharing and message passing can be done by passing a reference. |

References: 
- [1] https://www.section.io/blog/scaling-horizontally-vs-vertically/#:~:text=Horizontal%20scaling%20means%20scaling%20by,as%20%E2%80%9Cscaling%20up%E2%80%9D).
