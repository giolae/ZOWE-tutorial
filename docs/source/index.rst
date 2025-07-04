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
	1.1. aprire il prompt powershell:
	```powershell
	 C:\Users\u0e1591>node --version
	"node" non è riconosciuto come comando interno o esterno, un programma eseguibile o un file batch.
	```
2. creare una cartella dove saranno ospitati i prodotti scaricati:
```powershell
	C:\Users\u0e1591> mkdir \portablesApps
	C:\Users\u0e1591>cd \portablesApps
	C:\portablesApps>
```
3. scompattiamo il file [node-v22.17.0-win-x64.zip](%5C%5Cscapmop1509%5CUsers%5Czowe%5Cnode-v22.17.0-win-x64.zip) che scaricato in precedenza con il cmd:
```powershell
tar  -xvf \\scapmop1509\Users\zowe\node-v22.17.0-win-x64.zip
```
4. aggiungere al PATH di Windows la directory (modifica le variabili di ambiente relative all'account...)

```powershell
C:\portablesApps\node-v22.17.0-win-x64\
PS C:\Users\u0e1591> $env:path -split ';'
C:\portablesApps\llvm-mingw-20241015-msvcrt-x86_64\bin
C:\portablesApps\apache-maven-3.9.9\bin
C:\portablesApps\Git\cmd
C:\portablesApps\node-v22.17.0-win-x64\
```
5. a questo punto possiamo verificare il corretto funzionamento di **node** e **npm** con i comandi:
```powershell 
PS C:\Users\u0e1591> node --version
v22.17.0
PS C:\Users\u0e1591> npm --version
10.9.2
PS C:\Users\u0e1591>
```
## installare zowe/CLI
sempre dal prompt di comandi installiamo @zowe/cli con:
```powershell
PS C:\Users\u0e1591> npm install --global @zowe/cli

added 315 packages in 2m

26 packages are looking for funding
  run `npm fund` for details
PS C:\Users\u0e1591> npm ls --global
C:\portablesApps\node-v22.17.0-win-x64
+-- @zowe/cli@8.24.1
+-- corepack@0.33.0
`-- npm@10.9.2
```
possiamo verificare la corretta installazione con il comando:
```powershell
PS C:\Users\u0e1591> zowe -V
CLI Version: 8.24.1
Zowe Release Version: v3.2.0
```
## Zowe team configuration file
per consentire a Zowe CLI o Zowe Explorer di connettersi a i sistemi z/OS è necessario fornire le informazioni relative agli endpoint quali:

-   `host`
-   `port`
-   `user`
-   `password`
-   etc…
questi dati sono organizzati in _profili_ e memorizzati nei **team configuration files** nella directory **.zowe** dell’utente
<pre><code>
PS C:\Users\u0e1591> ls .zowe
    Directory: C:\Users\u0e1591\.zowe
Mode                 LastWriteTime         Length Name

d-----        22/05/2025     14:47                .events
d-----        22/05/2025     15:20                logs
d-----        05/06/2025     12:16                plugins
d-----        22/05/2025     14:47                settings
d-----        30/06/2025     16:48                web-help
-a----        02/07/2025     11:54            591 extenders.json
-a----        05/06/2025     14:30           5495 **zowe.config.json**
-a----        02/07/2025     11:54          30488 zowe.schema.json
</code></pre>
## dove sono memorizzate le Users e le Passwords?
quando ci colleghiamo per la prima volta a un sistema z/OS , ci viene chiesta la nostra UserID e PSWD. esse vengono memorizzate nel gestore delle credenziali di W11 a cui possiamo accedere da:
>pannello di controllo > gestore delle credenziali > credenziali Windows

![Local image](./images/Screenshot 2025-07-04 115903.png)
![enter image description here](./docs/images/Screenshot%202025-07-04%20115903.png)
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
eyJoaXN0b3J5IjpbMTcxMTEwODYxMCwxMzIxMzU2MjQwLDEzMz
MzNDU2NzksLTY1NDg2Njg3Nyw0NTI3ODA2MzAsLTE2OTM3MzUz
MzgsLTE4NzE5MTMxNTQsMTM3MjgzNTU2MiwxMzk3OTY2OTUyLD
Y4OTg3MTU0OSwtODgzNTkxODg3LDg1ODU2NTg1MSwtNDE3MTMw
NzcxLDExMzQ3NDg3MzEsMTIxNDY1MTEzOSwtOTAyMzQ5ODYsLT
EwMzgyMTI4NDksMjQ3Nzc2NDE3LC0yMDQwNjI5MjE1LC0xNzY4
ODQ4NDgyXX0=
-->