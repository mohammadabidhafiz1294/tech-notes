**Port Triggering** sets up the router so that computers can access public services outside the network or on the Internet, such as web servers, File Transfer Protocol (FTP) servers, email servers, game servers or other Internet applications.  
  
 ** #Port-forwarding** : sets up public services on your network such as web servers, FTP servers, e-mail servers, or other specialized Internet applications.  When users send this type of request to your network via the Internet, the router will forward these requests to the appropriate computer.  When clients cannot access an FTP Server that’s connected to a Linksys router, the ports for FTP have to be forwarded to the server for the request to be recognized.  This is configured on a router if you are using a server computer or a game server.  
  
There are **two** types of **Port Forwarding**:

**1. Single Port Forwarding**  
  
This type allows you to set up public services one by one on your network such as web servers, FTP servers, email servers, or other specialized Internet applications.  Before using forwarding, you should assign static IP addresses to the designated computers.

**NOTE:**  Specialized Internet applications are any applications that use Internet access to perform functions such as videoconferencing or online gaming.  Some Internet applications may not require any forwarding.

**2. Port Range Forwarding**  
  
This type allows you to set up public services in a group which means a range of ports, for example from 20 ~ 25.  Certain applications may require opening specific ports so they can function correctly.  Examples of these applications include servers and some online games.  When a request for a certain port comes in from the Internet, the router will route the data to the computer you specify.

**NOTE:**  Due to security concerns, you may want to limit Port Forwarding to only those ports you are using, and remember to uncheck the **Enable** checkbox after you are finished.

To understand the difference between the two (2), refer to the scenarios below.

**Scenario 1:**  
  
The game player request to access a game server.  The request will be sent from the computer to the router first and then directed straight to the Internet.  When this happens, the request, which is coming from the Internet, will be forwarded to the game server by the router.  This is called **Port Forwarding**.

**Scenario 2:**  
  
Another instance when you can use **Port Triggering** is when you can’t download files while connected to a Linksys router.  This process of downloading files is called an **FTP request**.  An FTP request uses **Port 20** and **Port 21**, which by default, are closed in a Linksys router.  Since the computer is connected to a Linksys router, both ports 20 and 21 have to be triggered by enabling **Port Triggering**.  