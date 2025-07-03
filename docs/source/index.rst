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
1.1 aprire il prompt powershell:
	```
	 C:\Users\u0e1591>node --version
	"node" non è riconosciuto come comando interno o esterno, un programma eseguibile o un file batch.
	```
	1.2 creare una cartella dove saranno ospitati i prodotti scaricati:
	```
	C:\Users\u0e1591> mkdir \portablesApps

	C:\Users\u0e1591>cd \portablesApps

	C:\portablesApps>

scompattiamo il file [node-v22.17.0-win-x64.zip](%5C%5Cscapmop1509%5CUsers%5Czowe%5Cnode-v22.17.0-win-x64.zip) che scaricato in precedenza con il cmd:
```

```yaml
{
    "$schema": "./zowe.schema.json",
    "profiles": {
        "zosmf": {
            "type": "zosmf",
            "properties": {
                "port": 443
            },
            "secure": []
        },
        "tso": {
            "type": "tso",
            "properties": {
                "account": "",
                "codePage": "1047",
                "logonProcedure": "IZUFPROC"
            },
            "secure": []
        },
        "ssh": {
            "type": "ssh",
            "properties": {
                "port": 22
            },
            "secure": []
        },
        "zftp": {
            "type": "zftp",
            "properties": {
                "port": 21,
                "secureFtp": false
            },
            "secure": []
        },
        "global_base": {
            "type": "base",
            "properties": {
                "host": "",
                "rejectUnauthorized": true
            },
            "secure": [
                "user",
                "password"
            ]
        },
        "TESTPLEX": {
            "properties": {
                "host": "zosmfsygx.mframe.sanpaoloimi.com"
            },
            "secure": [
                "user",
                "password"
            ],
            "profiles": {
                "zosmf": {
                    "type": "zosmf",
                    "properties": {
                        "account": "u0e1591",
                        "protocol": "https",
                        "rejectUnauthorized": false,
                        "port": 443
                    }
                },
                "tso": {
                    "type": "tso",
                    "properties": {
                        "account": "u0e1591",
                        "rejectUnauthorized": false,
                        "codePage": "1047",
                        "logonProcedure": "IZUFPROC"
                    },
                    "secure": []
                },
                "zftp": {
                    "type": "zftp",
                    "properties": {
                        "host": "syg0.mframe.sanpaoloimi.com",
                        "account": "u0e1591",
                        "rejectUnauthorized": false,
                        "port": 21,
                        "secureFtp": false
                    }
                },
                "ssh": {
                    "type": "ssh",
                    "properties": {
                        "port": 22
                    },
                    "secure": []
                }
            }
        },
        "SVILPLEX": {
            "properties": {
                "host": "zosmfsyax.mframe.sanpaoloimi.com"
            },
            "secure": [
                "user",
                "password"
            ],
            "profiles": {
                "zosmf": {
                    "type": "zosmf",
                    "properties": {
                        "account": "u0e1591",
                        "protocol": "https",
                        "rejectUnauthorized": false,
                        "port": 443
                    }
                },
                "zftp": {
                    "type": "zftp",
                    "properties": {
                        "host": "sya0.mframe.sanpaoloimi.com",
                        "account": "u0e1591",
                        "rejectUnauthorized": false,
                        "port": 21,
                        "secureFtp": false
                    }
                },
                "tso": {
                    "type": "tso",
                    "properties": {
                        "account": "u0e1591",
                        "codePage": "1047",
                        "rejectUnauthorized": false,
                        "logonProcedure": "IZUFPROC"
                    },
                    "secure": []
                },
                "ssh": {
                    "type": "ssh",
                    "properties": {
                        "port": 22
                    },
                    "secure": []
                }
            }
        },
        "OPERPLEX": {
            "properties": {
                "host": "zosmfsybx.mframe.sanpaoloimi.com"
            },
            "secure": [
                "user",
                "password"
            ],
            "profiles": {
                "zosmf": {
                    "type": "zosmf",
                    "properties": {
                        "account": "u0e1591",
                        "protocol": "https",
                        "rejectUnauthorized": false,
                        "port": 443
                    }
                },
                "tso": {
                    "type": "tso",
                    "properties": {
                        "account": "u0e1591",
                        "codePage": "1047",
                        "rejectUnauthorized": false,
                        "logonProcedure": "IZUFPROC"
                    },
                    "secure": []
                },
                "ssh": {
                    "type": "ssh",
                    "properties": {
                        "port": 22
                    },
                    "secure": []
                }
            }
        }
    },
    "defaults": {
        "zosmf": "TESTPLEX.zosmf",
        "tso": "tso",
        "ssh": "ssh",
        "rse": "rse",
        "zftp": "zftp",
        "base": "global_base"
    },
    "autoStore": true
}




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
eyJoaXN0b3J5IjpbLTQxODgzMDYzMCwtNDE3MTMwNzcxLDExMz
Q3NDg3MzEsMTIxNDY1MTEzOSwtOTAyMzQ5ODYsLTEwMzgyMTI4
NDksMjQ3Nzc2NDE3LC0yMDQwNjI5MjE1LC0xNzY4ODQ4NDgyLC
0zMjY2NDYzOTcsMTc1ODU4OTk2Miw5NDI0MjQ3MTEsLTE5MTg0
NDUyNDQsMTE1MjIyNTMxMywzODk5NDQ2MDIsMTU2MzcxNjU2MF
19
-->