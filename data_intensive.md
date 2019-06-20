# Designing Data-Intensive Applications: The Big Ideas Behind Reliable, Scalable, and Maintainable Systems

Three concerns that are important in most software systems :
* *Reliability* - The system should continue to work correctly even at the face of adversity (HW or SW faults or human error)
* *Scalability* - As the system grows (data, traffic, complexity), there should be a reasonable ways of dealing with the growth.
* *Maintainability* - Over the time, many different people will work on the system, and they should all be able to work on it productively

Mean is not z very good metric if you want to know "typical" response time, because it doesn't tell you how many users usually experienced that delay.  
**Usually it is better to use percentiles**  Median is also known 50th percentile.  
In order to figure out how bad your outliers are, you can look at higher percentiles: the 95th, 99th and 99.9th percentiles are common.
**They are the response time thresholds at which 95%, 99% and 99.9% of requests are faster than particular threshold.**
For example, if the 95th percentile response time is 1.5 seconds, that means 95 out 100 requests take less than 1.5 seconds and 5 out of 100 requests take 1.5 seconds or more.  

For example, Amazon describes response time 99.9th percentile, even though it only affects 1 in 1000 people.  
This is because the customers with the slowest requests are often those who have the most data on their accounts because they have made many purchases - **they are the most valuable customers**.

It only takes small number of requests to to hold up processing of subsequent requests - an effect sometimes known as *head-of line blocking* 

If you want to add response time percentiles to the monitoring dashboard for your services, you need to efficiently calculate them on an ongoing basis. 
For example, you may want to keep rolling window of response times of requests in the last 10 minutes.  
Every minute you calculate the median and various percentiles over the values in that window and plot those metrics on graph.

Ways how to do it effectively :
* forward decay
* t-digest
* HdrHistogram

An architecture that is appropriate for one level of load is unlikely to cope with 10 times that load.  
If you are working on a fast-growing service, it is therefore likely that you need to rethink your architecture every order of magnitude load increase - or perhaps even more often than that.

Three design principles for software systems:
* *Operability* Make it easy for operations team to keep the systems running smoothly
* *Simplicity* Make it easy for new engineers to understand the system by removing much complexity as possible from the system
* *Evolvability* Make it easy for engineers to make changes to the system in the future

   