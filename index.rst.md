---


---

<h1 id="zowe-cli-e-zowe-vscode-plugin-installation">ZOWE CLI e ZOWE VSCode plugin installation</h1>
<p>questa breve guida indica i passi necessari per consentire di utilizzare ZOWE su una postazione W11 (senza l’uso dei privilegi di Amministratore) .<br>
al termine saremo in grado di utilizzare ZOWE da:</p>
<ul>
<li>CLI (command Line Interface)</li>
<li>VSCode</li>
</ul>
<h2 id="prerequisiti">prerequisiti</h2>
<p>per fare questo sono necessari i seguenti prerequisiti:</p>
<ul>
<li>500MB di spazio disco</li>
</ul>
<p>al termine  saranno installati i seguenti prodotti:</p>
<ul>
<li>
<p><a href="https://nodejs.org/en">Node.js</a> Node.js® is a free, open-source,   cross-platform JavaScript runtime environment that lets developers<br>
create servers, web apps, command line tools and scripts.</p>
</li>
<li>
<p><a href="https://www.npmjs.com/">npm</a>  is a <a href="https://en.wikipedia.org/wiki/Package_manager" title="Package manager">package manager</a> for the <a href="https://en.wikipedia.org/wiki/JavaScript" title="JavaScript">JavaScript</a> programming language maintained by npm</p>
</li>
<li>
<p><a href="https://code.visualstudio.com/">Visual Studio Code</a>  The open source IDE  developed by Microsoft</p>
</li>
<li>
<p><a href="https://github.com/zowe/community#zowe-explorer" title="https://github.com/zowe/community#zowe-explorer">Zowe Explorer for VS Code</a> provides access to mainframe resources in Visual Studio Code. Zowe Explorer provides a modern, familiar, user-friendly interface for mainframe developers and system programmers</p>
</li>
</ul>
<h2 id="quick-start-steps">Quick-Start Steps:</h2>
<ol>
<li>
<p>verificare che Node.js e npm.js non siano già installati:</p>
</li>
<li>
<p>aprire il prompt powershell:</p>
<pre class=" language-powershell"><code class="prism  language-powershell">C:\Users\u0e1591&gt;node <span class="token operator">--</span>version
<span class="token string">"node"</span> non è riconosciuto come comando interno o esterno<span class="token punctuation">,</span> un programma eseguibile o un file batch<span class="token punctuation">.</span>
</code></pre>
</li>
<li>
<p>creare una cartella dove saranno ospitati i prodotti scaricati:</p>
<pre class=" language-powershell"><code class="prism  language-powershell">C:\Users\u0e1591&gt; mkdir \portablesApps

C:\Users\u0e1591&gt;cd \portablesApps

C:\portablesApps&gt;
</code></pre>
</li>
<li>
<p>scompattiamo il file <a href="%5C%5Cscapmop1509%5CUsers%5Czowe%5Cnode-v22.17.0-win-x64.zip">node-v22.17.0-win-x64.zip</a> che ho  scaricato in precedenza con il cmd:</p>
<pre class=" language-powershell"><code class="prism  language-powershell">tar  <span class="token operator">-</span>xvf \\scapmop1509\Users\zowe\node<span class="token operator">-</span>v22<span class="token punctuation">.</span>17<span class="token punctuation">.</span>0<span class="token operator">-</span>win<span class="token operator">-</span>x64<span class="token punctuation">.</span>zip
</code></pre>
</li>
<li>
<p>aggiungere al PATH di Windows la directory (modifica le variabili di ambiente relative all’account…)</p>
<pre class=" language-powershell"><code class="prism  language-powershell">C:\portablesApps\node<span class="token operator">-</span>v22<span class="token punctuation">.</span>17<span class="token punctuation">.</span>0<span class="token operator">-</span>win<span class="token operator">-</span>x64\
<span class="token function">PS</span> C:\Users\u0e1591&gt; <span class="token variable">$env</span>:path <span class="token operator">-</span>split <span class="token string">';'</span>
C:\portablesApps\llvm<span class="token operator">-</span>mingw<span class="token operator">-</span>20241015<span class="token operator">-</span>msvcrt<span class="token operator">-</span>x86_64\bin
C:\portablesApps\apache<span class="token operator">-</span>maven<span class="token operator">-</span>3<span class="token punctuation">.</span>9<span class="token punctuation">.</span>9\bin
C:\portablesApps\Git\cmd
C:\portablesApps\node<span class="token operator">-</span>v22<span class="token punctuation">.</span>17<span class="token punctuation">.</span>0<span class="token operator">-</span>win<span class="token operator">-</span>x64\
</code></pre>
</li>
<li>
<p>a questo punto possiamo verificare il corretto funzionamento di <strong>node</strong> e <strong>npm</strong> con i comandi:</p>
<pre class=" language-powershell"><code class="prism  language-powershell"><span class="token function">PS</span> C:\Users\u0e1591&gt; node <span class="token operator">--</span>version
v22<span class="token punctuation">.</span>17<span class="token punctuation">.</span>0
<span class="token function">PS</span> C:\Users\u0e1591&gt; npm <span class="token operator">--</span>version
10<span class="token punctuation">.</span>9<span class="token punctuation">.</span>2
<span class="token function">PS</span> C:\Users\u0e1591&gt;
</code></pre>
</li>
</ol>
<h2 id="installare-zowecli">installare zowe/CLI</h2>
<p>sempre dal prompt di comandi installiamo @zowe/cli con:</p>
<pre class=" language-powershell"><code class="prism  language-powershell"><span class="token function">PS</span> C:\Users\u0e1591&gt; npm install <span class="token operator">--</span>global @zowe<span class="token operator">/</span><span class="token function">cli</span>

added 315 packages in 2m

26 packages are looking <span class="token keyword">for</span> funding
  run `npm fund` <span class="token keyword">for</span> details
<span class="token function">PS</span> C:\Users\u0e1591&gt; npm <span class="token function">ls</span> <span class="token operator">--</span>global
C:\portablesApps\node<span class="token operator">-</span>v22<span class="token punctuation">.</span>17<span class="token punctuation">.</span>0<span class="token operator">-</span>win<span class="token operator">-</span>x64
<span class="token operator">+</span>-<span class="token operator">-</span> @zowe<span class="token operator">/</span><span class="token function">cli</span>@8<span class="token punctuation">.</span>24<span class="token punctuation">.</span>1
<span class="token operator">+</span>-<span class="token operator">-</span> corepack@0<span class="token punctuation">.</span>33<span class="token punctuation">.</span>0
`<span class="token operator">--</span> npm@10<span class="token punctuation">.</span>9<span class="token punctuation">.</span>2
</code></pre>
<p>possiamo verificare la corretta installazione con il comando:</p>
<pre class=" language-powershell"><code class="prism  language-powershell"><span class="token function">PS</span> C:\Users\u0e1591&gt; zowe <span class="token operator">--</span>help

 DESCRIPTION
 <span class="token operator">--</span>-<span class="token operator">--</span>-<span class="token operator">--</span>-<span class="token operator">--</span>

   Welcome to Zowe <span class="token function">CLI</span><span class="token operator">!</span>

   Zowe <span class="token function">CLI</span> is a command line interface <span class="token punctuation">(</span><span class="token function">CLI</span><span class="token punctuation">)</span> that provides a simple and streamlined way to interact with IBM z<span class="token operator">/</span>OS<span class="token punctuation">.</span>

   <span class="token keyword">For</span> additional Zowe <span class="token function">CLI</span> documentation<span class="token punctuation">,</span> visit https:<span class="token operator">/</span><span class="token operator">/</span>docs<span class="token punctuation">.</span>zowe<span class="token punctuation">.</span>org

   <span class="token keyword">For</span> Zowe <span class="token function">CLI</span> support<span class="token punctuation">,</span> visit https:<span class="token operator">/</span><span class="token operator">/</span>www<span class="token punctuation">.</span>zowe<span class="token punctuation">.</span>org
</code></pre>
<h4 id="zowe-team-configuration-file">Zowe team configuration file</h4>
<p>per consentire a  Zowe CLI o Zowe Explorerdi connetersi a i sistemi  z/OS è necessario fornire le informazioni relative agli  endpoint quali:</p>
<ul>
<li><code>host</code></li>
<li><code>port</code></li>
<li><code>user</code></li>
<li><code>password</code></li>
<li>etc…</li>
</ul>
<p>questi dati sono organizzati in <em>profili</em> e memorizzati nei <strong>team configuration files</strong>  nella directory <strong>.zowe</strong>  dell’utente</p>
<pre><code>
PS C:\Users\u0e1591&gt; ls .zowe
    Directory: C:\Users\u0e1591\.zowe

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        22/05/2025     14:47                .events
d-----        22/05/2025     15:20                logs
d-----        05/06/2025     12:16                plugins
d-----        22/05/2025     14:47                settings
d-----        30/06/2025     16:48                web-help
-a----        02/07/2025     11:54            591 extenders.json
-a----        05/06/2025     14:30           5495 <b>zowe.config.json</b>
-a----        02/07/2025     11:54          30488 zowe.schema.json
</code></pre>
<h2 id="dove-sono-memorizzate-le-users-e-le-passwords">dove sono memorizzate le Users e le Passwords?</h2>
<p>quando ci colleghiamo per la prima volta a un sistema z/OS , ci viene chiesta la nostra UserID e PSWD. esse vengono memorizzate nel gestore delle credenziali di W11 a cui possiamo accedere dal pannello di controllo &gt; gestore delle credenziali &gt; credenziali Windows</p>
<pre class=" language-yaml"><code class="prism  language-yaml"><span class="token punctuation">{</span>
    <span class="token key atrule">"$schema"</span><span class="token punctuation">:</span> <span class="token string">"./zowe.schema.json"</span><span class="token punctuation">,</span>
    <span class="token key atrule">"profiles"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token key atrule">"zosmf"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
            <span class="token key atrule">"type"</span><span class="token punctuation">:</span> <span class="token string">"zosmf"</span><span class="token punctuation">,</span>
            <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                <span class="token key atrule">"port"</span><span class="token punctuation">:</span> <span class="token number">443</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token key atrule">"secure"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        <span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token key atrule">"tso"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
            <span class="token key atrule">"type"</span><span class="token punctuation">:</span> <span class="token string">"tso"</span><span class="token punctuation">,</span>
            <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                <span class="token key atrule">"account"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
                <span class="token key atrule">"codePage"</span><span class="token punctuation">:</span> <span class="token string">"1047"</span><span class="token punctuation">,</span>
                <span class="token key atrule">"logonProcedure"</span><span class="token punctuation">:</span> <span class="token string">"IZUFPROC"</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token key atrule">"secure"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        <span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token key atrule">"ssh"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
            <span class="token key atrule">"type"</span><span class="token punctuation">:</span> <span class="token string">"ssh"</span><span class="token punctuation">,</span>
            <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                <span class="token key atrule">"port"</span><span class="token punctuation">:</span> <span class="token number">22</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token key atrule">"secure"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        <span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token key atrule">"zftp"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
            <span class="token key atrule">"type"</span><span class="token punctuation">:</span> <span class="token string">"zftp"</span><span class="token punctuation">,</span>
            <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                <span class="token key atrule">"port"</span><span class="token punctuation">:</span> <span class="token number">21</span><span class="token punctuation">,</span>
                <span class="token key atrule">"secureFtp"</span><span class="token punctuation">:</span> <span class="token boolean important">false</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token key atrule">"secure"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        <span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token key atrule">"global_base"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
            <span class="token key atrule">"type"</span><span class="token punctuation">:</span> <span class="token string">"base"</span><span class="token punctuation">,</span>
            <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                <span class="token key atrule">"host"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
                <span class="token key atrule">"rejectUnauthorized"</span><span class="token punctuation">:</span> <span class="token boolean important">true</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token key atrule">"secure"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
                <span class="token string">"user"</span><span class="token punctuation">,</span>
                <span class="token string">"password"</span>
            <span class="token punctuation">]</span>
        <span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token key atrule">"TESTPLEX"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
            <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                <span class="token key atrule">"host"</span><span class="token punctuation">:</span> <span class="token string">"zosmfsygx.mframe.sanpaoloimi.com"</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token key atrule">"secure"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
                <span class="token string">"user"</span><span class="token punctuation">,</span>
                <span class="token string">"password"</span>
            <span class="token punctuation">]</span><span class="token punctuation">,</span>
            <span class="token key atrule">"profiles"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                <span class="token key atrule">"zosmf"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                    <span class="token key atrule">"type"</span><span class="token punctuation">:</span> <span class="token string">"zosmf"</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                        <span class="token key atrule">"account"</span><span class="token punctuation">:</span> <span class="token string">"u0e1591"</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"protocol"</span><span class="token punctuation">:</span> <span class="token string">"https"</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"rejectUnauthorized"</span><span class="token punctuation">:</span> <span class="token boolean important">false</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"port"</span><span class="token punctuation">:</span> <span class="token number">443</span>
                    <span class="token punctuation">}</span>
                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                <span class="token key atrule">"tso"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                    <span class="token key atrule">"type"</span><span class="token punctuation">:</span> <span class="token string">"tso"</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                        <span class="token key atrule">"account"</span><span class="token punctuation">:</span> <span class="token string">"u0e1591"</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"rejectUnauthorized"</span><span class="token punctuation">:</span> <span class="token boolean important">false</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"codePage"</span><span class="token punctuation">:</span> <span class="token string">"1047"</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"logonProcedure"</span><span class="token punctuation">:</span> <span class="token string">"IZUFPROC"</span>
                    <span class="token punctuation">}</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"secure"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                <span class="token key atrule">"zftp"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                    <span class="token key atrule">"type"</span><span class="token punctuation">:</span> <span class="token string">"zftp"</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                        <span class="token key atrule">"host"</span><span class="token punctuation">:</span> <span class="token string">"syg0.mframe.sanpaoloimi.com"</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"account"</span><span class="token punctuation">:</span> <span class="token string">"u0e1591"</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"rejectUnauthorized"</span><span class="token punctuation">:</span> <span class="token boolean important">false</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"port"</span><span class="token punctuation">:</span> <span class="token number">21</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"secureFtp"</span><span class="token punctuation">:</span> <span class="token boolean important">false</span>
                    <span class="token punctuation">}</span>
                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                <span class="token key atrule">"ssh"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                    <span class="token key atrule">"type"</span><span class="token punctuation">:</span> <span class="token string">"ssh"</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                        <span class="token key atrule">"port"</span><span class="token punctuation">:</span> <span class="token number">22</span>
                    <span class="token punctuation">}</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"secure"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
                <span class="token punctuation">}</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token key atrule">"SVILPLEX"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
            <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                <span class="token key atrule">"host"</span><span class="token punctuation">:</span> <span class="token string">"zosmfsyax.mframe.sanpaoloimi.com"</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token key atrule">"secure"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
                <span class="token string">"user"</span><span class="token punctuation">,</span>
                <span class="token string">"password"</span>
            <span class="token punctuation">]</span><span class="token punctuation">,</span>
            <span class="token key atrule">"profiles"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                <span class="token key atrule">"zosmf"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                    <span class="token key atrule">"type"</span><span class="token punctuation">:</span> <span class="token string">"zosmf"</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                        <span class="token key atrule">"account"</span><span class="token punctuation">:</span> <span class="token string">"u0e1591"</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"protocol"</span><span class="token punctuation">:</span> <span class="token string">"https"</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"rejectUnauthorized"</span><span class="token punctuation">:</span> <span class="token boolean important">false</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"port"</span><span class="token punctuation">:</span> <span class="token number">443</span>
                    <span class="token punctuation">}</span>
                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                <span class="token key atrule">"zftp"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                    <span class="token key atrule">"type"</span><span class="token punctuation">:</span> <span class="token string">"zftp"</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                        <span class="token key atrule">"host"</span><span class="token punctuation">:</span> <span class="token string">"sya0.mframe.sanpaoloimi.com"</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"account"</span><span class="token punctuation">:</span> <span class="token string">"u0e1591"</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"rejectUnauthorized"</span><span class="token punctuation">:</span> <span class="token boolean important">false</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"port"</span><span class="token punctuation">:</span> <span class="token number">21</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"secureFtp"</span><span class="token punctuation">:</span> <span class="token boolean important">false</span>
                    <span class="token punctuation">}</span>
                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                <span class="token key atrule">"tso"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                    <span class="token key atrule">"type"</span><span class="token punctuation">:</span> <span class="token string">"tso"</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                        <span class="token key atrule">"account"</span><span class="token punctuation">:</span> <span class="token string">"u0e1591"</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"codePage"</span><span class="token punctuation">:</span> <span class="token string">"1047"</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"rejectUnauthorized"</span><span class="token punctuation">:</span> <span class="token boolean important">false</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"logonProcedure"</span><span class="token punctuation">:</span> <span class="token string">"IZUFPROC"</span>
                    <span class="token punctuation">}</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"secure"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                <span class="token key atrule">"ssh"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                    <span class="token key atrule">"type"</span><span class="token punctuation">:</span> <span class="token string">"ssh"</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                        <span class="token key atrule">"port"</span><span class="token punctuation">:</span> <span class="token number">22</span>
                    <span class="token punctuation">}</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"secure"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
                <span class="token punctuation">}</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token key atrule">"OPERPLEX"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
            <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                <span class="token key atrule">"host"</span><span class="token punctuation">:</span> <span class="token string">"zosmfsybx.mframe.sanpaoloimi.com"</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token key atrule">"secure"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
                <span class="token string">"user"</span><span class="token punctuation">,</span>
                <span class="token string">"password"</span>
            <span class="token punctuation">]</span><span class="token punctuation">,</span>
            <span class="token key atrule">"profiles"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                <span class="token key atrule">"zosmf"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                    <span class="token key atrule">"type"</span><span class="token punctuation">:</span> <span class="token string">"zosmf"</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                        <span class="token key atrule">"account"</span><span class="token punctuation">:</span> <span class="token string">"u0e1591"</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"protocol"</span><span class="token punctuation">:</span> <span class="token string">"https"</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"rejectUnauthorized"</span><span class="token punctuation">:</span> <span class="token boolean important">false</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"port"</span><span class="token punctuation">:</span> <span class="token number">443</span>
                    <span class="token punctuation">}</span>
                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                <span class="token key atrule">"tso"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                    <span class="token key atrule">"type"</span><span class="token punctuation">:</span> <span class="token string">"tso"</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                        <span class="token key atrule">"account"</span><span class="token punctuation">:</span> <span class="token string">"u0e1591"</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"codePage"</span><span class="token punctuation">:</span> <span class="token string">"1047"</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"rejectUnauthorized"</span><span class="token punctuation">:</span> <span class="token boolean important">false</span><span class="token punctuation">,</span>
                        <span class="token key atrule">"logonProcedure"</span><span class="token punctuation">:</span> <span class="token string">"IZUFPROC"</span>
                    <span class="token punctuation">}</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"secure"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                <span class="token key atrule">"ssh"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                    <span class="token key atrule">"type"</span><span class="token punctuation">:</span> <span class="token string">"ssh"</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
                        <span class="token key atrule">"port"</span><span class="token punctuation">:</span> <span class="token number">22</span>
                    <span class="token punctuation">}</span><span class="token punctuation">,</span>
                    <span class="token key atrule">"secure"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
                <span class="token punctuation">}</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token key atrule">"defaults"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token key atrule">"zosmf"</span><span class="token punctuation">:</span> <span class="token string">"TESTPLEX.zosmf"</span><span class="token punctuation">,</span>
        <span class="token key atrule">"tso"</span><span class="token punctuation">:</span> <span class="token string">"tso"</span><span class="token punctuation">,</span>
        <span class="token key atrule">"ssh"</span><span class="token punctuation">:</span> <span class="token string">"ssh"</span><span class="token punctuation">,</span>
        <span class="token key atrule">"rse"</span><span class="token punctuation">:</span> <span class="token string">"rse"</span><span class="token punctuation">,</span>
        <span class="token key atrule">"zftp"</span><span class="token punctuation">:</span> <span class="token string">"zftp"</span><span class="token punctuation">,</span>
        <span class="token key atrule">"base"</span><span class="token punctuation">:</span> <span class="token string">"global_base"</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token key atrule">"autoStore"</span><span class="token punctuation">:</span> <span class="token boolean important">true</span>
<span class="token punctuation">}</span>




2.  Install  <span class="token punctuation">[</span>Node.js and npm<span class="token punctuation">]</span>(https<span class="token punctuation">:</span>//www.npmjs.com/get<span class="token punctuation">-</span>npm)  on your laptop if you don’t already have it. This is a pre<span class="token punctuation">-</span>requisite for Zowe CLI<span class="token punctuation">,</span> similar to how Java or C++ runtimes are pre<span class="token punctuation">-</span>requisites for many other tools. If you can’t download Node.js and npm from npmjs.com<span class="token punctuation">,</span> you may need to check your company’s techstack of approved software to acquire it from there.
  

</code></pre>
<p>git clone <a href="https://github.com/openliberty/guide-microprofile-openapi.git">https://github.com/openliberty/guide-microprofile-openapi.git</a><br>
cd guide-microprofile-openapi</p>
<pre><code>
The  `start`  directory contains the starting project that you will build upon.

The  `finish`  directory contains the finished project that you will build.

Before you begin, make sure you have all the necessary  prerequisites.

### Try what you’ll build

The  `finish`  directory in the root of this guide contains the finished application. Give it a try before you proceed.

To try out the application, first go to the  `finish`  directory and run the following Maven goal to build the application and deploy it to Open Liberty:

`**WINDOWS**`

`**MAC**`

`**LINUX**`

</code></pre>
<p>cd finish<br>
mvnw.cmd liberty:run</p>
<pre><code>
After you see the following message, your Liberty instance is ready:


</code></pre>

