# ucode module: `log`

> **Source:** [`lib/log.c`](https://github.com/jow-/ucode/blob/master/lib/log.c)
> **Live docs:** https://ucode.mein.io/module-log.html
> **Generated:** 2026-05-01 03:18 UTC from commit `0beaa9d`

---

## Modules

<dl>
<dt><a href="#module_log">log</a></dt>
<dd><h1 id="system-logging-functions">System logging functions</h1>
<p>The <code>log</code> module provides bindings to the POSIX syslog functions <code>openlog()</code>,
<code>syslog()</code> and <code>closelog()</code> as well as - when available - the OpenWrt
specific ulog library functions.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { openlog, syslog, LOG_PID, LOG_USER, LOG_ERR } from 'log';

<p>openlog(&quot;my-log-ident&quot;, LOG_PID, LOG_USER);
syslog(LOG_ERR, &quot;An error occurred!&quot;);</p>
<p>// OpenWrt specific ulog functions
import { ulog_open, ulog, ULOG_SYSLOG, LOG_DAEMON, LOG_INFO } from &#39;log&#39;;</p>
<p>ulog_open(ULOG_SYSLOG, LOG_DAEMON, &quot;my-log-ident&quot;);
ulog(LOG_INFO, &quot;The current epoch is %d&quot;, time());
</code></pre></p>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as log from 'log';

<p>log.openlog(&quot;my-log-ident&quot;, log.LOG_PID, log.LOG_USER);
log.syslog(log.LOG_ERR, &quot;An error occurred!&quot;);</p>
<p>// OpenWrt specific ulog functions
log.ulog_open(log.ULOG_SYSLOG, log.LOG_DAEMON, &quot;my-log-ident&quot;);
log.ulog(log.LOG_INFO, &quot;The current epoch is %d&quot;, time());
</code></pre></p>
<p>Additionally, the log module namespace may also be imported by invoking the
<code>ucode</code> interpreter with the <code>-llog</code> switch.</p>
<h2 id="constants">Constants</h2>
<p>The <code>log</code> module declares a number of numeric constants to specify logging
facility, priority and option values, as well as ulog specific channels.</p>
<h3 id="syslog-options">Syslog Options</h3>
<table>
<thead>
<tr>
<th>Constant Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>LOG_PID</code></td>
<td>Include PID with each message.</td>
</tr>
<tr>
<td><code>LOG_CONS</code></td>
<td>Log to console if error occurs while sending to syslog.</td>
</tr>
<tr>
<td><code>LOG_NDELAY</code></td>
<td>Open the connection to the logger immediately.</td>
</tr>
<tr>
<td><code>LOG_ODELAY</code></td>
<td>Delay open until the first message is logged.</td>
</tr>
<tr>
<td><code>LOG_NOWAIT</code></td>
<td>Do not wait for child processes created during logging.</td>
</tr>
</tbody>
</table>
<h3 id="syslog-facilities">Syslog Facilities</h3>
<table>
<thead>
<tr>
<th>Constant Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>LOG_AUTH</code></td>
<td>Authentication/authorization messages.</td>
</tr>
<tr>
<td><code>LOG_AUTHPRIV</code></td>
<td>Private authentication messages.</td>
</tr>
<tr>
<td><code>LOG_CRON</code></td>
<td>Clock daemon (cron and at commands).</td>
</tr>
<tr>
<td><code>LOG_DAEMON</code></td>
<td>System daemons without separate facility values.</td>
</tr>
<tr>
<td><code>LOG_FTP</code></td>
<td>FTP server daemon.</td>
</tr>
<tr>
<td><code>LOG_KERN</code></td>
<td>Kernel messages.</td>
</tr>
<tr>
<td><code>LOG_LPR</code></td>
<td>Line printer subsystem.</td>
</tr>
<tr>
<td><code>LOG_MAIL</code></td>
<td>Mail system.</td>
</tr>
<tr>
<td><code>LOG_NEWS</code></td>
<td>Network news subsystem.</td>
</tr>
<tr>
<td><code>LOG_SYSLOG</code></td>
<td>Messages generated internally by syslogd.</td>
</tr>
<tr>
<td><code>LOG_USER</code></td>
<td>Generic user-level messages.</td>
</tr>
<tr>
<td><code>LOG_UUCP</code></td>
<td>UUCP subsystem.</td>
</tr>
<tr>
<td><code>LOG_LOCAL0</code></td>
<td>Local use 0 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL1</code></td>
<td>Local use 1 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL2</code></td>
<td>Local use 2 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL3</code></td>
<td>Local use 3 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL4</code></td>
<td>Local use 4 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL5</code></td>
<td>Local use 5 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL6</code></td>
<td>Local use 6 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL7</code></td>
<td>Local use 7 (custom facility).</td>
</tr>
</tbody>
</table>
<h3 id="syslog-priorities">Syslog Priorities</h3>
<table>
<thead>
<tr>
<th>Constant Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>LOG_EMERG</code></td>
<td>System is unusable.</td>
</tr>
<tr>
<td><code>LOG_ALERT</code></td>
<td>Action must be taken immediately.</td>
</tr>
<tr>
<td><code>LOG_CRIT</code></td>
<td>Critical conditions.</td>
</tr>
<tr>
<td><code>LOG_ERR</code></td>
<td>Error conditions.</td>
</tr>
<tr>
<td><code>LOG_WARNING</code></td>
<td>Warning conditions.</td>
</tr>
<tr>
<td><code>LOG_NOTICE</code></td>
<td>Normal, but significant, condition.</td>
</tr>
<tr>
<td><code>LOG_INFO</code></td>
<td>Informational message.</td>
</tr>
<tr>
<td><code>LOG_DEBUG</code></td>
<td>Debug-level message.</td>
</tr>
</tbody>
</table>
<h3 id="ulog-channels">Ulog channels</h3>
<table>
<thead>
<tr>
<th>Constant Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>ULOG_KMSG</code></td>
<td>Log messages to <code>/dev/kmsg</code> (dmesg).</td>
</tr>
<tr>
<td><code>ULOG_STDIO</code></td>
<td>Log messages to stdout.</td>
</tr>
<tr>
<td><code>ULOG_SYSLOG</code></td>
<td>Log messages to syslog.</td>
</tr>
</tbody>
</table></dd>
<dt><a href="#module_debug">debug</a></dt>
<dd><h1 id="debugger-module">Debugger Module</h1>
<p>This module provides runtime debug functionality for ucode scripts.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { memdump, traceback } from 'debug';

<p>let stacktrace = traceback(1);</p>
<p>memdump(&quot;/tmp/dump.txt&quot;);
</code></pre></p>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as debug from 'debug';

<p>let stacktrace = debug.traceback(1);</p>
<p>debug.memdump(&quot;/tmp/dump.txt&quot;);
</code></pre></p>
<p>Additionally, the debug module namespace may also be imported by invoking the
<code>ucode</code> interpreter with the <code>-ldebug</code> switch.</p>
<p>Upon loading, the <code>debug</code> module will register a <code>SIGUSR2</code> signal handler
which, upon receipt of the signal, will write a memory dump of the currently
running program to <code>/tmp/ucode.$timestamp.$pid.memdump</code>. This default
behavior can be inhibited by setting the <code>UCODE_DEBUG_MEMDUMP_ENABLED</code>
environment variable to <code>0</code> when starting the process. The memory dump signal
and output directory can be overridden with the <code>UCODE_DEBUG_MEMDUMP_SIGNAL</code>
and <code>UCODE_DEBUG_MEMDUMP_PATH</code> environment variables respectively.</p></dd>
<dt><a href="#module_digest">digest</a></dt>
<dd><h1 id="digest-functions">Digest Functions</h1>
<p>The <code>digest</code> module bundles various digest functions.</p></dd>
<dt><a href="#module_fs">fs</a></dt>
<dd><h1 id="filesystem-access">Filesystem Access</h1>
<p>The <code>fs</code> module provides functions for interacting with the file system.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { readlink, popen } from 'fs';

<p>let dest = readlink(&#39;/sys/class/net/eth0&#39;);
let proc = popen(&#39;ps ww&#39;);
</code></pre></p>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as fs from 'fs';

<p>let dest = fs.readlink(&#39;/sys/class/net/eth0&#39;);
let proc = fs.popen(&#39;ps ww&#39;);
</code></pre></p>
<p>Additionally, the filesystem module namespace may also be imported by invoking
the <code>ucode</code> interpreter with the <code>-lfs</code> switch.</p></dd>
<dt><a href="#module_io">io</a></dt>
<dd><h1 id="i%2Fo-operations">I/O Operations</h1>
<p>The <code>io</code> module provides object-oriented access to UNIX file descriptors.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { open, O_RDWR } from 'io';

<p>let handle = open(&#39;/tmp/test.txt&#39;, O_RDWR);
handle.write(&#39;Hello World\n&#39;);
handle.close();
</code></pre></p>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as io from 'io';

<p>let handle = io.open(&#39;/tmp/test.txt&#39;, io.O_RDWR);
handle.write(&#39;Hello World\n&#39;);
handle.close();
</code></pre></p>
<p>Additionally, the io module namespace may also be imported by invoking
the <code>ucode</code> interpreter with the <code>-lio</code> switch.</p></dd>
<dt><a href="#module_log">log</a></dt>
<dd><h1 id="system-logging-functions">System logging functions</h1>
<p>The <code>log</code> module provides bindings to the POSIX syslog functions <code>openlog()</code>,
<code>syslog()</code> and <code>closelog()</code> as well as - when available - the OpenWrt
specific ulog library functions.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { openlog, syslog, LOG_PID, LOG_USER, LOG_ERR } from 'log';

<p>openlog(&quot;my-log-ident&quot;, LOG_PID, LOG_USER);
syslog(LOG_ERR, &quot;An error occurred!&quot;);</p>
<p>// OpenWrt specific ulog functions
import { ulog_open, ulog, ULOG_SYSLOG, LOG_DAEMON, LOG_INFO } from &#39;log&#39;;</p>
<p>ulog_open(ULOG_SYSLOG, LOG_DAEMON, &quot;my-log-ident&quot;);
ulog(LOG_INFO, &quot;The current epoch is %d&quot;, time());
</code></pre></p>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as log from 'log';

<p>log.openlog(&quot;my-log-ident&quot;, log.LOG_PID, log.LOG_USER);
log.syslog(log.LOG_ERR, &quot;An error occurred!&quot;);</p>
<p>// OpenWrt specific ulog functions
log.ulog_open(log.ULOG_SYSLOG, log.LOG_DAEMON, &quot;my-log-ident&quot;);
log.ulog(log.LOG_INFO, &quot;The current epoch is %d&quot;, time());
</code></pre></p>
<p>Additionally, the log module namespace may also be imported by invoking the
<code>ucode</code> interpreter with the <code>-llog</code> switch.</p>
<h2 id="constants">Constants</h2>
<p>The <code>log</code> module declares a number of numeric constants to specify logging
facility, priority and option values, as well as ulog specific channels.</p>
<h3 id="syslog-options">Syslog Options</h3>
<table>
<thead>
<tr>
<th>Constant Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>LOG_PID</code></td>
<td>Include PID with each message.</td>
</tr>
<tr>
<td><code>LOG_CONS</code></td>
<td>Log to console if error occurs while sending to syslog.</td>
</tr>
<tr>
<td><code>LOG_NDELAY</code></td>
<td>Open the connection to the logger immediately.</td>
</tr>
<tr>
<td><code>LOG_ODELAY</code></td>
<td>Delay open until the first message is logged.</td>
</tr>
<tr>
<td><code>LOG_NOWAIT</code></td>
<td>Do not wait for child processes created during logging.</td>
</tr>
</tbody>
</table>
<h3 id="syslog-facilities">Syslog Facilities</h3>
<table>
<thead>
<tr>
<th>Constant Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>LOG_AUTH</code></td>
<td>Authentication/authorization messages.</td>
</tr>
<tr>
<td><code>LOG_AUTHPRIV</code></td>
<td>Private authentication messages.</td>
</tr>
<tr>
<td><code>LOG_CRON</code></td>
<td>Clock daemon (cron and at commands).</td>
</tr>
<tr>
<td><code>LOG_DAEMON</code></td>
<td>System daemons without separate facility values.</td>
</tr>
<tr>
<td><code>LOG_FTP</code></td>
<td>FTP server daemon.</td>
</tr>
<tr>
<td><code>LOG_KERN</code></td>
<td>Kernel messages.</td>
</tr>
<tr>
<td><code>LOG_LPR</code></td>
<td>Line printer subsystem.</td>
</tr>
<tr>
<td><code>LOG_MAIL</code></td>
<td>Mail system.</td>
</tr>
<tr>
<td><code>LOG_NEWS</code></td>
<td>Network news subsystem.</td>
</tr>
<tr>
<td><code>LOG_SYSLOG</code></td>
<td>Messages generated internally by syslogd.</td>
</tr>
<tr>
<td><code>LOG_USER</code></td>
<td>Generic user-level messages.</td>
</tr>
<tr>
<td><code>LOG_UUCP</code></td>
<td>UUCP subsystem.</td>
</tr>
<tr>
<td><code>LOG_LOCAL0</code></td>
<td>Local use 0 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL1</code></td>
<td>Local use 1 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL2</code></td>
<td>Local use 2 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL3</code></td>
<td>Local use 3 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL4</code></td>
<td>Local use 4 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL5</code></td>
<td>Local use 5 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL6</code></td>
<td>Local use 6 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL7</code></td>
<td>Local use 7 (custom facility).</td>
</tr>
</tbody>
</table>
<h3 id="syslog-priorities">Syslog Priorities</h3>
<table>
<thead>
<tr>
<th>Constant Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>LOG_EMERG</code></td>
<td>System is unusable.</td>
</tr>
<tr>
<td><code>LOG_ALERT</code></td>
<td>Action must be taken immediately.</td>
</tr>
<tr>
<td><code>LOG_CRIT</code></td>
<td>Critical conditions.</td>
</tr>
<tr>
<td><code>LOG_ERR</code></td>
<td>Error conditions.</td>
</tr>
<tr>
<td><code>LOG_WARNING</code></td>
<td>Warning conditions.</td>
</tr>
<tr>
<td><code>LOG_NOTICE</code></td>
<td>Normal, but significant, condition.</td>
</tr>
<tr>
<td><code>LOG_INFO</code></td>
<td>Informational message.</td>
</tr>
<tr>
<td><code>LOG_DEBUG</code></td>
<td>Debug-level message.</td>
</tr>
</tbody>
</table>
<h3 id="ulog-channels">Ulog channels</h3>
<table>
<thead>
<tr>
<th>Constant Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>ULOG_KMSG</code></td>
<td>Log messages to <code>/dev/kmsg</code> (dmesg).</td>
</tr>
<tr>
<td><code>ULOG_STDIO</code></td>
<td>Log messages to stdout.</td>
</tr>
<tr>
<td><code>ULOG_SYSLOG</code></td>
<td>Log messages to syslog.</td>
</tr>
</tbody>
</table></dd>
<dt><a href="#module_math">math</a></dt>
<dd><h1 id="mathematical-functions">Mathematical Functions</h1>
<p>The <code>math</code> module bundles various mathematical and trigonometrical functions.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { pow, rand } from 'math';

<p>let x = pow(2, 5);
let y = rand();
</code></pre></p>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as math from 'math';

<p>let x = math.pow(2, 5);
let y = math.rand();
</code></pre></p>
<p>Additionally, the math module namespace may also be imported by invoking the
<code>ucode</code> interpreter with the <code>-lmath</code> switch.</p></dd>
<dt><a href="#module_nl80211">nl80211</a></dt>
<dd><h1 id="wireless-netlink">Wireless Netlink</h1>
<p>The <code>nl80211</code> module provides functions for interacting with the nl80211 netlink interface
for wireless networking configuration and management.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source lang-javascript"><code>import { error, request, listener, waitfor, const } from 'nl80211';

<p>// Send a nl80211 request
let response = request(const.NL80211_CMD_GET_WIPHY, 0, { wiphy: 0 });</p>
<p>// Create a listener for wireless events
let wifiListener = listener((msg) =&gt; {
    print(&#39;Received wireless event:&#39;, msg, &#39;\n&#39;);
}, [const.NL80211_CMD_NEW_INTERFACE, const.NL80211_CMD_DEL_INTERFACE]);</p>
<p>// Wait for a specific nl80211 event
let event = waitfor([const.NL80211_CMD_NEW_SCAN_RESULTS], 5000);
if (event)
    print(&#39;Received scan results:&#39;, event.msg, &#39;\n&#39;);
</code></pre></p>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source lang-javascript"><code>import * as nl80211 from 'nl80211';

<p>// Send a nl80211 request
let response = nl80211.request(nl80211.const.NL80211_CMD_GET_WIPHY, 0, { wiphy: 0 });</p>
<p>// Create a listener for wireless events
let listener = nl80211.listener((msg) =&gt; {
    print(&#39;Received wireless event:&#39;, msg, &#39;\n&#39;);
}, [nl80211.const.NL80211_CMD_NEW_INTERFACE, nl80211.const.NL80211_CMD_DEL_INTERFACE]);
</code></pre></p>
<p>Additionally, the nl80211 module namespace may also be imported by invoking
the <code>ucode</code> interpreter with the <code>-lnl80211</code> switch.</p></dd>
<dt><a href="#module_resolv">resolv</a></dt>
<dd><h1 id="dns-resolution-module">DNS Resolution Module</h1>
<p>The <code>resolv</code> module provides DNS resolution functionality for ucode, allowing
you to perform DNS queries for various record types and handle responses.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { query } from 'resolv';

<p>let result = query(&#39;example.com&#39;, { type: [&#39;A&#39;] });
</code></pre></p>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as resolv from 'resolv';

<p>let result = resolv.query(&#39;example.com&#39;, { type: [&#39;A&#39;] });
</code></pre></p>
<p>Additionally, the resolv module namespace may also be imported by invoking
the <code>ucode</code> interpreter with the <code>-lresolv</code> switch.</p>
<h2 id="record-types">Record Types</h2>
<p>The module supports the following DNS record types:</p>
<table>
<thead>
<tr>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>A</code></td>
<td>IPv4 address record</td>
</tr>
<tr>
<td><code>AAAA</code></td>
<td>IPv6 address record</td>
</tr>
<tr>
<td><code>CNAME</code></td>
<td>Canonical name record</td>
</tr>
<tr>
<td><code>MX</code></td>
<td>Mail exchange record</td>
</tr>
<tr>
<td><code>NS</code></td>
<td>Name server record</td>
</tr>
<tr>
<td><code>PTR</code></td>
<td>Pointer record (reverse DNS)</td>
</tr>
<tr>
<td><code>SOA</code></td>
<td>Start of authority record</td>
</tr>
<tr>
<td><code>SRV</code></td>
<td>Service record</td>
</tr>
<tr>
<td><code>TXT</code></td>
<td>Text record</td>
</tr>
<tr>
<td><code>ANY</code></td>
<td>Any available record type</td>
</tr>
</tbody>
</table>
<h2 id="response-codes">Response Codes</h2>
<p>DNS queries can return the following response codes:</p>
<table>
<thead>
<tr>
<th>Code</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>NOERROR</code></td>
<td>No error, query successful</td>
</tr>
<tr>
<td><code>FORMERR</code></td>
<td>Format error in query</td>
</tr>
<tr>
<td><code>SERVFAIL</code></td>
<td>Server failure</td>
</tr>
<tr>
<td><code>NXDOMAIN</code></td>
<td>Non-existent domain</td>
</tr>
<tr>
<td><code>NOTIMP</code></td>
<td>Not implemented</td>
</tr>
<tr>
<td><code>REFUSED</code></td>
<td>Query refused</td>
</tr>
<tr>
<td><code>TIMEOUT</code></td>
<td>Query timed out</td>
</tr>
</tbody>
</table>
<h2 id="response-format">Response Format</h2>
<p>DNS query results are returned as objects where:</p>
<ul>
<li>Keys are the queried domain names</li>
<li>Values are objects containing arrays of records grouped by type</li>
<li>Special <code>rcode</code> property indicates query status for failed queries</li>
</ul>
<h3 id="record-format-by-type">Record Format by Type</h3>
<p><strong>A and AAAA records:</strong></p>
<pre class="prettyprint source lang-javascript"><code>{
  &quot;example.com&quot;: {
    &quot;A&quot;: [&quot;192.0.2.1&quot;, &quot;192.0.2.2&quot;],
    &quot;AAAA&quot;: [&quot;2001:db8::1&quot;, &quot;2001:db8::2&quot;]
  }
}
</code></pre>
<p><strong>MX records:</strong></p>
<pre class="prettyprint source lang-javascript"><code>{
  &quot;example.com&quot;: {
    &quot;MX&quot;: [
      [10, &quot;mail1.example.com&quot;],
      [20, &quot;mail2.example.com&quot;]
    ]
  }
}
</code></pre>
<p><strong>SRV records:</strong></p>
<pre class="prettyprint source lang-javascript"><code>{
  &quot;_http._tcp.example.com&quot;: {
    &quot;SRV&quot;: [
      [10, 5, 80, &quot;web1.example.com&quot;],
      [10, 10, 80, &quot;web2.example.com&quot;]
    ]
  }
}
</code></pre>
<p><strong>SOA records:</strong></p>
<pre class="prettyprint source lang-javascript"><code>{
  &quot;example.com&quot;: {
    &quot;SOA&quot;: [
      [
        &quot;ns1.example.com&quot;,      // primary nameserver
        &quot;admin.example.com&quot;,    // responsible mailbox
        2023010101,             // serial number
        3600,                   // refresh interval
        1800,                   // retry interval
        604800,                 // expire time
        86400                   // minimum TTL
      ]
    ]
  }
}
</code></pre>
<p><strong>TXT, NS, CNAME, PTR records:</strong></p>
<pre class="prettyprint source lang-javascript"><code>{
  &quot;example.com&quot;: {
    &quot;TXT&quot;: [&quot;v=spf1 include:_spf.example.com ~all&quot;],
    &quot;NS&quot;: [&quot;ns1.example.com&quot;, &quot;ns2.example.com&quot;],
    &quot;CNAME&quot;: [&quot;alias.example.com&quot;]
  }
}
</code></pre>
<p><strong>Error responses:</strong></p>
<pre class="prettyprint source lang-javascript"><code>{
  &quot;nonexistent.example.com&quot;: {
    &quot;rcode&quot;: &quot;NXDOMAIN&quot;
  }
}
</code></pre>
<h2 id="examples">Examples</h2>
<p>Basic A record lookup:</p>
<pre class="prettyprint source lang-javascript"><code>import { query } from 'resolv';

<p>const result = query([&#39;example.com&#39;]);
print(result, &quot;\n&quot;);
// {
//   &quot;example.com&quot;: {
//     &quot;A&quot;: [&quot;192.0.2.1&quot;],
//     &quot;AAAA&quot;: [&quot;2001:db8::1&quot;]
//   }
// }
</code></pre></p>
<p>Specific record type query:</p>
<pre class="prettyprint source lang-javascript"><code>const mxRecords = query(['example.com'], { type: ['MX'] });
print(mxRecords, &quot;\n&quot;);
// {
//   &quot;example.com&quot;: {
//     &quot;MX&quot;: [[10, &quot;mail.example.com&quot;]]
//   }
// }
</code></pre>
<p>Multiple domains and types:</p>
<pre class="prettyprint source lang-javascript"><code>const results = query(
  ['example.com', 'google.com'],
  { 
    type: ['A', 'MX'],
    timeout: 10000,
    nameserver: ['8.8.8.8', '1.1.1.1']
  }
);
</code></pre>
<p>Reverse DNS lookup:</p>
<pre class="prettyprint source lang-javascript"><code>const ptrResult = query(['192.0.2.1'], { type: ['PTR'] });
print(ptrResult, &quot;\n&quot;);
// {
//   &quot;1.2.0.192.in-addr.arpa&quot;: {
//     &quot;PTR&quot;: [&quot;example.com&quot;]
//   }
// }
</code></pre></dd>
<dt><a href="#module_rtnl">rtnl</a></dt>
<dd><h1 id="routing-netlink">Routing Netlink</h1>
<p>The <code>rtnl</code> module provides functions for interacting with the routing netlink interface.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source lang-javascript"><code>import { error, request, listener, RTM_GETROUTE, RTM_NEWROUTE, RTM_DELROUTE, AF_INET } from 'rtnl';

<p>// Send a netlink request
let response = request(RTM_GETROUTE, 0, { family: AF_INET });</p>
<p>// Create a listener for route changes
let routeListener = listener((msg) =&gt; {
    print(&#39;Received route message:&#39;, msg, &#39;\n&#39;);
}, [RTM_NEWROUTE, RTM_DELROUTE]);
</code></pre></p>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source lang-javascript"><code>import * as rtnl from 'rtnl';

<p>// Send a netlink request
let response = rtnl.request(rtnl.RTM_GETROUTE, 0, { family: rtnl.AF_INET });</p>
<p>// Create a listener for route changes
let listener = rtnl.listener((msg) =&gt; {
    print(&#39;Received route message:&#39;, msg, &#39;\n&#39;);
}, [rtnl.RTM_NEWROUTE, rtnl.RTM_DELROUTE]);
</code></pre></p>
<p>Additionally, the rtnl module namespace may also be imported by invoking
the <code>ucode</code> interpreter with the <code>-lrtnl</code> switch.</p></dd>
<dt><a href="#module_socket">socket</a></dt>
<dd><h1 id="socket-module">Socket Module</h1>
<p>The <code>socket</code> module provides functions for interacting with sockets.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source lang-javascript"><code>import { AF_INET, SOCK_STREAM, create as socket } from 'socket';

<p>let sock = socket(AF_INET, SOCK_STREAM, 0);
sock.connect(&#39;192.168.1.1&#39;, 80);
sock.send(…);
sock.recv(…);
sock.close();
</code></pre></p>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source lang-javascript"><code>import * as socket from 'socket';

<p>let sock = socket.create(socket.AF_INET, socket.SOCK_STREAM, 0);
sock.connect(&#39;192.168.1.1&#39;, 80);
sock.send(…);
sock.recv(…);
sock.close();
</code></pre></p>
<p>Additionally, the socket module namespace may also be imported by invoking
the <code>ucode</code> interpreter with the <code>-lsocket</code> switch.</p></dd>
<dt><a href="#module_struct">struct</a></dt>
<dd><h1 id="handle-packed-binary-data">Handle Packed Binary Data</h1>
<p>The <code>struct</code> module provides routines for interpreting byte strings as packed
binary data.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { pack, unpack } from 'struct';

<p>let buffer = pack(&#39;bhl&#39;, -13, 1234, 444555666);
let values = unpack(&#39;bhl&#39;, buffer);
</code></pre></p>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as struct from 'struct';

<p>let buffer = struct.pack(&#39;bhl&#39;, -13, 1234, 444555666);
let values = struct.unpack(&#39;bhl&#39;, buffer);
</code></pre></p>
<p>Additionally, the struct module namespace may also be imported by invoking
the <code>ucode</code> interpreter with the <code>-lstruct</code> switch.</p>
<h2 id="format-strings">Format Strings</h2>
<p>Format strings describe the data layout when packing and unpacking data.
They are built up from format-characters, which specify the type of data
being packed/unpacked. In addition, special characters control the byte
order, size and alignment.</p>
<p>Each format string consists of an optional prefix character which describes
the overall properties of the data and one or more format characters which
describe the actual data values and padding.</p>
<h3 id="byte-order%2C-size%2C-and-alignment">Byte Order, Size, and Alignment</h3>
<p>By default, C types are represented in the machine's native format and byte
order, and properly aligned by skipping pad bytes if necessary (according to
the rules used by the C compiler).</p>
<p>This behavior is chosen so that the bytes of a packed struct correspond
exactly to the memory layout of the corresponding C struct.</p>
<p>Whether to use native byte ordering and padding or standard formats depends
on the application.</p>
<p>Alternatively, the first character of the format string can be used to indicate
the byte order, size and alignment of the packed data, according to the
following table:</p>
<table>
<thead>
<tr>
<th>Character</th>
<th>Byte order</th>
<th>Size</th>
<th>Alignment</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>@</code></td>
<td>native</td>
<td>native</td>
<td>native</td>
</tr>
<tr>
<td><code>=</code></td>
<td>native</td>
<td>standard</td>
<td>none</td>
</tr>
<tr>
<td><code>&lt;</code></td>
<td>little-endian</td>
<td>standard</td>
<td>none</td>
</tr>
<tr>
<td><code>&gt;</code></td>
<td>big-endian</td>
<td>standard</td>
<td>none</td>
</tr>
<tr>
<td><code>!</code></td>
<td>network (= big-endian)</td>
<td>standard</td>
<td>none</td>
</tr>
</tbody>
</table>
<p>If the first character is not one of these, <code>'@'</code> is assumed.</p>
<p>Native byte order is big-endian or little-endian, depending on the
host system. For example, Intel x86, AMD64 (x86-64), and Apple M1 are
little-endian; IBM z and many legacy architectures are big-endian.</p>
<p>Native size and alignment are determined using the C compiler's
<code>sizeof</code> expression. This is always combined with native byte order.</p>
<p>Standard size depends only on the format character; see the table in
the <code>format-characters</code> section.</p>
<p>Note the difference between <code>'@'</code> and <code>'='</code>: both use native byte order,
but the size and alignment of the latter is standardized.</p>
<p>The form <code>'!'</code> represents the network byte order which is always big-endian
as defined in <code>IETF RFC 1700</code>.</p>
<p>There is no way to indicate non-native byte order (force byte-swapping); use
the appropriate choice of <code>'&lt;'</code> or <code>'&gt;'</code>.</p>
<p>Notes:</p>
<p>(1) Padding is only automatically added between successive structure members.
No padding is added at the beginning or the end of the encoded struct.</p>
<p>(2) No padding is added when using non-native size and alignment, e.g.
with '&lt;', '&gt;', '=', and '!'.</p>
<p>(3) To align the end of a structure to the alignment requirement of a
particular type, end the format with the code for that type with a repeat
count of zero.</p>
<h3 id="format-characters">Format Characters</h3>
<p>Format characters have the following meaning; the conversion between C and
ucode values should be obvious given their types.  The 'Standard size' column
refers to the size of the packed value in bytes when using standard size;
that is, when the format string starts with one of <code>'&lt;'</code>, <code>'&gt;'</code>, <code>'!'</code> or
<code>'='</code>.  When using native size, the size of the packed value is platform
dependent.</p>
<table>
<thead>
<tr>
<th>Format</th>
<th>C Type</th>
<th>Ucode type</th>
<th>Standard size</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>x</code></td>
<td><em>pad byte</em></td>
<td><em>no value</em></td>
<td></td>
<td>(7)</td>
</tr>
<tr>
<td><code>c</code></td>
<td><code>char</code></td>
<td>string</td>
<td>1</td>
<td></td>
</tr>
<tr>
<td><code>b</code></td>
<td><code>signed char</code></td>
<td>int</td>
<td>1</td>
<td>(1), (2)</td>
</tr>
<tr>
<td><code>B</code></td>
<td><code>unsigned char</code></td>
<td>int</td>
<td>1</td>
<td>(2)</td>
</tr>
<tr>
<td><code>?</code></td>
<td><code>_Bool</code></td>
<td>bool</td>
<td>1</td>
<td>(1)</td>
</tr>
<tr>
<td><code>h</code></td>
<td><code>short</code></td>
<td>int</td>
<td>2</td>
<td>(2)</td>
</tr>
<tr>
<td><code>H</code></td>
<td><code>unsigned short</code></td>
<td>int</td>
<td>2</td>
<td>(2)</td>
</tr>
<tr>
<td><code>i</code></td>
<td><code>int</code></td>
<td>int</td>
<td>4</td>
<td>(2)</td>
</tr>
<tr>
<td><code>I</code></td>
<td><code>unsigned int</code></td>
<td>int</td>
<td>4</td>
<td>(2)</td>
</tr>
<tr>
<td><code>l</code></td>
<td><code>long</code></td>
<td>int</td>
<td>4</td>
<td>(2)</td>
</tr>
<tr>
<td><code>L</code></td>
<td><code>unsigned long</code></td>
<td>int</td>
<td>4</td>
<td>(2)</td>
</tr>
<tr>
<td><code>q</code></td>
<td><code>long long</code></td>
<td>int</td>
<td>8</td>
<td>(2)</td>
</tr>
<tr>
<td><code>Q</code></td>
<td><code>unsigned long long</code></td>
<td>int</td>
<td>8</td>
<td>(2)</td>
</tr>
<tr>
<td><code>n</code></td>
<td><code>ssize_t</code></td>
<td>int</td>
<td></td>
<td>(3)</td>
</tr>
<tr>
<td><code>N</code></td>
<td><code>size_t</code></td>
<td>int</td>
<td></td>
<td>(3)</td>
</tr>
<tr>
<td><code>e</code></td>
<td>(6)</td>
<td>double</td>
<td>2</td>
<td>(4)</td>
</tr>
<tr>
<td><code>f</code></td>
<td><code>float</code></td>
<td>double</td>
<td>4</td>
<td>(4)</td>
</tr>
<tr>
<td><code>d</code></td>
<td><code>double</code></td>
<td>double</td>
<td>8</td>
<td>(4)</td>
</tr>
<tr>
<td><code>s</code></td>
<td><code>char[]</code></td>
<td>double</td>
<td></td>
<td>(9)</td>
</tr>
<tr>
<td><code>p</code></td>
<td><code>char[]</code></td>
<td>double</td>
<td></td>
<td>(8)</td>
</tr>
<tr>
<td><code>P</code></td>
<td><code>void *</code></td>
<td>int</td>
<td></td>
<td>(5)</td>
</tr>
<tr>
<td><code>*</code></td>
<td><code>char[]</code></td>
<td>string</td>
<td></td>
<td>(10)</td>
</tr>
<tr>
<td><code>X</code></td>
<td><code>char[]</code></td>
<td>string</td>
<td></td>
<td>(11)</td>
</tr>
<tr>
<td><code>Z</code></td>
<td><code>char[]</code></td>
<td>string</td>
<td></td>
<td>(12)</td>
</tr>
</tbody>
</table>
<p>Notes:</p>
<ul>
<li>
<p>(1) The <code>'?'</code> conversion code corresponds to the <code>_Bool</code> type defined by
C99. If this type is not available, it is simulated using a <code>char</code>. In
standard mode, it is always represented by one byte.</p>
</li>
<li>
<p>(2) When attempting to pack a non-integer using any of the integer
conversion codes, this module attempts to convert the given value into an
integer. If the value is not convertible, a type error exception is thrown.</p>
</li>
<li>
<p>(3) The <code>'n'</code> and <code>'N'</code> conversion codes are only available for the native
size (selected as the default or with the <code>'@'</code> byte order character).
For the standard size, you can use whichever of the other integer formats
fits your application.</p>
</li>
<li>
<p>(4) For the <code>'f'</code>, <code>'d'</code> and <code>'e'</code> conversion codes, the packed
representation uses the IEEE 754 binary32, binary64 or binary16 format
(for <code>'f'</code>, <code>'d'</code> or <code>'e'</code> respectively), regardless of the floating-point
format used by the platform.</p>
</li>
<li>
<p>(5) The <code>'P'</code> format character is only available for the native byte
ordering (selected as the default or with the <code>'@'</code> byte order character).
The byte order character <code>'='</code> chooses to use little- or big-endian
ordering based on the host system. The struct module does not interpret
this as native ordering, so the <code>'P'</code> format is not available.</p>
</li>
<li>
<p>(6) The IEEE 754 binary16 &quot;half precision&quot; type was introduced in the 2008
revision of the <code>IEEE 754</code> standard. It has a sign bit, a 5-bit exponent
and 11-bit precision (with 10 bits explicitly stored), and can represent
numbers between approximately <code>6.1e-05</code> and <code>6.5e+04</code> at full precision.
This type is not widely supported by C compilers: on a typical machine, an
unsigned short can be used for storage, but not for math operations. See
the Wikipedia page on the <code>half-precision floating-point format</code> for more
information.</p>
</li>
<li>
<p>(7) When packing, <code>'x'</code> inserts one NUL byte.</p>
</li>
<li>
<p>(8) The <code>'p'</code> format character encodes a &quot;Pascal string&quot;, meaning a short
variable-length string stored in a <em>fixed number of bytes</em>, given by the
count. The first byte stored is the length of the string, or 255,
whichever is smaller.  The bytes of the string follow.  If the string
passed in to <code>pack()</code> is too long (longer than the count minus 1), only
the leading <code>count-1</code> bytes of the string are stored.  If the string is
shorter than <code>count-1</code>, it is padded with null bytes so that exactly count
bytes in all are used.  Note that for <code>unpack()</code>, the <code>'p'</code> format
character consumes <code>count</code> bytes, but that the string returned can never
contain more than 255 bytes.</p>
</li>
<li>
<p>(9) For the <code>'s'</code> format character, the count is interpreted as the length
of the bytes, not a repeat count like for the other format characters; for
example, <code>'10s'</code> means a single 10-byte string mapping to or from a single
ucode byte string, while <code>'10c'</code> means 10 separate one byte character
elements (e.g., <code>cccccccccc</code>) mapping to or from ten different ucode byte
strings. If a count is not given, it defaults to 1. For packing, the
string is truncated or padded with null bytes as appropriate to make it
fit. For unpacking, the resulting bytes object always has exactly the
specified number of bytes.  As a special case, <code>'0s'</code> means a single,
empty string (while <code>'0c'</code> means 0 characters).</p>
</li>
<li>
<p>(10) The <code>*</code> format character serves as wildcard. For <code>pack()</code> it will
append the corresponding byte argument string as-is, not applying any
padding or zero filling. When a repeat count is given, that many bytes of
the input byte string argument will be appended at most on <code>pack()</code>,
effectively truncating longer input strings. For <code>unpack()</code>, the wildcard
format will yield a byte string containing the entire remaining input data
bytes, or - when a repeat count is given - that many bytes of input data
at most.</p>
</li>
<li>
<p>(11) The <code>X</code> format character handles hexadecimal encoding of binary data.
On <code>pack()</code>, the argument is a hexadecimal string; with no repeat count the
entire string is decoded into binary, while a repeat count limits the
number of output bytes (truncating longer input). On <code>unpack()</code>, the input
binary data is converted into a hexadecimal string, using all remaining
bytes by default, or at most the specified number of bytes when a repeat
count is given. Decoding accepts both upper- and lowercase hex digits, but
encoding always produces lowercase output. The encoded text length is
exactly twice the number of processed binary bytes.</p>
</li>
<li>
<p>(12) The <code>Z</code> format character behaves like <code>X</code>, but uses base64 encoding
instead of hexadecimal. On <code>pack()</code>, the argument is a base64 string; by
default the entire string is decoded into binary, or at most the specified
number of bytes when a repeat count is given. On <code>unpack()</code>, the input
binary data is converted into a base64 string, consuming all remaining
bytes by default, or at most the repeat count if given. The encoded base64
string is approximately 1.4 times the size of the processed binary data.</p>
</li>
</ul>
<p>A format character may be preceded by an integral repeat count.  For example,
the format string <code>'4h'</code> means exactly the same as <code>'hhhh'</code>.</p>
<p>Whitespace characters between formats are ignored; a count and its format
must not contain whitespace though.</p>
<p>When packing a value <code>x</code> using one of the integer formats (<code>'b'</code>,
<code>'B'</code>, <code>'h'</code>, <code>'H'</code>, <code>'i'</code>, <code>'I'</code>, <code>'l'</code>, <code>'L'</code>,
<code>'q'</code>, <code>'Q'</code>), if <code>x</code> is outside the valid range for that format, a type
error exception is raised.</p>
<p>For the <code>'?'</code> format character, the return value is either <code>true</code> or <code>false</code>.
When packing, the truish result value of the argument is used. Either 0 or 1
in the native or standard bool representation will be packed, and any
non-zero value will be <code>true</code> when unpacking.</p>
<h2 id="examples">Examples</h2>
<p>Note:
Native byte order examples (designated by the <code>'@'</code> format prefix or
lack of any prefix character) may not match what the reader's
machine produces as
that depends on the platform and compiler.</p>
<p>Pack and unpack integers of three different sizes, using big endian
ordering:</p>
<pre class="prettyprint source"><code>import { pack, unpack } from 'struct';

<p>pack(&quot;&gt;bhl&quot;, 1, 2, 3);  // &quot;\x01\x00\x02\x00\x00\x00\x03&quot;
unpack(&quot;&gt;bhl&quot;, &quot;\x01\x00\x02\x00\x00\x00\x03&quot;);  // [ 1, 2, 3 ]
</code></pre></p>
<p>Attempt to pack an integer which is too large for the defined field:</p>
<pre class="prettyprint source lang-bash"><code>$ ucode -lstruct -p 'struct.pack(&quot;>h&quot;, 99999)'
Type error: Format 'h' requires numeric argument between -32768 and 32767
In [-p argument], line 1, byte 24:

<p> <code>struct.pack(&amp;quot;&gt;h&amp;quot;, 99999)</code>
  Near here -------------^
</code></pre></p>
<p>Demonstrate the difference between <code>'s'</code> and <code>'c'</code> format characters:</p>
<pre class="prettyprint source"><code>import { pack } from 'struct';

<p>pack(&quot;@ccc&quot;, &quot;1&quot;, &quot;2&quot;, &quot;3&quot;);  // &quot;123&quot;
pack(&quot;@3s&quot;, &quot;123&quot;);           // &quot;123&quot;
</code></pre></p>
<p>The ordering of format characters may have an impact on size in native
mode since padding is implicit. In standard mode, the user is
responsible for inserting any desired padding.</p>
<p>Note in the first <code>pack()</code> call below that three NUL bytes were added after
the packed <code>'#'</code> to align the following integer on a four-byte boundary.
In this example, the output was produced on a little endian machine:</p>
<pre class="prettyprint source"><code>import { pack } from 'struct';

<p>pack(&quot;@ci&quot;, &quot;#&quot;, 0x12131415);  // &quot;#\x00\x00\x00\x15\x14\x13\x12&quot;
pack(&quot;@ic&quot;, 0x12131415, &quot;#&quot;);  // &quot;\x15\x14\x13\x12#&quot;
</code></pre></p>
<p>The following format <code>'ih0i'</code> results in two pad bytes being added at the
end, assuming the platform's ints are aligned on 4-byte boundaries:</p>
<pre class="prettyprint source"><code>import { pack } from 'struct';

<p>pack(&quot;ih0i&quot;, 0x01010101, 0x0202);  // &quot;\x01\x01\x01\x01\x02\x02\x00\x00&quot;
</code></pre></p>
<p>Use the wildcard format to extract the remainder of the input data:</p>
<pre class="prettyprint source"><code>import { unpack } from 'struct';

<p>unpack(&quot;ccc*&quot;, &quot;foobarbaz&quot;);   // [ &quot;f&quot;, &quot;o&quot;, &quot;o&quot;, &quot;barbaz&quot; ]
unpack(&quot;ccc3*&quot;, &quot;foobarbaz&quot;);  // [ &quot;f&quot;, &quot;o&quot;, &quot;o&quot;, &quot;bar&quot; ]
</code></pre></p>
<p>Use the wildcard format to pack binary stings as-is into the result data:</p>
<pre class="prettyprint source"><code>import { pack } from 'struct';

<p>pack(&quot;h<em>h&quot;, 0x0101, &quot;\x02\x00\x03&quot;, 0x0404);  // &quot;\x01\x01\x02\x00\x03\x04\x04&quot;
pack(&quot;c3</em>c&quot;, &quot;a&quot;, &quot;foobar&quot;, &quot;c&quot;);  // &quot;afooc&quot;
</code></pre></p>
</dd>
<dt><a href="#module_ubus">ubus</a></dt>
<dd><h1 id="ubus-ipc">Ubus IPC</h1>
<p>The <code>ubus</code> module provides functions for OpenWrt inter-process
communication, including access to ubus registered modules and their
methods, as well as monitoring and publish/subscribe activity on the
ubus message bus.</p>
<p>Functions can be individually imported using named import syntax:</p>
<pre class="prettyprint source language-javascript"><code>import { connect } from 'ubus';

<p>const ubus = connect();
const result = ubus.call(&quot;session&quot;, &quot;get&quot;, { key: &quot;value&quot; });
</code></pre></p>
<p>Alternatively, the module namespace can be imported using a wildcard
import:</p>
<pre class="prettyprint source lang-js"><code>import * as ubus from 'ubus';

<p>const ctx = ubus.connect();
</code></pre></p>
<p>The <code>ubus</code> module may also be loaded via the <code>-lubus</code> interpreter switch.</p>
<h2 id="architecture">Architecture</h2>
<p>Ubus uses a broker pattern architecture with three main components:</p>
<ul>
<li><strong><code>ubusd</code></strong>: The central message router/broker that manages
registrations and forwards messages between objects</li>
<li><strong>Server objects</strong>: Interfaces/daemons that register methods for
clients to call</li>
<li><strong>Client objects</strong>: Callers that invoke server object methods</li>
</ul>
<p>All connections go through <code>ubusd</code>, significantly reducing the number
of IPC connections compared to traditional client-server models.</p>
<h2 id="communication-schemes">Communication Schemes</h2>
<p>Ubus provides three delivery schemes for IPC:</p>
<ol>
<li><strong>Invoke</strong> (one-to-one): Direct method calls to a specific object
by ID</li>
<li><strong>Subscribe/Notify</strong> (one-to-many, group by object): Notifications
sent to all subscribers of a particular object</li>
<li><strong>Event Broadcast</strong> (one-to-many, group by event): Events broadcast
to all listeners registered for a matching event pattern</li>
</ol>
<h2 id="roles-in-ubus">Roles in Ubus</h2>
<ul>
<li><strong>Object</strong>: Process registered to <code>ubusd</code>, including services and
service callers</li>
<li><strong>Method</strong>: Procedures provided by objects; servers can provide
multiple methods</li>
<li><strong>Data</strong>: Information in JSON format carried by requests or replies</li>
<li><strong>Subscriber</strong>: Object subscribed to a target service; notified when
the target sends notifications</li>
<li><strong>Event</strong>: Identified by a string event pattern; objects can register
to events and send data with matching patterns</li>
<li><strong>Event Registrant</strong>: Object registered to an event pattern; receives
forwarded data when matching messages are received</li>
</ul>
<h2 id="data-format">Data Format</h2>
<p>All data is transferred in JSON format via <code>blobmsg</code>. Method calls,
requests, and replies all use JSON for data serialization.</p>
<h2 id="usage-examples">Usage Examples</h2>
<h3 id="basic-connection-and-method-call">Basic connection and method call</h3>
<pre class="prettyprint source lang-js"><code>const ubus = require(&quot;ubus&quot;);

<p>// Connect to ubus and call a method
const conn = ubus.connect();
if (conn) {
    const result = conn.call(&quot;network.interface&quot;, &quot;status&quot;, {});
    printf(&quot;Interface status: %.J\n&quot;, result);
    conn.disconnect();
}
</code></pre></p>
<h3 id="asynchronous-method-invocation-with-callback">Asynchronous method invocation with callback</h3>
<pre class="prettyprint source lang-js"><code>const ubus = require(&quot;ubus&quot;);

<p>// Typical pattern: async call with callback
const conn = ubus.connect();</p>
<p>conn.defer(&quot;some.object&quot;, &quot;some_method&quot;, {}, (rc, result) =&gt; {
    if (rc == 0) {
        printf(&quot;Result: %.J\n&quot;, result);
    }
});
</code></pre></p>
<h3 id="persistent-connection-pattern">Persistent connection pattern</h3>
<pre class="prettyprint source lang-js"><code>const ubus = require(&quot;ubus&quot;);

<p>// Keep connection alive to prevent GC
const ubus_conn = ubus.connect();</p>
<p>function handle_request(request) {
    ubus_conn.defer(&quot;some.object&quot;, &quot;some_method&quot;, {}, (rc, data) =&gt; {
        request.reply({ result: data });
    });
}
</code></pre></p>
<h3 id="publishing-an-object">Publishing an object</h3>
<pre class="prettyprint source lang-js"><code>const ubus = require(&quot;ubus&quot;);

<p>const conn = ubus.connect();
const obj = conn.publish(&quot;my.service&quot;, {
    &quot;hello&quot;: (req, msg) =&gt; {
        req.reply({ message: &quot;Hello from &quot; + msg.name });
    }
});
</code></pre></p>
<h3 id="event-broadcasting">Event broadcasting</h3>
<pre class="prettyprint source lang-js"><code>const ubus = require(&quot;ubus&quot;);

<p>const conn = ubus.connect();</p>
<p>// Register as event listener
const listener = conn.listener(&quot;my.event.*&quot;, (pattern, data) =&gt; {
    printf(&quot;Received event: %s %.J\n&quot;, pattern, data);
});</p>
<p>// Send an event
conn.event(&quot;my.event.test&quot;, { data: &quot;test payload&quot; });
</code></pre></p>
</dd>
<dt><a href="#module_uci">uci</a></dt>
<dd><h1 id="openwrt-uci-configuration">OpenWrt UCI configuration</h1>
<p>The <code>uci</code> module provides access to the native OpenWrt
[libuci](https://github.com/openwrt/uci) API for reading and
manipulating UCI configuration files.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { cursor } from 'uci';

<p>let ctx = cursor();
let hostname = ctx.get_first(&#39;system&#39;, &#39;system&#39;, &#39;hostname&#39;);
</code></pre></p>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as uci from 'uci';

<p>let ctx = uci.cursor();
let hostname = ctx.get_first(&#39;system&#39;, &#39;system&#39;, &#39;hostname&#39;);
</code></pre></p>
<p>Additionally, the uci module namespace may also be imported by invoking
the <code>ucode</code> interpreter with the <code>-luci</code> switch.</p></dd>
<dt><a href="#module_uloop">uloop</a></dt>
<dd><h1 id="openwrt-uloop-event-loop">OpenWrt uloop event loop</h1>
<p>The <code>uloop</code> binding provides functions for integrating with the OpenWrt
[uloop library](https://github.com/openwrt/libubox/blob/master/uloop.h).</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source lang-javascript"><code>import { init, handle, timer, interval, process, signal, task, run } from 'uloop';

<p>init();</p>
<p>handle(…);
timer(…);
interval(…);
process(…);
signal(…);
task(…);</p>
<p>run();
</code></pre></p>
<p>Alternatively, the module namespace can be imported using a wildcard import
statement:</p>
<pre class="prettyprint source lang-javascript"><code>import * as uloop from 'uloop';

<p>uloop.init();</p>
<p>uloop.handle(…);
uloop.timer(…);
uloop.interval(…);
uloop.process(…);
uloop.signal(…);
uloop.task(…);</p>
<p>uloop.run();
</code></pre></p>
<p>Additionally, the uloop binding namespace may also be imported by invoking
the <code>ucode</code> interpreter with the <code>-luloop</code> switch.</p></dd>
<dt><a href="#module_zlib">zlib</a></dt>
<dd><h1 id="zlib-bindings">Zlib bindings</h1>
<p>The <code>zlib</code> module provides single-call and stream-oriented functions for interacting with zlib data.</p></dd>
<dt><a href="#module_core">core</a></dt>
<dd><h1 id="builtin-functions">Builtin functions</h1>
<p>The core namespace is not an actual module but refers to the set of
builtin functions and properties available to <code>ucode</code> scripts.</p></dd>
</dl>

<a name="module_log"></a>

## log
<h1 id="system-logging-functions">System logging functions</h1>
<p>The <code>log</code> module provides bindings to the POSIX syslog functions <code>openlog()</code>,
<code>syslog()</code> and <code>closelog()</code> as well as - when available - the OpenWrt
specific ulog library functions.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { openlog, syslog, LOG_PID, LOG_USER, LOG_ERR } from 'log';

openlog(&quot;my-log-ident&quot;, LOG_PID, LOG_USER);
syslog(LOG_ERR, &quot;An error occurred!&quot;);

// OpenWrt specific ulog functions
import { ulog_open, ulog, ULOG_SYSLOG, LOG_DAEMON, LOG_INFO } from 'log';

ulog_open(ULOG_SYSLOG, LOG_DAEMON, &quot;my-log-ident&quot;);
ulog(LOG_INFO, &quot;The current epoch is %d&quot;, time());
</code></pre>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as log from 'log';

log.openlog(&quot;my-log-ident&quot;, log.LOG_PID, log.LOG_USER);
log.syslog(log.LOG_ERR, &quot;An error occurred!&quot;);

// OpenWrt specific ulog functions
log.ulog_open(log.ULOG_SYSLOG, log.LOG_DAEMON, &quot;my-log-ident&quot;);
log.ulog(log.LOG_INFO, &quot;The current epoch is %d&quot;, time());
</code></pre>
<p>Additionally, the log module namespace may also be imported by invoking the
<code>ucode</code> interpreter with the <code>-llog</code> switch.</p>
<h2 id="constants">Constants</h2>
<p>The <code>log</code> module declares a number of numeric constants to specify logging
facility, priority and option values, as well as ulog specific channels.</p>
<h3 id="syslog-options">Syslog Options</h3>
<table>
<thead>
<tr>
<th>Constant Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>LOG_PID</code></td>
<td>Include PID with each message.</td>
</tr>
<tr>
<td><code>LOG_CONS</code></td>
<td>Log to console if error occurs while sending to syslog.</td>
</tr>
<tr>
<td><code>LOG_NDELAY</code></td>
<td>Open the connection to the logger immediately.</td>
</tr>
<tr>
<td><code>LOG_ODELAY</code></td>
<td>Delay open until the first message is logged.</td>
</tr>
<tr>
<td><code>LOG_NOWAIT</code></td>
<td>Do not wait for child processes created during logging.</td>
</tr>
</tbody>
</table>
<h3 id="syslog-facilities">Syslog Facilities</h3>
<table>
<thead>
<tr>
<th>Constant Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>LOG_AUTH</code></td>
<td>Authentication/authorization messages.</td>
</tr>
<tr>
<td><code>LOG_AUTHPRIV</code></td>
<td>Private authentication messages.</td>
</tr>
<tr>
<td><code>LOG_CRON</code></td>
<td>Clock daemon (cron and at commands).</td>
</tr>
<tr>
<td><code>LOG_DAEMON</code></td>
<td>System daemons without separate facility values.</td>
</tr>
<tr>
<td><code>LOG_FTP</code></td>
<td>FTP server daemon.</td>
</tr>
<tr>
<td><code>LOG_KERN</code></td>
<td>Kernel messages.</td>
</tr>
<tr>
<td><code>LOG_LPR</code></td>
<td>Line printer subsystem.</td>
</tr>
<tr>
<td><code>LOG_MAIL</code></td>
<td>Mail system.</td>
</tr>
<tr>
<td><code>LOG_NEWS</code></td>
<td>Network news subsystem.</td>
</tr>
<tr>
<td><code>LOG_SYSLOG</code></td>
<td>Messages generated internally by syslogd.</td>
</tr>
<tr>
<td><code>LOG_USER</code></td>
<td>Generic user-level messages.</td>
</tr>
<tr>
<td><code>LOG_UUCP</code></td>
<td>UUCP subsystem.</td>
</tr>
<tr>
<td><code>LOG_LOCAL0</code></td>
<td>Local use 0 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL1</code></td>
<td>Local use 1 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL2</code></td>
<td>Local use 2 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL3</code></td>
<td>Local use 3 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL4</code></td>
<td>Local use 4 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL5</code></td>
<td>Local use 5 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL6</code></td>
<td>Local use 6 (custom facility).</td>
</tr>
<tr>
<td><code>LOG_LOCAL7</code></td>
<td>Local use 7 (custom facility).</td>
</tr>
</tbody>
</table>
<h3 id="syslog-priorities">Syslog Priorities</h3>
<table>
<thead>
<tr>
<th>Constant Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>LOG_EMERG</code></td>
<td>System is unusable.</td>
</tr>
<tr>
<td><code>LOG_ALERT</code></td>
<td>Action must be taken immediately.</td>
</tr>
<tr>
<td><code>LOG_CRIT</code></td>
<td>Critical conditions.</td>
</tr>
<tr>
<td><code>LOG_ERR</code></td>
<td>Error conditions.</td>
</tr>
<tr>
<td><code>LOG_WARNING</code></td>
<td>Warning conditions.</td>
</tr>
<tr>
<td><code>LOG_NOTICE</code></td>
<td>Normal, but significant, condition.</td>
</tr>
<tr>
<td><code>LOG_INFO</code></td>
<td>Informational message.</td>
</tr>
<tr>
<td><code>LOG_DEBUG</code></td>
<td>Debug-level message.</td>
</tr>
</tbody>
</table>
<h3 id="ulog-channels">Ulog channels</h3>
<table>
<thead>
<tr>
<th>Constant Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>ULOG_KMSG</code></td>
<td>Log messages to <code>/dev/kmsg</code> (dmesg).</td>
</tr>
<tr>
<td><code>ULOG_STDIO</code></td>
<td>Log messages to stdout.</td>
</tr>
<tr>
<td><code>ULOG_SYSLOG</code></td>
<td>Log messages to syslog.</td>
</tr>
</tbody>
</table>


* [log](#module_log)
    * _instance_
        * [.openlog([ident], [options], [facility])](#module_log+openlog) ⇒ <code>boolean</code>
        * [.syslog(priority, format, [...args])](#module_log+syslog) ⇒ <code>boolean</code>
        * [.closelog()](#module_log+closelog)
        * [.ulog_open([channel], [facility], [ident])](#module_log+ulog_open) ⇒ <code>boolean</code>
        * [.ulog(priority, format, [...args])](#module_log+ulog) ⇒ <code>boolean</code>
        * [.ulog_close()](#module_log+ulog_close)
        * [.ulog_threshold([priority])](#module_log+ulog_threshold) ⇒ <code>boolean</code>
        * [.INFO(format, [...args])](#module_log+INFO) ⇒ <code>boolean</code>
        * [.NOTE(format, [...args])](#module_log+NOTE) ⇒ <code>boolean</code>
        * [.WARN(format, [...args])](#module_log+WARN) ⇒ <code>boolean</code>
        * [.ERR(format, [...args])](#module_log+ERR) ⇒ <code>boolean</code>
        * [.openlog([ident], [options], [facility])](#module_log+openlog) ⇒ <code>boolean</code>
        * [.syslog(priority, format, [...args])](#module_log+syslog) ⇒ <code>boolean</code>
        * [.closelog()](#module_log+closelog)
        * [.ulog_open([channel], [facility], [ident])](#module_log+ulog_open) ⇒ <code>boolean</code>
        * [.ulog(priority, format, [...args])](#module_log+ulog) ⇒ <code>boolean</code>
        * [.ulog_close()](#module_log+ulog_close)
        * [.ulog_threshold([priority])](#module_log+ulog_threshold) ⇒ <code>boolean</code>
        * [.INFO(format, [...args])](#module_log+INFO) ⇒ <code>boolean</code>
        * [.NOTE(format, [...args])](#module_log+NOTE) ⇒ <code>boolean</code>
        * [.WARN(format, [...args])](#module_log+WARN) ⇒ <code>boolean</code>
        * [.ERR(format, [...args])](#module_log+ERR) ⇒ <code>boolean</code>
    * _static_
        * [.LogOption](#module_log.LogOption) : <code>enum</code>
        * [.LogFacility](#module_log.LogFacility) : <code>enum</code>
        * [.LogPriority](#module_log.LogPriority) : <code>enum</code>
        * [.UlogChannel](#module_log.UlogChannel) : <code>enum</code>
        * [.LogOption](#module_log.LogOption) : <code>enum</code>
        * [.LogFacility](#module_log.LogFacility) : <code>enum</code>
        * [.LogPriority](#module_log.LogPriority) : <code>enum</code>
        * [.UlogChannel](#module_log.UlogChannel) : <code>enum</code>

<a name="module_log+openlog"></a>

### log.openlog([ident], [options], [facility]) ⇒ <code>boolean</code>
<p>Open connection to system logger.</p>
<p>The <code>openlog()</code> function instructs the program to establish a connection to
the system log service and configures the default facility and identification
for use in subsequent log operations. It may be omitted, in which case the
first call to <code>syslog()</code> will implicitly call <code>openlog()</code> with a default
ident value representing the program name and a default <code>LOG_USER</code> facility.</p>
<p>The log option argument may be either a single string value containing an
option name, an array of option name strings or a numeric value representing
a bitmask of <code>LOG_*</code> option constants.</p>
<p>The facility argument may be either a single string value containing a
facility name or one of the numeric <code>LOG_*</code> facility constants in the module
namespace.</p>
<p>Returns <code>true</code> if the system <code>openlog()</code> function was invoked.</p>
<p>Returns <code>false</code> if an invalid argument, such as an unrecognized option or
facility name, was provided.</p>

**Kind**: instance method of [<code>log</code>](#module_log)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [ident] | <code>string</code> |  | <p>A string identifying the program name. If omitted, the name of the calling process is used by default.</p> |
| [options] | <code>number</code> \| [<code>LogOption</code>](#module_log.LogOption) \| [<code>Array.&lt;LogOption&gt;</code>](#module_log.LogOption) |  | <p>Logging options to use.</p> <p>See [LogOption](#module_log.LogOption) for recognized option names.</p> |
| [facility] | <code>number</code> \| [<code>LogFacility</code>](#module_log.LogFacility) | <code>&quot;user&quot;</code> | <p>The facility to use for log messages generated by subsequent syslog calls.</p> <p>See [LogFacility](#module_log.LogFacility) for recognized facility names.</p> |

**Example**  
```js
// Example usage of openlog function
openlog("myapp", LOG_PID | LOG_NDELAY, LOG_LOCAL0);

// Using option names instead of bitmask and LOG_USER facility
openlog("myapp", [ "pid", "ndelay" ], "user");
```
<a name="module_log+syslog"></a>

### log.syslog(priority, format, [...args]) ⇒ <code>boolean</code>
<p>Log a message to the system logger.</p>
<p>This function logs a message to the system logger. The function behaves in a
sprintf-like manner, allowing the use of format strings and associated
arguments to construct log messages.</p>
<p>If the <code>openlog</code> function has not been called explicitly before, <code>syslog()</code>
implicitly calls <code>openlog()</code>, using a default ident and <code>LOG_USER</code> facility
value before logging the message.</p>
<p>If the <code>format</code> argument is not a string and not <code>null</code>, it will be
implicitly converted to a string and logged as-is, without further format
string processing.</p>
<p>Returns <code>true</code> if a message was passed to the system <code>syslog()</code> function.</p>
<p>Returns <code>false</code> if an invalid priority value or an empty message was given.</p>

**Kind**: instance method of [<code>log</code>](#module_log)  

| Param | Type | Description |
| --- | --- | --- |
| priority | <code>number</code> \| [<code>LogPriority</code>](#module_log.LogPriority) | <p>Log message priority. May be either a number value (potentially bitwise OR-ed with a log facility constant) which is passed as-is to the system <code>syslog()</code> function or a priority name string.</p> <p>See [LogPriority](#module_log.LogPriority) for recognized priority names.</p> |
| format | <code>\*</code> | <p>The sprintf-like format string for the log message, or any other, non-null, non-string value type which will be implicitly stringified and logged as-is.</p> |
| [...args] | <code>\*</code> | <p>In case a format string value was provided in the previous argument, then all subsequent arguments are used to replace the placeholders in the format string.</p> |

**Example**  
```js
// Example usage of syslog function with format string and arguments
const username = "user123";
const errorCode = 404;
syslog(LOG_ERR, "User %s encountered error: %d", username, errorCode);

// If openlog has not been called explicitly, it is implicitly called with defaults:
syslog(LOG_INFO, "This message will be logged with default settings.");

// Selectively override used facility by OR-ing numeric constant
const password =" secret";
syslog(LOG_DEBUG|LOG_AUTHPRIV, "The password %s has been wrong", secret);

// Using priority names for logging
syslog("emerg", "System shutdown imminent!");

// Implicit stringification
syslog("debug", { foo: 1, bar: true, baz: [1, 2, 3] });
```
<a name="module_log+closelog"></a>

### log.closelog()
<p>Close connection to system logger.</p>
<p>The usage of this function is optional, and usually an explicit log
connection tear down is not required.</p>

**Kind**: instance method of [<code>log</code>](#module_log)  
<a name="module_log+ulog_open"></a>

### log.ulog\_open([channel], [facility], [ident]) ⇒ <code>boolean</code>
<p>Configure ulog logger.</p>
<p>This functions configures the ulog mechanism and is analogous to using the
<code>openlog()</code> function in conjunction with <code>syslog()</code>.</p>
<p>The <code>ulog_open()</code> function is OpenWrt specific and may not be present on
other systems. Use <code>openlog()</code> and <code>syslog()</code> instead for portability to
non-OpenWrt environments.</p>
<p>A program may use multiple channels to simultaneously output messages using
different means. The channel argument may either be a single string value
containing a channel name, an array of channel names or a numeric value
representing a bitmask of <code>ULOG_*</code> channel constants.</p>
<p>The facility argument may be either a single string value containing a
facility name or one of the numeric <code>LOG_*</code> facility constants in the module
namespace.</p>
<p>The default facility value varies, depending on the execu
