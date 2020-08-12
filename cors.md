---
title: Access control allow origin
author: Aquif Zubair
date: 2020-08-14
slug: access-control-allow-origin
excerpt: In this article, we will get to know what is access control allow origin.

---

# Access control allow origin

For understanding the concept of **access control allow origin**, we will have to learn that from where it is coming, where are we using this. For that, We will have to learn **Cross-Origin Resource Sharing(CORS)**.

## What is CORS?

CORS stands for Cross-Origin Resource Sharing, It is a mechanism that browser uses to handle cases when an application running at a particular origin, want to access resources from another application running at another origin. You may wonder what exactly the **origin** is?

**Origin is defined by the protocol, domain, and port of the URL used to access it. Two objects are said to be of the same origin when the protocol, host, and port all match.**

Let's understand it by an example.

```
http://google.com/index.html  
http://google.com/index.html
```


Same origins because the same protocol(HTTP) and host(google.com)

```
http://google.com:80 
http://google.com
```



Same origins because same protocols(HTTP), host(google.com) and port(80). You may notice that in the second URL there is no port number mentioned, If there is no port number mentioned then, HTTP serves it on port 80 by default.
```
https://google.com
http://google.com
```
Different origin because the protocol and ports are different. because default port no of HTTP is 80 and for HTTPS is 443.
```
https://google.com:443
https://facebook.com:443
```
Different origins because host names are different.
```
http://google.com:80
http://google.com:1234
```
Different origins because ports are different.

But Why browser need this mechanism? The reason is that most browsers implement a security policy known as 'Same Origin Policy'. Due to this policy we can't access the resources from another origin. This is the main reason browser need CORS to get the resources from a different origin.

## How does it work?

When a client application at the origin A tries to access resources from the server application running at origin B, It can't access the resource unless some specific CORS HTTP headers are present in the request and response, and it will throw cors error in console. If the request header is the same as the response header client will fetch the resources. You may wonder which type of header are we discussing here. I am explaining it below.

For some types of access requests that can possibly cause side effects to server e.g a DELETE request. In this case, a **preflight request** would be automatically sent by the browser to inform the server about the actual request. After that server will approve or reject the request by analyzing the request headers.

## CORS HTTP Headers.

It can be grouped into two request headers i.e headers in the request from the client and the and Response headers i.e headers in the response from the server.

### Request Headers

There are three types of request headers.

1. **Origin**: It let the server know the Origin of the client application.

2. **Access-Control-Request-Method**: This header lets the server know, what HTTP method the client intends to send. It is set by the browser during preflight request.

3. **Access-Control-Request-Headers**: This method lets the server know what HTTP headers the client intends to send. This is also set by the browser during preflight requests.

### Response Headers

1. **Acces-Control-Allow-Origin**: This specifies the origin that the server wants to allow to access the resource. Confusing? let me explain it if we will put the value of this header like this(`'access-control-allow-origin': '*'`).  **\*** is defining here that all origin can access the resource of this server. If we want to give access to this server to only a particular client we will put the URL of that request client.
   e.g { `'allow-access-control-origin' : 'http://google.com'`}
   In the previous example server wants to give access to his resources only to `google.com`.
2. **Access-Control-Allow-Headers**: This specifies the set of headers that can be in client requests. If this doesn't match then the browser will throw a cors error.
3. **Access-Control-Allow-Methods**: This specifies the set of methods that can be used for client requests. If the server wants to give access to different methods, it may be specified as comma-separated.
   e.g { access-control-allow-methods': GET, POST, DELETE }

There are whole other types of response headers, You can see on this [MDN link]('https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS):

## How to handle CORS?

It is very simple to handle cors. This is something that has to be done at the server application.

If you want to specify that which origin should access the resource of your server, you can use access-contro-allow origin, If you want to specify which HTTP method can any client use from your server you can use access-control-allow-methods. Like this, you can use different types of response header properties according to your use.

## Summary

I tried my best to convey my knowledge to you. I hope I was able to provide you at least a basic understanding of cors and how does it work? If You want to go deep more into it, follow the
[MDN Documentation]('https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS). This is a very good place to start.
