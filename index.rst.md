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
-a----        05/06/2025     14:30           5495 <b>zowe.config.json </b>
-a----        02/07/2025     11:54          30488 zowe.schema.json
</code></pre>
per generare questa configurazione usiamo il comando:
## dove sono memorizzate le Users e le Passwords?
quando ci colleghiamo per la prima volta a un sistema z/OS , ci viene chiesta la nostra UserID e PSWD. esse vengono memorizzate nel gestore delle credenziali di W11 a cui possiamo accedere da:
>pannello di controllo > gestore delle credenziali > credenziali Windows

![gestione credenziali](./docs/images/Screenshot%202025-07-04%20115903.png)

eventualmente possiamo cancellare o modificare le credenziali

## inizializziamo l'environment ZOWE
per configurare i .profiles.json usiamo il CMD
> zowe config init --global-config

che con una procedura interattiva genera i files descritti. il parametro **--global-config** genera una configurazione valida per l'utente valida per ogni progetto.
il CMD 
> zowe config init

senza global-config genera un file di configurazione nella directory corrente che overrida eventualmente le specifiche in global.config
```powershell
PS C:\Users\u0e1591> zowe config init
Enter host (Host name of service on the mainframe.) - Press ENTER to skip:
Enter user (User name to authenticate to service on the mainframe.) - Press ENTER to skip:
Enter password (Password to authenticate to service on the mainframe.) - Press ENTER to skip:
Saved config template to C:\Users\u0e1591\zowe.config.json
PS C:\Users\u0e1591> zowe config init --global-config
Enter host (Host name of service on the mainframe.) - Press ENTER to skip:
Enter user (User name to authenticate to service on the mainframe.) - Press ENTER to skip:
Enter password (Password to authenticate to service on the mainframe.) - Press ENTER to skip:
Saved config template to C:\Users\u0e1591\.zowe\zowe.config.json
```
dal punto di vista della gestione,  **i gestori** del prodotto possono creare e distribuire un file di configurazione *ufficiale* che può essere importato dagli utenti con il CMD:

```powershell
PS C:\Users\u0e1591> zowe config import \\scapmop1509\Users\zowe\zowe.config.json  --overwrite --global-config
Imported config and schema to C:\Users\u0e1591\.zowe\zowe.config.json
PS C:\Users\u0e1591>
```
## quali sono i files di configurazione usati da i CMD zowe?
con il CMD :

<pre><code>
PS C:\Users\u0e1591> zowe config list --locations --root
C:\Users\u0e1591\<b>zowe.config.json</b>
C:\Users\u0e1591\.zowe\<b>zowe.config.json</b>
PS C:\Users\u0e1591>
</code></pre>

possiamo listare i files di configurazione che sono utilizzati da i comandi zowe e con il CMD:
<pre><code>
PS C:\Users\u0e1591> zowe tso issue command "netstat" --zosmf-profile TESTPLEX.zosmf --show-inputs-only
commandValues:
  suppress-startup-messages: true
  stateful:                  false
  account:                   u0e1591
  character-set:             697
  code-page:                 1047
  columns:                   80
  logon-procedure:           IZUFPROC
  region-size:               4096
  rows:                      24
  host:                      zosmfsygx.mframe.sanpaoloimi.com
  port:                      443
  reject-unauthorized:       false
  protocol:                  https
  show-inputs-only:          true
  zosmf-profile:             TESTPLEX.zosmf
authenticationType: none
authTypeOrder:      basic,token,bearer,cert-pem
optionalProfiles:
  - zosmf
  - tso
  - base
locations:
  - C:\Users\u0e1591\zowe.config.json
  - C:\Users\u0e1591\.zowe\zowe.config.json
</code></pre>

possiamo listare i parametri utilizzati dallo specifico CMD.

questo è il file di configurazione che ho preparato per gli ambienti 
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
                "account": "u0e1591",
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

```
## diamo i primi CMD
eseguiamo il  semplice CMD TSO LU sull'ambiente TESTPLEX. la sintassi è:
<pre><code>
PS C:\Users\u0e1591> <b>zowe tso issue command "LU" --zosmf-profile TESTPLEX.zosmf</b>
Some required connection properties have not been specified in your Zowe client configuration. Therefore, you
will be asked for the connection properties that are required to complete your command.

Enter the user name for your service (will be hidden):
Enter the password for your service (will be hidden):
Stored properties in C:\Users\u0e1591\zowe.config.json: user, password
USER=U0E1591  NAME=GIOLITO-TECHNITES     OWNER=U011441   CREATED=04.142
 DEFAULT-GROUP=GSY0G000 PASSDATE=25.147 PASS-INTERVAL=N/A PHRASEDATE=N/A
</code></pre>

## VSCode 
l'istallazione dell'IDE  VSCode ci permette di interagire con i CMD Zowe senza conoscerne la sintassi e di poter visualizzare files z/OS, USS, code jes2 ed altro  dentro l'applicazione.
l'installazione parte da:
[VSCode download partable](https://code.visualstudio.com/download#)
unzip in \portablesApps

## Zowe CLI FTP plugin
<pre><code>
PS C:\Users\u0e1591> zowe plugins install @zowe/zos-ftp-for-zowe-cli@latest
Plug-ins within the Imperative CLI Framework can legitimately gain
control of the zowe CLI application during the execution of every command.
Install 3rd party plug-ins at your own risk.


_______________________________________________________________
Location = https://registry.npmjs.org/

Installed plugin name = '@zowe/zos-ftp-for-zowe-cli'

_____ Validation results for plugin '@zowe/zos-ftp-for-zowe-cli' _____
This plugin was successfully validated. Enjoy the plugin.
</code></pre>

possiamo ora utilizzare il profilo 
>  --zftp-profile SVILPLEX.zftp

per listare i nostri files sotto la cartella /u/users
<pre><code>
PS C:\Users\u0e1591> zowe zos-ftp list uss "/u/u0e1591/stopx37" --zftp-profile SVILPLEX.zftp
Some required connection properties have not been specified in your Zowe client configuration. Therefore, you
will be asked for the connection properties that are required to complete your command.

Enter the user name for your service (will be hidden):
Enter the password for your service (will be hidden):
Stored properties in C:\Users\u0e1591\zowe.config.json: user, password
PS C:\Users\u0e1591> zowe zos-ftp list uss "/u/u0e1591/stopx37" --zftp-profile SVILPLEX.zftp
PS C:\Users\u0e1591> zowe zos-ftp list uss "/u/u0e1591/" --zftp-profile SVILPLEX.zftp
APP1.both.amblist                          89792    U0E1591 GDFSGRP -rw-r--r--
CACERT02.ca.cer                            1819     U0E1591 GDFSGRP -rw-------
CACERT02.caE.cer                           1796     U0E1591 GDFSGRP -rw-r--r--
CAROOT02.ca.cer                            1354     U0E1591 GDFSGRP -rw-------
</code></pre>


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ3MTExMjAsLTI3MjEzMTQwNSwtMTMyMT
EyMjU3MywtNDgyMDkyMDE0LC02NjgwMjE4NTQsMjA2NDE0MDI0
Nyw0MTgxNjIyNjEsNjE1NzQ0OTU2LDE4MTA5NDM3NzcsLTI2Nz
UwNTAwMyw0NzQyMzM0MjMsNjMzMzAzNjQzLDc4NDI5OTE3OSw5
NjI0MDA5MTksLTEwODQyNTAxMTEsLTU3MDkwMzQ4NiwtNTIwNT
kxNTI4LDE3MTExMDg2MTBdfQ==
-->