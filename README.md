# HTTP Basic Auth. Challenge

LetsDefend challenge requiring the use of WireShark to analyse a pcap file to gather information.

# Analysis

The first step is to connect to the LetsDefend lab environment and open the pcap file in WireShark.

![image](/assets/images/wireshark01.png)

### **How many HTTP GET requests are in pcap?**

![image](/assets/images/wireshark02.png)

By filtering to ‘http’, the GET requests can easily be counted in this case to a total of 5.

### Server Information

There are multiple questions on the server information which can all be seen together by opening a HTTP frame where the source is the server IP.

**What is the server operating system?**

![image](/assets/images/wireshark03.png)

**Server OS:** `FreeBSD`

**What is the name and version of the web server software?**

![image](/assets/images/wireshark04.png)

**Version:** `Apache/2.2.15`

**What is the version of OpenSSL running on the server?**

![image](/assets/images/wireshark05.png)

**OpenSSL Version:** `OpenSSL/0.9.8n`

### **What is the client's user-agent information?**

The client user-agent information can be found by opening a HTTP packet with the client as the source IP.

![image](/assets/images/wireshark06.png)

**User-Agent:** `Lynx/2.8.7rel.1 libwww-FM/2.14 SSL-MM/1.4.1 OpenSSL/0.9.8n`

### Credentials used for Basic Authentication

Finally the challenge requires the username and password used to gain access.

![image](/assets/images/wireshark07.png)

When looking at the HTTP frames, multiple GET requests with response ‘401 Authorization Required’ can be observed. Frame 57 has a HTTP GET request which had a server response of ‘200’ which indicates the user likely gained access. Expanding the frame shows the credentials used:

**Username:** `webadmin`

**Password:** `W3b4Dm1n`

## Conclusion

The analysis indicates that the user gained access, in a professional environment the client IP would be analysed and the case would be escalated to T2.
