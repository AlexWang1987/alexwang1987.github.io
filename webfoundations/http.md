# Overview of HTTP(Hypertext Transfer Protocol)

HTTP is crutial and foundamental for every developer devloping network program and relating web development.

## What is Webserver
Web server is a piece of software which speaks HTTP protocol, and one of most important rules is to store tons of resources.
## What resources a web server provide with
Theoretically, Web server can provide any information through HTTP protocol, but here are some common types of static resources.`html`,`jpeg`,`png`,`javascript`,`css`,`video`,`audios`,`pdf`,ect. what about dynamic resources?, like the data retrieved from databases or other places. Web server also hold programs that execute on demand. They are just  running in background, without having to delivering to clients. 

## MediaTypes

Because many resources that are stored in the web server, It's necessary to identify what types they are when they are being transferred.
like `images/jepg`,`images/png`,`text/html`,`text/plain`,`video/mp4`,etc.

## URIs(URLs,URNs).

URI(Uniform Resource Identifier) which is unique to identify a resource in the web server. such as, `http://www.alexwang.com/logo.png`,This is a typical URL(Uniform Resource Locator), which clearly describe the scheme(`http://)`,server address(`www.alexwang.com`),local resource path(`/logo.png`). Almost every URI is a URL. **URN**(Uniform Resource Name) is still not widely adopted yet.

## Transactions
Client(**Http Request**)<-> Server(**Http Response**) they are all speaks HTTP language, and the messages they are speaking are formatted and encapsulated into **Http message**.

## HTTP Methods (commands)

Here are the most commonly used **commands(add,delete,update,select,get-description)**

| Method | Description |
| -- | -- |
| GET | give me the named resource |
| PUT | save my data into the named resource |
| DELETE | delete the named resource |
| POST | save my resource  |
| HEAD | give me description of the named resource  |

## Status Codes(HTTP Response)

Every **HTTP Response** must come back with a status code which is a tree-digit numeric code to indicate if the **HTTP Request** succeeded.

| HTTP SC | Description |
| -- | -- |
| 200 | named resource was found and its data was retrieved back as well|
| 302 | Redirect, go to this URI, which has the same resource you desired |
| 404 | can not found the named resourced |

## HTTP Message






