
![[network1.png]]


>Protocol
   A protocol defines the format and the order of messages exchanged between two or more communicating entities, as well as the actions taken on the transmission and/or receipt of a message or other event.


Computer Networks follow a layered architecture. Each protocol belongs to one of the layers. Each layer provides its service by (1) performing certain actions within that layer and by (2) using the services of the layer directly below it.

| Layer       | Entity    | Example                     | Description                                                                                                                                                                                                                                                                                                                                        |
| ----------- | --------- | --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Application | Message   | HTTP, <br>FTP, <br>SMTP     | Here the network applications and their application-layer protocols reside.                                                                                                                                                                                                                                                                        |
| Transport   | Segment   | TCP, <br>UDP                | Transports application-layer messages between application endpoints.                                                                                                                                                                                                                                                                               |
| Network     | Datagrams | IP                          | Responsible for moves datagrams from one host to another. Transport Layer passes a transport-layer segment and a destination address to the network layer.                                                                                                                                                                                         |
| Link        | Frames    | Ethernet, WiFi              | Network layer routes a datagram through a series of routers between the source and destination. To move a packet from one node (host or router) to the next node in the route, the network layer relies on the  link layer. Network layer passes the datagram down to the link layer, which delivers the datagram to the next node along the route |
| Physical    | Bits      | Twisted Pair, Optical Fiber | Move the individual bits within the frame from one node to the next. Examples are not really protocols but mediums for which protocols are built.                                                                                                                                                                                                  |

### Application Layer

There are two types of application architecture w.r.t. networking. Client-Server and Peer-to-peer
#### Client Server Architecture
![[client-server 1.png]]

In a client-server architecture, there is an always-on host, called the server, which services requests from many other hosts, called clients. Another characteristic of the client-server architecture is that the server has a fixed, well-known address, called an IP address. 
Often in a client-server application, a single-server host is incapable of keeping up with all the requests from clients. For this reason, a data center, housing a large number of hosts, is often used to create a powerful virtual server.
Examples : Web, FTP, Telnet

#### P2P Architecture

![[peer-to-peer.png]]
In a P2P architecture, there is minimal (or no) reliance on dedicated servers in data centres.  Instead the application exploits direct communication between pairs of intermittently connected hosts, called peers. The peers are not owned by the service provider, but are instead desktops and laptops controlled by users. Example : bit torrent

#### Communication

Processes on two different end systems communicate with each other by exchanging messages across the computer network. A process sends messages into, and receives messages from, the network through a software interface called a socket. A socket is the interface between the application layer and the transport layer within a host. It is also referred to as the Application Programming Interface (API). 

![[application-layer.png]]
To identify the receiving process, two pieces of information need to be specified: 
1. the address of the host (IP Address)
2. an identifier that specifies the receiving process in the destination host (Port)

#### Studying Application Layer protocols

##### HTTP
The HyperText Transfer Protocol (HTTP), the Web’s application-layer protocol, defines the structure of messages and how the client and server exchange the messages. HTTP communication is ***stateless***. The default mode of HTTP uses ***persistent connections*** (introduced in Http 1.1) which means the server leaves the TCP connection open after sending a response. Subsequent requests and responses between the same client and server can be sent over the same connection.

Typical HTTP request message :

```
GET /somedir/page.html HTTP/1.1
Host: www.someschool.edu
Connection: close
User-agent: Mozilla/5.0
Accept-language: fr
```

The first line of an HTTP request message is called the request line; the subsequent lines are called the header lines. The request line has three fields: the method field, the URL field, and the HTTP version field. 

Typical HTTP response message : 

```
HTTP/1.1 200 OK
Connection: close
Date: Tue, 18 Aug 2015 15:44:04 GMT
Server: Apache/2.2.3 (CentOS)
Last-Modified: Tue, 18 Aug 2015 15:11:03 GMT
Content-Length: 6821
Content-Type: text/html

(data data data data data ...)
```

The status line has three fields: the protocol version field, a status code, and a corresponding status message.

When a server receives a request with the ***HEAD*** method, it responds with an HTTP message but it leaves out the requested object. Used fro debugging.

***Cookies*** can be used to create a user session layer on top of stateless HTTP. When responding to a client request, the server creates a unique identification number and creates an entry in its back- end database that is indexed by the identification number. 

Header added in response : 
```
Set-cookie: 1678
```

The client upon receiving this response then appends a line to the special cookie file that it manages. This line includes the hostname of the server and the identification number in the Set-cookie: header. This is then added to subsequent requests.

Header added to subsequent requests : 
```
Cookie: 1678
```

A ***Web cache*** —also called a proxy server—is a network entity that satisfies HTTP requests on the behalf of an origin Web server. The Web cache has its own disk storage and keeps copies of recently requested objects in this storage. A CDN company installs many geographically distributed caches throughout the Internet, thereby localising much of the traffic. There are shared CDNs (such as Akamai and Limelight) and dedicated CDNs (such as Google and Netflix).

An HTTP request message is a so-called ***conditional GET*** message if 
1. the request message uses the GET method and 
2. the request message includes an If-Modified-Since: header line.

```
GET /fruit/kiwi.gif HTTP/1.1
Host: www.exotiquecuisine.com
If-modified-since: Wed, 9 Sep 2015 09:23:24
```

Objects in web cache might be stale. So it does a up-to-date check from time to time  by issuing a conditional GET. If object is not modified the response does not contain the requested object and has a status code of 304.

```
HTTP/1.1 304 Not Modified
Date: Sat, 10 Oct 2015 15:39:29
Server: Apache/1.3.0 (Unix)

(empty entity body)
```


