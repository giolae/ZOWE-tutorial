 ZOWE CLI e ZOWE VSCode plugin installation
====================
questa breve guida indica i passi necessari per consentire di utilizzare ZOWE su una postazione W11 (senza l'uso dei privilegi di Amministratore) .
al termine saremo in grado di utilizzare ZOWE da:

 - CLI (command Line Interface)
 -  VSCode

## prerequisiti
per fare questo sono necessari i seguenti prerequisiti:
 
 - 500MB di spazio disco
 
al termine  saranno installati i seguenti prodotti:
 - [Node.js](https://nodejs.org/en) Node.js® is a free, open-source,   cross-platform JavaScript runtime environment that lets developers
   create servers, web apps, command line tools and scripts.
 
 -  [npm](https://www.npmjs.com/)  is a [package manager](https://en.wikipedia.org/wiki/Package_manager "Package manager") for the [JavaScript](https://en.wikipedia.org/wiki/JavaScript "JavaScript") programming language maintained by npm
 
   - [Visual Studio Code](https://code.visualstudio.com/)  The open source IDE  developed by Microsoft
   -  [Zowe Explorer for VS Code](https://github.com/zowe/community#zowe-explorer "https://github.com/zowe/community#zowe-explorer") provides access to mainframe resources in Visual Studio Code. Zowe Explorer provides a modern, familiar, user-friendly interface for mainframe developers and system programmers 
## Quick-Start Steps:

1. verificare che Node.js e npm.js siano già installati:

2.  Install  [Node.js and npm](https://www.npmjs.com/get-npm)  on your laptop if you don’t already have it. This is a pre-requisite for Zowe CLI, similar to how Java or C++ runtimes are pre-requisites for many other tools. If you can’t download Node.js and npm from npmjs.com, you may need to check your company’s techstack of approved software to acquire it from there.
  
![arrow](https://openliberty.io/img/arrow_white.svg)

# Documenting RESTful APIs

![duration](https://openliberty.io/img/guide_duration_clock_icon_large.svg)  20 minutes

Explore how to document and filter RESTful APIs from code or static files by using MicroProfile OpenAPI.

## What you’ll learn

You will learn how to document and filter RESTful APIs from annotations, POJOs, and static OpenAPI files by using MicroProfile OpenAPI.

The OpenAPI specification, previously known as the Swagger specification, defines a standard interface for documenting and exposing RESTful APIs. This specification allows both humans and computers to understand or process the functionalities of services without requiring direct access to underlying source code or documentation. The MicroProfile OpenAPI specification provides a set of Java interfaces and programming models that allow Java developers to natively produce OpenAPI v3 documents from their JAX-RS applications.

You will document the RESTful APIs of the provided  `inventory`  service, which serves two endpoints,  `inventory/systems`  and  `inventory/properties`. These two endpoints function the same way as in the other MicroProfile guides.

Before you proceed, note that the 1.0 version of the MicroProfile OpenAPI specification does not define how the  `/openapi`  endpoint may be partitioned in the event of multiple JAX-RS applications running on the same server. In other words, you must stick to one JAX-RS application per server instance as the behaviour for handling multiple applications is currently undefined.

## Getting started

The fastest way to work through this guide is to clone the  [Git repository](https://github.com/openliberty/guide-microprofile-openapi.git)  and use the projects that are provided inside:

```
git clone https://github.com/openliberty/guide-microprofile-openapi.git
cd guide-microprofile-openapi
```

The  `start`  directory contains the starting project that you will build upon.

The  `finish`  directory contains the finished project that you will build.

Before you begin, make sure you have all the necessary  prerequisites.

### Try what you’ll build

The  `finish`  directory in the root of this guide contains the finished application. Give it a try before you proceed.

To try out the application, first go to the  `finish`  directory and run the following Maven goal to build the application and deploy it to Open Liberty:

`**WINDOWS**`

`**MAC**`

`**LINUX**`

```
cd finish
mvnw.cmd liberty:run
```

After you see the following message, your Liberty instance is ready:


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIxNjcyNzMyMSwtMTc2ODg0ODQ4MiwtMz
I2NjQ2Mzk3LDE3NTg1ODk5NjIsOTQyNDI0NzExLC0xOTE4NDQ1
MjQ0LDExNTIyMjUzMTMsMzg5OTQ0NjAyLDE1NjM3MTY1NjBdfQ
==
-->