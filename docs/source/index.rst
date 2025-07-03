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

1. verificare che Node.js e npm.js non siano già installati:
	1.1 aprire il prompt powershell
	``` 
	> 
	C:\Users\u0e1591>node --version
	"MODL" non è riconosciuto come comando interno o esterno,
 un programma eseguibile o un file batch.




2.  Install  [Node.js and npm](https://www.npmjs.com/get-npm)  on your laptop if you don’t already have it. This is a pre-requisite for Zowe CLI, similar to how Java or C++ runtimes are pre-requisites for many other tools. If you can’t download Node.js and npm from npmjs.com, you may need to check your company’s techstack of approved software to acquire it from there.
  

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
eyJoaXN0b3J5IjpbMTY5NDc4MTMxOCwtMTAzODIxMjg0OSwyND
c3NzY0MTcsLTIwNDA2MjkyMTUsLTE3Njg4NDg0ODIsLTMyNjY0
NjM5NywxNzU4NTg5OTYyLDk0MjQyNDcxMSwtMTkxODQ0NTI0NC
wxMTUyMjI1MzEzLDM4OTk0NDYwMiwxNTYzNzE2NTYwXX0=
-->