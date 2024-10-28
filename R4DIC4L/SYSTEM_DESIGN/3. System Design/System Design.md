---
noteID: 42a6811d-49dc-4f2a-af3f-6c4758218345
---
#### SCALE FROM ZERO TO MILLIONS OF USERS


1. **Single Server** 
![[single-server.png]]
2. **Separate out database** 
![[single-server-data.png]]
Non-relational databases might be the right choice if:
*  Your application requires super-low latency.  
* Your data are unstructured, or you do not have any relational data.  
* You only need to serialize and deserialize data (JSON, XML, YAML, etc.). 
* You need to store a massive amount of data.

3. **Adding More servers and routing through load balancer**
![[load-balancer.png]]
A load balancer evenly distributes incoming traffic among web servers that are defined in a load-balanced set. For better security, private IPs are used for communication between servers. A private IP is an IP address reachable only between servers in the same network;

4. **Database Replication**
![[data-rep.png]]
Example of a load balancer is **NGINX** . NGINX uses a non-blocking, asynchronous event-driven model. Instead of creating a new thread or process for each request, it utilizes a small number of worker processes that handle many connections simultaneously. Once a request is received, NGINX parses the request headers and determines how to route it based on its configuration.

5. **Adding Cache Tier**

![[cache-tier.png]]

6. **Add CDN for static content**

![[cdn.png]]
7. **Adding Data Centers**

To improve availability and provide a better user experience across wider geographical areas, supporting multiple data centers is crucial. users are geoDNS-routed, also known as geo-routed, to the closest data center.

![[Screenshot 2024-09-22 at 8.06.59 PM.png]]


