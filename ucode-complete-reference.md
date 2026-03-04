# ucode Complete API Reference

> **Source:** https://github.com/jow-/ucode (commit: `e87be9d`)
> **Live docs:** https://ucode.mein.io/
> **Generated:** 2026-03-04 13:27 UTC
> **Standalone use:** This file is self-contained. TOC links use
> in-page anchors. Cross-reference links point to the modular
> ucode-docs/ files; the linked content is also embedded in this file.

ucode is a tiny ECMAScript-like scripting language for OpenWrt system
scripting. Provides bindings for ubus, uci, uloop, netlink, and other
OpenWrt APIs. Synchronous, procedural, no OOP standard library.

---

## Table of Contents

- [ucode module: `debug`](#ucode-module-debug)
- [ucode module: `digest`](#ucode-module-digest)
- [ucode module: `fs`](#ucode-module-fs)
- [ucode module: `io`](#ucode-module-io)
- [ucode module: `log`](#ucode-module-log)
- [ucode module: `math`](#ucode-module-math)
- [ucode module: `nl80211`](#ucode-module-nl80211)
- [ucode module: `resolv`](#ucode-module-resolv)
- [ucode module: `rtnl`](#ucode-module-rtnl)
- [ucode module: `socket`](#ucode-module-socket)
- [ucode module: `struct`](#ucode-module-struct)
- [ucode module: `ubus`](#ucode-module-ubus)
- [ucode module: `uci`](#ucode-module-uci)
- [ucode module: `uloop`](#ucode-module-uloop)
- [ucode module: `zlib`](#ucode-module-zlib)

---

<a id="ucode-module-debug"></a>
# ucode module: `debug`

> **Source:** [`lib/debug.c`](https://github.com/jow-/ucode/blob/master/lib/debug.c)
> **Live docs:** https://ucode.mein.io/module-debug.html
> **Generated:** 2026-03-04 13:26 UTC from commit `e87be9d`

---

## Modules

<dl>
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

<a name="module_debug"></a>

## debug
<h1 id="debugger-module">Debugger Module</h1>
<p>This module provides runtime debug functionality for ucode scripts.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { memdump, traceback } from 'debug';

let stacktrace = traceback(1);

memdump(&quot;/tmp/dump.txt&quot;);
</code></pre>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as debug from 'debug';

let stacktrace = debug.traceback(1);

debug.memdump(&quot;/tmp/dump.txt&quot;);
</code></pre>
<p>Additionally, the debug module namespace may also be imported by invoking the
<code>ucode</code> interpreter with the <code>-ldebug</code> switch.</p>
<p>Upon loading, the <code>debug</code> module will register a <code>SIGUSR2</code> signal handler
which, upon receipt of the signal, will write a memory dump of the currently
running program to <code>/tmp/ucode.$timestamp.$pid.memdump</code>. This default
behavior can be inhibited by setting the <code>UCODE_DEBUG_MEMDUMP_ENABLED</code>
environment variable to <code>0</code> when starting the process. The memory dump signal
and output directory can be overridden with the <code>UCODE_DEBUG_MEMDUMP_SIGNAL</code>
and <code>UCODE_DEBUG_MEMDUMP_PATH</code> environment variables respectively.</p>


* [debug](#module_debug)
    * _instance_
        * [.memdump(file)](#module_debug+memdump) ⇒ <code>boolean</code>
        * [.traceback([level])](#module_debug+traceback) ⇒ [<code>Array.&lt;StackTraceEntry&gt;</code>](#module_debug.StackTraceEntry)
        * [.sourcepos()](#module_debug+sourcepos) ⇒ [<code>SourcePosition</code>](#module_debug.SourcePosition)
        * [.getinfo(value)](#module_debug+getinfo) ⇒ [<code>ValueInformation</code>](#module_debug.ValueInformation)
        * [.getlocal([level], variable)](#module_debug+getlocal) ⇒ [<code>LocalInfo</code>](#module_debug.LocalInfo)
        * [.setlocal([level], variable, [value])](#module_debug+setlocal) ⇒ [<code>LocalInfo</code>](#module_debug.LocalInfo)
        * [.getupval(target, variable)](#module_debug+getupval) ⇒ [<code>UpvalInfo</code>](#module_debug.UpvalInfo)
        * [.setupval(target, variable, value)](#module_debug+setupval) ⇒ [<code>UpvalInfo</code>](#module_debug.UpvalInfo)
        * [.memdump(file)](#module_debug+memdump) ⇒ <code>boolean</code>
        * [.traceback([level])](#module_debug+traceback) ⇒ [<code>Array.&lt;StackTraceEntry&gt;</code>](#module_debug.StackTraceEntry)
        * [.sourcepos()](#module_debug+sourcepos) ⇒ [<code>SourcePosition</code>](#module_debug.SourcePosition)
        * [.getinfo(value)](#module_debug+getinfo) ⇒ [<code>ValueInformation</code>](#module_debug.ValueInformation)
        * [.getlocal([level], variable)](#module_debug+getlocal) ⇒ [<code>LocalInfo</code>](#module_debug.LocalInfo)
        * [.setlocal([level], variable, [value])](#module_debug+setlocal) ⇒ [<code>LocalInfo</code>](#module_debug.LocalInfo)
        * [.getupval(target, variable)](#module_debug+getupval) ⇒ [<code>UpvalInfo</code>](#module_debug.UpvalInfo)
        * [.setupval(target, variable, value)](#module_debug+setupval) ⇒ [<code>UpvalInfo</code>](#module_debug.UpvalInfo)
    * _static_
        * [.StackTraceEntry](#module_debug.StackTraceEntry) : <code>Object</code>
        * [.SourcePosition](#module_debug.SourcePosition) : <code>Object</code>
        * [.UpvalRef](#module_debug.UpvalRef) : <code>Object</code>
        * [.ValueInformation](#module_debug.ValueInformation) : <code>Object</code>
        * [.LocalInfo](#module_debug.LocalInfo) : <code>Object</code>
        * [.UpvalInfo](#module_debug.UpvalInfo) : <code>Object</code>
        * [.StackTraceEntry](#module_debug.StackTraceEntry) : <code>Object</code>
        * [.SourcePosition](#module_debug.SourcePosition) : <code>Object</code>
        * [.UpvalRef](#module_debug.UpvalRef) : <code>Object</code>
        * [.ValueInformation](#module_debug.ValueInformation) : <code>Object</code>
        * [.LocalInfo](#module_debug.LocalInfo) : <code>Object</code>
        * [.UpvalInfo](#module_debug.UpvalInfo) : <code>Object</code>

<a name="module_debug+memdump"></a>

### debug.memdump(file) ⇒ <code>boolean</code>
<p>Write a memory dump report to the given file.</p>
<p>This function generates a human readable memory dump of ucode values
currently managed by the running VM which is useful to track down logical
memory leaks in scripts.</p>
<p>The file parameter can be either a string value containing a file path, in
which case this function tries to create and write the report file at the
given location, or an already open file handle this function should write to.</p>
<p>Returns <code>true</code> if the report has been written.</p>
<p>Returns <code>null</code> if the file could not be opened or if the handle was invalid.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Description |
| --- | --- | --- |
| file | <code>string</code> \| [<code>file</code>](#module_fs.file) \| [<code>proc</code>](#module_fs.proc) | <p>The file path or open file handle to write report to.</p> |

<a name="module_debug+traceback"></a>

### debug.traceback([level]) ⇒ [<code>Array.&lt;StackTraceEntry&gt;</code>](#module_debug.StackTraceEntry)
<p>Capture call stack trace.</p>
<p>This function captures the current call stack and returns it. The optional
level parameter controls how many calls up the trace should start. It
defaults to <code>1</code>, that is the function calling this <code>traceback()</code> function.</p>
<p>Returns an array of stack trace entries describing the function invocations
up to the point where <code>traceback()</code> is called.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [level] | <code>number</code> | <code>1</code> | <p>The number of callframes up the call trace should start, <code>0</code> is this function itself, <code>1</code> the function calling it and so on.</p> |

<a name="module_debug+sourcepos"></a>

### debug.sourcepos() ⇒ [<code>SourcePosition</code>](#module_debug.SourcePosition)
<p>Obtain information about the current source position.</p>
<p>The <code>sourcepos()</code> function determines the source code position of the
current instruction invoking this function.</p>
<p>Returns a dictionary containing the filename, line number and line byte
offset of the call site.</p>
<p>Returns <code>null</code> if this function was invoked from C code.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  
<a name="module_debug+getinfo"></a>

### debug.getinfo(value) ⇒ [<code>ValueInformation</code>](#module_debug.ValueInformation)
<p>Obtain information about the given value.</p>
<p>The <code>getinfo()</code> function allows querying internal information about the
given ucode value, such as the current reference count, the mark bit state
etc.</p>
<p>Returns a dictionary with value type specific details.</p>
<p>Returns <code>null</code> if a <code>null</code> value was provided.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Description |
| --- | --- | --- |
| value | <code>\*</code> | <p>The value to query information for.</p> |

<a name="module_debug+getlocal"></a>

### debug.getlocal([level], variable) ⇒ [<code>LocalInfo</code>](#module_debug.LocalInfo)
<p>Obtain local variable.</p>
<p>The <code>getlocal()</code> function retrieves information about the specified local
variable at the given call stack depth.</p>
<p>The call stack depth specifies the amount of levels up local variables should
be queried. A value of <code>0</code> refers to this <code>getlocal()</code> function call itself,
<code>1</code> to the function calling <code>getlocal()</code> and so on.</p>
<p>The variable to query might be either specified by name or by its index with
index numbers following the source code declaration order.</p>
<p>Returns a dictionary holding information about the given variable.</p>
<p>Returns <code>null</code> if the stack depth exceeds the size of the current call stack.</p>
<p>Returns <code>null</code> if the invocation at the given stack depth is a C call.</p>
<p>Returns <code>null</code> if the given variable name is not found or the given variable
index is invalid.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [level] | <code>number</code> | <code>1</code> | <p>The amount of call stack levels up local variables should be queried.</p> |
| variable | <code>string</code> \| <code>number</code> |  | <p>The variable index or variable name to obtain information for.</p> |

<a name="module_debug+setlocal"></a>

### debug.setlocal([level], variable, [value]) ⇒ [<code>LocalInfo</code>](#module_debug.LocalInfo)
<p>Set local variable.</p>
<p>The <code>setlocal()</code> function manipulates the value of the specified local
variable at the given call stack depth.</p>
<p>The call stack depth specifies the amount of levels up local variables should
be updated. A value of <code>0</code> refers to this <code>setlocal()</code> function call itself,
<code>1</code> to the function calling <code>setlocal()</code> and so on.</p>
<p>The variable to update might be either specified by name or by its index with
index numbers following the source code declaration order.</p>
<p>Returns a dictionary holding information about the updated variable.</p>
<p>Returns <code>null</code> if the stack depth exceeds the size of the current call stack.</p>
<p>Returns <code>null</code> if the invocation at the given stack depth is a C call.</p>
<p>Returns <code>null</code> if the given variable name is not found or the given variable
index is invalid.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [level] | <code>number</code> | <code>1</code> | <p>The amount of call stack levels up local variables should be updated.</p> |
| variable | <code>string</code> \| <code>number</code> |  | <p>The variable index or variable name to update.</p> |
| [value] | <code>\*</code> | <code></code> | <p>The value to set the local variable to.</p> |

<a name="module_debug+getupval"></a>

### debug.getupval(target, variable) ⇒ [<code>UpvalInfo</code>](#module_debug.UpvalInfo)
<p>Obtain captured variable (upvalue).</p>
<p>The <code>getupval()</code> function retrieves information about the specified captured
variable associated with the given function value or the invoked function at
the given call stack depth.</p>
<p>The call stack depth specifies the amount of levels up the function should be
selected to query associated captured variables for. A value of <code>0</code> refers to
this <code>getupval()</code> function call itself, <code>1</code> to the function calling
<code>getupval()</code> and so on.</p>
<p>The variable to query might be either specified by name or by its index with
index numbers following the source code declaration order.</p>
<p>Returns a dictionary holding information about the given variable.</p>
<p>Returns <code>null</code> if the given function value is not a closure.</p>
<p>Returns <code>null</code> if the stack depth exceeds the size of the current call stack.</p>
<p>Returns <code>null</code> if the invocation at the given stack depth is not a closure.</p>
<p>Returns <code>null</code> if the given variable name is not found or the given variable
index is invalid.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Description |
| --- | --- | --- |
| target | <code>function</code> \| <code>number</code> | <p>Either a function value referring to a closure to query upvalues for or a stack depth number selecting a closure that many levels up.</p> |
| variable | <code>string</code> \| <code>number</code> | <p>The variable index or variable name to obtain information for.</p> |

<a name="module_debug+setupval"></a>

### debug.setupval(target, variable, value) ⇒ [<code>UpvalInfo</code>](#module_debug.UpvalInfo)
<p>Set upvalue.</p>
<p>The <code>setupval()</code> function manipulates the value of the specified captured
variable associated with the given function value or the invoked function at
the given call stack depth.</p>
<p>The call stack depth specifies the amount of levels up the function should be
selected to update associated captured variables for. A value of <code>0</code> refers
to this <code>setupval()</code> function call itself, <code>1</code> to the function calling
<code>setupval()</code> and so on.</p>
<p>The variable to update might be either specified by name or by its index with
index numbers following the source code declaration order.</p>
<p>Returns a dictionary holding information about the updated variable.</p>
<p>Returns <code>null</code> if the given function value is not a closure.</p>
<p>Returns <code>null</code> if the stack depth exceeds the size of the current call stack.</p>
<p>Returns <code>null</code> if the invocation at the given stack depth is not a closure.</p>
<p>Returns <code>null</code> if the given variable name is not found or the given variable
index is invalid.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Description |
| --- | --- | --- |
| target | <code>function</code> \| <code>number</code> | <p>Either a function value referring to a closure to update upvalues for or a stack depth number selecting a closure that many levels up.</p> |
| variable | <code>string</code> \| <code>number</code> | <p>The variable index or variable name to update.</p> |
| value | <code>\*</code> | <p>The value to set the variable to.</p> |

<a name="module_debug+memdump"></a>

### debug.memdump(file) ⇒ <code>boolean</code>
<p>Write a memory dump report to the given file.</p>
<p>This function generates a human readable memory dump of ucode values
currently managed by the running VM which is useful to track down logical
memory leaks in scripts.</p>
<p>The file parameter can be either a string value containing a file path, in
which case this function tries to create and write the report file at the
given location, or an already open file handle this function should write to.</p>
<p>Returns <code>true</code> if the report has been written.</p>
<p>Returns <code>null</code> if the file could not be opened or if the handle was invalid.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Description |
| --- | --- | --- |
| file | <code>string</code> \| [<code>file</code>](#module_fs.file) \| [<code>proc</code>](#module_fs.proc) | <p>The file path or open file handle to write report to.</p> |

<a name="module_debug+traceback"></a>

### debug.traceback([level]) ⇒ [<code>Array.&lt;StackTraceEntry&gt;</code>](#module_debug.StackTraceEntry)
<p>Capture call stack trace.</p>
<p>This function captures the current call stack and returns it. The optional
level parameter controls how many calls up the trace should start. It
defaults to <code>1</code>, that is the function calling this <code>traceback()</code> function.</p>
<p>Returns an array of stack trace entries describing the function invocations
up to the point where <code>traceback()</code> is called.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [level] | <code>number</code> | <code>1</code> | <p>The number of callframes up the call trace should start, <code>0</code> is this function itself, <code>1</code> the function calling it and so on.</p> |

<a name="module_debug+sourcepos"></a>

### debug.sourcepos() ⇒ [<code>SourcePosition</code>](#module_debug.SourcePosition)
<p>Obtain information about the current source position.</p>
<p>The <code>sourcepos()</code> function determines the source code position of the
current instruction invoking this function.</p>
<p>Returns a dictionary containing the filename, line number and line byte
offset of the call site.</p>
<p>Returns <code>null</code> if this function was invoked from C code.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  
<a name="module_debug+getinfo"></a>

### debug.getinfo(value) ⇒ [<code>ValueInformation</code>](#module_debug.ValueInformation)
<p>Obtain information about the given value.</p>
<p>The <code>getinfo()</code> function allows querying internal information about the
given ucode value, such as the current reference count, the mark bit state
etc.</p>
<p>Returns a dictionary with value type specific details.</p>
<p>Returns <code>null</code> if a <code>null</code> value was provided.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Description |
| --- | --- | --- |
| value | <code>\*</code> | <p>The value to query information for.</p> |

<a name="module_debug+getlocal"></a>

### debug.getlocal([level], variable) ⇒ [<code>LocalInfo</code>](#module_debug.LocalInfo)
<p>Obtain local variable.</p>
<p>The <code>getlocal()</code> function retrieves information about the specified local
variable at the given call stack depth.</p>
<p>The call stack depth specifies the amount of levels up local variables should
be queried. A value of <code>0</code> refers to this <code>getlocal()</code> function call itself,
<code>1</code> to the function calling <code>getlocal()</code> and so on.</p>
<p>The variable to query might be either specified by name or by its index with
index numbers following the source code declaration order.</p>
<p>Returns a dictionary holding information about the given variable.</p>
<p>Returns <code>null</code> if the stack depth exceeds the size of the current call stack.</p>
<p>Returns <code>null</code> if the invocation at the given stack depth is a C call.</p>
<p>Returns <code>null</code> if the given variable name is not found or the given variable
index is invalid.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [level] | <code>number</code> | <code>1</code> | <p>The amount of call stack levels up local variables should be queried.</p> |
| variable | <code>string</code> \| <code>number</code> |  | <p>The variable index or variable name to obtain information for.</p> |

<a name="module_debug+setlocal"></a>

### debug.setlocal([level], variable, [value]) ⇒ [<code>LocalInfo</code>](#module_debug.LocalInfo)
<p>Set local variable.</p>
<p>The <code>setlocal()</code> function manipulates the value of the specified local
variable at the given call stack depth.</p>
<p>The call stack depth specifies the amount of levels up local variables should
be updated. A value of <code>0</code> refers to this <code>setlocal()</code> function call itself,
<code>1</code> to the function calling <code>setlocal()</code> and so on.</p>
<p>The variable to update might be either specified by name or by its index with
index numbers following the source code declaration order.</p>
<p>Returns a dictionary holding information about the updated variable.</p>
<p>Returns <code>null</code> if the stack depth exceeds the size of the current call stack.</p>
<p>Returns <code>null</code> if the invocation at the given stack depth is a C call.</p>
<p>Returns <code>null</code> if the given variable name is not found or the given variable
index is invalid.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [level] | <code>number</code> | <code>1</code> | <p>The amount of call stack levels up local variables should be updated.</p> |
| variable | <code>string</code> \| <code>number</code> |  | <p>The variable index or variable name to update.</p> |
| [value] | <code>\*</code> | <code></code> | <p>The value to set the local variable to.</p> |

<a name="module_debug+getupval"></a>

### debug.getupval(target, variable) ⇒ [<code>UpvalInfo</code>](#module_debug.UpvalInfo)
<p>Obtain captured variable (upvalue).</p>
<p>The <code>getupval()</code> function retrieves information about the specified captured
variable associated with the given function value or the invoked function at
the given call stack depth.</p>
<p>The call stack depth specifies the amount of levels up the function should be
selected to query associated captured variables for. A value of <code>0</code> refers to
this <code>getupval()</code> function call itself, <code>1</code> to the function calling
<code>getupval()</code> and so on.</p>
<p>The variable to query might be either specified by name or by its index with
index numbers following the source code declaration order.</p>
<p>Returns a dictionary holding information about the given variable.</p>
<p>Returns <code>null</code> if the given function value is not a closure.</p>
<p>Returns <code>null</code> if the stack depth exceeds the size of the current call stack.</p>
<p>Returns <code>null</code> if the invocation at the given stack depth is not a closure.</p>
<p>Returns <code>null</code> if the given variable name is not found or the given variable
index is invalid.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Description |
| --- | --- | --- |
| target | <code>function</code> \| <code>number</code> | <p>Either a function value referring to a closure to query upvalues for or a stack depth number selecting a closure that many levels up.</p> |
| variable | <code>string</code> \| <code>number</code> | <p>The variable index or variable name to obtain information for.</p> |

<a name="module_debug+setupval"></a>

### debug.setupval(target, variable, value) ⇒ [<code>UpvalInfo</code>](#module_debug.UpvalInfo)
<p>Set upvalue.</p>
<p>The <code>setupval()</code> function manipulates the value of the specified captured
variable associated with the given function value or the invoked function at
the given call stack depth.</p>
<p>The call stack depth specifies the amount of levels up the function should be
selected to update associated captured variables for. A value of <code>0</code> refers
to this <code>setupval()</code> function call itself, <code>1</code> to the function calling
<code>setupval()</code> and so on.</p>
<p>The variable to update might be either specified by name or by its index with
index numbers following the source code declaration order.</p>
<p>Returns a dictionary holding information about the updated variable.</p>
<p>Returns <code>null</code> if the given function value is not a closure.</p>
<p>Returns <code>null</code> if the stack depth exceeds the size of the current call stack.</p>
<p>Returns <code>null</code> if th


---

<a id="ucode-module-digest"></a>
# ucode module: `digest`

> **Source:** [`lib/digest.c`](https://github.com/jow-/ucode/blob/master/lib/digest.c)
> **Live docs:** https://ucode.mein.io/module-digest.html
> **Generated:** 2026-03-04 13:26 UTC from commit `e87be9d`

---

## Modules

<dl>
<dt><a href="#module_digest">digest</a></dt>
<dd><h1 id="digest-functions">Digest Functions</h1>
<p>The <code>digest</code> module bundles various digest functions.</p></dd>
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

<a name="module_digest"></a>

## digest
<h1 id="digest-functions">Digest Functions</h1>
<p>The <code>digest</code> module bundles various digest functions.</p>


* [digest](#module_digest)
    * [.md5(str)](#module_digest+md5) ⇒ <code>string</code>
    * [.sha1(str)](#module_digest+sha1) ⇒ <code>string</code>
    * [.sha256(str)](#module_digest+sha256) ⇒ <code>string</code>
    * [.md2(str)](#module_digest+md2) ⇒ <code>string</code>
    * [.md4(str)](#module_digest+md4) ⇒ <code>string</code>
    * [.sha384(str)](#module_digest+sha384) ⇒ <code>string</code>
    * [.sha512(str)](#module_digest+sha512) ⇒ <code>string</code>
    * [.md5_file(path)](#module_digest+md5_file) ⇒ <code>string</code>
    * [.sha1_file(path)](#module_digest+sha1_file) ⇒ <code>string</code>
    * [.sha256_file(path)](#module_digest+sha256_file) ⇒ <code>string</code>
    * [.md2_file(path)](#module_digest+md2_file) ⇒ <code>string</code>
    * [.md4_file(path)](#module_digest+md4_file) ⇒ <code>string</code>
    * [.sha384_file(path)](#module_digest+sha384_file) ⇒ <code>string</code>
    * [.sha512_file(path)](#module_digest+sha512_file) ⇒ <code>string</code>
    * [.md5(str)](#module_digest+md5) ⇒ <code>string</code>
    * [.sha1(str)](#module_digest+sha1) ⇒ <code>string</code>
    * [.sha256(str)](#module_digest+sha256) ⇒ <code>string</code>
    * [.md2(str)](#module_digest+md2) ⇒ <code>string</code>
    * [.md4(str)](#module_digest+md4) ⇒ <code>string</code>
    * [.sha384(str)](#module_digest+sha384) ⇒ <code>string</code>
    * [.sha512(str)](#module_digest+sha512) ⇒ <code>string</code>
    * [.md5_file(path)](#module_digest+md5_file) ⇒ <code>string</code>
    * [.sha1_file(path)](#module_digest+sha1_file) ⇒ <code>string</code>
    * [.sha256_file(path)](#module_digest+sha256_file) ⇒ <code>string</code>
    * [.md2_file(path)](#module_digest+md2_file) ⇒ <code>string</code>
    * [.md4_file(path)](#module_digest+md4_file) ⇒ <code>string</code>
    * [.sha384_file(path)](#module_digest+sha384_file) ⇒ <code>string</code>
    * [.sha512_file(path)](#module_digest+sha512_file) ⇒ <code>string</code>

<a name="module_digest+md5"></a>

### digest.md5(str) ⇒ <code>string</code>
<p>Calculates the MD5 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| str | <code>string</code> | <p>The string to hash.</p> |

**Example**  
```js
md5("This is a test");  // Returns "ce114e4501d2f4e2dcea3e17b546f339"
md5(123);               // Returns null
```
<a name="module_digest+sha1"></a>

### digest.sha1(str) ⇒ <code>string</code>
<p>Calculates the SHA1 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| str | <code>string</code> | <p>The string to hash.</p> |

**Example**  
```js
sha1("This is a test");  // Returns "a54d88e06612d820bc3be72877c74f257b561b19"
sha1(123);               // Returns null
```
<a name="module_digest+sha256"></a>

### digest.sha256(str) ⇒ <code>string</code>
<p>Calculates the SHA256 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| str | <code>string</code> | <p>The string to hash.</p> |

**Example**  
```js
sha256("This is a test");  // Returns "c7be1ed902fb8dd4d48997c6452f5d7e509fbcdbe2808b16bcf4edce4c07d14e"
sha256(123);               // Returns null
```
<a name="module_digest+md2"></a>

### digest.md2(str) ⇒ <code>string</code>
<p>Calculates the MD2 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| str | <code>string</code> | <p>The string to hash.</p> |

**Example**  
```js
md2("This is a test");  // Returns "dc378580fd0722e56b82666a6994c718"
md2(123);               // Returns null
```
<a name="module_digest+md4"></a>

### digest.md4(str) ⇒ <code>string</code>
<p>Calculates the MD4 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| str | <code>string</code> | <p>The string to hash.</p> |

**Example**  
```js
md4("This is a test");  // Returns "3b487cf6856af7e330bc4b1b7d977ef8"
md4(123);               // Returns null
```
<a name="module_digest+sha384"></a>

### digest.sha384(str) ⇒ <code>string</code>
<p>Calculates the SHA384 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| str | <code>string</code> | <p>The string to hash.</p> |

**Example**  
```js
sha384("This is a test");  // Returns "a27c7667e58200d4c0688ea136968404a0da366b1a9fc19bb38a0c7a609a1eef2bcc82837f4f4d92031a66051494b38c"
sha384(123);               // Returns null
```
<a name="module_digest+sha512"></a>

### digest.sha512(str) ⇒ <code>string</code>
<p>Calculates the SHA512 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| str | <code>string</code> | <p>The string to hash.</p> |

**Example**  
```js
sha512("This is a test");  // Returns "a028d4f74b602ba45eb0a93c9a4677240dcf281a1a9322f183bd32f0bed82ec72de9c3957b2f4c9a1ccf7ed14f85d73498df38017e703d47ebb9f0b3bf116f69"
sha512(123);               // Returns null
```
<a name="module_digest+md5_file"></a>

### digest.md5\_file(path) ⇒ <code>string</code>
<p>Calculates the MD5 hash of a given file and returns that hash.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the file.</p> |

<a name="module_digest+sha1_file"></a>

### digest.sha1\_file(path) ⇒ <code>string</code>
<p>Calculates the SHA1 hash of a given file and returns that hash.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the file.</p> |

<a name="module_digest+sha256_file"></a>

### digest.sha256\_file(path) ⇒ <code>string</code>
<p>Calculates the SHA256 hash of a given file and returns that hash.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the file.</p> |

<a name="module_digest+md2_file"></a>

### digest.md2\_file(path) ⇒ <code>string</code>
<p>Calculates the MD2 hash of a given file and returns that hash.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the file.</p> |

<a name="module_digest+md4_file"></a>

### digest.md4\_file(path) ⇒ <code>string</code>
<p>Calculates the MD4 hash of a given file and returns that hash.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the file.</p> |

<a name="module_digest+sha384_file"></a>

### digest.sha384\_file(path) ⇒ <code>string</code>
<p>Calculates the SHA384 hash of a given file and returns that hash.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the file.</p> |

<a name="module_digest+sha512_file"></a>

### digest.sha512\_file(path) ⇒ <code>string</code>
<p>Calculates the SHA512 hash of a given file and returns that hash.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the file.</p> |

<a name="module_digest+md5"></a>

### digest.md5(str) ⇒ <code>string</code>
<p>Calculates the MD5 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| str | <code>string</code> | <p>The string to hash.</p> |

**Example**  
```js
md5("This is a test");  // Returns "ce114e4501d2f4e2dcea3e17b546f339"
md5(123);               // Returns null
```
<a name="module_digest+sha1"></a>

### digest.sha1(str) ⇒ <code>string</code>
<p>Calculates the SHA1 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| str | <code>string</code> | <p>The string to hash.</p> |

**Example**  
```js
sha1("This is a test");  // Returns "a54d88e06612d820bc3be72877c74f257b561b19"
sha1(123);               // Returns null
```
<a name="module_digest+sha256"></a>

### digest.sha256(str) ⇒ <code>string</code>
<p>Calculates the SHA256 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| str | <code>string</code> | <p>The string to hash.</p> |

**Example**  
```js
sha256("This is a test");  // Returns "c7be1ed902fb8dd4d48997c6452f5d7e509fbcdbe2808b16bcf4edce4c07d14e"
sha256(123);               // Returns null
```
<a name="module_digest+md2"></a>

### digest.md2(str) ⇒ <code>string</code>
<p>Calculates the MD2 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| str | <code>string</code> | <p>The string to hash.</p> |

**Example**  
```js
md2("This is a test");  // Returns "dc378580fd0722e56b82666a6994c718"
md2(123);               // Returns null
```
<a name="module_digest+md4"></a>

### digest.md4(str) ⇒ <code>string</code>
<p>Calculates the MD4 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| str | <code>string</code> | <p>The string to hash.</p> |

**Example**  
```js
md4("This is a test");  // Returns "3b487cf6856af7e330bc4b1b7d977ef8"
md4(123);               // Returns null
```
<a name="module_digest+sha384"></a>

### digest.sha384(str) ⇒ <code>string</code>
<p>Calculates the SHA384 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| str | <code>string</code> | <p>The string to hash.</p> |

**Example**  
```js
sha384("This is a test");  // Returns "a27c7667e58200d4c0688ea136968404a0da366b1a9fc19bb38a0c7a609a1eef2bcc82837f4f4d92031a66051494b38c"
sha384(123);               // Returns null
```
<a name="module_digest+sha512"></a>

### digest.sha512(str) ⇒ <code>string</code>
<p>Calculates the SHA512 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| str | <code>string</code> | <p>The string to hash.</p> |

**Example**  
```js
sha512("This is a test");  // Returns "a028d4f74b602ba45eb0a93c9a4677240dcf281a1a9322f183bd32f0bed82ec72de9c3957b2f4c9a1ccf7ed14f85d73498df38017e703d47ebb9f0b3bf116f69"
sha512(123);               // Returns null
```
<a name="module_digest+md5_file"></a>

### digest.md5\_file(path) ⇒ <code>string</code>
<p>Calculates the MD5 hash of a given file and returns that hash.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the file.</p> |

<a name="module_digest+sha1_file"></a>

### digest.sha1\_file(path) ⇒ <code>string</code>
<p>Calculates the SHA1 hash of a given file and returns that hash.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the file.</p> |

<a name="module_digest+sha256_file"></a>

### digest.sha256\_file(path) ⇒ <code>string</code>
<p>Calculates the SHA256 hash of a given file and returns that hash.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the file.</p> |

<a name="module_digest+md2_file"></a>

### digest.md2\_file(path) ⇒ <code>string</code>
<p>Calculates the MD2 hash of a given file and returns that hash.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the file.</p> |

<a name="module_digest+md4_file"></a>

### digest.md4\_file(path) ⇒ <code>string</code>
<p>Calculates the MD4 hash of a given file and returns that hash.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the file.</p> |

<a name="module_digest+sha384_file"></a>

### digest.sha384\_file(path) ⇒ <code>string</code>
<p>Calculates the SHA384 hash of a given file and returns that hash.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the file.</p> |

<a name="module_digest+sha512_file"></a>

### digest.sha512\_file(path) ⇒ <code>string</code>
<p>Calculates the SHA512 hash of a given file and returns that hash.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the file.</p> |

<a name="module_debug"></a>

## debug
<h1 id="debugger-module">Debugger Module</h1>
<p>This module provides runtime debug functionality for ucode scripts.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { memdump, traceback } from 'debug';

let stacktrace = traceback(1);

memdump(&quot;/tmp/dump.txt&quot;);
</code></pre>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as debug from 'debug';

let stacktrace = debug.traceback(1);

debug.memdump(&quot;/tmp/dump.txt&quot;);
</code></pre>
<p>Additionally, the debug module namespace may also be imported by invoking the
<code>ucode</code> interpreter with the <code>-ldebug</code> switch.</p>
<p>Upon loading, the <code>debug</code> module will register a <code>SIGUSR2</code> signal handler
which, upon receipt of the signal, will write a memory dump of the currently
running program to <code>/tmp/ucode.$timestamp.$pid.memdump</code>. This default
behavior can be inhibited by setting the <code>UCODE_DEBUG_MEMDUMP_ENABLED</code>
environment variable to <code>0</code> when starting the process. The memory dump signal
and output directory can be overridden with the <code>UCODE_DEBUG_MEMDUMP_SIGNAL</code>
and <code>UCODE_DEBUG_MEMDUMP_PATH</code> environment variables respectively.</p>


* [debug](#module_debug)
    * _instance_
        * [.memdump(file)](#module_debug+memdump) ⇒ <code>boolean</code>
        * [.traceback([level])](#module_debug+traceback) ⇒ [<code>Array.&lt;StackTraceEntry&gt;</code>](#module_debug.StackTraceEntry)
        * [.sourcepos()](#module_debug+sourcepos) ⇒ [<code>SourcePosition</code>](#module_debug.SourcePosition)
        * [.getinfo(value)](#module_debug+getinfo) ⇒ [<code>ValueInformation</code>](#module_debug.ValueInformation)
        * [.getlocal([level], variable)](#module_debug+getlocal) ⇒ [<code>LocalInfo</code>](#module_debug.LocalInfo)
        * [.setlocal([level], variable, [value])](#module_debug+setlocal) ⇒ [<code>LocalInfo</code>](#module_debug.LocalInfo)
        * [.getupval(target, variable)](#module_debug+getupval) ⇒ [<code>UpvalInfo</code>](#module_debug.UpvalInfo)
        * [.setupval(target, variable, value)](#module_debug+setupval) ⇒ [<code>UpvalInfo</code>](#module_debug.UpvalInfo)
    * _static_
        * [.StackTraceEntry](#module_debug.StackTraceEntry) : <code>Object</code>
        * [.SourcePosition](#module_debug.SourcePosition) : <code>Object</code>
        * [.UpvalRef](#module_debug.UpvalRef) : <code>Object</code>
        * [.ValueInformation](#module_debug.ValueInformation) : <code>Object</code>
        * [.LocalInfo](#module_debug.LocalInfo) : <code>Object</code>
        * [.UpvalInfo](#module_debug.UpvalInfo) : <code>Object</code>

<a name="module_debug+memdump"></a>

### debug.memdump(file) ⇒ <code>boolean</code>
<p>Write a memory dump report to the given file.</p>
<p>This function generates a human readable memory dump of ucode values
currently managed by the running VM which is useful to track down logical
memory leaks in scripts.</p>
<p>The file parameter can be either a string value containing a file path, in
which case this function tries to create and write the report file at the
given location, or an already open file handle this function should write to.</p>
<p>Returns <code>true</code> if the report has been written.</p>
<p>Returns <code>null</code> if the file could not be opened or if the handle was invalid.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Description |
| --- | --- | --- |
| file | <code>string</code> \| [<code>file</code>](#module_fs.file) \| [<code>proc</code>](#module_fs.proc) | <p>The file path or open file handle to write report to.</p> |

<a name="module_debug+traceback"></a>

### debug.traceback([level]) ⇒ [<code>Array.&lt;StackTraceEntry&gt;</code>](#module_debug.StackTraceEntry)
<p>Capture call stack trace.</p>
<p>This function captures the current call stack and returns it. The optional
level parameter controls how many calls up the trace should start. It
defaults to <code>1</code>, that is the function calling this <code>traceback()</code> function.</p>
<p>Returns an array of stack trace entries describing the function invocations
up to the point where <code>traceback()</code> is called.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [level] | <code>number</code> | <code>1</code> | <p>The number of callframes up the call trace should start, <code>0</code> is this function itself, <code>1</code> the function calling it and so on.</p> |

<a name="module_debug+sourcepos"></a>

### debug.sourcepos() ⇒ [<code>SourcePosition</code>](#module_debug.SourcePosition)
<p>Obtain information about the current source position.</p>
<p>The <code>sourcepos()</code> function determines the source code position of the
current instruction invoking this function.</p>
<p>Returns a dictionary containing the filename, line number and line byte
offset of the call site.</p>
<p>Returns <code>null</code> if this function was invoked from C code.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  
<a name="module_debug+getinfo"></a>

### debug.getinfo(value) ⇒ [<code>ValueInformation</code>](#module_debug.ValueInformation)
<p>Obtain information about the given value.</p>
<p>The <code>getinfo()</code> function allows querying internal information about the
given ucode value, such as the current reference count, the mark bit state
etc.</p>
<p>Returns a dictionary with value type specific details.</p>
<p>Returns <code>null</code> if a <code>null</code> value was provided.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Description |
| --- | --- | --- |
| value | <code>\*</code> | <p>The value to query information for.</p> |

<a name="module_debug+getlocal"></a>

### debug.getlocal([level], variable) ⇒ [<code>LocalInfo</code>](#module_debug.LocalInfo)
<p>Obtain local variable.</p>
<p>The <code>getlocal()</code> function retrieves information about the specified local
variable at the given call stack depth.</p>
<p>The call stack depth specifies the amount of levels up local variables should
be queried. A value of <code>0</code> refers to this <code>getlocal()</code> function call itself,
<code>1</code> to the function calling <code>getlocal()</code> and so on.</p>
<p>The variable to query might be either specified by name or by its index with
index numbers following the source code declaration order.</p>
<p>Returns a dictionary holding information about the given variable.</p>
<p>Returns <code>null</code> if the stack depth exceeds the size of the current call stack.</p>
<p>Returns <code>null</code> if the invocation at the given stack depth is a C call.</p>
<p>Returns <code>null</code> if the given variable name is not found or the given variable
index is invalid.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [level] | <code>number</code> | <code>1</code> | <p>The amount of call stack levels up local variables should be queried.</p> |
| variable | <code>string</code> \| <code>number</code> |  | <p>The variable index or variable name to obtain information for.</p> |

<a name="module_debug+setlocal"></a>

### debug.setlocal([level], variable, [value]) ⇒ [<code>LocalInfo</code>](#module_debug.LocalInfo)
<p>Set local variable.</p>
<p>The <code>setlocal()</code> function manipulates the value of the specified local
variable at the given call stack depth.</p>
<p>The call stack depth specifies the amount of levels up local variables should
be updated. A value of <code>0</code> refers to this <code>setlocal()</code> function call itself,
<code>1</code> to the function calling <code>setlocal()</code> and so on.</p>
<p>The variable to update might be either specified by name or by its index with
index numbers following the source code declaration order.</p>
<p>Returns a dictionary holding information about the updated variable.</p>
<p>Returns <code>null</code> if the stack depth exceeds the size of the current call stack.</p>
<p>Returns <code>null</code> if the invocation at the given stack depth is a C call.</p>
<p>Returns <code>null</code> if the given variable name is not found or the given variable
index is invalid.</p>

**Kind**: instance method of [<code>debug</code>](#


---

<a id="ucode-module-fs"></a>
# ucode module: `fs`

> **Source:** [`lib/fs.c`](https://github.com/jow-/ucode/blob/master/lib/fs.c)
> **Live docs:** https://ucode.mein.io/module-fs.html
> **Generated:** 2026-03-04 13:26 UTC from commit `e87be9d`

---

## Modules

<dl>
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

<a name="module_fs"></a>

## fs
<h1 id="filesystem-access">Filesystem Access</h1>
<p>The <code>fs</code> module provides functions for interacting with the file system.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { readlink, popen } from 'fs';

let dest = readlink('/sys/class/net/eth0');
let proc = popen('ps ww');
</code></pre>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as fs from 'fs';

let dest = fs.readlink('/sys/class/net/eth0');
let proc = fs.popen('ps ww');
</code></pre>
<p>Additionally, the filesystem module namespace may also be imported by invoking
the <code>ucode</code> interpreter with the <code>-lfs</code> switch.</p>


* [fs](#module_fs)
    * _instance_
        * [.error()](#module_fs+error) ⇒ <code>string</code>
        * [.popen(command, [mode])](#module_fs+popen) ⇒ [<code>proc</code>](#module_fs.proc)
        * [.open(path, [mode], [perm])](#module_fs+open) ⇒ [<code>file</code>](#module_fs.file)
        * [.fdopen(fd, [mode])](#module_fs+fdopen) ⇒ <code>Object</code>
        * [.dup2(oldfd, newfd)](#module_fs+dup2) ⇒ <code>boolean</code>
        * [.opendir(path)](#module_fs+opendir) ⇒ [<code>dir</code>](#module_fs.dir)
        * [.readlink(path)](#module_fs+readlink) ⇒ <code>string</code>
        * [.stat(path)](#module_fs+stat) ⇒ [<code>FileStatResult</code>](#module_fs.FileStatResult)
        * [.lstat(path)](#module_fs+lstat) ⇒ [<code>FileStatResult</code>](#module_fs.FileStatResult)
        * [.mkdir(path)](#module_fs+mkdir) ⇒ <code>boolean</code>
        * [.rmdir(path)](#module_fs+rmdir) ⇒ <code>boolean</code>
        * [.symlink(target, path)](#module_fs+symlink) ⇒ <code>boolean</code>
        * [.unlink(path)](#module_fs+unlink) ⇒ <code>boolean</code>
        * [.getcwd()](#module_fs+getcwd) ⇒ <code>string</code>
        * [.chdir(path)](#module_fs+chdir) ⇒ <code>boolean</code>
        * [.chmod(path, mode)](#module_fs+chmod) ⇒ <code>boolean</code>
        * [.chown(path, [uid], [gid])](#module_fs+chown) ⇒ <code>boolean</code>
        * [.rename(oldPath, newPath)](#module_fs+rename) ⇒ <code>boolean</code>
        * [.dirname(path)](#module_fs+dirname) ⇒ <code>string</code>
        * [.basename(path)](#module_fs+basename) ⇒ <code>string</code>
        * [.lsdir(path)](#module_fs+lsdir) ⇒ <code>Array.&lt;string&gt;</code>
        * [.mkstemp([template])](#module_fs+mkstemp) ⇒ [<code>file</code>](#module_fs.file)
        * [.mkdtemp([template])](#module_fs+mkdtemp) ⇒ <code>string</code>
        * [.access(path, [mode])](#module_fs+access) ⇒ <code>boolean</code>
        * [.readfile(path, [limit])](#module_fs+readfile) ⇒ <code>string</code>
        * [.writefile(path, data, [limit])](#module_fs+writefile) ⇒ <code>number</code>
        * [.realpath(path)](#module_fs+realpath) ⇒ <code>string</code>
        * [.pipe()](#module_fs+pipe) ⇒ [<code>Array.&lt;file&gt;</code>](#module_fs.file)
        * [.error()](#module_fs+error) ⇒ <code>string</code>
        * [.popen(command, [mode])](#module_fs+popen) ⇒ [<code>proc</code>](#module_fs.proc)
        * [.open(path, [mode], [perm])](#module_fs+open) ⇒ [<code>file</code>](#module_fs.file)
        * [.fdopen(fd, [mode])](#module_fs+fdopen) ⇒ <code>Object</code>
        * [.dup2(oldfd, newfd)](#module_fs+dup2) ⇒ <code>boolean</code>
        * [.opendir(path)](#module_fs+opendir) ⇒ [<code>dir</code>](#module_fs.dir)
        * [.readlink(path)](#module_fs+readlink) ⇒ <code>string</code>
        * [.stat(path)](#module_fs+stat) ⇒ [<code>FileStatResult</code>](#module_fs.FileStatResult)
        * [.lstat(path)](#module_fs+lstat) ⇒ [<code>FileStatResult</code>](#module_fs.FileStatResult)
        * [.mkdir(path)](#module_fs+mkdir) ⇒ <code>boolean</code>
        * [.rmdir(path)](#module_fs+rmdir) ⇒ <code>boolean</code>
        * [.symlink(target, path)](#module_fs+symlink) ⇒ <code>boolean</code>
        * [.unlink(path)](#module_fs+unlink) ⇒ <code>boolean</code>
        * [.getcwd()](#module_fs+getcwd) ⇒ <code>string</code>
        * [.chdir(path)](#module_fs+chdir) ⇒ <code>boolean</code>
        * [.chmod(path, mode)](#module_fs+chmod) ⇒ <code>boolean</code>
        * [.chown(path, [uid], [gid])](#module_fs+chown) ⇒ <code>boolean</code>
        * [.rename(oldPath, newPath)](#module_fs+rename) ⇒ <code>boolean</code>
        * [.dirname(path)](#module_fs+dirname) ⇒ <code>string</code>
        * [.basename(path)](#module_fs+basename) ⇒ <code>string</code>
        * [.lsdir(path)](#module_fs+lsdir) ⇒ <code>Array.&lt;string&gt;</code>
        * [.mkstemp([template])](#module_fs+mkstemp) ⇒ [<code>file</code>](#module_fs.file)
        * [.mkdtemp([template])](#module_fs+mkdtemp) ⇒ <code>string</code>
        * [.access(path, [mode])](#module_fs+access) ⇒ <code>boolean</code>
        * [.readfile(path, [limit])](#module_fs+readfile) ⇒ <code>string</code>
        * [.writefile(path, data, [limit])](#module_fs+writefile) ⇒ <code>number</code>
        * [.realpath(path)](#module_fs+realpath) ⇒ <code>string</code>
        * [.pipe()](#module_fs+pipe) ⇒ [<code>Array.&lt;file&gt;</code>](#module_fs.file)
    * _static_
        * [.proc](#module_fs.proc)
            * [.close()](#module_fs.proc+close) ⇒ <code>number</code>
            * [.read(length)](#module_fs.proc+read) ⇒ <code>string</code>
            * [.write(data)](#module_fs.proc+write) ⇒ <code>number</code>
            * [.flush()](#module_fs.proc+flush) ⇒ <code>boolean</code>
            * [.fileno()](#module_fs.proc+fileno) ⇒ <code>number</code>
            * [.close()](#module_fs.proc+close) ⇒ <code>number</code>
            * [.read(length)](#module_fs.proc+read) ⇒ <code>string</code>
            * [.write(data)](#module_fs.proc+write) ⇒ <code>number</code>
            * [.flush()](#module_fs.proc+flush) ⇒ <code>boolean</code>
            * [.fileno()](#module_fs.proc+fileno) ⇒ <code>number</code>
            * [.error()](#module_fs.proc+error) ⇒ <code>string</code>
            * [.error()](#module_fs.proc+error) ⇒ <code>string</code>
            * [.error()](#module_fs.proc+error) ⇒ <code>string</code>
            * [.error()](#module_fs.proc+error) ⇒ <code>string</code>
        * [.file](#module_fs.file)
            * [.close()](#module_fs.file+close) ⇒ <code>boolean</code>
            * [.read(length)](#module_fs.file+read) ⇒ <code>string</code>
            * [.write(data)](#module_fs.file+write) ⇒ <code>number</code>
            * [.seek([offset], [position])](#module_fs.file+seek) ⇒ <code>boolean</code>
            * [.truncate([offset])](#module_fs.file+truncate) ⇒ <code>boolean</code>
            * [.lock([op])](#module_fs.file+lock) ⇒ <code>boolean</code>
            * [.tell()](#module_fs.file+tell) ⇒ <code>number</code>
            * [.isatty()](#module_fs.file+isatty) ⇒ <code>boolean</code>
            * [.flush()](#module_fs.file+flush) ⇒ <code>boolean</code>
            * [.fileno()](#module_fs.file+fileno) ⇒ <code>number</code>
            * [.ioctl(direction, type, num, [value])](#module_fs.file+ioctl) ⇒ <code>number</code> \| <code>string</code>
            * [.close()](#module_fs.file+close) ⇒ <code>boolean</code>
            * [.read(length)](#module_fs.file+read) ⇒ <code>string</code>
            * [.write(data)](#module_fs.file+write) ⇒ <code>number</code>
            * [.seek([offset], [position])](#module_fs.file+seek) ⇒ <code>boolean</code>
            * [.truncate([offset])](#module_fs.file+truncate) ⇒ <code>boolean</code>
            * [.lock([op])](#module_fs.file+lock) ⇒ <code>boolean</code>
            * [.tell()](#module_fs.file+tell) ⇒ <code>number</code>
            * [.isatty()](#module_fs.file+isatty) ⇒ <code>boolean</code>
            * [.flush()](#module_fs.file+flush) ⇒ <code>boolean</code>
            * [.fileno()](#module_fs.file+fileno) ⇒ <code>number</code>
            * [.ioctl(direction, type, num, [value])](#module_fs.file+ioctl) ⇒ <code>number</code> \| <code>string</code>
            * [.error()](#module_fs.file+error) ⇒ <code>string</code>
            * [.error()](#module_fs.file+error) ⇒ <code>string</code>
            * [.error()](#module_fs.file+error) ⇒ <code>string</code>
            * [.error()](#module_fs.file+error) ⇒ <code>string</code>
        * [.dir](#module_fs.dir)
            * [.fileno()](#module_fs.dir+fileno) ⇒ <code>number</code>
            * [.read()](#module_fs.dir+read) ⇒ <code>string</code>
            * [.tell()](#module_fs.dir+tell) ⇒ <code>number</code>
            * [.seek(offset)](#module_fs.dir+seek) ⇒ <code>boolean</code>
            * [.close()](#module_fs.dir+close) ⇒ <code>boolean</code>
            * [.fileno()](#module_fs.dir+fileno) ⇒ <code>number</code>
            * [.read()](#module_fs.dir+read) ⇒ <code>string</code>
            * [.tell()](#module_fs.dir+tell) ⇒ <code>number</code>
            * [.seek(offset)](#module_fs.dir+seek) ⇒ <code>boolean</code>
            * [.close()](#module_fs.dir+close) ⇒ <code>boolean</code>
            * [.error()](#module_fs.dir+error) ⇒ <code>string</code>
            * [.error()](#module_fs.dir+error) ⇒ <code>string</code>
            * [.error()](#module_fs.dir+error) ⇒ <code>string</code>
            * [.error()](#module_fs.dir+error) ⇒ <code>string</code>
        * [.proc](#module_fs.proc)
            * [.close()](#module_fs.proc+close) ⇒ <code>number</code>
            * [.read(length)](#module_fs.proc+read) ⇒ <code>string</code>
            * [.write(data)](#module_fs.proc+write) ⇒ <code>number</code>
            * [.flush()](#module_fs.proc+flush) ⇒ <code>boolean</code>
            * [.fileno()](#module_fs.proc+fileno) ⇒ <code>number</code>
            * [.close()](#module_fs.proc+close) ⇒ <code>number</code>
            * [.read(length)](#module_fs.proc+read) ⇒ <code>string</code>
            * [.write(data)](#module_fs.proc+write) ⇒ <code>number</code>
            * [.flush()](#module_fs.proc+flush) ⇒ <code>boolean</code>
            * [.fileno()](#module_fs.proc+fileno) ⇒ <code>number</code>
            * [.error()](#module_fs.proc+error) ⇒ <code>string</code>
            * [.error()](#module_fs.proc+error) ⇒ <code>string</code>
            * [.error()](#module_fs.proc+error) ⇒ <code>string</code>
            * [.error()](#module_fs.proc+error) ⇒ <code>string</code>
        * [.file](#module_fs.file)
            * [.close()](#module_fs.file+close) ⇒ <code>boolean</code>
            * [.read(length)](#module_fs.file+read) ⇒ <code>string</code>
            * [.write(data)](#module_fs.file+write) ⇒ <code>number</code>
            * [.seek([offset], [position])](#module_fs.file+seek) ⇒ <code>boolean</code>
            * [.truncate([offset])](#module_fs.file+truncate) ⇒ <code>boolean</code>
            * [.lock([op])](#module_fs.file+lock) ⇒ <code>boolean</code>
            * [.tell()](#module_fs.file+tell) ⇒ <code>number</code>
            * [.isatty()](#module_fs.file+isatty) ⇒ <code>boolean</code>
            * [.flush()](#module_fs.file+flush) ⇒ <code>boolean</code>
            * [.fileno()](#module_fs.file+fileno) ⇒ <code>number</code>
            * [.ioctl(direction, type, num, [value])](#module_fs.file+ioctl) ⇒ <code>number</code> \| <code>string</code>
            * [.close()](#module_fs.file+close) ⇒ <code>boolean</code>
            * [.read(length)](#module_fs.file+read) ⇒ <code>string</code>
            * [.write(data)](#module_fs.file+write) ⇒ <code>number</code>
            * [.seek([offset], [position])](#module_fs.file+seek) ⇒ <code>boolean</code>
            * [.truncate([offset])](#module_fs.file+truncate) ⇒ <code>boolean</code>
            * [.lock([op])](#module_fs.file+lock) ⇒ <code>boolean</code>
            * [.tell()](#module_fs.file+tell) ⇒ <code>number</code>
            * [.isatty()](#module_fs.file+isatty) ⇒ <code>boolean</code>
            * [.flush()](#module_fs.file+flush) ⇒ <code>boolean</code>
            * [.fileno()](#module_fs.file+fileno) ⇒ <code>number</code>
            * [.ioctl(direction, type, num, [value])](#module_fs.file+ioctl) ⇒ <code>number</code> \| <code>string</code>
            * [.error()](#module_fs.file+error) ⇒ <code>string</code>
            * [.error()](#module_fs.file+error) ⇒ <code>string</code>
            * [.error()](#module_fs.file+error) ⇒ <code>string</code>
            * [.error()](#module_fs.file+error) ⇒ <code>string</code>
        * [.dir](#module_fs.dir)
            * [.fileno()](#module_fs.dir+fileno) ⇒ <code>number</code>
            * [.read()](#module_fs.dir+read) ⇒ <code>string</code>
            * [.tell()](#module_fs.dir+tell) ⇒ <code>number</code>
            * [.seek(offset)](#module_fs.dir+seek) ⇒ <code>boolean</code>
            * [.close()](#module_fs.dir+close) ⇒ <code>boolean</code>
            * [.fileno()](#module_fs.dir+fileno) ⇒ <code>number</code>
            * [.read()](#module_fs.dir+read) ⇒ <code>string</code>
            * [.tell()](#module_fs.dir+tell) ⇒ <code>number</code>
            * [.seek(offset)](#module_fs.dir+seek) ⇒ <code>boolean</code>
            * [.close()](#module_fs.dir+close) ⇒ <code>boolean</code>
            * [.error()](#module_fs.dir+error) ⇒ <code>string</code>
            * [.error()](#module_fs.dir+error) ⇒ <code>string</code>
            * [.error()](#module_fs.dir+error) ⇒ <code>string</code>
            * [.error()](#module_fs.dir+error) ⇒ <code>string</code>
        * [.FileStatResult](#module_fs.FileStatResult) : <code>Object</code>
        * [.FileStatResult](#module_fs.FileStatResult) : <code>Object</code>

<a name="module_fs+error"></a>

### fs.error() ⇒ <code>string</code>
<p>Query error information.</p>
<p>Returns a string containing a description of the last occurred error or
<code>null</code> if there is no error information.</p>

**Kind**: instance method of [<code>fs</code>](#module_fs)  
**Example**  
```js
// Trigger file system error
unlink('/path/does/not/exist');

// Print error (should yield "No such file or directory")
print(error(), "\n");
```
<a name="module_fs+popen"></a>

### fs.popen(command, [mode]) ⇒ [<code>proc</code>](#module_fs.proc)
<p>Starts a process and returns a handle representing the executed process.</p>
<p>The handle will be connected to the process stdin or stdout, depending on the
value of the mode argument.</p>
<p>The mode argument may be either &quot;r&quot; to open the process for reading (connect
to its stdin) or &quot;w&quot; to open the process for writing (connect to its stdout).</p>
<p>The mode character &quot;r&quot; or &quot;w&quot; may be optionally followed by &quot;e&quot; to apply the
FD_CLOEXEC flag onto the open descriptor.</p>
<p>Returns a process handle referring to the executed process.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>fs</code>](#module_fs)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| command | <code>string</code> |  | <p>The command to be executed.</p> |
| [mode] | <code>string</code> | <code>&quot;\&quot;r\&quot;&quot;</code> | <p>The open mode of the process handle.</p> |

**Example**  
```js
// Open a process
const process = popen('command', 'r');
```
<a name="module_fs+open"></a>

### fs.open(path, [mode], [perm]) ⇒ [<code>file</code>](#module_fs.file)
<p>Opens a file.</p>
<p>The mode argument specifies the way the file is opened, it may
start with one of the following values:</p>
<table>
<thead>
<tr>
<th>Mode</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>&quot;r&quot;</td>
<td>Opens a file for reading. The file must exist.</td>
</tr>
<tr>
<td>&quot;w&quot;</td>
<td>Opens a file for writing. If the file exists, it is truncated. If the file does not exist, it is created.</td>
</tr>
<tr>
<td>&quot;a&quot;</td>
<td>Opens a file for appending. Data is written at the end of the file. If the file does not exist, it is created.</td>
</tr>
<tr>
<td>&quot;r+&quot;</td>
<td>Opens a file for both reading and writing. The file must exist.</td>
</tr>
<tr>
<td>&quot;w+&quot;</td>
<td>Opens a file for both reading and writing. If the file exists, it is truncated. If the file does not exist, it is created.</td>
</tr>
<tr>
<td>&quot;a+&quot;</td>
<td>Opens a file for both reading and appending. Data can be read and written at the end of the file. If the file does not exist, it is created.</td>
</tr>
</tbody>
</table>
<p>Additionally, the following flag characters may be appended to
the mode value:</p>
<table>
<thead>
<tr>
<th>Flag</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>&quot;x&quot;</td>
<td>Opens a file for exclusive creation. If the file exists, the <code>open</code> call fails.</td>
</tr>
<tr>
<td>&quot;e&quot;</td>
<td>Opens a file with the <code>O_CLOEXEC</code> flag set, ensuring that the file descriptor is closed on <code>exec</code> calls.</td>
</tr>
</tbody>
</table>
<p>If the mode is one of <code>&quot;w…&quot;</code> or <code>&quot;a…&quot;</code>, the permission argument
controls the filesystem permissions bits used when creating
the file.</p>
<p>Returns a file handle object associated with the opened file.</p>

**Kind**: instance method of [<code>fs</code>](#module_fs)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| path | <code>string</code> |  | <p>The path to the file.</p> |
| [mode] | <code>string</code> | <code>&quot;\&quot;r\&quot;&quot;</code> | <p>The file opening mode.</p> |
| [perm] | <code>number</code> | <code>0o666</code> | <p>The file creation permissions (for modes <code>w…</code> and <code>a…</code>)</p> |

**Example**  
```js
// Open a file in read-only mode
const fileHandle = open('file.txt', 'r');
```
<a name="module_fs+fdopen"></a>

### fs.fdopen(fd, [mode]) ⇒ <code>Object</code>
<p>Associates a file descriptor number with a file handle object.</p>
<p>The mode argument controls how the file handle object is opened
and must match the open mode of the underlying descriptor.</p>
<p>It may be set to one of the following values:</p>
<table>
<thead>
<tr>
<th>Mode</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>&quot;r&quot;</td>
<td>Opens a file stream for reading. The file descriptor must be valid and opened in read mode.</td>
</tr>
<tr>
<td>&quot;w&quot;</td>
<td>Opens a file stream for writing. The file descriptor must be valid and opened in write mode.</td>
</tr>
<tr>
<td>&quot;a&quot;</td>
<td>Opens a file stream for appending. The file descriptor must be valid and opened in write mode.</td>
</tr>
<tr>
<td>&quot;r+&quot;</td>
<td>Opens a file stream for both reading and writing. The file descriptor must be valid and opened in read/write mode.</td>
</tr>
<tr>
<td>&quot;w+&quot;</td>
<td>Opens a file stream for both reading and writing. The file descriptor must be valid and opened in read/write mode.</td>
</tr>
<tr>
<td>&quot;a+&quot;</td>
<td>Opens a file stream for both reading and appending. The file descriptor must be valid and opened in read/write mode.</td>
</tr>
</tbody>
</table>
<p>Returns the file handle object associated with the file descriptor.</p>

**Kind**: instance method of [<code>fs</code>](#module_fs)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| fd | <code>number</code> |  | <p>The file descriptor.</p> |
| [mode] | <code>string</code> | <code>&quot;\&quot;r\&quot;&quot;</code> | <p>The open mode.</p> |

**Example**  
```js
// Associate file descriptors of stdin and stdout with handles
const stdinHandle = fdopen(0, 'r');
const stdoutHandle = fdopen(1, 'w');
```
<a name="module_fs+dup2"></a>

### fs.dup2(oldfd, newfd) ⇒ <code>boolean</code>
<p>Duplicates a file descriptor.</p>
<p>This function duplicates the file descriptor <code>oldfd</code> to <code>newfd</code>. If <code>newfd</code>
was previously open, it is silently closed before being reused.</p>
<p>Returns <code>true</code> on success.
Returns <code>null</code> on error.</p>

**Kind**: instance method of [<code>fs</code>](#module_fs)  

| Param | Type | Description |
| --- | --- | --- |
| oldfd | <code>number</code> | <p>The file descriptor to duplicate.</p> |
| newfd | <code>number</code> | <p>The file descriptor number to duplicate to.</p> |

**Example**  
```js
// Redirect stderr to a log file
const logfile = open('/tmp/error.log', 'w');
dup2(logfile.fileno(), 2);
logfile.close();
```
<a name="module_fs+opendir"></a>

### fs.opendir(path) ⇒ [<code>dir</code>](#module_fs.dir)
<p>Opens a directory and returns a directory handle associated with the open
directory descriptor.</p>
<p>Returns a director handle referring to the open directory.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>fs</code>](#module_fs)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the directory.</p> |

**Example**  
```js
// Open a directory
const directory = opendir('path/to/directory');
```
<a name="module_fs+readlink"></a>

### fs.readlink(path) ⇒ <code>string</code>
<p>Reads the target path of a symbolic link.</p>
<p>Returns a string containing the target path.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>fs</code>](#module_fs)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the symbolic link.</p> |

**Example**  
```js
// Read the value of a symbolic link
const targetPath = readlink('symbolicLink');
```
<a name="module_fs+stat"></a>

### fs.stat(path) ⇒ [<code>FileStatResult</code>](#module_fs.FileStatResult)
<p>Retrieves information about a file or directory.</p>
<p>Returns an object containing information about the file or directory.</p>
<p>Returns <code>null</code> if an error occurred, e.g. due to insufficient permissions.</p>

**Kind**: instance method of [<code>fs</code>](#module_fs)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the file or directory.</p> |

**Example**  
```js
// Get information about a file
const fileInfo = stat('path/to/file');
```
<a name="module_fs+lstat"></a>

### fs.lstat(path) ⇒ [<code>FileStatResult</code>](#module_fs.FileStatResult)
<p>Retrieves information about a file or directory, without following symbolic
links.</p>
<p>Returns an object containing information about the file or directory.</p>
<p>Returns <code>null</code> if an error occurred, e.g. due to insufficient permissions.</p>

**Kind**: instance method of [<code>fs</code>](#module_fs)  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | <p>The path to the file or directory.</p> |

**Example**  
```js
// Get information about a directory
const dirInfo = lstat('path/to/directory');
```
<a name="module_fs+mkdir"></a>

### fs.mkdir(path) ⇒ <code>boolean</code>
<p>Creates a new directory.</p>
<p>Returns <code>true</code> if the directory was successfully created.</p>
<p>Returns <code>null</code> if an error occurred, e.g. due to inexistent path.</p>

**Kind**: instance method of [<code>fs</code>](#module_fs)  

| Param | Type | Description |
| --- | --- | --- |
| 


---

<a id="ucode-module-io"></a>
# ucode module: `io`

> **Source:** [`lib/io.c`](https://github.com/jow-/ucode/blob/master/lib/io.c)
> **Live docs:** https://ucode.mein.io/module-io.html
> **Generated:** 2026-03-04 13:26 UTC from commit `e87be9d`

---

## Modules

<dl>
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

<a name="module_io"></a>

## io
<h1 id="i%2Fo-operations">I/O Operations</h1>
<p>The <code>io</code> module provides object-oriented access to UNIX file descriptors.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { open, O_RDWR } from 'io';

let handle = open('/tmp/test.txt', O_RDWR);
handle.write('Hello World\n');
handle.close();
</code></pre>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as io from 'io';

let handle = io.open('/tmp/test.txt', io.O_RDWR);
handle.write('Hello World\n');
handle.close();
</code></pre>
<p>Additionally, the io module namespace may also be imported by invoking
the <code>ucode</code> interpreter with the <code>-lio</code> switch.</p>


* [io](#module_io)
    * _instance_
        * [.error()](#module_io+error) ⇒ <code>string</code>
        * [.new(fd)](#module_io+new) ⇒ [<code>handle</code>](#module_io.handle)
        * [.open(path, [flags], [mode])](#module_io+open) ⇒ [<code>handle</code>](#module_io.handle)
        * [.pipe()](#module_io+pipe) ⇒ [<code>Array.&lt;handle&gt;</code>](#module_io.handle)
        * [.from(value)](#module_io+from) ⇒ [<code>handle</code>](#module_io.handle)
        * [.error()](#module_io+error) ⇒ <code>string</code>
        * [.new(fd)](#module_io+new) ⇒ [<code>handle</code>](#module_io.handle)
        * [.open(path, [flags], [mode])](#module_io+open) ⇒ [<code>handle</code>](#module_io.handle)
        * [.pipe()](#module_io+pipe) ⇒ [<code>Array.&lt;handle&gt;</code>](#module_io.handle)
        * [.from(value)](#module_io+from) ⇒ [<code>handle</code>](#module_io.handle)
    * _static_
        * [.handle](#module_io.handle)
            * [.ptsname()](#module_io.handle+ptsname) ⇒ <code>string</code>
            * [.tcgetattr()](#module_io.handle+tcgetattr) ⇒ <code>object</code>
            * [.tcsetattr(attrs, [when])](#module_io.handle+tcsetattr) ⇒ <code>boolean</code>
            * [.grantpt()](#module_io.handle+grantpt) ⇒ <code>boolean</code>
            * [.unlockpt()](#module_io.handle+unlockpt) ⇒ <code>boolean</code>
            * [.read(length)](#module_io.handle+read) ⇒ <code>string</code>
            * [.write(data)](#module_io.handle+write) ⇒ <code>number</code>
            * [.seek([offset], [whence])](#module_io.handle+seek) ⇒ <code>boolean</code>
            * [.tell()](#module_io.handle+tell) ⇒ <code>number</code>
            * [.dup()](#module_io.handle+dup) ⇒ [<code>handle</code>](#module_io.handle)
            * [.dup2(newfd)](#module_io.handle+dup2) ⇒ <code>boolean</code>
            * [.fileno()](#module_io.handle+fileno) ⇒ <code>number</code>
            * [.fcntl(cmd, [arg])](#module_io.handle+fcntl) ⇒ <code>number</code> \| [<code>handle</code>](#module_io.handle)
            * [.ioctl(direction, type, num, [value])](#module_io.handle+ioctl) ⇒ <code>number</code> \| <code>string</code>
            * [.isatty()](#module_io.handle+isatty) ⇒ <code>boolean</code>
            * [.close()](#module_io.handle+close) ⇒ <code>boolean</code>
            * [.ptsname()](#module_io.handle+ptsname) ⇒ <code>string</code>
            * [.tcgetattr()](#module_io.handle+tcgetattr) ⇒ <code>object</code>
            * [.tcsetattr(attrs, [when])](#module_io.handle+tcsetattr) ⇒ <code>boolean</code>
            * [.grantpt()](#module_io.handle+grantpt) ⇒ <code>boolean</code>
            * [.unlockpt()](#module_io.handle+unlockpt) ⇒ <code>boolean</code>
            * [.read(length)](#module_io.handle+read) ⇒ <code>string</code>
            * [.write(data)](#module_io.handle+write) ⇒ <code>number</code>
            * [.seek([offset], [whence])](#module_io.handle+seek) ⇒ <code>boolean</code>
            * [.tell()](#module_io.handle+tell) ⇒ <code>number</code>
            * [.dup()](#module_io.handle+dup) ⇒ [<code>handle</code>](#module_io.handle)
            * [.dup2(newfd)](#module_io.handle+dup2) ⇒ <code>boolean</code>
            * [.fileno()](#module_io.handle+fileno) ⇒ <code>number</code>
            * [.fcntl(cmd, [arg])](#module_io.handle+fcntl) ⇒ <code>number</code> \| [<code>handle</code>](#module_io.handle)
            * [.ioctl(direction, type, num, [value])](#module_io.handle+ioctl) ⇒ <code>number</code> \| <code>string</code>
            * [.isatty()](#module_io.handle+isatty) ⇒ <code>boolean</code>
            * [.close()](#module_io.handle+close) ⇒ <code>boolean</code>
            * [.error()](#module_io.handle+error) ⇒ <code>string</code>
            * [.error()](#module_io.handle+error) ⇒ <code>string</code>
            * [.error()](#module_io.handle+error) ⇒ <code>string</code>
            * [.error()](#module_io.handle+error) ⇒ <code>string</code>
        * [.handle](#module_io.handle)
            * [.ptsname()](#module_io.handle+ptsname) ⇒ <code>string</code>
            * [.tcgetattr()](#module_io.handle+tcgetattr) ⇒ <code>object</code>
            * [.tcsetattr(attrs, [when])](#module_io.handle+tcsetattr) ⇒ <code>boolean</code>
            * [.grantpt()](#module_io.handle+grantpt) ⇒ <code>boolean</code>
            * [.unlockpt()](#module_io.handle+unlockpt) ⇒ <code>boolean</code>
            * [.read(length)](#module_io.handle+read) ⇒ <code>string</code>
            * [.write(data)](#module_io.handle+write) ⇒ <code>number</code>
            * [.seek([offset], [whence])](#module_io.handle+seek) ⇒ <code>boolean</code>
            * [.tell()](#module_io.handle+tell) ⇒ <code>number</code>
            * [.dup()](#module_io.handle+dup) ⇒ [<code>handle</code>](#module_io.handle)
            * [.dup2(newfd)](#module_io.handle+dup2) ⇒ <code>boolean</code>
            * [.fileno()](#module_io.handle+fileno) ⇒ <code>number</code>
            * [.fcntl(cmd, [arg])](#module_io.handle+fcntl) ⇒ <code>number</code> \| [<code>handle</code>](#module_io.handle)
            * [.ioctl(direction, type, num, [value])](#module_io.handle+ioctl) ⇒ <code>number</code> \| <code>string</code>
            * [.isatty()](#module_io.handle+isatty) ⇒ <code>boolean</code>
            * [.close()](#module_io.handle+close) ⇒ <code>boolean</code>
            * [.ptsname()](#module_io.handle+ptsname) ⇒ <code>string</code>
            * [.tcgetattr()](#module_io.handle+tcgetattr) ⇒ <code>object</code>
            * [.tcsetattr(attrs, [when])](#module_io.handle+tcsetattr) ⇒ <code>boolean</code>
            * [.grantpt()](#module_io.handle+grantpt) ⇒ <code>boolean</code>
            * [.unlockpt()](#module_io.handle+unlockpt) ⇒ <code>boolean</code>
            * [.read(length)](#module_io.handle+read) ⇒ <code>string</code>
            * [.write(data)](#module_io.handle+write) ⇒ <code>number</code>
            * [.seek([offset], [whence])](#module_io.handle+seek) ⇒ <code>boolean</code>
            * [.tell()](#module_io.handle+tell) ⇒ <code>number</code>
            * [.dup()](#module_io.handle+dup) ⇒ [<code>handle</code>](#module_io.handle)
            * [.dup2(newfd)](#module_io.handle+dup2) ⇒ <code>boolean</code>
            * [.fileno()](#module_io.handle+fileno) ⇒ <code>number</code>
            * [.fcntl(cmd, [arg])](#module_io.handle+fcntl) ⇒ <code>number</code> \| [<code>handle</code>](#module_io.handle)
            * [.ioctl(direction, type, num, [value])](#module_io.handle+ioctl) ⇒ <code>number</code> \| <code>string</code>
            * [.isatty()](#module_io.handle+isatty) ⇒ <code>boolean</code>
            * [.close()](#module_io.handle+close) ⇒ <code>boolean</code>
            * [.error()](#module_io.handle+error) ⇒ <code>string</code>
            * [.error()](#module_io.handle+error) ⇒ <code>string</code>
            * [.error()](#module_io.handle+error) ⇒ <code>string</code>
            * [.error()](#module_io.handle+error) ⇒ <code>string</code>

<a name="module_io+error"></a>

### io.error() ⇒ <code>string</code>
<p>Query error information.</p>
<p>Returns a string containing a description of the last occurred error or
<code>null</code> if there is no error information.</p>

**Kind**: instance method of [<code>io</code>](#module_io)  
**Example**  
```js
// Trigger an error
io.open('/path/does/not/exist');

// Print error (should yield "No such file or directory")
print(io.error(), "\n");
```
<a name="module_io+new"></a>

### io.new(fd) ⇒ [<code>handle</code>](#module_io.handle)
<p>Creates an io.handle from a file descriptor number.</p>
<p>Wraps the given file descriptor number in an io.handle object.</p>
<p>Returns an io.handle object.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>io</code>](#module_io)  

| Param | Type | Description |
| --- | --- | --- |
| fd | <code>number</code> | <p>The file descriptor number.</p> |

**Example**  
```js
// Wrap stdin
const stdin = io.new(0);
const data = stdin.read(100);
```
<a name="module_io+open"></a>

### io.open(path, [flags], [mode]) ⇒ [<code>handle</code>](#module_io.handle)
<p>Opens a file and returns an io.handle.</p>
<p>Opens the specified file with the given flags and mode, returning an
io.handle wrapping the resulting file descriptor.</p>
<p>Returns an io.handle object.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>io</code>](#module_io)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| path | <code>string</code> |  | <p>The path to the file.</p> |
| [flags] | <code>number</code> | <code>O_RDONLY</code> | <p>The open flags (O_RDONLY, O_WRONLY, O_RDWR, etc.).</p> |
| [mode] | <code>number</code> | <code>0o666</code> | <p>The file creation mode (used with O_CREAT).</p> |

**Example**  
```js
const handle = io.open('/tmp/test.txt', O_RDWR | O_CREAT, 0o644);
handle.write('Hello World\n');
handle.close();
```
<a name="module_io+pipe"></a>

### io.pipe() ⇒ [<code>Array.&lt;handle&gt;</code>](#module_io.handle)
<p>Creates a pipe.</p>
<p>Creates a unidirectional data channel (pipe) that can be used for
inter-process communication. Returns an array containing two io.handle
objects: the first is the read end of the pipe, the second is the write end.</p>
<p>Data written to the write end can be read from the read end.</p>
<p>Returns an array <code>[read_handle, write_handle]</code> on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>io</code>](#module_io)  
**Example**  
```js
const [reader, writer] = io.pipe();
writer.write('Hello from pipe!');
const data = reader.read(100);
print(data, "\n");  // Prints: Hello from pipe!
```
<a name="module_io+from"></a>

### io.from(value) ⇒ [<code>handle</code>](#module_io.handle)
<p>Creates an io.handle from various value types.</p>
<p>Creates an io.handle by extracting the file descriptor from the given value.
The value can be:</p>
<ul>
<li>An integer file descriptor number</li>
<li>An fs.file, fs.proc, or socket resource</li>
<li>Any object/array/resource with a fileno() method</li>
</ul>
<p>Returns an io.handle object.</p>
<p>Returns <code>null</code> if an error occurred or the value cannot be converted.</p>

**Kind**: instance method of [<code>io</code>](#module_io)  

| Param | Type | Description |
| --- | --- | --- |
| value | <code>\*</code> | <p>The value to convert.</p> |

**Example**  
```js
import { open as fsopen } from 'fs';
const fp = fsopen('/tmp/test.txt', 'r');
const handle = io.from(fp);
const data = handle.read(100);
```
<a name="module_io+error"></a>

### io.error() ⇒ <code>string</code>
<p>Query error information.</p>
<p>Returns a string containing a description of the last occurred error or
<code>null</code> if there is no error information.</p>

**Kind**: instance method of [<code>io</code>](#module_io)  
**Example**  
```js
// Trigger an error
io.open('/path/does/not/exist');

// Print error (should yield "No such file or directory")
print(io.error(), "\n");
```
<a name="module_io+new"></a>

### io.new(fd) ⇒ [<code>handle</code>](#module_io.handle)
<p>Creates an io.handle from a file descriptor number.</p>
<p>Wraps the given file descriptor number in an io.handle object.</p>
<p>Returns an io.handle object.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>io</code>](#module_io)  

| Param | Type | Description |
| --- | --- | --- |
| fd | <code>number</code> | <p>The file descriptor number.</p> |

**Example**  
```js
// Wrap stdin
const stdin = io.new(0);
const data = stdin.read(100);
```
<a name="module_io+open"></a>

### io.open(path, [flags], [mode]) ⇒ [<code>handle</code>](#module_io.handle)
<p>Opens a file and returns an io.handle.</p>
<p>Opens the specified file with the given flags and mode, returning an
io.handle wrapping the resulting file descriptor.</p>
<p>Returns an io.handle object.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>io</code>](#module_io)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| path | <code>string</code> |  | <p>The path to the file.</p> |
| [flags] | <code>number</code> | <code>O_RDONLY</code> | <p>The open flags (O_RDONLY, O_WRONLY, O_RDWR, etc.).</p> |
| [mode] | <code>number</code> | <code>0o666</code> | <p>The file creation mode (used with O_CREAT).</p> |

**Example**  
```js
const handle = io.open('/tmp/test.txt', O_RDWR | O_CREAT, 0o644);
handle.write('Hello World\n');
handle.close();
```
<a name="module_io+pipe"></a>

### io.pipe() ⇒ [<code>Array.&lt;handle&gt;</code>](#module_io.handle)
<p>Creates a pipe.</p>
<p>Creates a unidirectional data channel (pipe) that can be used for
inter-process communication. Returns an array containing two io.handle
objects: the first is the read end of the pipe, the second is the write end.</p>
<p>Data written to the write end can be read from the read end.</p>
<p>Returns an array <code>[read_handle, write_handle]</code> on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>io</code>](#module_io)  
**Example**  
```js
const [reader, writer] = io.pipe();
writer.write('Hello from pipe!');
const data = reader.read(100);
print(data, "\n");  // Prints: Hello from pipe!
```
<a name="module_io+from"></a>

### io.from(value) ⇒ [<code>handle</code>](#module_io.handle)
<p>Creates an io.handle from various value types.</p>
<p>Creates an io.handle by extracting the file descriptor from the given value.
The value can be:</p>
<ul>
<li>An integer file descriptor number</li>
<li>An fs.file, fs.proc, or socket resource</li>
<li>Any object/array/resource with a fileno() method</li>
</ul>
<p>Returns an io.handle object.</p>
<p>Returns <code>null</code> if an error occurred or the value cannot be converted.</p>

**Kind**: instance method of [<code>io</code>](#module_io)  

| Param | Type | Description |
| --- | --- | --- |
| value | <code>\*</code> | <p>The value to convert.</p> |

**Example**  
```js
import { open as fsopen } from 'fs';
const fp = fsopen('/tmp/test.txt', 'r');
const handle = io.from(fp);
const data = handle.read(100);
```
<a name="module_io.handle"></a>

### io.handle
**Kind**: static class of [<code>io</code>](#module_io)  
**See**

- [new()](#module_io+new)
- [open()](#module_io+open)
- [from()](#module_io+from)


* [.handle](#module_io.handle)
    * [.ptsname()](#module_io.handle+ptsname) ⇒ <code>string</code>
    * [.tcgetattr()](#module_io.handle+tcgetattr) ⇒ <code>object</code>
    * [.tcsetattr(attrs, [when])](#module_io.handle+tcsetattr) ⇒ <code>boolean</code>
    * [.grantpt()](#module_io.handle+grantpt) ⇒ <code>boolean</code>
    * [.unlockpt()](#module_io.handle+unlockpt) ⇒ <code>boolean</code>
    * [.read(length)](#module_io.handle+read) ⇒ <code>string</code>
    * [.write(data)](#module_io.handle+write) ⇒ <code>number</code>
    * [.seek([offset], [whence])](#module_io.handle+seek) ⇒ <code>boolean</code>
    * [.tell()](#module_io.handle+tell) ⇒ <code>number</code>
    * [.dup()](#module_io.handle+dup) ⇒ [<code>handle</code>](#module_io.handle)
    * [.dup2(newfd)](#module_io.handle+dup2) ⇒ <code>boolean</code>
    * [.fileno()](#module_io.handle+fileno) ⇒ <code>number</code>
    * [.fcntl(cmd, [arg])](#module_io.handle+fcntl) ⇒ <code>number</code> \| [<code>handle</code>](#module_io.handle)
    * [.ioctl(direction, type, num, [value])](#module_io.handle+ioctl) ⇒ <code>number</code> \| <code>string</code>
    * [.isatty()](#module_io.handle+isatty) ⇒ <code>boolean</code>
    * [.close()](#module_io.handle+close) ⇒ <code>boolean</code>
    * [.ptsname()](#module_io.handle+ptsname) ⇒ <code>string</code>
    * [.tcgetattr()](#module_io.handle+tcgetattr) ⇒ <code>object</code>
    * [.tcsetattr(attrs, [when])](#module_io.handle+tcsetattr) ⇒ <code>boolean</code>
    * [.grantpt()](#module_io.handle+grantpt) ⇒ <code>boolean</code>
    * [.unlockpt()](#module_io.handle+unlockpt) ⇒ <code>boolean</code>
    * [.read(length)](#module_io.handle+read) ⇒ <code>string</code>
    * [.write(data)](#module_io.handle+write) ⇒ <code>number</code>
    * [.seek([offset], [whence])](#module_io.handle+seek) ⇒ <code>boolean</code>
    * [.tell()](#module_io.handle+tell) ⇒ <code>number</code>
    * [.dup()](#module_io.handle+dup) ⇒ [<code>handle</code>](#module_io.handle)
    * [.dup2(newfd)](#module_io.handle+dup2) ⇒ <code>boolean</code>
    * [.fileno()](#module_io.handle+fileno) ⇒ <code>number</code>
    * [.fcntl(cmd, [arg])](#module_io.handle+fcntl) ⇒ <code>number</code> \| [<code>handle</code>](#module_io.handle)
    * [.ioctl(direction, type, num, [value])](#module_io.handle+ioctl) ⇒ <code>number</code> \| <code>string</code>
    * [.isatty()](#module_io.handle+isatty) ⇒ <code>boolean</code>
    * [.close()](#module_io.handle+close) ⇒ <code>boolean</code>
    * [.error()](#module_io.handle+error) ⇒ <code>string</code>
    * [.error()](#module_io.handle+error) ⇒ <code>string</code>
    * [.error()](#module_io.handle+error) ⇒ <code>string</code>
    * [.error()](#module_io.handle+error) ⇒ <code>string</code>

<a name="module_io.handle+ptsname"></a>

#### handle.ptsname() ⇒ <code>string</code>
<p>Gets the name of the pseudo-terminal slave.</p>
<p>Returns the name of the pseudo-terminal slave device associated with
the master file descriptor.</p>
<p>Returns a string containing the slave device name.</p>
<p>Returns <code>null</code> if an error occurred or if the descriptor is not a
pseudo-terminal master.</p>

**Kind**: instance method of [<code>handle</code>](#module_io.handle)  
**Example**  
```js
const master = io.open('/dev/ptmx', O_RDWR);
const slave_name = master.ptsname();
print(slave_name, "\n");
```
<a name="module_io.handle+tcgetattr"></a>

#### handle.tcgetattr() ⇒ <code>object</code>
<p>Gets terminal attributes.</p>
<p>Retrieves the terminal attributes for the file descriptor.</p>
<p>Returns an object containing terminal attributes (iflag, oflag, cflag, lflag,
ispeed, ospeed, and cc array).</p>
<p>Returns <code>null</code> if an error occurred or if the descriptor is not a terminal.</p>

**Kind**: instance method of [<code>handle</code>](#module_io.handle)  
**Example**  
```js
const handle = io.open('/dev/tty', O_RDWR);
const attrs = handle.tcgetattr();
if (attrs)
    print("Input flags: ", attrs.iflag, "\n");
```
<a name="module_io.handle+tcsetattr"></a>

#### handle.tcsetattr(attrs, [when]) ⇒ <code>boolean</code>
<p>Sets terminal attributes.</p>
<p>Sets the terminal attributes for the file descriptor.</p>
<p>The attrs parameter should be an object with properties:</p>
<ul>
<li>iflag: input flags</li>
<li>oflag: output flags</li>
<li>cflag: control flags</li>
<li>lflag: local flags</li>
<li>ispeed: input speed</li>
<li>ospeed: output speed</li>
<li>cc: array of control characters (optional)</li>
</ul>
<p>Returns <code>true</code> on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>handle</code>](#module_io.handle)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| attrs | <code>object</code> |  | <p>The terminal attributes to set.</p> |
| [when] | <code>number</code> | <code>0</code> | <p>When to apply the changes (TCSANOW, TCSADRAIN, TCSAFLUSH).</p> |

**Example**  
```js
const handle = io.open('/dev/tty', O_RDWR);
const attrs = handle.tcgetattr();
attrs.lflag &= ~0x0000008; // Disable ECHO
handle.tcsetattr(attrs, TCSANOW);
```
<a name="module_io.handle+grantpt"></a>

#### handle.grantpt() ⇒ <code>boolean</code>
<p>Grants access to a pseudo-terminal slave device.</p>
<p>Allows the owner of the pseudo-terminal master device to grant the
appropriate permissions on the corresponding slave device so that it
may be opened.</p>
<p>This function is typically called before opening the slave device.</p>
<p>Returns <code>true</code> on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>handle</code>](#module_io.handle)  
**Example**  
```js
const master = io.open('/dev/ptmx', O_RDWR);
if (master.grantpt()) {
    print("Granted access to slave device\n");
}
```
<a name="module_io.handle+unlockpt"></a>

#### handle.unlockpt() ⇒ <code>boolean</code>
<p>Unlocks a pseudo-terminal slave device.</p>
<p>Unlocks the pseudo-terminal slave device associated with the master device
referred to by the file descriptor. This function is typically called after
grantpt() and before opening the slave device.</p>
<p>Returns <code>true</code> on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>handle</code>](#module_io.handle)  
**Example**  
```js
const master = io.open('/dev/ptmx', O_RDWR);
master.grantpt();
if (master.unlockpt()) {
    print("Unlocked slave device\n");
}
```
<a name="module_io.handle+read"></a>

#### handle.read(length) ⇒ <code>string</code>
<p>Reads data from the file descriptor.</p>
<p>Reads up to the specified number of bytes from the file descriptor.</p>
<p>Returns a string containing the read data.</p>
<p>Returns an empty string on EOF.</p>
<p>Returns <code>null</code> if a read error occurred.</p>

**Kind**: instance method of [<code>handle</code>](#module_io.handle)  

| Param | Type | Description |
| --- | --- | --- |
| length | <code>number</code> | <p>The maximum number of bytes to read.</p> |

**Example**  
```js
const handle = io.open('/tmp/test.txt', O_RDONLY);
const data = handle.read(1024);
```
<a name="module_io.handle+write"></a>

#### handle.write(data) ⇒ <code>number</code>
<p>Writes data to the file descriptor.</p>
<p>Writes the given data to the file descriptor. Non-string values are
converted to strings before being written.</p>
<p>Returns the number of bytes written.</p>
<p>Returns <code>null</code> if a write error occurred.</p>

**Kind**: instance method of [<code>handle</code>](#module_io.handle)  

| Param | Type | Description |
| --- | --- | --- |
| data | <code>\*</code> | <p>The data to write.</p> |

**Example**  
```js
const handle = io.open('/tmp/test.txt', O_WRONLY | O_CREAT);
handle.write('Hello World\n');
```
<a name="module_io.handle+seek"></a>

#### handle.seek([offset], [whence]) ⇒ <code>boolean</code>
<p>Sets the file descriptor position.</p>
<p>Sets the file position of the


---

<a id="ucode-module-log"></a>
# ucode module: `log`

> **Source:** [`lib/log.c`](https://github.com/jow-/ucode/blob/master/lib/log.c)
> **Live docs:** https://ucode.mein.io/module-log.html
> **Generated:** 2026-03-04 13:26 UTC from commit `e87be9d`

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
<p>This functions configures the ulog mechanism and is analogeous to using the
<code>openlog()</code> function in conjuncton with <code>syslog()</code>.</p>
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
<p>The default facility value varies, depending on the execution context of the
program. In OpenWrt's preinit boot phase, or when stdout is not connected to
an interactive terminal, the facility defaults to <code>&quot;daemon&quot;</code> (<code>LOG_DAEMON</code>),
otherwise to <code>&quot;user&quot;</code> (<code>LOG_USER</code>).</p>
<p>Likewise, the default channel is selected depending on the context. During
OpenWrt's preinit boot phase, the <code>&quot;kmsg&quot;</code> channel is used, for interactive
terminals the <code>&quot;stdio&quot;</code> one and for all other cases the <code>&quot;syslog&quot;</code> channel
is selected.</p>
<p>Returns <code>true</code> if ulog was configured.</p>
<p>Returns <code>false</code> if an invalid argument, such as an unrecognized channel or
facility name, was provided.</p>

**Kind**: instance method of [<code>log</code>](#module_log)  

| Param | Type | Description |
| --- | --- | --- |
| [channel] | <code>number</code> \| [<code>UlogChannel</code>](#module_log.UlogChannel) \| [<code>Array.&lt;UlogChannel&gt;</code>](#module_log.UlogChannel) | <p>Specifies the log channels to use.</p> <p>See [UlogChannel](#module_log.UlogChannel) for recognized channel names.</p> |
| [facility] | <code>number</code> \| [<code>LogFacility</code>](#module_log.LogFacility) | <p>The facility to use for log messages generated by subsequent <code>ulog()</code> calls.</p> <p>See [LogFacility](#module_log.LogFacility) for recognized facility names.</p> |
| [ident] | <code>string</code> | <p>A string identifying the program name. If omitted, the name of the calling process is used by default.</p> |

**Example**  
```js
// Log to dmesg and stderr
ulog_open(["stdio", "kmsg"], "daemon", "my-program");

// Use numeric constants and use implicit default ident
ulog_open(ULOG_SYSLOG, LOG_LOCAL0);
```
<a name="module_log+ulog"></a>

### log.ulog(priority, format, [...args]) ⇒ <code>boolean</code>
<p>Log a message via the ulog mechanism.</p>
<p>The <code>ulog()</code> function outputs the given log message to all configured ulog
channels unless the given priority level exceeds the globally configured ulog
priority threshold. See [ulog_threshold()](#module_log+ulog_threshold)
for details.</p>
<p>The <code>ulog()</code> function is OpenWrt specific and may not be present on other
systems. Use <code>syslog()</code> instead for portability to non-OpenWrt environments.</p>
<p>Like <code>syslog()</code>, the function behaves in a sprintf-like manner, allowing the
use of format strings and associated arguments to construct log messages.</p>
<p>If the <code>ulog_open()</code> function has not been called explicitly before, <code>ulog()</code>
implicitly configures certain defaults, see
[ulog_open()](#module_log+ulog_open) for a detailled description.</p>
<p>If the <code>format</code> argument is not a string and not <code>null</code>, it will be
implicitly converted to a string and logged as-is, without further format
string processing.</p>
<p>Returns <code>true</code> if a message was passed to the underlying <code>ulog()</code> function.</p>
<p>Returns <code>false</code> if an invalid priority value or an empty message was given.</p>

**Kind**: instance method of [<code>log</code>](#module_log)  
**See**

- module:log#ulog_open
- module:log#ulog_threshold
- module:log#syslog


| Param | Type | Description |
| --- | --- | --- |
| priority | <code>number</code> \| [<code>LogPriority</code>](#module_log.LogPriority) | <p>Log message priority. May be either a number value or a priority name string.</p> <p>See [LogPriority](#module_log.LogPriority) for recognized priority names.</p> |
| format | <code>\*</code> | <p>The sprintf-like format string for the log message, or any other, non-null, non-string value type which will be implicitly stringified and logged as-is.</p> |
| [...args] | <code>\*</code> | <p>In case a format string value was provided in the previous argument, then all subsequent arguments are used to replace the placeholders in the format string.</p> |

**Example**  
```js
// Example usage of ulog function with format string and arguments
const username = "user123";
const errorCode = 404;
ulog(LOG_ERR, "User %s encountered error: %d", username, errorCode);

// Using priority names for logging
ulog("err", "General error encountered");

// Implicit stringification
ulog("debug", { foo: 1, bar: true, baz: [1, 2, 3] });
```
<a name="module_log+ulog_close"></a>

### log.ulog\_close()
<p>Close ulog logger.</p>
<p>Resets the ulog channels, the default facility and the log ident value to
defaults.</p>
<p>In case the <code>&quot;syslog&quot;</code> channel has been configured, the underlying
<code>closelog()</code> function will be invoked.</p>
<p>The usage of this function is optional, and usually an explicit ulog teardown
is not required.</p>
<p>The <code>ulog_close()</code> function is OpenWrt specific and may not be present on
other systems. Use <code>closelog()</code> in conjunction with <code>syslog()</code> instead for
portability to non-OpenWrt environments.</p>

**Kind**: instance method of [<code>log</code>](#module_log)  
**See**: module:log#closelog  
<a name="module_log+ulog_threshold"></a>

### log.ulog\_threshold([priority]) ⇒ <code>boolean</code>


---

<a id="ucode-module-math"></a>
# ucode module: `math`

> **Source:** [`lib/math.c`](https://github.com/jow-/ucode/blob/master/lib/math.c)
> **Live docs:** https://ucode.mein.io/module-math.html
> **Generated:** 2026-03-04 13:26 UTC from commit `e87be9d`

---

## Modules

<dl>
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

<a name="module_math"></a>

## math
<h1 id="mathematical-functions">Mathematical Functions</h1>
<p>The <code>math</code> module bundles various mathematical and trigonometrical functions.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { pow, rand } from 'math';

let x = pow(2, 5);
let y = rand();
</code></pre>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as math from 'math';

let x = math.pow(2, 5);
let y = math.rand();
</code></pre>
<p>Additionally, the math module namespace may also be imported by invoking the
<code>ucode</code> interpreter with the <code>-lmath</code> switch.</p>


* [math](#module_math)
    * [.abs(number)](#module_math+abs) ⇒ <code>number</code>
    * [.atan2(y, x)](#module_math+atan2) ⇒ <code>number</code>
    * [.cos(x)](#module_math+cos) ⇒ <code>number</code>
    * [.exp(x)](#module_math+exp) ⇒ <code>number</code>
    * [.log(x)](#module_math+log) ⇒ <code>number</code>
    * [.sin(x)](#module_math+sin) ⇒ <code>number</code>
    * [.sqrt(x)](#module_math+sqrt) ⇒ <code>number</code>
    * [.pow(x, y)](#module_math+pow) ⇒ <code>number</code>
    * [.rand([a], [b])](#module_math+rand) ⇒ <code>number</code>
    * [.srand(seed)](#module_math+srand)
    * [.isnan(x)](#module_math+isnan) ⇒ <code>boolean</code>
    * [.abs(number)](#module_math+abs) ⇒ <code>number</code>
    * [.atan2(y, x)](#module_math+atan2) ⇒ <code>number</code>
    * [.cos(x)](#module_math+cos) ⇒ <code>number</code>
    * [.exp(x)](#module_math+exp) ⇒ <code>number</code>
    * [.log(x)](#module_math+log) ⇒ <code>number</code>
    * [.sin(x)](#module_math+sin) ⇒ <code>number</code>
    * [.sqrt(x)](#module_math+sqrt) ⇒ <code>number</code>
    * [.pow(x, y)](#module_math+pow) ⇒ <code>number</code>
    * [.rand([a], [b])](#module_math+rand) ⇒ <code>number</code>
    * [.srand(seed)](#module_math+srand)
    * [.isnan(x)](#module_math+isnan) ⇒ <code>boolean</code>

<a name="module_math+abs"></a>

### math.abs(number) ⇒ <code>number</code>
<p>Returns the absolute value of the given numeric value.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  
**Returns**: <code>number</code> - <p>Returns the absolute value or <code>NaN</code> if the given argument could
not be converted to a number.</p>  

| Param | Type | Description |
| --- | --- | --- |
| number | <code>\*</code> | <p>The number to return the absolute value for.</p> |

<a name="module_math+atan2"></a>

### math.atan2(y, x) ⇒ <code>number</code>
<p>Calculates the principal value of the arc tangent of <code>y</code>/<code>x</code>,
using the signs of the two arguments to determine the quadrant
of the result.</p>
<p>On success, this function returns the principal value of the arc
tangent of <code>y</code>/<code>x</code> in radians; the return value is in the range [-pi, pi].</p>
<ul>
<li>If <code>y</code> is +0 (-0) and <code>x</code> is less than 0, +pi (-pi) is returned.</li>
<li>If <code>y</code> is +0 (-0) and <code>x</code> is greater than 0, +0 (-0) is returned.</li>
<li>If <code>y</code> is less than 0 and <code>x</code> is +0 or -0, -pi/2 is returned.</li>
<li>If <code>y</code> is greater than 0 and <code>x</code> is +0 or -0, pi/2 is returned.</li>
<li>If either <code>x</code> or <code>y</code> is NaN, a NaN is returned.</li>
<li>If <code>y</code> is +0 (-0) and <code>x</code> is -0, +pi (-pi) is returned.</li>
<li>If <code>y</code> is +0 (-0) and <code>x</code> is +0, +0 (-0) is returned.</li>
<li>If <code>y</code> is a finite value greater (less) than 0, and <code>x</code> is negative
infinity, +pi (-pi) is returned.</li>
<li>If <code>y</code> is a finite value greater (less) than 0, and <code>x</code> is positive
infinity, +0 (-0) is returned.</li>
<li>If <code>y</code> is positive infinity (negative infinity), and <code>x</code> is finite,
pi/2 (-pi/2) is returned.</li>
<li>If <code>y</code> is positive infinity (negative infinity) and <code>x</code> is negative
infinity, +3<em>pi/4 (-3</em>pi/4) is returned.</li>
<li>If <code>y</code> is positive infinity (negative infinity) and <code>x</code> is positive
infinity, +pi/4 (-pi/4) is returned.</li>
</ul>
<p>When either <code>x</code> or <code>y</code> can't be converted to a numeric value, <code>NaN</code> is
returned.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  

| Param | Type | Description |
| --- | --- | --- |
| y | <code>\*</code> | <p>The <code>y</code> value.</p> |
| x | <code>\*</code> | <p>The <code>x</code> value.</p> |

<a name="module_math+cos"></a>

### math.cos(x) ⇒ <code>number</code>
<p>Calculates the cosine of <code>x</code>, where <code>x</code> is given in radians.</p>
<p>Returns the resulting consine value.</p>
<p>Returns <code>NaN</code> if the <code>x</code> value can't be converted to a number.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  

| Param | Type | Description |
| --- | --- | --- |
| x | <code>number</code> | <p>Radians value to calculate cosine for.</p> |

<a name="module_math+exp"></a>

### math.exp(x) ⇒ <code>number</code>
<p>Calculates the value of <code>e</code> (the base of natural logarithms)
raised to the power of <code>x</code>.</p>
<p>On success, returns the exponential value of <code>x</code>.</p>
<ul>
<li>If <code>x</code> is positive infinity, positive infinity is returned.</li>
<li>If <code>x</code> is negative infinity, <code>+0</code> is returned.</li>
<li>If the result underflows, a range error occurs, and zero is returned.</li>
<li>If the result overflows, a range error occurs, and <code>Infinity</code> is returned.</li>
</ul>
<p>Returns <code>NaN</code> if the <code>x</code> value can't be converted to a number.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  

| Param | Type | Description |
| --- | --- | --- |
| x | <code>number</code> | <p>Power to raise <code>e</code> to.</p> |

<a name="module_math+log"></a>

### math.log(x) ⇒ <code>number</code>
<p>Calculates the natural logarithm of <code>x</code>.</p>
<p>On success, returns the natural logarithm of <code>x</code>.</p>
<ul>
<li>If <code>x</code> is <code>1</code>, the result is <code>+0</code>.</li>
<li>If <code>x</code> is positive nfinity, positive infinity is returned.</li>
<li>If <code>x</code> is zero, then a pole error occurs, and the function
returns negative infinity.</li>
<li>If <code>x</code> is negative (including negative infinity), then a domain
error occurs, and <code>NaN</code> is returned.</li>
</ul>
<p>Returns <code>NaN</code> if the <code>x</code> value can't be converted to a number.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  

| Param | Type | Description |
| --- | --- | --- |
| x | <code>number</code> | <p>Value to calulate natural logarithm of.</p> |

<a name="module_math+sin"></a>

### math.sin(x) ⇒ <code>number</code>
<p>Calculates the sine of <code>x</code>, where <code>x</code> is given in radians.</p>
<p>Returns the resulting sine value.</p>
<ul>
<li>When <code>x</code> is positive or negative infinity, a domain error occurs
and <code>NaN</code> is returned.</li>
</ul>
<p>Returns <code>NaN</code> if the <code>x</code> value can't be converted to a number.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  

| Param | Type | Description |
| --- | --- | --- |
| x | <code>number</code> | <p>Radians value to calculate sine for.</p> |

<a name="module_math+sqrt"></a>

### math.sqrt(x) ⇒ <code>number</code>
<p>Calculates the nonnegative square root of <code>x</code>.</p>
<p>Returns the resulting square root value.</p>
<ul>
<li>If <code>x</code> is <code>+0</code> (<code>-0</code>) then <code>+0</code> (<code>-0</code>) is returned.</li>
<li>If <code>x</code> is positive infinity, positive infinity is returned.</li>
<li>If <code>x</code> is less than <code>-0</code>, a domain error occurs, and <code>NaN</code> is returned.</li>
</ul>
<p>Returns <code>NaN</code> if the <code>x</code> value can't be converted to a number.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  

| Param | Type | Description |
| --- | --- | --- |
| x | <code>number</code> | <p>Value to calculate square root for.</p> |

<a name="module_math+pow"></a>

### math.pow(x, y) ⇒ <code>number</code>
<p>Calculates the value of <code>x</code> raised to the power of <code>y</code>.</p>
<p>On success, returns the value of <code>x</code> raised to the power of <code>y</code>.</p>
<ul>
<li>If the result overflows, a range error occurs, and the function
returns <code>Infinity</code>.</li>
<li>If result underflows, and is not representable, a range error
occurs, and <code>0.0</code> with the appropriate sign is returned.</li>
<li>If <code>x</code> is <code>+0</code> or <code>-0</code>, and <code>y</code> is an odd integer less than <code>0</code>,
a pole error occurs <code>Infinity</code> is returned, with the same sign
as <code>x</code>.</li>
<li>If <code>x</code> is <code>+0</code> or <code>-0</code>, and <code>y</code> is less than <code>0</code> and not an odd
integer, a pole error occurs and <code>Infinity</code> is returned.</li>
<li>If <code>x</code> is <code>+0</code> (<code>-0</code>), and <code>y</code> is an odd integer greater than <code>0</code>,
the result is <code>+0</code> (<code>-0</code>).</li>
<li>If <code>x</code> is <code>0</code>, and <code>y</code> greater than <code>0</code> and not an odd integer,
the result is <code>+0</code>.</li>
<li>If <code>x</code> is <code>-1</code>, and <code>y</code> is positive infinity or negative infinity,
the result is <code>1.0</code>.</li>
<li>If <code>x</code> is <code>+1</code>, the result is <code>1.0</code> (even if <code>y</code> is <code>NaN</code>).</li>
<li>If <code>y</code> is <code>0</code>, the result is <code>1.0</code> (even if <code>x</code> is <code>NaN</code>).</li>
<li>If <code>x</code> is a finite value less than <code>0</code>, and <code>y</code> is a finite
noninteger, a domain error occurs, and <code>NaN</code> is returned.</li>
<li>If the absolute value of <code>x</code> is less than <code>1</code>, and <code>y</code> is negative
infinity, the result is positive infinity.</li>
<li>If the absolute value of <code>x</code> is greater than <code>1</code>, and <code>y</code> is
negative infinity, the result is <code>+0</code>.</li>
<li>If the absolute value of <code>x</code> is less than <code>1</code>, and <code>y</code> is positive
infinity, the result is <code>+0</code>.</li>
<li>If the absolute value of <code>x</code> is greater than <code>1</code>, and <code>y</code> is positive
infinity, the result is positive infinity.</li>
<li>If <code>x</code> is negative infinity, and <code>y</code> is an odd integer less than <code>0</code>,
the result is <code>-0</code>.</li>
<li>If <code>x</code> is negative infinity, and <code>y</code> less than <code>0</code> and not an odd
integer, the result is <code>+0</code>.</li>
<li>If <code>x</code> is negative infinity, and <code>y</code> is an odd integer greater than
<code>0</code>, the result is negative infinity.</li>
<li>If <code>x</code> is negative infinity, and <code>y</code> greater than <code>0</code> and not an odd
integer, the result is positive infinity.</li>
<li>If <code>x</code> is positive infinity, and <code>y</code> less than <code>0</code>, the result is <code>+0</code>.</li>
<li>If <code>x</code> is positive infinity, and <code>y</code> greater than <code>0</code>, the result is
positive infinity.</li>
</ul>
<p>Returns <code>NaN</code> if either the <code>x</code> or <code>y</code> value can't be converted to a number.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  

| Param | Type | Description |
| --- | --- | --- |
| x | <code>number</code> | <p>The base value.</p> |
| y | <code>number</code> | <p>The power value.</p> |

<a name="module_math+rand"></a>

### math.rand([a], [b]) ⇒ <code>number</code>
<p>Depending on the arguments, it produces a pseudo-random positive integer,
or a pseudo-random number in a supplied range.</p>
<p>Without arguments it returns the calculated pseuo-random value. The value
is within the range <code>0</code> to <code>RAND_MAX</code> inclusive where <code>RAND_MAX</code> is a platform
specific value guaranteed to be at least <code>32767</code>.</p>
<p>With 2 arguments <code>a, b</code> it returns a number in the range <code>a</code> to <code>b</code> inclusive.
With a single argument <code>a</code> it returns a number in the range <code>0</code> to <code>a</code> inclusive.</p>
<p>The [<code>srand()</code>](module:math~srand) function sets its argument as the
seed for a new sequence of pseudo-random integers to be returned by <code>rand()</code>.
These sequences are repeatable by calling [<code>srand()</code>](module:math~srand)
with the same seed value.</p>
<p>If no seed value is explicitly set by calling
[<code>srand()</code>](module:math~srand) prior to the first call to <code>rand()</code>,
the math module will automatically seed the PRNG once, using the current
time of day in milliseconds as seed value.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  

| Param | Type | Description |
| --- | --- | --- |
| [a] | <code>number</code> | <p>End of the desired range.</p> |
| [b] | <code>number</code> | <p>The other end of the desired range.</p> |

<a name="module_math+srand"></a>

### math.srand(seed)
<p>Seeds the pseudo-random number generator.</p>
<p>This functions seeds the PRNG with the given value and thus affects the
pseudo-random integer sequence produced by subsequent calls to
[<code>rand()</code>](module:math~rand).</p>
<p>Setting the same seed value will result in the same pseudo-random numbers
produced by [<code>rand()</code>](module:math~rand).</p>

**Kind**: instance method of [<code>math</code>](#module_math)  

| Param | Type | Description |
| --- | --- | --- |
| seed | <code>number</code> | <p>The seed value.</p> |

<a name="module_math+isnan"></a>

### math.isnan(x) ⇒ <code>boolean</code>
<p>Tests whether <code>x</code> is a <code>NaN</code> double.</p>
<p>This functions checks whether the given argument is of type <code>double</code> with
a <code>NaN</code> (not a number) value.</p>
<p>Returns <code>true</code> if the value is <code>NaN</code>, otherwise false.</p>
<p>Note that a value can also be checked for <code>NaN</code> with the expression
<code>x !== x</code> which only evaluates to <code>true</code> if <code>x</code> is <code>NaN</code>.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  

| Param | Type | Description |
| --- | --- | --- |
| x | <code>number</code> | <p>The value to test.</p> |

<a name="module_math+abs"></a>

### math.abs(number) ⇒ <code>number</code>
<p>Returns the absolute value of the given numeric value.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  
**Returns**: <code>number</code> - <p>Returns the absolute value or <code>NaN</code> if the given argument could
not be converted to a number.</p>  

| Param | Type | Description |
| --- | --- | --- |
| number | <code>\*</code> | <p>The number to return the absolute value for.</p> |

<a name="module_math+atan2"></a>

### math.atan2(y, x) ⇒ <code>number</code>
<p>Calculates the principal value of the arc tangent of <code>y</code>/<code>x</code>,
using the signs of the two arguments to determine the quadrant
of the result.</p>
<p>On success, this function returns the principal value of the arc
tangent of <code>y</code>/<code>x</code> in radians; the return value is in the range [-pi, pi].</p>
<ul>
<li>If <code>y</code> is +0 (-0) and <code>x</code> is less than 0, +pi (-pi) is returned.</li>
<li>If <code>y</code> is +0 (-0) and <code>x</code> is greater than 0, +0 (-0) is returned.</li>
<li>If <code>y</code> is less than 0 and <code>x</code> is +0 or -0, -pi/2 is returned.</li>
<li>If <code>y</code> is greater than 0 and <code>x</code> is +0 or -0, pi/2 is returned.</li>
<li>If either <code>x</code> or <code>y</code> is NaN, a NaN is returned.</li>
<li>If <code>y</code> is +0 (-0) and <code>x</code> is -0, +pi (-pi) is returned.</li>
<li>If <code>y</code> is +0 (-0) and <code>x</code> is +0, +0 (-0) is returned.</li>
<li>If <code>y</code> is a finite value greater (less) than 0, and <code>x</code> is negative
infinity, +pi (-pi) is returned.</li>
<li>If <code>y</code> is a finite value greater (less) than 0, and <code>x</code> is positive
infinity, +0 (-0) is returned.</li>
<li>If <code>y</code> is positive infinity (negative infinity), and <code>x</code> is finite,
pi/2 (-pi/2) is returned.</li>
<li>If <code>y</code> is positive infinity (negative infinity) and <code>x</code> is negative
infinity, +3<em>pi/4 (-3</em>pi/4) is returned.</li>
<li>If <code>y</code> is positive infinity (negative infinity) and <code>x</code> is positive
infinity, +pi/4 (-pi/4) is returned.</li>
</ul>
<p>When either <code>x</code> or <code>y</code> can't be converted to a numeric value, <code>NaN</code> is
returned.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  

| Param | Type | Description |
| --- | --- | --- |
| y | <code>\*</code> | <p>The <code>y</code> value.</p> |
| x | <code>\*</code> | <p>The <code>x</code> value.</p> |

<a name="module_math+cos"></a>

### math.cos(x) ⇒ <code>number</code>
<p>Calculates the cosine of <code>x</code>, where <code>x</code> is given in radians.</p>
<p>Returns the resulting consine value.</p>
<p>Returns <code>NaN</code> if the <code>x</code> value can't be converted to a number.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  

| Param | Type | Description |
| --- | --- | --- |
| x | <code>number</code> | <p>Radians value to calculate cosine for.</p> |

<a name="module_math+exp"></a>

### math.exp(x) ⇒ <code>number</code>
<p>Calculates the value of <code>e</code> (the base of natural logarithms)
raised to the power of <code>x</code>.</p>
<p>On success, returns the exponential value of <code>x</code>.</p>
<ul>
<li>If <code>x</code> is positive infinity, positive infinity is returned.</li>
<li>If <code>x</code> is negative infinity, <code>+0</code> is returned.</li>
<li>If the result underflows, a range error occurs, and zero is returned.</li>
<li>If the result overflows, a range error occurs, and <code>Infinity</code> is returned.</li>
</ul>
<p>Returns <code>NaN</code> if the <code>x</code> value can't be converted to a number.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  

| Param | Type | Description |
| --- | --- | --- |
| x | <code>number</code> | <p>Power to raise <code>e</code> to.</p> |

<a name="module_math+log"></a>

### math.log(x) ⇒ <code>number</code>
<p>Calculates the natural logarithm of <code>x</code>.</p>
<p>On success, returns the natural logarithm of <code>x</code>.</p>
<ul>
<li>If <code>x</code> is <code>1</code>, the result is <code>+0</code>.</li>
<li>If <code>x</code> is positive nfinity, positive infinity is returned.</li>
<li>If <code>x</code> is zero, then a pole error occurs, and the function
returns negative infinity.</li>
<li>If <code>x</code> is negative (including negative infinity), then a domain
error occurs, and <code>NaN</code> is returned.</li>
</ul>
<p>Returns <code>NaN</code> if the <code>x</code> value can't be converted to a number.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  

| Param | Type | Description |
| --- | --- | --- |
| x | <code>number</code> | <p>Value to calulate natural logarithm of.</p> |

<a name="module_math+sin"></a>

### math.sin(x) ⇒ <code>number</code>
<p>Calculates the sine of <code>x</code>, where <code>x</code> is given in radians.</p>
<p>Returns the resulting sine value.</p>
<ul>
<li>When <code>x</code> is positive or negative infinity, a domain error occurs
and <code>NaN</code> is returned.</li>
</ul>
<p>Returns <code>NaN</code> if the <code>x</code> value can't be converted to a number.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  

| Param | Type | Description |
| --- | --- | --- |
| x | <code>number</code> | <p>Radians value to calculate sine for.</p> |

<a name="module_math+sqrt"></a>

### math.sqrt(x) ⇒ <code>number</code>
<p>Calculates the nonnegative square root of <code>x</code>.</p>
<p>Returns the resulting square root value.</p>
<ul>
<li>If <code>x</code> is <code>+0</code> (<code>-0</code>) then <code>+0</code> (<code>-0</code>) is returned.</li>
<li>If <code>x</code> is positive infinity, positive infinity is returned.</li>
<li>If <code>x</code> is less than <code>-0</code>, a domain error occurs, and <code>NaN</code> is returned.</li>
</ul>
<p>Returns <code>NaN</code> if the <code>x</code> value can't be converted to a number.</p>

**Kind**: instance method of [<code>math</code>](#module_math)  

| Param | Type | Description |
| --- | --- | --- |
| x | <code>number</code> | <p>Value to calculate square root for.</p> |

<a name="module_math+pow"></a>

### math.pow(x, y) ⇒ <code>number</code>
<p>Calculates the value of <code>x</code> raised to the power of <code>y</code>.</p>
<p>On success, returns the value of <code>x</code> raised to the power of <code>y</code>.</p>
<ul>
<li>If the result overflows, a range error occurs, and the function
returns <code>Infinity</code>.</li>
<li>If result underflows, and is not representable, a range error
occurs, and <code>0.0</code> with the appropriate sign is returned.</li>
<li>If <code>x</code> is <code>+0</code> or <code>-0</code>, and <code>y</code> is an odd integer less than <code>0</code>,
a pole error occurs <code>Infinity</code> is returned, with the same sign
as <code>x</code>.</li>
<li>If <code>x</code> is <code>+0</code> or <code>-0</code>, and <code>y</code> is less than <code>0</code> and not an odd
integer, a pole error occurs and <code>Infinity</code> is returned.</li>
<li>If <code>x</code> is <code>+0</code> (<code>-0</code>), and <code>y</code> is an odd integer greater than <code>0</code>,
the result is <code>+0</code> (<code>-0</code>).</li>
<li>If <code>x</code> is <code>0</code>, and <code>y</code> greater than <code>0</code> and not an odd integer,
the result is <code>+0</code>.</li>
<li>If <code>x</code> is <code>-1</code>, and <code>y</code> is positive infinity or negative infinity,
the result is <code>1.0</code>.</li>
<li>If <code>x</code> is <code>+1</code>, the result is <code>1.0</code> (even if <code>y</code> is <code>NaN</code>).</li>
<li>If <code>y</code> is <code>0</code>, the result is <code>1.0</code> (even if <code>x</code> is <code>NaN</code>).</li>
<li>If <code>x</code> is a finite value less than <code>0</code>, and <code>y</code> is a finite
noninteger, a domain error occurs, and <code>NaN</code> is returned.</li>
<li>If the absolute value of <code>x</code> is less than <code>1</code>, and <code>y</code> is negative
infinity, the result is positive infinity.</li>
<li>If the absolute value of <code>x</code> is greater than <code>1</code>, and <code>y</code> is
negative infinity, the result is <code>+0</code>.</li>
<li>If the absolute value of <code>x</code> is less than <code>1</code>, and <code>y</code> is positive
infinity, the result is <code>+0</code>.</li>
<li>If the absolute value of <code>x</code> is greater than <code>1</code>, and <code>y</code> is positive
infinity, the result is positive infinity.</li>
<li>If <code>x</code> is negative infinity, and <code>y</code> is an odd integer less than <code>0</cod


---

<a id="ucode-module-nl80211"></a>
# ucode module: `nl80211`

> **Source:** [`lib/nl80211.c`](https://github.com/jow-/ucode/blob/master/lib/nl80211.c)
> **Live docs:** https://ucode.mein.io/module-nl80211.html
> **Generated:** 2026-03-04 13:26 UTC from commit `e87be9d`

---

## Modules

<dl>
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

<a name="module_nl80211"></a>

## nl80211
<h1 id="wireless-netlink">Wireless Netlink</h1>
<p>The <code>nl80211</code> module provides functions for interacting with the nl80211 netlink interface
for wireless networking configuration and management.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source lang-javascript"><code>import { error, request, listener, waitfor, const } from 'nl80211';

// Send a nl80211 request
let response = request(const.NL80211_CMD_GET_WIPHY, 0, { wiphy: 0 });

// Create a listener for wireless events
let wifiListener = listener((msg) => {
    print('Received wireless event:', msg, '\n');
}, [const.NL80211_CMD_NEW_INTERFACE, const.NL80211_CMD_DEL_INTERFACE]);

// Wait for a specific nl80211 event
let event = waitfor([const.NL80211_CMD_NEW_SCAN_RESULTS], 5000);
if (event)
    print('Received scan results:', event.msg, '\n');
</code></pre>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source lang-javascript"><code>import * as nl80211 from 'nl80211';

// Send a nl80211 request
let response = nl80211.request(nl80211.const.NL80211_CMD_GET_WIPHY, 0, { wiphy: 0 });

// Create a listener for wireless events
let listener = nl80211.listener((msg) => {
    print('Received wireless event:', msg, '\n');
}, [nl80211.const.NL80211_CMD_NEW_INTERFACE, nl80211.const.NL80211_CMD_DEL_INTERFACE]);
</code></pre>
<p>Additionally, the nl80211 module namespace may also be imported by invoking
the <code>ucode</code> interpreter with the <code>-lnl80211</code> switch.</p>


* [nl80211](#module_nl80211)
    * _static_
        * [.listener](#module_nl80211.listener)
        * [.listener](#module_nl80211.listener)
    * _inner_
        * [~Netlink message flags](#module_nl80211..Netlink message flags)
        * [~nl80211 commands](#module_nl80211..nl80211 commands)
        * [~Scan flags](#module_nl80211..Scan flags)
        * [~BSS status constants](#module_nl80211..BSS status constants)
        * [~BSS use-for and cannot-use-reasons constants](#module_nl80211..BSS use-for and cannot-use-reasons constants)
        * [~HWSIM commands](#module_nl80211..HWSIM commands)
        * [~Interface types](#module_nl80211..Interface types)
        * [~Netlink message flags](#module_nl80211..Netlink message flags)
        * [~nl80211 commands](#module_nl80211..nl80211 commands)
        * [~Scan flags](#module_nl80211..Scan flags)
        * [~BSS status constants](#module_nl80211..BSS status constants)
        * [~BSS use-for and cannot-use-reasons constants](#module_nl80211..BSS use-for and cannot-use-reasons constants)
        * [~HWSIM commands](#module_nl80211..HWSIM commands)
        * [~Interface types](#module_nl80211..Interface types)

<a name="module_nl80211.listener"></a>

### nl80211.listener
**Kind**: static class of [<code>nl80211</code>](#module_nl80211)  
**See**: [listener()](module:nl80211#listener)  
<a name="module_nl80211.listener"></a>

### nl80211.listener
**Kind**: static class of [<code>nl80211</code>](#module_nl80211)  
**See**: [listener()](module:nl80211#listener)  
<a name="module_nl80211..Netlink message flags"></a>

### nl80211~Netlink message flags
**Kind**: inner typedef of [<code>nl80211</code>](#module_nl80211)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| NLM_F_ACK | <code>number</code> | <p>Request for acknowledgment</p> |
| NLM_F_ACK_TLVS | <code>number</code> | <p>Request for acknowledgment with TLVs</p> |
| NLM_F_APPEND | <code>number</code> | <p>Append to existing list</p> |
| NLM_F_ATOMIC | <code>number</code> | <p>Atomic operation</p> |
| NLM_F_CAPPED | <code>number</code> | <p>Request capped</p> |
| NLM_F_CREATE | <code>number</code> | <p>Create if not exists</p> |
| NLM_F_DUMP | <code>number</code> | <p>Dump request</p> |
| NLM_F_DUMP_FILTERED | <code>number</code> | <p>Dump filtered request</p> |
| NLM_F_DUMP_INTR | <code>number</code> | <p>Dump interrupted</p> |
| NLM_F_ECHO | <code>number</code> | <p>Echo request</p> |
| NLM_F_EXCL | <code>number</code> | <p>Exclusive creation</p> |
| NLM_F_MATCH | <code>number</code> | <p>Match request</p> |
| NLM_F_MULTI | <code>number</code> | <p>Multi-part message</p> |
| NLM_F_NONREC | <code>number</code> | <p>Non-recursive operation</p> |
| NLM_F_REPLACE | <code>number</code> | <p>Replace existing</p> |
| NLM_F_REQUEST | <code>number</code> | <p>Request message</p> |
| NLM_F_ROOT | <code>number</code> | <p>Root operation</p> |

<a name="module_nl80211..nl80211 commands"></a>

### nl80211~nl80211 commands
**Kind**: inner typedef of [<code>nl80211</code>](#module_nl80211)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| NL80211_CMD_GET_WIPHY | <code>number</code> | <p>Get wireless PHY attributes</p> |
| NL80211_CMD_SET_WIPHY | <code>number</code> | <p>Set wireless PHY attributes</p> |
| NL80211_CMD_NEW_WIPHY | <code>number</code> | <p>Create new wireless PHY</p> |
| NL80211_CMD_DEL_WIPHY | <code>number</code> | <p>Delete wireless PHY</p> |
| NL80211_CMD_GET_INTERFACE | <code>number</code> | <p>Get interface information</p> |
| NL80211_CMD_SET_INTERFACE | <code>number</code> | <p>Set interface attributes</p> |
| NL80211_CMD_NEW_INTERFACE | <code>number</code> | <p>Create new interface</p> |
| NL80211_CMD_DEL_INTERFACE | <code>number</code> | <p>Delete interface</p> |
| NL80211_CMD_GET_KEY | <code>number</code> | <p>Get key</p> |
| NL80211_CMD_SET_KEY | <code>number</code> | <p>Set key</p> |
| NL80211_CMD_NEW_KEY | <code>number</code> | <p>Add new key</p> |
| NL80211_CMD_DEL_KEY | <code>number</code> | <p>Delete key</p> |
| NL80211_CMD_GET_BEACON | <code>number</code> | <p>Get beacon</p> |
| NL80211_CMD_SET_BEACON | <code>number</code> | <p>Set beacon</p> |
| NL80211_CMD_NEW_BEACON | <code>number</code> | <p>Set beacon (alias)</p> |
| NL80211_CMD_STOP_AP | <code>number</code> | <p>Stop AP operation</p> |
| NL80211_CMD_DEL_BEACON | <code>number</code> | <p>Delete beacon</p> |
| NL80211_CMD_GET_STATION | <code>number</code> | <p>Get station information</p> |
| NL80211_CMD_SET_STATION | <code>number</code> | <p>Set station attributes</p> |
| NL80211_CMD_NEW_STATION | <code>number</code> | <p>Add new station</p> |
| NL80211_CMD_DEL_STATION | <code>number</code> | <p>Delete station</p> |
| NL80211_CMD_GET_MPATH | <code>number</code> | <p>Get mesh path</p> |
| NL80211_CMD_SET_MPATH | <code>number</code> | <p>Set mesh path</p> |
| NL80211_CMD_NEW_MPATH | <code>number</code> | <p>Add new mesh path</p> |
| NL80211_CMD_DEL_MPATH | <code>number</code> | <p>Delete mesh path</p> |
| NL80211_CMD_SET_BSS | <code>number</code> | <p>Set BSS attributes</p> |
| NL80211_CMD_SET_REG | <code>number</code> | <p>Set regulatory domain</p> |
| NL80211_CMD_REQ_SET_REG | <code>number</code> | <p>Request regulatory domain change</p> |
| NL80211_CMD_GET_MESH_CONFIG | <code>number</code> | <p>Get mesh configuration</p> |
| NL80211_CMD_SET_MESH_CONFIG | <code>number</code> | <p>Set mesh configuration</p> |
| NL80211_CMD_GET_REG | <code>number</code> | <p>Get regulatory domain</p> |
| NL80211_CMD_GET_SCAN | <code>number</code> | <p>Get scan results</p> |
| NL80211_CMD_TRIGGER_SCAN | <code>number</code> | <p>Trigger scan</p> |
| NL80211_CMD_NEW_SCAN_RESULTS | <code>number</code> | <p>New scan results available</p> |
| NL80211_CMD_SCAN_ABORTED | <code>number</code> | <p>Scan aborted</p> |
| NL80211_CMD_REG_CHANGE | <code>number</code> | <p>Regulatory domain change</p> |
| NL80211_CMD_AUTHENTICATE | <code>number</code> | <p>Authenticate</p> |
| NL80211_CMD_ASSOCIATE | <code>number</code> | <p>Associate</p> |
| NL80211_CMD_DEAUTHENTICATE | <code>number</code> | <p>Deauthenticate</p> |
| NL80211_CMD_DISASSOCIATE | <code>number</code> | <p>Disassociate</p> |
| NL80211_CMD_MICHAEL_MIC_FAILURE | <code>number</code> | <p>Michael MIC failure</p> |
| NL80211_CMD_REG_BEACON_HINT | <code>number</code> | <p>Beacon regulatory hint</p> |
| NL80211_CMD_JOIN_IBSS | <code>number</code> | <p>Join IBSS</p> |
| NL80211_CMD_LEAVE_IBSS | <code>number</code> | <p>Leave IBSS</p> |
| NL80211_CMD_TESTMODE | <code>number</code> | <p>Test mode</p> |
| NL80211_CMD_CONNECT | <code>number</code> | <p>Connect</p> |
| NL80211_CMD_ROAM | <code>number</code> | <p>Roam</p> |
| NL80211_CMD_DISCONNECT | <code>number</code> | <p>Disconnect</p> |
| NL80211_CMD_SET_WIPHY_NETNS | <code>number</code> | <p>Set wireless PHY network namespace</p> |
| NL80211_CMD_GET_SURVEY | <code>number</code> | <p>Get survey data</p> |
| NL80211_CMD_NEW_SURVEY_RESULTS | <code>number</code> | <p>New survey results</p> |
| NL80211_CMD_SET_PMKSA | <code>number</code> | <p>Set PMKSA</p> |
| NL80211_CMD_DEL_PMKSA | <code>number</code> | <p>Delete PMKSA</p> |
| NL80211_CMD_FLUSH_PMKSA | <code>number</code> | <p>Flush PMKSA</p> |
| NL80211_CMD_REMAIN_ON_CHANNEL | <code>number</code> | <p>Remain on channel</p> |
| NL80211_CMD_CANCEL_REMAIN_ON_CHANNEL | <code>number</code> | <p>Cancel remain on channel</p> |
| NL80211_CMD_SET_TX_BITRATE_MASK | <code>number</code> | <p>Set TX bitrate mask</p> |
| NL80211_CMD_REGISTER_FRAME | <code>number</code> | <p>Register frame</p> |
| NL80211_CMD_REGISTER_ACTION | <code>number</code> | <p>Register action frame</p> |
| NL80211_CMD_FRAME | <code>number</code> | <p>Frame</p> |
| NL80211_CMD_ACTION | <code>number</code> | <p>Action frame</p> |
| NL80211_CMD_FRAME_TX_STATUS | <code>number</code> | <p>Frame TX status</p> |
| NL80211_CMD_ACTION_TX_STATUS | <code>number</code> | <p>Action TX status</p> |
| NL80211_CMD_SET_POWER_SAVE | <code>number</code> | <p>Set power save</p> |
| NL80211_CMD_GET_POWER_SAVE | <code>number</code> | <p>Get power save</p> |
| NL80211_CMD_SET_CQM | <code>number</code> | <p>Set CQM</p> |
| NL80211_CMD_NOTIFY_CQM | <code>number</code> | <p>Notify CQM</p> |
| NL80211_CMD_SET_CHANNEL | <code>number</code> | <p>Set channel</p> |
| NL80211_CMD_SET_WDS_PEER | <code>number</code> | <p>Set WDS peer</p> |
| NL80211_CMD_FRAME_WAIT_CANCEL | <code>number</code> | <p>Cancel frame wait</p> |
| NL80211_CMD_JOIN_MESH | <code>number</code> | <p>Join mesh</p> |
| NL80211_CMD_LEAVE_MESH | <code>number</code> | <p>Leave mesh</p> |
| NL80211_CMD_UNPROT_DEAUTHENTICATE | <code>number</code> | <p>Unprotected deauthenticate</p> |
| NL80211_CMD_UNPROT_DISASSOCIATE | <code>number</code> | <p>Unprotected disassociate</p> |
| NL80211_CMD_NEW_PEER_CANDIDATE | <code>number</code> | <p>New peer candidate</p> |
| NL80211_CMD_GET_WOWLAN | <code>number</code> | <p>Get WoWLAN</p> |
| NL80211_CMD_SET_WOWLAN | <code>number</code> | <p>Set WoWLAN</p> |
| NL80211_CMD_START_SCHED_SCAN | <code>number</code> | <p>Start scheduled scan</p> |
| NL80211_CMD_STOP_SCHED_SCAN | <code>number</code> | <p>Stop scheduled scan</p> |
| NL80211_CMD_SCHED_SCAN_RESULTS | <code>number</code> | <p>Scheduled scan results</p> |
| NL80211_CMD_SCHED_SCAN_STOPPED | <code>number</code> | <p>Scheduled scan stopped</p> |
| NL80211_CMD_SET_REKEY_OFFLOAD | <code>number</code> | <p>Set rekey offload</p> |
| NL80211_CMD_PMKSA_CANDIDATE | <code>number</code> | <p>PMKSA candidate</p> |
| NL80211_CMD_TDLS_OPER | <code>number</code> | <p>TDLS operation</p> |
| NL80211_CMD_TDLS_MGMT | <code>number</code> | <p>TDLS management</p> |
| NL80211_CMD_UNEXPECTED_FRAME | <code>number</code> | <p>Unexpected frame</p> |
| NL80211_CMD_PROBE_CLIENT | <code>number</code> | <p>Probe client</p> |
| NL80211_CMD_REGISTER_BEACONS | <code>number</code> | <p>Register beacons</p> |
| NL80211_CMD_UNEXPECTED_4ADDR_FRAME | <code>number</code> | <p>Unexpected 4-address frame</p> |
| NL80211_CMD_SET_NOACK_MAP | <code>number</code> | <p>Set no-ack map</p> |
| NL80211_CMD_CH_SWITCH_NOTIFY | <code>number</code> | <p>Channel switch notify</p> |
| NL80211_CMD_START_P2P_DEVICE | <code>number</code> | <p>Start P2P device</p> |
| NL80211_CMD_STOP_P2P_DEVICE | <code>number</code> | <p>Stop P2P device</p> |
| NL80211_CMD_CONN_FAILED | <code>number</code> | <p>Connection failed</p> |
| NL80211_CMD_SET_MCAST_RATE | <code>number</code> | <p>Set multicast rate</p> |
| NL80211_CMD_SET_MAC_ACL | <code>number</code> | <p>Set MAC ACL</p> |
| NL80211_CMD_RADAR_DETECT | <code>number</code> | <p>Radar detect</p> |
| NL80211_CMD_GET_PROTOCOL_FEATURES | <code>number</code> | <p>Get protocol features</p> |
| NL80211_CMD_UPDATE_FT_IES | <code>number</code> | <p>Update FT IEs</p> |
| NL80211_CMD_FT_EVENT | <code>number</code> | <p>FT event</p> |
| NL80211_CMD_CRIT_PROTOCOL_START | <code>number</code> | <p>Start critical protocol</p> |
| NL80211_CMD_CRIT_PROTOCOL_STOP | <code>number</code> | <p>Stop critical protocol</p> |
| NL80211_CMD_GET_COALESCE | <code>number</code> | <p>Get coalesce</p> |
| NL80211_CMD_SET_COALESCE | <code>number</code> | <p>Set coalesce</p> |
| NL80211_CMD_CHANNEL_SWITCH | <code>number</code> | <p>Channel switch</p> |
| NL80211_CMD_VENDOR | <code>number</code> | <p>Vendor command</p> |
| NL80211_CMD_SET_QOS_MAP | <code>number</code> | <p>Set QoS map</p> |
| NL80211_CMD_ADD_TX_TS | <code>number</code> | <p>Add TX TS</p> |
| NL80211_CMD_DEL_TX_TS | <code>number</code> | <p>Delete TX TS</p> |
| NL80211_CMD_GET_MPP | <code>number</code> | <p>Get MPP</p> |
| NL80211_CMD_JOIN_OCB | <code>number</code> | <p>Join OCB</p> |
| NL80211_CMD_LEAVE_OCB | <code>number</code> | <p>Leave OCB</p> |
| NL80211_CMD_CH_SWITCH_STARTED_NOTIFY | <code>number</code> | <p>Channel switch started notify</p> |
| NL80211_CMD_TDLS_CHANNEL_SWITCH | <code>number</code> | <p>TDLS channel switch</p> |
| NL80211_CMD_TDLS_CANCEL_CHANNEL_SWITCH | <code>number</code> | <p>Cancel TDLS channel switch</p> |
| NL80211_CMD_ABORT_SCAN | <code>number</code> | <p>Abort scan</p> |

<a name="module_nl80211..Scan flags"></a>

### nl80211~Scan flags
<p>Constants for NL80211_ATTR_SCAN_FLAGS bitmask.</p>

**Kind**: inner typedef of [<code>nl80211</code>](#module_nl80211)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| NL80211_SCAN_FLAG_LOW_PRIORITY | <code>number</code> | <p>Low priority scan</p> |
| NL80211_SCAN_FLAG_FLUSH | <code>number</code> | <p>Flush scan results before returning</p> |
| NL80211_SCAN_FLAG_AP | <code>number</code> | <p>Force AP mode scan</p> |
| NL80211_SCAN_FLAG_RANDOM_ADDR | <code>number</code> | <p>Randomize source MAC address</p> |
| NL80211_SCAN_FLAG_FILS_MAX_CHANNEL_TIME | <code>number</code> | <p>FILS max channel time</p> |
| NL80211_SCAN_FLAG_ACCEPT_BCAST_PROBE_RESP | <code>number</code> | <p>Accept broadcast probe responses</p> |
| NL80211_SCAN_FLAG_OCE_PROBE_REQ_HIGH_TX_RATE | <code>number</code> | <p>OCE high TX rate probe requests</p> |
| NL80211_SCAN_FLAG_OCE_PROBE_REQ_DEFERRAL_SUPPRESSION | <code>number</code> | <p>OCE probe request deferral suppression</p> |
| NL80211_SCAN_FLAG_LOW_SPAN | <code>number</code> | <p>Low span scan</p> |
| NL80211_SCAN_FLAG_LOW_POWER | <code>number</code> | <p>Low power scan</p> |
| NL80211_SCAN_FLAG_HIGH_ACCURACY | <code>number</code> | <p>High accuracy scan</p> |
| NL80211_SCAN_FLAG_RANDOM_SN | <code>number</code> | <p>Randomize sequence number</p> |
| NL80211_SCAN_FLAG_MIN_PREQ_CONTENT | <code>number</code> | <p>Minimize probe request content</p> |
| NL80211_SCAN_FLAG_FREQ_KHZ | <code>number</code> | <p>Report scan results with frequency in KHz</p> |
| NL80211_SCAN_FLAG_COLOCATED_6GHZ | <code>number</code> | <p>Scan colocated 6GHz BSS</p> |

<a name="module_nl80211..BSS status constants"></a>

### nl80211~BSS status constants
<p>Constants for BSS status values.</p>

**Kind**: inner typedef of [<code>nl80211</code>](#module_nl80211)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| NL80211_BSS_STATUS_AUTHENTICATED | <code>number</code> | <p>Authenticated with BSS</p> |
| NL80211_BSS_STATUS_ASSOCIATED | <code>number</code> | <p>Associated with BSS</p> |
| NL80211_BSS_STATUS_IBSS_JOINED | <code>number</code> | <p>Joined IBSS</p> |

<a name="module_nl80211..BSS use-for and cannot-use-reasons constants"></a>

### nl80211~BSS use-for and cannot-use-reasons constants
<p>Constants for BSS use-for and cannot-use-reasons bitmasks.</p>

**Kind**: inner typedef of [<code>nl80211</code>](#module_nl80211)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| NL80211_BSS_USE_FOR_NORMAL | <code>number</code> | <p>Use BSS for normal connection</p> |
| NL80211_BSS_USE_FOR_MLD_LINK | <code>number</code> | <p>Use BSS as MLD link</p> |
| NL80211_BSS_CANNOT_USE_NSTR_NONPRIMARY | <code>number</code> | <p>NSTR nonprimary link not usable</p> |
| NL80211_BSS_CANNOT_USE_6GHZ_PWR_MISMATCH | <code>number</code> | <p>6GHz power mode mismatch</p> |

<a name="module_nl80211..HWSIM commands"></a>

### nl80211~HWSIM commands
**Kind**: inner typedef of [<code>nl80211</code>](#module_nl80211)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| HWSIM_CMD_REGISTER | <code>number</code> | <p>Register radio</p> |
| HWSIM_CMD_FRAME | <code>number</code> | <p>Send frame</p> |
| HWSIM_CMD_TX_INFO_FRAME | <code>number</code> | <p>Send TX info frame</p> |
| HWSIM_CMD_NEW_RADIO | <code>number</code> | <p>Create new radio</p> |
| HWSIM_CMD_DEL_RADIO | <code>number</code> | <p>Delete radio</p> |
| HWSIM_CMD_GET_RADIO | <code>number</code> | <p>Get radio information</p> |
| HWSIM_CMD_ADD_MAC_ADDR | <code>number</code> | <p>Add MAC address</p> |
| HWSIM_CMD_DEL_MAC_ADDR | <code>number</code> | <p>Delete MAC address</p> |
| HWSIM_CMD_START_PMSR | <code>number</code> | <p>Start peer measurement</p> |
| HWSIM_CMD_ABORT_PMSR | <code>number</code> | <p>Abort peer measurement</p> |
| HWSIM_CMD_REPORT_PMSR | <code>number</code> | <p>Report peer measurement</p> |

<a name="module_nl80211..Interface types"></a>

### nl80211~Interface types
**Kind**: inner typedef of [<code>nl80211</code>](#module_nl80211)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| NL80211_IFTYPE_ADHOC | <code>number</code> | <p>IBSS/ad-hoc interface</p> |
| NL80211_IFTYPE_STATION | <code>number</code> | <p>Station interface</p> |
| NL80211_IFTYPE_AP | <code>number</code> | <p>Access point interface</p> |
| NL80211_IFTYPE_AP_VLAN | <code>number</code> | <p>AP VLAN interface</p> |
| NL80211_IFTYPE_WDS | <code>number</code> | <p>WDS interface</p> |
| NL80211_IFTYPE_MONITOR | <code>number</code> | <p>Monitor interface</p> |
| NL80211_IFTYPE_MESH_POINT | <code>number</code> | <p>Mesh point interface</p> |
| NL80211_IFTYPE_P2P_CLIENT | <code>number</code> | <p>P2P client interface</p> |
| NL80211_IFTYPE_P2P_GO | <code>number</code> | <p>P2P group owner interface</p> |
| NL80211_IFTYPE_P2P_DEVICE | <code>number</code> | <p>P2P device interface</p> |
| NL80211_IFTYPE_OCB | <code>number</code> | <p>Outside context of BSS (OCB) interface</p> |

<a name="module_nl80211..Netlink message flags"></a>

### nl80211~Netlink message flags
**Kind**: inner typedef of [<code>nl80211</code>](#module_nl80211)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| NLM_F_ACK | <code>number</code> | <p>Request for acknowledgment</p> |
| NLM_F_ACK_TLVS | <code>number</code> | <p>Request for acknowledgment with TLVs</p> |
| NLM_F_APPEND | <code>number</code> | <p>Append to existing list</p> |
| NLM_F_ATOMIC | <code>number</code> | <p>Atomic operation</p> |
| NLM_F_CAPPED | <code>number</code> | <p>Request capped</p> |
| NLM_F_CREATE | <code>number</code> | <p>Create if not exists</p> |
| NLM_F_DUMP | <code>number</code> | <p>Dump request</p> |
| NLM_F_DUMP_FILTERED | <code>number</code> | <p>Dump filtered request</p> |
| NLM_F_DUMP_INTR | <code>number</code> | <p>Dump interrupted</p> |
| NLM_F_ECHO | <code>number</code> | <p>Echo request</p> |
| NLM_F_EXCL | <code>number</code> | <p>Exclusive creation</p> |
| NLM_F_MATCH | <code>number</code> | <p>Match request</p> |
| NLM_F_MULTI | <code>number</code> | <p>Multi-part message</p> |
| NLM_F_NONREC | <code>number</code> | <p>Non-recursive operation</p> |
| NLM_F_REPLACE | <code>number</code> | <p>Replace existing</p> |
| NLM_F_REQUEST | <code>number</code> | <p>Request message</p> |
| NLM_F_ROOT | <code>number</code> | <p>Root operation</p> |

<a name="module_nl80211..nl80211 commands"></a>

### nl80211~nl80211 commands
**Kind**: inner typedef of [<code>nl80211</code>](#module_nl80211)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| NL80211_CMD_GET_WIPHY | <code>number</code> | <p>Get wireless PHY attributes</p> |
| NL80211_CMD_SET_WIPHY | <code>number</code> | <p>Set wireless PHY attributes</p> |
| NL80211_CMD_NEW_WIPHY | <code>number</code> | <p>Create new wireless PHY</p> |
| NL80211_CMD_DEL_WIPHY | <code>number</code> | <p>Delete wireless PHY</p> |
| NL80211_CMD_GET_INTERFACE | <code>number</code> | <p>Get interface information</p> |
| NL80211_CMD_SET_INTERFACE | <code>number</code> | <p>Set interface attributes</p> |
| NL80211_CMD_NEW_INTERFACE | <code>number</code> | <p>Create new interface</p> |
| NL80211_CMD_DEL_INTERFACE | <code>number</code> | <p>Delete interface</p> |
| NL80211_CMD_GET_KEY | <code>number</code> | <p>Get key</p> |
| NL80211_CMD_SET_KEY | <code>number</code> | <p>Set key</p> |
| NL80211_CMD_NEW_KEY | <code>number</code> | <p>Add new key</p> |
| NL80211_CMD_DEL_KEY | <code>number</code> | <p>Delete key</p> |
| NL80211_CMD_GET_BEACON | <code>number</code> | <p>Get beacon</p> |
| NL80211_CMD_SET_BEACON | <code>number</code> | <p>Set beacon</p> |
| NL80211_CMD_NEW_BEACON | <code>number</code> | <p>Set beacon (alias)</p> |
| NL80211_CMD_STOP_AP | <code>number</code> | <p>Stop AP operation</p> |
| NL80211_CMD_DEL_BEACON | <code>number</code> | <p>Delete beacon</p> |
| NL80211_CMD_GET_STATION | <code>number</code> | <p>Get station information</p> |
| NL80211_CMD_SET_STATION | <code>number</code> | <p>Set station attributes</p> |
| NL80211_CMD_NEW_STATION | <code>number</code> | <p>Add new station</p> |
| NL80211_CMD_DEL_STATION | <code>number</code> | <p>Delete station</p> |
| NL80211_CMD_GET_MPATH | <code>number</code> | <p>Get mesh path</p> |
| NL80211_CMD_SET_MPATH | <code>number</code> | <p>Set mesh path</p> |
| NL80211_CMD_NEW_MPATH | <code>number</code> | <p>Add new mesh path</p> |
| NL80211_CMD_DEL_MPATH | <code>number</code> | <p>Delete mesh path</p> |
| NL80211_CMD_SET_BSS | <code>number</code> | <p>Set BSS attributes</p> |
| NL80211_CMD_SET_REG | <code>number</code> | <p>Set regulatory domain</p> |
| NL80211_CMD_REQ_SET_REG | <code>number</code> | <p>Request regulatory domain change</p> |
| NL80211_CMD_GET_MESH_CONFIG | <code>number</code> | <p>Get mesh configuration</p> |
| NL80211_CMD_SET_MESH_CONFIG | <code>number</code> | <p>Set mesh configuration</p> |
| NL80211_CMD_GET_REG | <code>n


---

<a id="ucode-module-resolv"></a>
# ucode module: `resolv`

> **Source:** [`lib/resolv.c`](https://github.com/jow-/ucode/blob/master/lib/resolv.c)
> **Live docs:** https://ucode.mein.io/module-resolv.html
> **Generated:** 2026-03-04 13:26 UTC from commit `e87be9d`

---

## Modules

<dl>
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

<a name="module_resolv"></a>

## resolv
<h1 id="dns-resolution-module">DNS Resolution Module</h1>
<p>The <code>resolv</code> module provides DNS resolution functionality for ucode, allowing
you to perform DNS queries for various record types and handle responses.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { query } from 'resolv';

let result = query('example.com', { type: ['A'] });
</code></pre>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as resolv from 'resolv';

let result = resolv.query('example.com', { type: ['A'] });
</code></pre>
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

const result = query(['example.com']);
print(result, &quot;\n&quot;);
// {
//   &quot;example.com&quot;: {
//     &quot;A&quot;: [&quot;192.0.2.1&quot;],
//     &quot;AAAA&quot;: [&quot;2001:db8::1&quot;]
//   }
// }
</code></pre>
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
</code></pre>


* [resolv](#module_resolv)
    * [.query(names, [options])](#module_resolv+query) ⇒ <code>object</code>
    * [.error()](#module_resolv+error) ⇒ <code>string</code> \| <code>null</code>
    * [.query(names, [options])](#module_resolv+query) ⇒ <code>object</code>
    * [.error()](#module_resolv+error) ⇒ <code>string</code> \| <code>null</code>

<a name="module_resolv+query"></a>

### resolv.query(names, [options]) ⇒ <code>object</code>
<p>Perform DNS queries for specified domain names.</p>
<p>The <code>query()</code> function performs DNS lookups for one or more domain names
according to the specified options. It returns a structured object containing
all resolved DNS records grouped by domain name and record type.</p>
<p>If no record types are specified in the options, the function will perform
both A and AAAA record lookups for regular domain names, or PTR record
lookups for IP addresses (reverse DNS).</p>
<p>Returns an object containing DNS query results organized by domain name.</p>
<p>Raises a runtime exception if invalid arguments are provided or if DNS
resolution encounters critical errors.</p>

**Kind**: instance method of [<code>resolv</code>](#module_resolv)  
**Returns**: <code>object</code> - <p>Object containing DNS query results. Keys are domain names, values are
objects containing arrays of records grouped by type, or error information
for failed queries.</p>  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| names | <code>string</code> \| <code>Array.&lt;string&gt;</code> |  | <p>Domain name(s) to query. Can be a single domain name string or an array of domain name strings. IP addresses can also be provided for reverse DNS lookups.</p> |
| [options] | <code>object</code> |  | <p>Query options object.</p> |
| [options.type] | <code>Array.&lt;string&gt;</code> |  | <p>Array of DNS record types to query for. Valid types are: 'A', 'AAAA', 'CNAME', 'MX', 'NS', 'PTR', 'SOA', 'SRV', 'TXT', 'ANY'. If not specified, defaults to 'A' and 'AAAA' for domain names, or 'PTR' for IP addresses.</p> |
| [options.nameserver] | <code>Array.&lt;string&gt;</code> |  | <p>Array of DNS nameserver addresses to query. Each address can optionally include a port number using '#' separator (e.g., '8.8.8.8#53'). IPv6 addresses can include interface scope using '%' separator. If not specified, nameservers are read from /etc/resolv.conf, falling back to '127.0.0.1'.</p> |
| [options.timeout] | <code>number</code> | <code>5000</code> | <p>Total timeout for all queries in milliseconds.</p> |
| [options.retries] | <code>number</code> | <code>2</code> | <p>Number of retry attempts for failed queries.</p> |
| [options.edns_maxsize] | <code>number</code> | <code>4096</code> | <p>Maximum UDP packet size for EDNS (Extension Mechanisms for DNS). Set to 0 to disable EDNS.</p> |
| [options.txt_as_array] | <code>boolean</code> | <code>false</code> | <p>Return TXT record strings as array elements instead of space-joining all record strings into one single string per record.</p> |

**Example**  
```js
// Basic A and AAAA record lookup
const result = query('example.com');
print(result, "\n");
// {
//   "example.com": {
//     "A": ["192.0.2.1"],
//     "AAAA": ["2001:db8::1"]
//   }
// }
```
**Example**  
```js
// Specific record type queries
const mxResult = query('example.com', { type: ['MX'] });
print(mxResult, "\n");
// {
//   "example.com": {
//     "MX": [[10, "mail.example.com"]]
//   }
// }
```
**Example**  
```js
// Multiple domains and types with custom nameserver
const results = query(
  ['example.com', 'google.com'],
  {
    type: ['A', 'MX'],
    nameserver: ['8.8.8.8', '1.1.1.1'],
    timeout: 10000
  }
);
```
**Example**  
```js
// Reverse DNS lookup
const ptrResult = query(['192.0.2.1'], { type: ['PTR'] });
print(ptrResult, "\n");
// {
//   "1.2.0.192.in-addr.arpa": {
//     "PTR": ["example.com"]
//   }
// }
```
**Example**  
```js
// TXT record with multiple elements
const txtResult = query(['_spf.facebook.com'], { type: ['TXT'], txt_as_array: true });
printf(txtResult, "\n");
// {
//   "_spf.facebook.com": {
//     "TXT": [
//       [
//         "v=spf1 ip4:66.220.144.128/25 ip4:66.220.155.0/24 ip4:66.220.157.0/25 ip4:69.63.178.128/25 ip4:69.63.181.0/24 ip4:69.63.184.0/25",
//         " ip4:69.171.232.0/24 ip4:69.171.244.0/23 -all"
//       ]
//     ]
//   }
// }
```
**Example**  
```js
// Handling errors
const errorResult = query(['nonexistent.example.com']);
print(errorResult, "\n");
// {
//   "nonexistent.example.com": {
//     "rcode": "NXDOMAIN"
//   }
// }
```
<a name="module_resolv+error"></a>

### resolv.error() ⇒ <code>string</code> \| <code>null</code>
<p>Get the last error message from DNS operations.</p>
<p>The <code>error()</code> function returns a descriptive error message for the last
failed DNS operation, or <code>null</code> if no error occurred. This function is
particularly useful for debugging DNS resolution issues.</p>
<p>After calling this function, the stored error state is cleared, so
subsequent calls will return <code>null</code> unless a new error occurs.</p>
<p>Returns a string describing the last error, or <code>null</code> if no error occurred.</p>

**Kind**: instance method of [<code>resolv</code>](#module_resolv)  
**Returns**: <code>string</code> \| <code>null</code> - <p>A descriptive error message for the last failed operation, or <code>null</code> if
no error occurred.</p>  
**Example**  
```js
// Check for errors after a failed query
const result = query("example.org", { nameserver: "invalid..domain" });
const err = error();
if (err) {
  print("DNS query failed: ", err, "\n");
}
```
<a name="module_resolv+query"></a>

### resolv.query(names, [options]) ⇒ <code>object</code>
<p>Perform DNS queries for specified domain names.</p>
<p>The <code>query()</code> function performs DNS lookups for one or more domain names
according to the specified options. It returns a structured object containing
all resolved DNS records grouped by domain name and record type.</p>
<p>If no record types are specified in the options, the function will perform
both A and AAAA record lookups for regular domain names, or PTR record
lookups for IP addresses (reverse DNS).</p>
<p>Returns an object containing DNS query results organized by domain name.</p>
<p>Raises a runtime exception if invalid arguments are provided or if DNS
resolution encounters critical errors.</p>

**Kind**: instance method of [<code>resolv</code>](#module_resolv)  
**Returns**: <code>object</code> - <p>Object containing DNS query results. Keys are domain names, values are
objects containing arrays of records grouped by type, or error information
for failed queries.</p>  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| names | <code>string</code> \| <code>Array.&lt;string&gt;</code> |  | <p>Domain name(s) to query. Can be a single domain name string or an array of domain name strings. IP addresses can also be provided for reverse DNS lookups.</p> |
| [options] | <code>object</code> |  | <p>Query options object.</p> |
| [options.type] | <code>Array.&lt;string&gt;</code> |  | <p>Array of DNS record types to query for. Valid types are: 'A', 'AAAA', 'CNAME', 'MX', 'NS', 'PTR', 'SOA', 'SRV', 'TXT', 'ANY'. If not specified, defaults to 'A' and 'AAAA' for domain names, or 'PTR' for IP addresses.</p> |
| [options.nameserver] | <code>Array.&lt;string&gt;</code> |  | <p>Array of DNS nameserver addresses to query. Each address can optionally include a port number using '#' separator (e.g., '8.8.8.8#53'). IPv6 addresses can include interface scope using '%' separator. If not specified, nameservers are read from /etc/resolv.conf, falling back to '127.0.0.1'.</p> |
| [options.timeout] | <code>number</code> | <code>5000</code> | <p>Total timeout for all queries in milliseconds.</p> |
| [options.retries] | <code>number</code> | <code>2</code> | <p>Number of retry attempts for failed queries.</p> |
| [options.edns_maxsize] | <code>number</code> | <code>4096</code> | <p>Maximum UDP packet size for EDNS (Extension Mechanisms for DNS). Set to 0 to disable EDNS.</p> |
| [options.txt_as_array] | <code>boolean</code> | <code>false</code> | <p>Return TXT record strings as array elements instead of space-joining all record strings into one single string per record.</p> |

**Example**  
```js
// Basic A and AAAA record lookup
const result = query('example.com');
print(result, "\n");
// {
//   "example.com": {
//     "A": ["192.0.2.1"],
//     "AAAA": ["2001:db8::1"]
//   }
// }
```
**Example**  
```js
// Specific record type queries
const mxResult = query('example.com', { type: ['MX'] });
print(mxResult, "\n");
// {
//   "example.com": {
//     "MX": [[10, "mail.example.com"]]
//   }
// }
```
**Example**  
```js
// Multiple domains and types with custom nameserver
const results = query(
  ['example.com', 'google.com'],
  {
    type: ['A', 'MX'],
    nameserver: ['8.8.8.8', '1.1.1.1'],
    timeout: 10000
  }
);
```
**Example**  
```js
// Reverse DNS lookup
const ptrResult = query(['192.0.2.1'], { type: ['PTR'] });
print(ptrResult, "\n");
// {
//   "1.2.0.192.in-addr.arpa": {
//     "PTR": ["example.com"]
//   }
// }
```
**Example**  
```js
// TXT record with multiple elements
const txtResult = query(['_spf.facebook.com'], { type: ['TXT'], txt_as_array: true });
printf(txtResult, "\n");
// {
//   "_spf.facebook.com": {
//     "TXT": [
//       [
//         "v=spf1 ip4:66.220.144.128/25 ip4:66.220.155.0/24 ip4:66.220.157.0/25 ip4:69.63.178.128/25 ip4:69.63.181.0/24 ip4:69.63.184.0/25",
//         " ip4:69.171.232.0/24 ip4:69.171.244.0/23 -all"
//       ]
//     ]
//   }
// }
```
**Example**  
```js
// Handling errors
const errorResult = query(['nonexistent.example.com']);
print(errorResult, "\n");
// {
//   "nonexistent.example.com": {
//     "rcode": "NXDOMAIN"
//   }
// }
```
<a name="module_resolv+error"></a>

### resolv.error() ⇒ <code>string</code> \| <code>null</code>
<p>Get the last error message from DNS operations.</p>
<p>The <code>error()</code> function returns a descriptive error message for the last
failed DNS operation, or <code>null</code> if no error occurred. This function is
particularly useful for debugging DNS resolution issues.</p>
<p>After calling this function, the stored error state is cleared, so
subsequent calls will return <code>null</code> unless a new error occurs.</p>
<p>Returns a string describing the last error, or <code>null</code> if no error occurred.</p>

**Kind**: instance method of [<code>resolv</code>](#module_resolv)  
**Returns**: <code>string</code> \| <code>null</code> - <p>A descriptive error message for the last failed operation, or <code>null</code> if
no error occurred.</p>  
**Example**  
```js
// Check for errors after a failed query
const result = query("example.org", { nameserver: "invalid..domain" });
const err = error();
if (err) {
  print("DNS query failed: ", err, "\n");
}
```
<a name="module_debug"></a>

## debug
<h1 id="debugger-module">Debugger Module</h1>
<p>This module provides runtime debug functionality for ucode scripts.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { memdump, traceback } from 'debug';

let stacktrace = traceback(1);

memdump(&quot;/tmp/dump.txt&quot;);
</code></pre>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as debug from 'debug';

let stacktrace = debug.traceback(1);

debug.memdump(&quot;/tmp/dump.txt&quot;);
</code></pre>
<p>Additionally, the debug module namespace may also be imported by invoking the
<code>ucode</code> interpreter with the <code>-ldebug</code> switch.</p>
<p>Upon loading, the <code>debug</code> module will register a <code>SIGUSR2</code> signal handler
which, upon receipt of the signal, will write a memory dump of the currently
running program to <code>/tmp/ucode.$timestamp.$pid.memdump</code>. This default
behavior can be inhibited by setting the <code>UCODE_DEBUG_MEMDUMP_ENABLED</code>
environment variable to <code>0</code> when starting the process. The memory dump sig


---

<a id="ucode-module-rtnl"></a>
# ucode module: `rtnl`

> **Source:** [`lib/rtnl.c`](https://github.com/jow-/ucode/blob/master/lib/rtnl.c)
> **Live docs:** https://ucode.mein.io/module-rtnl.html
> **Generated:** 2026-03-04 13:26 UTC from commit `e87be9d`

---

## Modules

<dl>
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

<a name="module_rtnl"></a>

## rtnl
<h1 id="routing-netlink">Routing Netlink</h1>
<p>The <code>rtnl</code> module provides functions for interacting with the routing netlink interface.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source lang-javascript"><code>import { error, request, listener, RTM_GETROUTE, RTM_NEWROUTE, RTM_DELROUTE, AF_INET } from 'rtnl';

// Send a netlink request
let response = request(RTM_GETROUTE, 0, { family: AF_INET });

// Create a listener for route changes
let routeListener = listener((msg) => {
    print('Received route message:', msg, '\n');
}, [RTM_NEWROUTE, RTM_DELROUTE]);
</code></pre>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source lang-javascript"><code>import * as rtnl from 'rtnl';

// Send a netlink request
let response = rtnl.request(rtnl.RTM_GETROUTE, 0, { family: rtnl.AF_INET });

// Create a listener for route changes
let listener = rtnl.listener((msg) => {
    print('Received route message:', msg, '\n');
}, [rtnl.RTM_NEWROUTE, rtnl.RTM_DELROUTE]);
</code></pre>
<p>Additionally, the rtnl module namespace may also be imported by invoking
the <code>ucode</code> interpreter with the <code>-lrtnl</code> switch.</p>


* [rtnl](#module_rtnl)
    * _instance_
        * [.error()](#module_rtnl+error) ⇒ <code>string</code>
        * [.request(cmd, flags, payload)](#module_rtnl+request) ⇒ <code>\*</code>
        * [.listener(callback, [commands], [groups])](#module_rtnl+listener) ⇒ [<code>listener</code>](#module_rtnl.listener)
        * [.error()](#module_rtnl+error) ⇒ <code>string</code>
        * [.request(cmd, flags, payload)](#module_rtnl+request) ⇒ <code>\*</code>
        * [.listener(callback, [commands], [groups])](#module_rtnl+listener) ⇒ [<code>listener</code>](#module_rtnl.listener)
    * _static_
        * [.listener](#module_rtnl.listener)
            * [.set_commands(commands)](#module_rtnl.listener+set_commands) ⇒ <code>boolean</code>
            * [.close()](#module_rtnl.listener+close) ⇒ <code>boolean</code>
            * [.set_commands(commands)](#module_rtnl.listener+set_commands) ⇒ <code>boolean</code>
            * [.close()](#module_rtnl.listener+close) ⇒ <code>boolean</code>
        * [.listener](#module_rtnl.listener)
            * [.set_commands(commands)](#module_rtnl.listener+set_commands) ⇒ <code>boolean</code>
            * [.close()](#module_rtnl.listener+close) ⇒ <code>boolean</code>
            * [.set_commands(commands)](#module_rtnl.listener+set_commands) ⇒ <code>boolean</code>
            * [.close()](#module_rtnl.listener+close) ⇒ <code>boolean</code>
    * _inner_
        * [~Netlink message flags](#module_rtnl..Netlink message flags)
        * [~IPv6 address generation modes](#module_rtnl..IPv6 address generation modes)
        * [~MACVLAN modes](#module_rtnl..MACVLAN modes)
        * [~MACVLAN MAC address commands](#module_rtnl..MACVLAN MAC address commands)
        * [~MACsec validation levels](#module_rtnl..MACsec validation levels)
        * [~MACsec offload modes](#module_rtnl..MACsec offload modes)
        * [~IPVLAN modes](#module_rtnl..IPVLAN modes)
        * [~VXLAN data frame flags](#module_rtnl..VXLAN data frame flags)
        * [~Geneve data frame flags](#module_rtnl..Geneve data frame flags)
        * [~GTP roles](#module_rtnl..GTP roles)
        * [~Port request types](#module_rtnl..Port request types)
        * [~Port VDP responses](#module_rtnl..Port VDP responses)
        * [~Port profile responses](#module_rtnl..Port profile responses)
        * [~IPoIB modes](#module_rtnl..IPoIB modes)
        * [~HSR protocols](#module_rtnl..HSR protocols)
        * [~Link extended statistics types](#module_rtnl..Link extended statistics types)
        * [~XDP attach types](#module_rtnl..XDP attach types)
        * [~FDB notification bits](#module_rtnl..FDB notification bits)
        * [~Route commands](#module_rtnl..Route commands)
        * [~Route types](#module_rtnl..Route types)
        * [~Route scopes](#module_rtnl..Route scopes)
        * [~Route tables](#module_rtnl..Route tables)
        * [~Route metrics](#module_rtnl..Route metrics)
        * [~Prefix types](#module_rtnl..Prefix types)
        * [~Neighbor discovery user option types](#module_rtnl..Neighbor discovery user option types)
        * [~Multicast groups](#module_rtnl..Multicast groups)
        * [~Route flags](#module_rtnl..Route flags)
        * [~Address families](#module_rtnl..Address families)
        * [~Generic Routing Encapsulation flags](#module_rtnl..Generic Routing Encapsulation flags)
        * [~Tunnel encapsulation types](#module_rtnl..Tunnel encapsulation types)
        * [~Tunnel encapsulation flags](#module_rtnl..Tunnel encapsulation flags)
        * [~IPv6 tunnel flags](#module_rtnl..IPv6 tunnel flags)
        * [~Interface flags](#module_rtnl..Interface flags)
        * [~Neighbor states](#module_rtnl..Neighbor states)
        * [~Address flags](#module_rtnl..Address flags)
        * [~FIB rule flags](#module_rtnl..FIB rule flags)
        * [~FIB rule actions](#module_rtnl..FIB rule actions)
        * [~Network configuration indices](#module_rtnl..Network configuration indices)
        * [~Bridge flags](#module_rtnl..Bridge flags)
        * [~Bridge modes](#module_rtnl..Bridge modes)
        * [~Bridge VLAN information flags](#module_rtnl..Bridge VLAN information flags)
        * [~Netlink message flags](#module_rtnl..Netlink message flags)
        * [~IPv6 address generation modes](#module_rtnl..IPv6 address generation modes)
        * [~MACVLAN modes](#module_rtnl..MACVLAN modes)
        * [~MACVLAN MAC address commands](#module_rtnl..MACVLAN MAC address commands)
        * [~MACsec validation levels](#module_rtnl..MACsec validation levels)
        * [~MACsec offload modes](#module_rtnl..MACsec offload modes)
        * [~IPVLAN modes](#module_rtnl..IPVLAN modes)
        * [~VXLAN data frame flags](#module_rtnl..VXLAN data frame flags)
        * [~Geneve data frame flags](#module_rtnl..Geneve data frame flags)
        * [~GTP roles](#module_rtnl..GTP roles)
        * [~Port request types](#module_rtnl..Port request types)
        * [~Port VDP responses](#module_rtnl..Port VDP responses)
        * [~Port profile responses](#module_rtnl..Port profile responses)
        * [~IPoIB modes](#module_rtnl..IPoIB modes)
        * [~HSR protocols](#module_rtnl..HSR protocols)
        * [~Link extended statistics types](#module_rtnl..Link extended statistics types)
        * [~XDP attach types](#module_rtnl..XDP attach types)
        * [~FDB notification bits](#module_rtnl..FDB notification bits)
        * [~Route commands](#module_rtnl..Route commands)
        * [~Route types](#module_rtnl..Route types)
        * [~Route scopes](#module_rtnl..Route scopes)
        * [~Route tables](#module_rtnl..Route tables)
        * [~Route metrics](#module_rtnl..Route metrics)
        * [~Prefix types](#module_rtnl..Prefix types)
        * [~Neighbor discovery user option types](#module_rtnl..Neighbor discovery user option types)
        * [~Multicast groups](#module_rtnl..Multicast groups)
        * [~Route flags](#module_rtnl..Route flags)
        * [~Address families](#module_rtnl..Address families)
        * [~Generic Routing Encapsulation flags](#module_rtnl..Generic Routing Encapsulation flags)
        * [~Tunnel encapsulation types](#module_rtnl..Tunnel encapsulation types)
        * [~Tunnel encapsulation flags](#module_rtnl..Tunnel encapsulation flags)
        * [~IPv6 tunnel flags](#module_rtnl..IPv6 tunnel flags)
        * [~Interface flags](#module_rtnl..Interface flags)
        * [~Neighbor states](#module_rtnl..Neighbor states)
        * [~Address flags](#module_rtnl..Address flags)
        * [~FIB rule flags](#module_rtnl..FIB rule flags)
        * [~FIB rule actions](#module_rtnl..FIB rule actions)
        * [~Network configuration indices](#module_rtnl..Network configuration indices)
        * [~Bridge flags](#module_rtnl..Bridge flags)
        * [~Bridge modes](#module_rtnl..Bridge modes)
        * [~Bridge VLAN information flags](#module_rtnl..Bridge VLAN information flags)

<a name="module_rtnl+error"></a>

### rtnl.error() ⇒ <code>string</code>
<p>Query error information.</p>
<p>Returns a string containing a description of the last occurred error or
<code>null</code> if there is no error information.</p>

**Kind**: instance method of [<code>rtnl</code>](#module_rtnl)  
**Example**  
```js
// Trigger rtnl error
request('invalid_command', {}, {});

// Print error (should yield error description)
print(error(), "\n");
```
<a name="module_rtnl+request"></a>

### rtnl.request(cmd, flags, payload) ⇒ <code>\*</code>
<p>Send a netlink request.</p>
<p>Sends a netlink request with the specified command, flags, and payload.</p>

**Kind**: instance method of [<code>rtnl</code>](#module_rtnl)  
**Returns**: <code>\*</code> - <ul>
<li>The response data or null on error</li>
</ul>  

| Param | Type | Description |
| --- | --- | --- |
| cmd | <code>string</code> | <p>The netlink command to send</p> |
| flags | <code>number</code> | <p>The netlink flags for the request</p> |
| payload | <code>\*</code> | <p>The payload data for the request</p> |

**Example**  
```js
// Send a route request
let response = request('RTM_GETROUTE', 0, { family: AF_INET });
```
<a name="module_rtnl+listener"></a>

### rtnl.listener(callback, [commands], [groups]) ⇒ [<code>listener</code>](#module_rtnl.listener)
<p>Create a netlink listener.</p>
<p>Creates a new netlink listener that will receive messages matching the specified
commands and multicast groups.</p>

**Kind**: instance method of [<code>rtnl</code>](#module_rtnl)  
**Returns**: [<code>listener</code>](#module_rtnl.listener) - <ul>
<li>A listener object with methods to control the listener</li>
</ul>  

| Param | Type | Description |
| --- | --- | --- |
| callback | <code>function</code> | <p>The callback function to invoke when a message is received</p> |
| [commands] | <code>Array.&lt;string&gt;</code> | <p>Array of netlink commands to listen for (optional)</p> |
| [groups] | <code>Array.&lt;number&gt;</code> | <p>Array of multicast groups to join (optional)</p> |

**Example**  
```js
// Create a listener for route changes
let routeListener = listener((msg) => {
    print('Received route message:', msg, '\n');
}, [RTM_NEWROUTE, RTM_DELROUTE]);
```
<a name="module_rtnl+error"></a>

### rtnl.error() ⇒ <code>string</code>
<p>Query error information.</p>
<p>Returns a string containing a description of the last occurred error or
<code>null</code> if there is no error information.</p>

**Kind**: instance method of [<code>rtnl</code>](#module_rtnl)  
**Example**  
```js
// Trigger rtnl error
request('invalid_command', {}, {});

// Print error (should yield error description)
print(error(), "\n");
```
<a name="module_rtnl+request"></a>

### rtnl.request(cmd, flags, payload) ⇒ <code>\*</code>
<p>Send a netlink request.</p>
<p>Sends a netlink request with the specified command, flags, and payload.</p>

**Kind**: instance method of [<code>rtnl</code>](#module_rtnl)  
**Returns**: <code>\*</code> - <ul>
<li>The response data or null on error</li>
</ul>  

| Param | Type | Description |
| --- | --- | --- |
| cmd | <code>string</code> | <p>The netlink command to send</p> |
| flags | <code>number</code> | <p>The netlink flags for the request</p> |
| payload | <code>\*</code> | <p>The payload data for the request</p> |

**Example**  
```js
// Send a route request
let response = request('RTM_GETROUTE', 0, { family: AF_INET });
```
<a name="module_rtnl+listener"></a>

### rtnl.listener(callback, [commands], [groups]) ⇒ [<code>listener</code>](#module_rtnl.listener)
<p>Create a netlink listener.</p>
<p>Creates a new netlink listener that will receive messages matching the specified
commands and multicast groups.</p>

**Kind**: instance method of [<code>rtnl</code>](#module_rtnl)  
**Returns**: [<code>listener</code>](#module_rtnl.listener) - <ul>
<li>A listener object with methods to control the listener</li>
</ul>  

| Param | Type | Description |
| --- | --- | --- |
| callback | <code>function</code> | <p>The callback function to invoke when a message is received</p> |
| [commands] | <code>Array.&lt;string&gt;</code> | <p>Array of netlink commands to listen for (optional)</p> |
| [groups] | <code>Array.&lt;number&gt;</code> | <p>Array of multicast groups to join (optional)</p> |

**Example**  
```js
// Create a listener for route changes
let routeListener = listener((msg) => {
    print('Received route message:', msg, '\n');
}, [RTM_NEWROUTE, RTM_DELROUTE]);
```
<a name="module_rtnl.listener"></a>

### rtnl.listener
**Kind**: static class of [<code>rtnl</code>](#module_rtnl)  
**See**: [listener()](#module_rtnl+listener)  

* [.listener](#module_rtnl.listener)
    * [.set_commands(commands)](#module_rtnl.listener+set_commands) ⇒ <code>boolean</code>
    * [.close()](#module_rtnl.listener+close) ⇒ <code>boolean</code>
    * [.set_commands(commands)](#module_rtnl.listener+set_commands) ⇒ <code>boolean</code>
    * [.close()](#module_rtnl.listener+close) ⇒ <code>boolean</code>

<a name="module_rtnl.listener+set_commands"></a>

#### listener.set\_commands(commands) ⇒ <code>boolean</code>
<p>Set the commands for a netlink listener.</p>
<p>Updates the set of netlink commands that the listener will receive.</p>

**Kind**: instance method of [<code>listener</code>](#module_rtnl.listener)  
**Returns**: <code>boolean</code> - <ul>
<li>true if successful, false on error</li>
</ul>  

| Param | Type | Description |
| --- | --- | --- |
| commands | <code>Array.&lt;string&gt;</code> | <p>Array of netlink commands to listen for</p> |

**Example**  
```js
// Update listener to only receive route messages
listener.set_commands([RTM_NEWROUTE, RTM_DELROUTE]);
```
<a name="module_rtnl.listener+close"></a>

#### listener.close() ⇒ <code>boolean</code>
<p>Close a netlink listener.</p>
<p>Closes the netlink listener and stops receiving messages.</p>

**Kind**: instance method of [<code>listener</code>](#module_rtnl.listener)  
**Returns**: <code>boolean</code> - <ul>
<li>true if successful, false on error</li>
</ul>  
**Example**  
```js
// Close the listener
listener.close();
```
<a name="module_rtnl.listener+set_commands"></a>

#### listener.set\_commands(commands) ⇒ <code>boolean</code>
<p>Set the commands for a netlink listener.</p>
<p>Updates the set of netlink commands that the listener will receive.</p>

**Kind**: instance method of [<code>listener</code>](#module_rtnl.listener)  
**Returns**: <code>boolean</code> - <ul>
<li>true if successful, false on error</li>
</ul>  

| Param | Type | Description |
| --- | --- | --- |
| commands | <code>Array.&lt;string&gt;</code> | <p>Array of netlink commands to listen for</p> |

**Example**  
```js
// Update listener to only receive route messages
listener.set_commands([RTM_NEWROUTE, RTM_DELROUTE]);
```
<a name="module_rtnl.listener+close"></a>

#### listener.close() ⇒ <code>boolean</code>
<p>Close a netlink listener.</p>
<p>Closes the netlink listener and stops receiving messages.</p>

**Kind**: instance method of [<code>listener</code>](#module_rtnl.listener)  
**Returns**: <code>boolean</code> - <ul>
<li>true if successful, false on error</li>
</ul>  
**Example**  
```js
// Close the listener
listener.close();
```
<a name="module_rtnl.listener"></a>

### rtnl.listener
**Kind**: static class of [<code>rtnl</code>](#module_rtnl)  
**See**: [listener()](#module_rtnl+listener)  

* [.listener](#module_rtnl.listener)
    * [.set_commands(commands)](#module_rtnl.listener+set_commands) ⇒ <code>boolean</code>
    * [.close()](#module_rtnl.listener+close) ⇒ <code>boolean</code>
    * [.set_commands(commands)](#module_rtnl.listener+set_commands) ⇒ <code>boolean</code>
    * [.close()](#module_rtnl.listener+close) ⇒ <code>boolean</code>

<a name="module_rtnl.listener+set_commands"></a>

#### listener.set\_commands(commands) ⇒ <code>boolean</code>
<p>Set the commands for a netlink listener.</p>
<p>Updates the set of netlink commands that the listener will receive.</p>

**Kind**: instance method of [<code>listener</code>](#module_rtnl.listener)  
**Returns**: <code>boolean</code> - <ul>
<li>true if successful, false on error</li>
</ul>  

| Param | Type | Description |
| --- | --- | --- |
| commands | <code>Array.&lt;string&gt;</code> | <p>Array of netlink commands to listen for</p> |

**Example**  
```js
// Update listener to only receive route messages
listener.set_commands([RTM_NEWROUTE, RTM_DELROUTE]);
```
<a name="module_rtnl.listener+close"></a>

#### listener.close() ⇒ <code>boolean</code>
<p>Close a netlink listener.</p>
<p>Closes the netlink listener and stops receiving messages.</p>

**Kind**: instance method of [<code>listener</code>](#module_rtnl.listener)  
**Returns**: <code>boolean</code> - <ul>
<li>true if successful, false on error</li>
</ul>  
**Example**  
```js
// Close the listener
listener.close();
```
<a name="module_rtnl.listener+set_commands"></a>

#### listener.set\_commands(commands) ⇒ <code>boolean</code>
<p>Set the commands for a netlink listener.</p>
<p>Updates the set of netlink commands that the listener will receive.</p>

**Kind**: instance method of [<code>listener</code>](#module_rtnl.listener)  
**Returns**: <code>boolean</code> - <ul>
<li>true if successful, false on error</li>
</ul>  

| Param | Type | Description |
| --- | --- | --- |
| commands | <code>Array.&lt;string&gt;</code> | <p>Array of netlink commands to listen for</p> |

**Example**  
```js
// Update listener to only receive route messages
listener.set_commands([RTM_NEWROUTE, RTM_DELROUTE]);
```
<a name="module_rtnl.listener+close"></a>

#### listener.close() ⇒ <code>boolean</code>
<p>Close a netlink listener.</p>
<p>Closes the netlink listener and stops receiving messages.</p>

**Kind**: instance method of [<code>listener</code>](#module_rtnl.listener)  
**Returns**: <code>boolean</code> - <ul>
<li>true if successful, false on error</li>
</ul>  
**Example**  
```js
// Close the listener
listener.close();
```
<a name="module_rtnl..Netlink message flags"></a>

### rtnl~Netlink message flags
**Kind**: inner typedef of [<code>rtnl</code>](#module_rtnl)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| NLM_F_ACK | <code>number</code> | <p>Request for acknowledgment</p> |
| NLM_F_ACK_TLVS | <code>number</code> | <p>Request for acknowledgment with TLVs</p> |
| NLM_F_APPEND | <code>number</code> | <p>Append to existing list</p> |
| NLM_F_ATOMIC | <code>number</code> | <p>Atomic operation</p> |
| NLM_F_CAPPED | <code>number</code> | <p>Request capped</p> |
| NLM_F_CREATE | <code>number</code> | <p>Create if not exists</p> |
| NLM_F_DUMP | <code>number</code> | <p>Dump request</p> |
| NLM_F_DUMP_FILTERED | <code>number</code> | <p>Dump filtered request</p> |
| NLM_F_DUMP_INTR | <code>number</code> | <p>Dump interrupted</p> |
| NLM_F_ECHO | <code>number</code> | <p>Echo request</p> |
| NLM_F_EXCL | <code>number</code> | <p>Exclusive creation</p> |
| NLM_F_MATCH | <code>number</code> | <p>Match request</p> |
| NLM_F_MULTI | <code>number</code> | <p>Multi-part message</p> |
| NLM_F_NONREC | <code>number</code> | <p>Non-recursive operation</p> |
| NLM_F_REPLACE | <code>number</code> | <p>Replace existing</p> |
| NLM_F_REQUEST | <code>number</code> | <p>Request message</p> |
| NLM_F_ROOT | <code>number</code> | <p>Root operation</p> |
| NLM_F_STRICT_CHK | <code>number</code> | <p>Strict checking</p> |

<a name="module_rtnl..IPv6 address generation modes"></a>

### rtnl~IPv6 address generation modes
**Kind**: inner typedef of [<code>rtnl</code>](#module_rtnl)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| IN6_ADDR_GEN_MODE_EUI64 | <code>number</code> | <p>EUI-64 mode</p> |
| IN6_ADDR_GEN_MODE_NONE | <code>number</code> | <p>No mode</p> |
| IN6_ADDR_GEN_MODE_STABLE_PRIVACY | <code>number</code> | <p>Stable privacy mode</p> |
| IN6_ADDR_GEN_MODE_RANDOM | <code>number</code> | <p>Random mode</p> |

<a name="module_rtnl..MACVLAN modes"></a>

### rtnl~MACVLAN modes
**Kind**: inner typedef of [<code>rtnl</code>](#module_rtnl)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| MACVLAN_MODE_PRIVATE | <code>number</code> | <p>Private mode</p> |
| MACVLAN_MODE_VEPA | <code>number</code> | <p>VEPA mode</p> |
| MACVLAN_MODE_BRIDGE | <code>number</code> | <p>Bridge mode</p> |
| MACVLAN_MODE_PASSTHRU | <code>number</code> | <p>Pass-through mode</p> |
| MACVLAN_MODE_SOURCE | <code>number</code> | <p>Source mode</p> |

<a name="module_rtnl..MACVLAN MAC address commands"></a>

### rtnl~MACVLAN MAC address commands
**Kind**: inner typedef of [<code>rtnl</code>](#module_rtnl)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| MACVLAN_MACADDR_ADD | <code>number</code> | <p>Add MAC address</p> |
| MACVLAN_MACADDR_DEL | <code>number</code> | <p>Delete MAC address</p> |
| MACVLAN_MACADDR_FLUSH | <code>number</code> | <p>Flush MAC addresses</p> |
| MACVLAN_MACADDR_SET | <code>number</code> | <p>Set MAC address</p> |

<a name="module_rtnl..MACsec validation levels"></a>

### rtnl~MACsec validation levels
**Kind**: inner typedef of [<code>rtnl</code>](#module_rtnl)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| MACSEC_VALIDATE_DISABLED | <code>number</code> | <p>Disabled validation</p> |
| MACSEC_VALIDATE_CHECK | <code>number</code> | <p>Check validation</p> |
| MACSEC_VALIDATE_STRICT | <code>number</code> | <p>Strict validation</p> |
| MACSEC_VALIDATE_MAX | <code>number</code> | <p>Maximum validation</p> |

<a name="module_rtnl..MACsec offload modes"></a>

### rtnl~MACsec offload modes
**Kind**: inner typedef of [<code>rtnl</code>](#module_rtnl)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| MACSEC_OFFLOAD_OFF | <code>number</code> | <p>Offload off</p> |
| MACSEC_OFFLOAD_PHY | <code>number</code> | <p>Physical offload</p> |
| MACSEC_OFFLOAD_MAC | <code>number</code> | <p>MAC offload</p> |
| MACSEC_OFFLOAD_MAX | <code>number</code> | <p>Maximum offload</p> |

<a name="module_rtnl..IPVLAN modes"></a>

### rtnl~IPVLAN modes
**Kind**: inner typedef of [<code>rtnl</code>](#module_rtnl)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| IPVLAN_MODE_L2 | <code>number</code> | <p>Layer 2 mode</p> |
| IPVLAN_MODE_L3 | <code>number</code> | <p>Layer 3 mode</p> |
| IPVLAN_MODE_L3S | <code>number</code> | <p>Layer 3 symmetric mode</p> |

<a name="module_rtnl..VXLAN data frame flags"></a>

### rtnl~VXLAN data frame flags
**Kind**: inner typedef of [<code>rtnl</code>](#module_rtnl)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| VXLAN_DF_UNSET | <code>number</code> | <p>Data frame unset</p> |
| VXLAN_DF_SET | <code>numbe


---

<a id="ucode-module-socket"></a>
# ucode module: `socket`

> **Source:** [`lib/socket.c`](https://github.com/jow-/ucode/blob/master/lib/socket.c)
> **Live docs:** https://ucode.mein.io/module-socket.html
> **Generated:** 2026-03-04 13:26 UTC from commit `e87be9d`

---

## Modules

<dl>
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

<a name="module_socket"></a>

## socket
<h1 id="socket-module">Socket Module</h1>
<p>The <code>socket</code> module provides functions for interacting with sockets.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source lang-javascript"><code>import { AF_INET, SOCK_STREAM, create as socket } from 'socket';

let sock = socket(AF_INET, SOCK_STREAM, 0);
sock.connect('192.168.1.1', 80);
sock.send(…);
sock.recv(…);
sock.close();
</code></pre>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source lang-javascript"><code>import * as socket from 'socket';

let sock = socket.create(socket.AF_INET, socket.SOCK_STREAM, 0);
sock.connect('192.168.1.1', 80);
sock.send(…);
sock.recv(…);
sock.close();
</code></pre>
<p>Additionally, the socket module namespace may also be imported by invoking
the <code>ucode</code> interpreter with the <code>-lsocket</code> switch.</p>


* [socket](#module_socket)
    * _instance_
        * [.error([numeric])](#module_socket+error) ⇒ <code>string</code> \| <code>number</code>
        * [.strerror(code)](#module_socket+strerror) ⇒ <code>string</code>
        * [.sockaddr(address)](#module_socket+sockaddr) ⇒ [<code>SocketAddress</code>](#module_socket.socket.SocketAddress)
        * [.nameinfo(address, [flags])](#module_socket+nameinfo) ⇒ <code>Object</code>
        * [.addrinfo(hostname, [service], [hints])](#module_socket+addrinfo) ⇒ [<code>Array.&lt;AddressInfo&gt;</code>](#module_socket.AddressInfo)
        * [.poll(timeout, ...sockets)](#module_socket+poll) ⇒ [<code>Array.&lt;PollSpec&gt;</code>](#module_socket.PollSpec)
        * [.connect(host, [service], [hints], [timeout])](#module_socket+connect) ⇒ [<code>socket</code>](#module_socket.socket)
        * [.listen(host, [service], [hints], [backlog], [reuseaddr])](#module_socket+listen) ⇒ [<code>socket</code>](#module_socket.socket)
        * [.create([domain], [type], [protocol])](#module_socket+create) ⇒ [<code>socket</code>](#module_socket.socket)
        * [.open([fd])](#module_socket+open) ⇒ [<code>socket</code>](#module_socket.socket)
        * [.pair([type])](#module_socket+pair) ⇒ <code>Array.&lt;?module:socket.socket&gt;</code>
        * [.error([numeric])](#module_socket+error) ⇒ <code>string</code> \| <code>number</code>
        * [.strerror(code)](#module_socket+strerror) ⇒ <code>string</code>
        * [.sockaddr(address)](#module_socket+sockaddr) ⇒ [<code>SocketAddress</code>](#module_socket.socket.SocketAddress)
        * [.nameinfo(address, [flags])](#module_socket+nameinfo) ⇒ <code>Object</code>
        * [.addrinfo(hostname, [service], [hints])](#module_socket+addrinfo) ⇒ [<code>Array.&lt;AddressInfo&gt;</code>](#module_socket.AddressInfo)
        * [.poll(timeout, ...sockets)](#module_socket+poll) ⇒ [<code>Array.&lt;PollSpec&gt;</code>](#module_socket.PollSpec)
        * [.connect(host, [service], [hints], [timeout])](#module_socket+connect) ⇒ [<code>socket</code>](#module_socket.socket)
        * [.listen(host, [service], [hints], [backlog], [reuseaddr])](#module_socket+listen) ⇒ [<code>socket</code>](#module_socket.socket)
        * [.create([domain], [type], [protocol])](#module_socket+create) ⇒ [<code>socket</code>](#module_socket.socket)
        * [.open([fd])](#module_socket+open) ⇒ [<code>socket</code>](#module_socket.socket)
        * [.pair([type])](#module_socket+pair) ⇒ <code>Array.&lt;?module:socket.socket&gt;</code>
    * _static_
        * [.socket](#module_socket.socket)
            * _instance_
                * [.setopt(level, option, value)](#module_socket.socket+setopt) ⇒ <code>boolean</code>
                * [.getopt(level, option)](#module_socket.socket+getopt) ⇒ <code>\*</code>
                * [.fileno()](#module_socket.socket+fileno) ⇒ <code>number</code>
                * [.connect(address, port)](#module_socket.socket+connect) ⇒ <code>boolean</code>
                * [.send(data, [flags], [address])](#module_socket.socket+send) ⇒ <code>number</code>
                * [.recv([length], [flags], [address])](#module_socket.socket+recv) ⇒ <code>string</code>
                * [.sendmsg([data], [ancillaryData], [address], [flags])](#module_socket.socket+sendmsg) ⇒ <code>number</code>
                * [.recvmsg([sizes], [ancillarySize], [flags])](#module_socket.socket+recvmsg) ⇒ [<code>ReceivedMessage</code>](#module_socket.socket.ReceivedMessage)
                * [.bind(address)](#module_socket.socket+bind) ⇒ <code>boolean</code>
                * [.listen([backlog])](#module_socket.socket+listen) ⇒ <code>boolean</code>
                * [.accept([address], [flags])](#module_socket.socket+accept) ⇒ [<code>socket</code>](#module_socket.socket)
                * [.shutdown(how)](#module_socket.socket+shutdown) ⇒ <code>boolean</code>
                * [.peercred()](#module_socket.socket+peercred) ⇒ [<code>PeerCredentials</code>](#module_socket.socket.PeerCredentials)
                * [.peername()](#module_socket.socket+peername) ⇒ [<code>SocketAddress</code>](#module_socket.socket.SocketAddress)
                * [.sockname()](#module_socket.socket+sockname) ⇒ [<code>SocketAddress</code>](#module_socket.socket.SocketAddress)
                * [.close()](#module_socket.socket+close) ⇒ <code>boolean</code>
                * [.setopt(level, option, value)](#module_socket.socket+setopt) ⇒ <code>boolean</code>
                * [.getopt(level, option)](#module_socket.socket+getopt) ⇒ <code>\*</code>
                * [.fileno()](#module_socket.socket+fileno) ⇒ <code>number</code>
                * [.connect(address, port)](#module_socket.socket+connect) ⇒ <code>boolean</code>
                * [.send(data, [flags], [address])](#module_socket.socket+send) ⇒ <code>number</code>
                * [.recv([length], [flags], [address])](#module_socket.socket+recv) ⇒ <code>string</code>
                * [.sendmsg([data], [ancillaryData], [address], [flags])](#module_socket.socket+sendmsg) ⇒ <code>number</code>
                * [.recvmsg([sizes], [ancillarySize], [flags])](#module_socket.socket+recvmsg) ⇒ [<code>ReceivedMessage</code>](#module_socket.socket.ReceivedMessage)
                * [.bind(address)](#module_socket.socket+bind) ⇒ <code>boolean</code>
                * [.listen([backlog])](#module_socket.socket+listen) ⇒ <code>boolean</code>
                * [.accept([address], [flags])](#module_socket.socket+accept) ⇒ [<code>socket</code>](#module_socket.socket)
                * [.shutdown(how)](#module_socket.socket+shutdown) ⇒ <code>boolean</code>
                * [.peercred()](#module_socket.socket+peercred) ⇒ [<code>PeerCredentials</code>](#module_socket.socket.PeerCredentials)
                * [.peername()](#module_socket.socket+peername) ⇒ [<code>SocketAddress</code>](#module_socket.socket.SocketAddress)
                * [.sockname()](#module_socket.socket+sockname) ⇒ [<code>SocketAddress</code>](#module_socket.socket.SocketAddress)
                * [.close()](#module_socket.socket+close) ⇒ <code>boolean</code>
                * [.error([numeric])](#module_socket.socket+error) ⇒ <code>string</code> \| <code>number</code>
                * [.error([numeric])](#module_socket.socket+error) ⇒ <code>string</code> \| <code>number</code>
                * [.error([numeric])](#module_socket.socket+error) ⇒ <code>string</code> \| <code>number</code>
                * [.error([numeric])](#module_socket.socket+error) ⇒ <code>string</code> \| <code>number</code>
            * _static_
                * [.SocketAddress](#module_socket.socket.SocketAddress) : <code>Object</code>
                * [.ControlMessage](#module_socket.socket.ControlMessage) : <code>Object</code>
                * [.ReceivedMessage](#module_socket.socket.ReceivedMessage) : <code>Object</code>
                * [.PeerCredentials](#module_socket.socket.PeerCredentials) : <code>Object</code>
                * [.SocketAddress](#module_socket.socket.SocketAddress) : <code>Object</code>
                * [.ControlMessage](#module_socket.socket.ControlMessage) : <code>Object</code>
                * [.ReceivedMessage](#module_socket.socket.ReceivedMessage) : <code>Object</code>
                * [.PeerCredentials](#module_socket.socket.PeerCredentials) : <code>Object</code>
        * [.socket](#module_socket.socket)
            * _instance_
                * [.setopt(level, option, value)](#module_socket.socket+setopt) ⇒ <code>boolean</code>
                * [.getopt(level, option)](#module_socket.socket+getopt) ⇒ <code>\*</code>
                * [.fileno()](#module_socket.socket+fileno) ⇒ <code>number</code>
                * [.connect(address, port)](#module_socket.socket+connect) ⇒ <code>boolean</code>
                * [.send(data, [flags], [address])](#module_socket.socket+send) ⇒ <code>number</code>
                * [.recv([length], [flags], [address])](#module_socket.socket+recv) ⇒ <code>string</code>
                * [.sendmsg([data], [ancillaryData], [address], [flags])](#module_socket.socket+sendmsg) ⇒ <code>number</code>
                * [.recvmsg([sizes], [ancillarySize], [flags])](#module_socket.socket+recvmsg) ⇒ [<code>ReceivedMessage</code>](#module_socket.socket.ReceivedMessage)
                * [.bind(address)](#module_socket.socket+bind) ⇒ <code>boolean</code>
                * [.listen([backlog])](#module_socket.socket+listen) ⇒ <code>boolean</code>
                * [.accept([address], [flags])](#module_socket.socket+accept) ⇒ [<code>socket</code>](#module_socket.socket)
                * [.shutdown(how)](#module_socket.socket+shutdown) ⇒ <code>boolean</code>
                * [.peercred()](#module_socket.socket+peercred) ⇒ [<code>PeerCredentials</code>](#module_socket.socket.PeerCredentials)
                * [.peername()](#module_socket.socket+peername) ⇒ [<code>SocketAddress</code>](#module_socket.socket.SocketAddress)
                * [.sockname()](#module_socket.socket+sockname) ⇒ [<code>SocketAddress</code>](#module_socket.socket.SocketAddress)
                * [.close()](#module_socket.socket+close) ⇒ <code>boolean</code>
                * [.setopt(level, option, value)](#module_socket.socket+setopt) ⇒ <code>boolean</code>
                * [.getopt(level, option)](#module_socket.socket+getopt) ⇒ <code>\*</code>
                * [.fileno()](#module_socket.socket+fileno) ⇒ <code>number</code>
                * [.connect(address, port)](#module_socket.socket+connect) ⇒ <code>boolean</code>
                * [.send(data, [flags], [address])](#module_socket.socket+send) ⇒ <code>number</code>
                * [.recv([length], [flags], [address])](#module_socket.socket+recv) ⇒ <code>string</code>
                * [.sendmsg([data], [ancillaryData], [address], [flags])](#module_socket.socket+sendmsg) ⇒ <code>number</code>
                * [.recvmsg([sizes], [ancillarySize], [flags])](#module_socket.socket+recvmsg) ⇒ [<code>ReceivedMessage</code>](#module_socket.socket.ReceivedMessage)
                * [.bind(address)](#module_socket.socket+bind) ⇒ <code>boolean</code>
                * [.listen([backlog])](#module_socket.socket+listen) ⇒ <code>boolean</code>
                * [.accept([address], [flags])](#module_socket.socket+accept) ⇒ [<code>socket</code>](#module_socket.socket)
                * [.shutdown(how)](#module_socket.socket+shutdown) ⇒ <code>boolean</code>
                * [.peercred()](#module_socket.socket+peercred) ⇒ [<code>PeerCredentials</code>](#module_socket.socket.PeerCredentials)
                * [.peername()](#module_socket.socket+peername) ⇒ [<code>SocketAddress</code>](#module_socket.socket.SocketAddress)
                * [.sockname()](#module_socket.socket+sockname) ⇒ [<code>SocketAddress</code>](#module_socket.socket.SocketAddress)
                * [.close()](#module_socket.socket+close) ⇒ <code>boolean</code>
                * [.error([numeric])](#module_socket.socket+error) ⇒ <code>string</code> \| <code>number</code>
                * [.error([numeric])](#module_socket.socket+error) ⇒ <code>string</code> \| <code>number</code>
                * [.error([numeric])](#module_socket.socket+error) ⇒ <code>string</code> \| <code>number</code>
                * [.error([numeric])](#module_socket.socket+error) ⇒ <code>string</code> \| <code>number</code>
            * _static_
                * [.SocketAddress](#module_socket.socket.SocketAddress) : <code>Object</code>
                * [.ControlMessage](#module_socket.socket.ControlMessage) : <code>Object</code>
                * [.ReceivedMessage](#module_socket.socket.ReceivedMessage) : <code>Object</code>
                * [.PeerCredentials](#module_socket.socket.PeerCredentials) : <code>Object</code>
                * [.SocketAddress](#module_socket.socket.SocketAddress) : <code>Object</code>
                * [.ControlMessage](#module_socket.socket.ControlMessage) : <code>Object</code>
                * [.ReceivedMessage](#module_socket.socket.ReceivedMessage) : <code>Object</code>
                * [.PeerCredentials](#module_socket.socket.PeerCredentials) : <code>Object</code>
        * [.AddressInfo](#module_socket.AddressInfo) : <code>Object</code>
        * [.PollSpec](#module_socket.PollSpec) : <code>Array</code>
        * [.AddressInfo](#module_socket.AddressInfo) : <code>Object</code>
        * [.PollSpec](#module_socket.PollSpec) : <code>Array</code>
    * _inner_
        * [~Address Families](#module_socket..Address Families)
        * [~Socket Types](#module_socket..Socket Types)
        * [~Message Flags](#module_socket..Message Flags)
        * [~IP Protocol Constants](#module_socket..IP Protocol Constants)
        * [~IPv6](#module_socket..IPv6) : <code>Object</code>
        * [~Socket Option Constants](#module_socket..Socket Option Constants)
        * [~TCP Protocol Constants](#module_socket..TCP Protocol Constants)
        * [~Packet Socket Constants](#module_socket..Packet Socket Constants)
        * [~UDP Protocol Constants](#module_socket..UDP Protocol Constants)
        * [~Shutdown Constants](#module_socket..Shutdown Constants)
        * [~Address Info Flags](#module_socket..Address Info Flags)
        * [~Name Info Constants](#module_socket..Name Info Constants)
        * [~Poll Event Constants](#module_socket..Poll Event Constants)
        * [~Address Families](#module_socket..Address Families)
        * [~Socket Types](#module_socket..Socket Types)
        * [~Message Flags](#module_socket..Message Flags)
        * [~IP Protocol Constants](#module_socket..IP Protocol Constants)
        * [~IPv6](#module_socket..IPv6) : <code>Object</code>
        * [~Socket Option Constants](#module_socket..Socket Option Constants)
        * [~TCP Protocol Constants](#module_socket..TCP Protocol Constants)
        * [~Packet Socket Constants](#module_socket..Packet Socket Constants)
        * [~UDP Protocol Constants](#module_socket..UDP Protocol Constants)
        * [~Shutdown Constants](#module_socket..Shutdown Constants)
        * [~Address Info Flags](#module_socket..Address Info Flags)
        * [~Name Info Constants](#module_socket..Name Info Constants)
        * [~Poll Event Constants](#module_socket..Poll Event Constants)

<a name="module_socket+error"></a>

### socket.error([numeric]) ⇒ <code>string</code> \| <code>number</code>
<p>Query error information.</p>
<p>Returns a string containing a description of the last occurred error when
the <em>numeric</em> argument is absent or false.</p>
<p>Returns a positive (<code>errno</code>) or negative (<code>EAI_*</code> constant) error code number
when the <em>numeric</em> argument is <code>true</code>.</p>
<p>Returns <code>null</code> if there is no error information.</p>

**Kind**: instance method of [<code>socket</code>](#module_socket)  

| Param | Type | Description |
| --- | --- | --- |
| [numeric] | <code>boolean</code> | <p>Whether to return a numeric error code (<code>true</code>) or a human readable error message (false).</p> |

**Example**  
```js
// Trigger socket error by attempting to bind IPv6 address with IPv4 socket
socket.create(socket.AF_INET, socket.SOCK_STREAM, 0).bind("::", 8080);

// Print error (should yield "Address family not supported by protocol")
print(socket.error(), "\n");

// Trigger resolve error
socket.addrinfo("doesnotexist.org");

// Query error code (should yield -2 for EAI_NONAME)
print(socket.error(true), "\n");  //
```
<a name="module_socket+strerror"></a>

### socket.strerror(code) ⇒ <code>string</code>
<p>Returns a string containing a description of the positive (<code>errno</code>) or
negative (<code>EAI_*</code> constant) error code number given by the <em>code</em> argument.</p>
<p>Returns <code>null</code> if the error code number is unknown.</p>

**Kind**: instance method of [<code>socket</code>](#module_socket)  

| Param | Type | Description |
| --- | --- | --- |
| code | <code>number</code> | <p>The error code.</p> |

**Example**  
```js
// Should output 'Name or service not known'.
print(socket.strerror(-2), '\n');

// Should output 'No route to host'.
print(socket.strerror(113), '\n');
```
<a name="module_socket+sockaddr"></a>

### socket.sockaddr(address) ⇒ [<code>SocketAddress</code>](#module_socket.socket.SocketAddress)
<p>Parses the provided address value into a socket address representation.</p>
<p>This function parses the given address value into a socket address
representation required for a number of socket operations. The address value
can be provided in various formats:</p>
<ul>
<li>For IPv4 addresses, it can be a string representing the IP address,
optionally followed by a port number separated by colon, e.g.
<code>192.168.0.1:8080</code>.</li>
<li>For IPv6 addresses, it must be an address string enclosed in square
brackets if a port number is specified, otherwise the brackets are
optional. The address string may also include a scope ID in the form
<code>%ifname</code> or <code>%number</code>, e.g. <code>[fe80::1%eth0]:8080</code> or <code>fe80::1%15</code>.</li>
<li>Any string value containing a slash is treated as UNIX domain socket path.</li>
<li>Alternatively, it can be provided as an array returned by
[iptoarr()](#module_core+iptoarr), representing the address octets.</li>
<li>It can also be an object representing a network address, with properties
for <code>address</code> (the IP address) and <code>port</code> or a single property <code>path</code> to
denote a UNIX domain socket address.</li>
</ul>

**Kind**: instance method of [<code>socket</code>](#module_socket)  
**Returns**: [<code>SocketAddress</code>](#module_socket.socket.SocketAddress) - <p>A socket address representation of the provided address value, or <code>null</code> if
the address could not be parsed.</p>  

| Param | Type | Description |
| --- | --- | --- |
| address | <code>string</code> \| <code>Array.&lt;number&gt;</code> \| [<code>SocketAddress</code>](#module_socket.socket.SocketAddress) | <p>The address value to parse.</p> |

**Example**  
```js
// Parse an IP address string with port
const address1 = sockaddr('192.168.0.1:8080');

// Parse an IPv6 address string with port and scope identifier
const address2 = sockaddr('[fe80::1%eth0]:8080');

// Parse an array representing an IP address
const address3 = sockaddr([192, 168, 0, 1]);

// Parse a network address object
const address4 = sockaddr({ address: '192.168.0.1', port: 8080 });

// Convert a path value to a UNIX domain socket address
const address5 = sockaddr('/var/run/daemon.sock');
```
<a name="module_socket+nameinfo"></a>

### socket.nameinfo(address, [flags]) ⇒ <code>Object</code>
<p>Resolves the given network address into hostname and service name.</p>
<p>The <code>nameinfo()</code> function provides an API for reverse DNS lookup and service
name resolution. It returns an object containing the following properties:</p>
<ul>
<li><code>hostname</code>: The resolved hostname.</li>
<li><code>service</code>: The resolved service name.</li>
</ul>
<p>Returns an object representing the resolved hostname and service name.
Return <code>null</code> if an error occurred during resolution.</p>

**Kind**: instance method of [<code>socket</code>](#module_socket)  
**See**

- {@link module:socket~"Socket Types"|Socket Types}
- {@link module:socket~"Name Info Constants"|AName Info Constants}


| Param | Type | Description |
| --- | --- | --- |
| address | <code>string</code> \| [<code>SocketAddress</code>](#module_socket.socket.SocketAddress) | <p>The network address to resolve. It can be specified as:</p> <ul> <li>A string representing the IP address.</li> <li>An object representing the address with properties <code>address</code> and <code>port</code>.</li> </ul> |
| [flags] | <code>number</code> | <p>Optional flags that provide additional control over the resolution process, specified as bitwise OR-ed number of <code>NI_*</code> constants.</p> |

**Example**  
```js
// Resolve a network address into hostname and service name
const result = network.getnameinfo('192.168.1.1:80');
print(result); // { "hostname": "example.com", "service": "http" }
```
<a name="module_socket+addrinfo"></a>

### socket.addrinfo(hostname, [service], [hints]) ⇒ [<code>Array.&lt;AddressInfo&gt;</code>](#module_socket.AddressInfo)
<p>Resolves the given hostname and optional service name into a list of network
addresses, according to the provided hints.</p>
<p>The <code>addrinfo()</code> function provides an API for performing DNS and service name
resolution. It returns an array of objects, each representing a resolved
address.</p>
<p>Returns an array of resolved addresses.
Returns <code>null</code> if an error occurred during resolution.</p>

**Kind**: instance method of [<code>socket</code>](#module_socket)  
**See**

- {@link module:socket~"Socket Types"|Socket Types}
- {@link module:socket~"Address Info Flags"|Address Info Flags}


| Param | Type | Description |
| --- | --- | --- |
| hostname | <code>string</code> | <p>The hostname to resolve.</p> |
| [service] | <code>string</code> | <p>Optional service name to resolve. If not provided, the service field of the resulting address information structures is left uninitialized.</p> |
| [hints] | <code>Object</code> | <p>Optional hints object that provides additional control over the resolution process. It can contain the following properties:</p> <ul> <li><code>family</code>: The preferred address family (<code>AF_INET</code> or <code>AF_INET6</code>).</li> <li><code>socktype</code>: The socket type (<code>SOCK_STREAM</code>, <code>SOCK_DGRAM</code>, etc.).</li> <li><code>protocol</code>: The protocol of returned addresses.</li> <li><code>flags</code>: Bitwise OR-ed <code>AI_*</code> flags to control the resolution behavior.</li> </ul> |

**Example**  
```js
// Resolve all addresses
const addresses = socket.addrinfo('example.org');

// Resolve IPv4 addresses for a given hostname and service
const ipv4addresses = socket.addrinfo('example.com', 'http', { family: socket.AF_INET });

// Resolve IPv6 addresses without specifying a service
const ipv6Addresses = socket.addrinfo


---

<a id="ucode-module-struct"></a>
# ucode module: `struct`

> **Source:** [`lib/struct.c`](https://github.com/jow-/ucode/blob/master/lib/struct.c)
> **Live docs:** https://ucode.mein.io/module-struct.html
> **Generated:** 2026-03-04 13:26 UTC from commit `e87be9d`

---

## Modules

<dl>
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

<a name="module_struct"></a>

## struct
<h1 id="handle-packed-binary-data">Handle Packed Binary Data</h1>
<p>The <code>struct</code> module provides routines for interpreting byte strings as packed
binary data.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { pack, unpack } from 'struct';

let buffer = pack('bhl', -13, 1234, 444555666);
let values = unpack('bhl', buffer);
</code></pre>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as struct from 'struct';

let buffer = struct.pack('bhl', -13, 1234, 444555666);
let values = struct.unpack('bhl', buffer);
</code></pre>
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
</tbo


---

<a id="ucode-module-ubus"></a>
# ucode module: `ubus`

> **Source:** [`lib/ubus.c`](https://github.com/jow-/ucode/blob/master/lib/ubus.c)
> **Live docs:** https://ucode.mein.io/module-ubus.html
> **Generated:** 2026-03-04 13:26 UTC from commit `e87be9d`

---

## Modules

<dl>
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

<a name="module_debug"></a>

## debug
<h1 id="debugger-module">Debugger Module</h1>
<p>This module provides runtime debug functionality for ucode scripts.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { memdump, traceback } from 'debug';

let stacktrace = traceback(1);

memdump(&quot;/tmp/dump.txt&quot;);
</code></pre>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as debug from 'debug';

let stacktrace = debug.traceback(1);

debug.memdump(&quot;/tmp/dump.txt&quot;);
</code></pre>
<p>Additionally, the debug module namespace may also be imported by invoking the
<code>ucode</code> interpreter with the <code>-ldebug</code> switch.</p>
<p>Upon loading, the <code>debug</code> module will register a <code>SIGUSR2</code> signal handler
which, upon receipt of the signal, will write a memory dump of the currently
running program to <code>/tmp/ucode.$timestamp.$pid.memdump</code>. This default
behavior can be inhibited by setting the <code>UCODE_DEBUG_MEMDUMP_ENABLED</code>
environment variable to <code>0</code> when starting the process. The memory dump signal
and output directory can be overridden with the <code>UCODE_DEBUG_MEMDUMP_SIGNAL</code>
and <code>UCODE_DEBUG_MEMDUMP_PATH</code> environment variables respectively.</p>


* [debug](#module_debug)
    * _instance_
        * [.memdump(file)](#module_debug+memdump) ⇒ <code>boolean</code>
        * [.traceback([level])](#module_debug+traceback) ⇒ [<code>Array.&lt;StackTraceEntry&gt;</code>](#module_debug.StackTraceEntry)
        * [.sourcepos()](#module_debug+sourcepos) ⇒ [<code>SourcePosition</code>](#module_debug.SourcePosition)
        * [.getinfo(value)](#module_debug+getinfo) ⇒ [<code>ValueInformation</code>](#module_debug.ValueInformation)
        * [.getlocal([level], variable)](#module_debug+getlocal) ⇒ [<code>LocalInfo</code>](#module_debug.LocalInfo)
        * [.setlocal([level], variable, [value])](#module_debug+setlocal) ⇒ [<code>LocalInfo</code>](#module_debug.LocalInfo)
        * [.getupval(target, variable)](#module_debug+getupval) ⇒ [<code>UpvalInfo</code>](#module_debug.UpvalInfo)
        * [.setupval(target, variable, value)](#module_debug+setupval) ⇒ [<code>UpvalInfo</code>](#module_debug.UpvalInfo)
    * _static_
        * [.StackTraceEntry](#module_debug.StackTraceEntry) : <code>Object</code>
        * [.SourcePosition](#module_debug.SourcePosition) : <code>Object</code>
        * [.UpvalRef](#module_debug.UpvalRef) : <code>Object</code>
        * [.ValueInformation](#module_debug.ValueInformation) : <code>Object</code>
        * [.LocalInfo](#module_debug.LocalInfo) : <code>Object</code>
        * [.UpvalInfo](#module_debug.UpvalInfo) : <code>Object</code>

<a name="module_debug+memdump"></a>

### debug.memdump(file) ⇒ <code>boolean</code>
<p>Write a memory dump report to the given file.</p>
<p>This function generates a human readable memory dump of ucode values
currently managed by the running VM which is useful to track down logical
memory leaks in scripts.</p>
<p>The file parameter can be either a string value containing a file path, in
which case this function tries to create and write the report file at the
given location, or an already open file handle this function should write to.</p>
<p>Returns <code>true</code> if the report has been written.</p>
<p>Returns <code>null</code> if the file could not be opened or if the handle was invalid.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Description |
| --- | --- | --- |
| file | <code>string</code> \| [<code>file</code>](#module_fs.file) \| [<code>proc</code>](#module_fs.proc) | <p>The file path or open file handle to write report to.</p> |

<a name="module_debug+traceback"></a>

### debug.traceback([level]) ⇒ [<code>Array.&lt;StackTraceEntry&gt;</code>](#module_debug.StackTraceEntry)
<p>Capture call stack trace.</p>
<p>This function captures the current call stack and returns it. The optional
level parameter controls how many calls up the trace should start. It
defaults to <code>1</code>, that is the function calling this <code>traceback()</code> function.</p>
<p>Returns an array of stack trace entries describing the function invocations
up to the point where <code>traceback()</code> is called.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [level] | <code>number</code> | <code>1</code> | <p>The number of callframes up the call trace should start, <code>0</code> is this function itself, <code>1</code> the function calling it and so on.</p> |

<a name="module_debug+sourcepos"></a>

### debug.sourcepos() ⇒ [<code>SourcePosition</code>](#module_debug.SourcePosition)
<p>Obtain information about the current source position.</p>
<p>The <code>sourcepos()</code> function determines the source code position of the
current instruction invoking this function.</p>
<p>Returns a dictionary containing the filename, line number and line byte
offset of the call site.</p>
<p>Returns <code>null</code> if this function was invoked from C code.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  
<a name="module_debug+getinfo"></a>

### debug.getinfo(value) ⇒ [<code>ValueInformation</code>](#module_debug.ValueInformation)
<p>Obtain information about the given value.</p>
<p>The <code>getinfo()</code> function allows querying internal information about the
given ucode value, such as the current reference count, the mark bit state
etc.</p>
<p>Returns a dictionary with value type specific details.</p>
<p>Returns <code>null</code> if a <code>null</code> value was provided.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Description |
| --- | --- | --- |
| value | <code>\*</code> | <p>The value to query information for.</p> |

<a name="module_debug+getlocal"></a>

### debug.getlocal([level], variable) ⇒ [<code>LocalInfo</code>](#module_debug.LocalInfo)
<p>Obtain local variable.</p>
<p>The <code>getlocal()</code> function retrieves information about the specified local
variable at the given call stack depth.</p>
<p>The call stack depth specifies the amount of levels up local variables should
be queried. A value of <code>0</code> refers to this <code>getlocal()</code> function call itself,
<code>1</code> to the function calling <code>getlocal()</code> and so on.</p>
<p>The variable to query might be either specified by name or by its index with
index numbers following the source code declaration order.</p>
<p>Returns a dictionary holding information about the given variable.</p>
<p>Returns <code>null</code> if the stack depth exceeds the size of the current call stack.</p>
<p>Returns <code>null</code> if the invocation at the given stack depth is a C call.</p>
<p>Returns <code>null</code> if the given variable name is not found or the given variable
index is invalid.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [level] | <code>number</code> | <code>1</code> | <p>The amount of call stack levels up local variables should be queried.</p> |
| variable | <code>string</code> \| <code>number</code> |  | <p>The variable index or variable name to obtain information for.</p> |

<a name="module_debug+setlocal"></a>

### debug.setlocal([level], variable, [value]) ⇒ [<code>LocalInfo</code>](#module_debug.LocalInfo)
<p>Set local variable.</p>
<p>The <code>setlocal()</code> function manipulates the value of the specified local
variable at the given call stack depth.</p>
<p>The call stack depth specifies the amount of levels up local variables should
be updated. A value of <code>0</code> refers to this <code>setlocal()</code> function call itself,
<code>1</code> to the function calling <code>setlocal()</code> and so on.</p>
<p>The variable to update might be either specified by name or by its index with
index numbers following the source code declaration order.</p>
<p>Returns a dictionary holding information about the updated variable.</p>
<p>Returns <code>null</code> if the stack depth exceeds the size of the current call stack.</p>
<p>Returns <code>null</code> if the invocation at the given stack depth is a C call.</p>
<p>Returns <code>null</code> if the given variable name is not found or the given variable
index is invalid.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [level] | <code>number</code> | <code>1</code> | <p>The amount of call stack levels up local variables should be updated.</p> |
| variable | <code>string</code> \| <code>number</code> |  | <p>The variable index or variable name to update.</p> |
| [value] | <code>\*</code> | <code></code> | <p>The value to set the local variable to.</p> |

<a name="module_debug+getupval"></a>

### debug.getupval(target, variable) ⇒ [<code>UpvalInfo</code>](#module_debug.UpvalInfo)
<p>Obtain captured variable (upvalue).</p>
<p>The <code>getupval()</code> function retrieves information about the specified captured
variable associated with the given function value or the invoked function at
the given call stack depth.</p>
<p>The call stack depth specifies the amount of levels up the function should be
selected to query associated captured variables for. A value of <code>0</code> refers to
this <code>getupval()</code> function call itself, <code>1</code> to the function calling
<code>getupval()</code> and so on.</p>
<p>The variable to query might be either specified by name or by its index with
index numbers following the source code declaration order.</p>
<p>Returns a dictionary holding information about the given variable.</p>
<p>Returns <code>null</code> if the given function value is not a closure.</p>
<p>Returns <code>null</code> if the stack depth exceeds the size of the current call stack.</p>
<p>Returns <code>null</code> if the invocation at the given stack depth is not a closure.</p>
<p>Returns <code>null</code> if the given variable name is not found or the given variable
index is invalid.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Description |
| --- | --- | --- |
| target | <code>function</code> \| <code>number</code> | <p>Either a function value referring to a closure to query upvalues for or a stack depth number selecting a closure that many levels up.</p> |
| variable | <code>string</code> \| <code>number</code> | <p>The variable index or variable name to obtain information for.</p> |

<a name="module_debug+setupval"></a>

### debug.setupval(target, variable, value) ⇒ [<code>UpvalInfo</code>](#module_debug.UpvalInfo)
<p>Set upvalue.</p>
<p>The <code>setupval()</code> function manipulates the value of the specified captured
variable associated with the given function value or the invoked function at
the given call stack depth.</p>
<p>The call stack depth specifies the amount of levels up the function should be
selected to update associated captured variables for. A value of <code>0</code> refers
to this <code>setupval()</code> function call itself, <code>1</code> to the function calling
<code>setupval()</code> and so on.</p>
<p>The variable to update might be either specified by name or by its index with
index numbers following the source code declaration order.</p>
<p>Returns a dictionary holding information about the updated variable.</p>
<p>Returns <code>null</code> if the given function value is not a closure.</p>
<p>Returns <code>null</code> if the stack depth exceeds the size of the current call stack.</p>
<p>Returns <code>null</code> if the invocation at the given stack depth is not a closure.</p>
<p>Returns <code>null</code> if the given variable name is not found or the given variable
index is invalid.</p>

**Kind**: instance method of [<code>debug</code>](#module_debug)  

| Param | Type | Description |
| --- | --- | --- |
| target | <code>function</code> \| <code>number</code> | <p>Either a function value referring to a closure to update upvalues for or a stack depth number selecting a closure that many levels up.</p> |
| variable | <code>string</code> \| <code>number</code> | <p>The variable index or variable name to update.</p> |
| value | <code>\*</code> | <p>The value to set the variable to.</p> |

<a name="module_debug.StackTraceEntry"></a>

### debug.StackTraceEntry : <code>Object</code>
**Kind**: static typedef of [<code>debug</code>](#module_debug)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| callee | <code>function</code> | <p>The function that was called.</p> |
| this | <code>\*</code> | <p>The <code>this</code> context the function was called with.</p> |
| mcall | <code>boolean</code> | <p>Indicates whether the function was invoked as a method.</p> |
| [strict] | <code>boolean</code> | <p>Indicates whether the VM was running in strict mode when the function was called (only applicable to non-C, pure ucode calls).</p> |
| [filename] | <code>string</code> | <p>The name of the source file that called the function (only applicable to non-C, pure ucode calls).</p> |
| [line] | <code>number</code> | <p>The source line of the function call (only applicable to non-C, pure ucode calls).</p> |
| [byte] | <code>number</code> | <p>The source line offset of the function call (only applicable to non-C, pure ucode calls).</p> |
| [context] | <code>string</code> | <p>The surrounding source code context formatted as human-readable string, useful for generating debug messages (only applicable to non-C, pure ucode calls).</p> |

<a name="module_debug.SourcePosition"></a>

### debug.SourcePosition : <code>Object</code>
**Kind**: static typedef of [<code>debug</code>](#module_debug)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| filename | <code>string</code> | <p>The name of the source file that called this function.</p> |
| line | <code>number</code> | <p>The source line of the function call.</p> |
| byte | <code>number</code> | <p>The source line offset of the function call.</p> |

<a name="module_debug.UpvalRef"></a>

### debug.UpvalRef : <code>Object</code>
**Kind**: static typedef of [<code>debug</code>](#module_debug)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| name | <code>string</code> | <p>The name of the captured variable.</p> |
| closed | <code>boolean</code> | <p>Indicates whether the captured variable (upvalue) is closed or not. A closed upvalue means that the function value outlived the declaration scope of the captured variable.</p> |
| value | <code>\*</code> | <p>The current value of the captured variable.</p> |
| [slot] | <code>number</code> | <p>The stack slot of the captured variable. Only applicable to open (non-closed) captured variables.</p> |

<a name="module_debug.ValueInformation"></a>

### debug.ValueInformation : <code>Object</code>
**Kind**: static typedef of [<code>debug</code>](#module_debug)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| type | <code>string</code> | <p>The name of the value type, one of <code>integer</code>, <code>boolean</code>, <code>string</code>, <code>double</code>, <code>array</code>, <code>object</code>, <code>regexp</code>, <code>cfunction</code>, <code>closure</code>, <code>upvalue</code> or <code>resource</code>.</p> |
| value | <code>\*</code> | <p>The value itself.</p> |
| tagged | <code>boolean</code> | <p>Indicates whether the given value is internally stored as tagged pointer without an additional heap allocation.</p> |
| [mark] | <code>boolean</code> | <p>Indicates whether the value has it's mark bit set, which is used for loop detection during recursive object traversal on garbage collection cycles or complex value stringification. Only applicable to non-tagged values.</p> |
| [refcount] | <code>number</code> | <p>The current reference count of the value. Note that the <code>getinfo()</code> function places a reference to the value into the <code>value</code> field of the resulting information dictionary, so the ref count will always be at least 2 - one reference for the function call argument and one for the value property in the result dictionary. Only applicable to non-tagged values.</p> |
| [unsigned] | <code>boolean</code> | <p>Whether the number value is internally stored as unsigned integer. Only applicable to non-tagged integer values.</p> |
| [address] | <code>number</code> | <p>The address of the underlying C heap memory. Only applicable to non-tagged <code>string</code>, <code>array</code>, <code>object</code>, <code>cfunction</code> or <code>resource</code> values.</p> |
| [length] | <code>number</code> | <p>The length of the underlying string memory. Only applicable to non-tagged <code>string</code> values.</p> |
| [count] | <code>number</code> | <p>The amount of elements in the underlying memory structure. Only applicable to <code>array</code> and <code>object</code> values.</p> |
| [constant] | <code>boolean</code> | <p>Indicates whether the value is constant (immutable). Only applicable to <code>array</code> and <code>object</code> values.</p> |
| [prototype] | <code>\*</code> | <p>The associated prototype value, if any. Only applicable to <code>array</code>, <code>object</code> and <code>prototype</code> values.</p> |
| [source] | <code>string</code> | <p>The original regex source pattern. Only applicable to <code>regexp</code> values.</p> |
| [icase] | <code>boolean</code> | <p>Whether the compiled regex has the <code>i</code> (ignore case) flag set. Only applicable to <code>regexp</code> values.</p> |
| [global] | <code>boolean</code> | <p>Whether the compiled regex has the <code>g</code> (global) flag set. Only applicable to <code>regexp</code> values.</p> |
| [newline] | <code>boolean</code> | <p>Whether the compiled regex has the <code>s</code> (single line) flag set. Only applicable to <code>regexp</code> values.</p> |
| [nsub] | <code>number</code> | <p>The amount of capture groups within the regular expression. Only applicable to <code>regexp</code> values.</p> |
| [name] | <code>string</code> | <p>The name of the non-anonymous function. Only applicable to <code>cfunction</code> and <code>closure</code> values. Set to <code>null</code> for anonymous function values.</p> |
| [arrow] | <code>boolean</code> | <p>Indicates whether the ucode function value is an arrow function. Only applicable to <code>closure</code> values.</p> |
| [module] | <code>boolean</code> | <p>Indicates whether the ucode function value is a module entry point. Only applicable to <code>closure</code> values.</p> |
| [strict] | <code>boolean</code> | <p>Indicates whether the function body will be executed in strict mode. Only applicable to <code>closure</code> values.</p> |
| [vararg] | <code>boolean</code> | <p>Indicates whether the ucode function takes a variable number of arguments. Only applicable to <code>closure</code> values.</p> |
| [nargs] | <code>number</code> | <p>The number of arguments expected by the ucode function, excluding a potential final variable argument ellipsis. Only applicable to <code>closure</code> values.</p> |
| [argnames] | <code>Array.&lt;string&gt;</code> | <p>The names of the function arguments in their declaration order. Only applicable to <code>closure</code> values.</p> |
| [nupvals] | <code>number</code> | <p>The number of upvalues associated with the ucode function. Only applicable to <code>closure</code> values.</p> |
| [upvals] | [<code>Array.&lt;UpvalRef&gt;</code>](#module_debug.UpvalRef) | <p>An array of upvalue information objects. Only applicable to <code>closure</code> values.</p> |
| [filename] | <code>string</code> | <p>The path of the source file the function was declared in. Only applicable to <code>closure</code> values.</p> |
| [line] | <code>number</code> | <p>The source line number the function was declared at. Only applicable to <code>closure</code> values.</p> |
| [byte] | <code>number</code> | <p>The source line offset the function was declared at. Only applicable to <code>closure</code> values.</p> |
| [type] | <code>string</code> | <p>The resource type name. Only applicable to <code>resource</code> values.</p> |

<a name="module_debug.LocalInfo"></a>

### debug.LocalInfo : <code>Object</code>
**Kind**: static typedef of [<code>debug</code>](#module_debug)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| index | <code>number</code> | <p>The index of the local variable.</p> |
| name | <code>string</code> | <p>The name of the local variable.</p> |
| value | <code>\*</code> | <p>The current value of the local variable.</p> |
| linefrom | <code>number</code> | <p>The source line number of the local variable declaration.</p> |
| bytefrom | <code>number</code> | <p>The source line offset of the local variable declaration.</p> |
| lineto | <code>number</code> | <p>The source line number where the local variable goes out of scope.</p> |
| byteto | <code>number</code> | <p>The source line offset where the local vatiable goes out of scope.</p> |

<a name="module_debug.UpvalInfo"></a>

### debug.UpvalInfo : <code>Object</code>
**Kind**: static typedef of [<code>debug</code>](#module_debug)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| index | <code>number</code> | <p>The index of the captured variable (upvalue).</p> |
| name | <code>string</code> | <p>The name of the captured variable.</p> |
| closed | <code>boolean</code> | <p>Indicates whether the captured variable is closed or not. A closed upvalue means that the function outlived the declaration scope of the captured variable.</p> |
| value | <code>\*</code> | <p>The current value of the captured variable.</p> |

<a name="module_digest"></a>

## digest
<h1 id="digest-functions">Digest Functions</h1>
<p>The <code>digest</code> module bundles various digest functions.</p>


* [digest](#module_digest)
    * [.md5(str)](#module_digest+md5) ⇒ <code>string</code>
    * [.sha1(str)](#module_digest+sha1) ⇒ <code>string</code>
    * [.sha256(str)](#module_digest+sha256) ⇒ <code>string</code>
    * [.md2(str)](#module_digest+md2) ⇒ <code>string</code>
    * [.md4(str)](#module_digest+md4) ⇒ <code>string</code>
    * [.sha384(str)](#module_digest+sha384) ⇒ <code>string</code>
    * [.sha512(str)](#module_digest+sha512) ⇒ <code>string</code>
    * [.md5_file(path)](#module_digest+md5_file) ⇒ <code>string</code>
    * [.sha1_file(path)](#module_digest+sha1_file) ⇒ <code>string</code>
    * [.sha256_file(path)](#module_digest+sha256_file) ⇒ <code>string</code>
    * [.md2_file(path)](#module_digest+md2_file) ⇒ <code>string</code>
    * [.md4_file(path)](#module_digest+md4_file) ⇒ <code>string</code>
    * [.sha384_file(path)](#module_digest+sha384_file) ⇒ <code>string</code>
    * [.sha512_file(path)](#module_digest+sha512_file) ⇒ <code>string</code>

<a name="module_digest+md5"></a>

### digest.md5(str) ⇒ <code>string</code>
<p>Calculates the MD5 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| str | <code>string</code> | <p>The string to hash.</p> |

**Example**  
```js
md5("This is a test");  // Returns "ce114e4501d2f4e2dcea3e17b546f339"
md5(123);               // Returns null
```
<a name="module_digest+sha1"></a>

### digest.sha1(str) ⇒ <code>string</code>
<p>Calculates the SHA1 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| --- | --- | --- |
| str | <code>string</code> | <p>The string to hash.</p> |

**Example**  
```js
sha1("This is a test");  // Returns "a54d88e06612d820bc3be72877c74f257b561b19"
sha1(123);               // Returns null
```
<a name="module_digest+sha256"></a>

### digest.sha256(str) ⇒ <code>string</code>
<p>Calculates the SHA256 hash of string and returns that hash.</p>
<p>Returns <code>null</code> if a non-string argument is given.</p>

**Kind**: instance method of [<code>digest</code>](#module_digest)  

| Param | Type | Description |
| -


---

<a id="ucode-module-uci"></a>
# ucode module: `uci`

> **Source:** [`lib/uci.c`](https://github.com/jow-/ucode/blob/master/lib/uci.c)
> **Live docs:** https://ucode.mein.io/module-uci.html
> **Generated:** 2026-03-04 13:26 UTC from commit `e87be9d`

---

## Modules

<dl>
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

<a name="module_uci"></a>

## uci
<h1 id="openwrt-uci-configuration">OpenWrt UCI configuration</h1>
<p>The <code>uci</code> module provides access to the native OpenWrt
[libuci](https://github.com/openwrt/uci) API for reading and
manipulating UCI configuration files.</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source"><code>import { cursor } from 'uci';

let ctx = cursor();
let hostname = ctx.get_first('system', 'system', 'hostname');
</code></pre>
<p>Alternatively, the module namespace can be imported
using a wildcard import statement:</p>
<pre class="prettyprint source"><code>import * as uci from 'uci';

let ctx = uci.cursor();
let hostname = ctx.get_first('system', 'system', 'hostname');
</code></pre>
<p>Additionally, the uci module namespace may also be imported by invoking
the <code>ucode</code> interpreter with the <code>-luci</code> switch.</p>


* [uci](#module_uci)
    * _instance_
        * [.error()](#module_uci+error) ⇒ <code>string</code>
        * [.cursor([config_dir], [delta_dir], [config2_dir], Parser)](#module_uci+cursor) ⇒ [<code>cursor</code>](#module_uci.cursor)
        * [.error()](#module_uci+error) ⇒ <code>string</code>
        * [.cursor([config_dir], [delta_dir], [config2_dir], Parser)](#module_uci+cursor) ⇒ [<code>cursor</code>](#module_uci.cursor)
    * _static_
        * [.cursor](#module_uci.cursor)
            * _instance_
                * [.load(config)](#module_uci.cursor+load) ⇒ <code>boolean</code>
                * [.unload(config)](#module_uci.cursor+unload) ⇒ <code>boolean</code>
                * [.get(config, section, [option])](#module_uci.cursor+get) ⇒ <code>string</code> \| <code>Array.&lt;string&gt;</code>
                * [.get_all(config, [section])](#module_uci.cursor+get_all) ⇒ <code>Object.&lt;string, module:uci.cursor.SectionObject&gt;</code> \| [<code>SectionObject</code>](#module_uci.cursor.SectionObject)
                * [.get_first(config, type, [option])](#module_uci.cursor+get_first) ⇒ <code>string</code> \| <code>Array.&lt;string&gt;</code>
                * [.add(config, type)](#module_uci.cursor+add) ⇒ <code>string</code>
                * [.set(config, section, option_or_type, [value])](#module_uci.cursor+set) ⇒ <code>boolean</code>
                * [.delete(config, section, [option])](#module_uci.cursor+delete) ⇒ <code>boolean</code>
                * [.list_append(config, section, option, value)](#module_uci.cursor+list_append) ⇒ <code>boolean</code>
                * [.list_remove(config, section, option, value)](#module_uci.cursor+list_remove) ⇒ <code>boolean</code>
                * [.rename(config, section, option_or_name, [name])](#module_uci.cursor+rename) ⇒ <code>boolean</code>
                * [.reorder(config, section, index)](#module_uci.cursor+reorder) ⇒ <code>boolean</code>
                * [.save([config])](#module_uci.cursor+save) ⇒ <code>boolean</code>
                * [.commit([config])](#module_uci.cursor+commit) ⇒ <code>boolean</code>
                * [.revert([config])](#module_uci.cursor+revert) ⇒ <code>boolean</code>
                * [.changes([config])](#module_uci.cursor+changes) ⇒ <code>Object.&lt;string, Array.&lt;module:uci.cursor.ChangeRecord&gt;&gt;</code>
                * [.foreach(config, type, callback)](#module_uci.cursor+foreach) ⇒ <code>boolean</code>
                * [.configs()](#module_uci.cursor+configs) ⇒ <code>Array.&lt;string&gt;</code>
                * [.load(config)](#module_uci.cursor+load) ⇒ <code>boolean</code>
                * [.unload(config)](#module_uci.cursor+unload) ⇒ <code>boolean</code>
                * [.get(config, section, [option])](#module_uci.cursor+get) ⇒ <code>string</code> \| <code>Array.&lt;string&gt;</code>
                * [.get_all(config, [section])](#module_uci.cursor+get_all) ⇒ <code>Object.&lt;string, module:uci.cursor.SectionObject&gt;</code> \| [<code>SectionObject</code>](#module_uci.cursor.SectionObject)
                * [.get_first(config, type, [option])](#module_uci.cursor+get_first) ⇒ <code>string</code> \| <code>Array.&lt;string&gt;</code>
                * [.add(config, type)](#module_uci.cursor+add) ⇒ <code>string</code>
                * [.set(config, section, option_or_type, [value])](#module_uci.cursor+set) ⇒ <code>boolean</code>
                * [.delete(config, section, [option])](#module_uci.cursor+delete) ⇒ <code>boolean</code>
                * [.list_append(config, section, option, value)](#module_uci.cursor+list_append) ⇒ <code>boolean</code>
                * [.list_remove(config, section, option, value)](#module_uci.cursor+list_remove) ⇒ <code>boolean</code>
                * [.rename(config, section, option_or_name, [name])](#module_uci.cursor+rename) ⇒ <code>boolean</code>
                * [.reorder(config, section, index)](#module_uci.cursor+reorder) ⇒ <code>boolean</code>
                * [.save([config])](#module_uci.cursor+save) ⇒ <code>boolean</code>
                * [.commit([config])](#module_uci.cursor+commit) ⇒ <code>boolean</code>
                * [.revert([config])](#module_uci.cursor+revert) ⇒ <code>boolean</code>
                * [.changes([config])](#module_uci.cursor+changes) ⇒ <code>Object.&lt;string, Array.&lt;module:uci.cursor.ChangeRecord&gt;&gt;</code>
                * [.foreach(config, type, callback)](#module_uci.cursor+foreach) ⇒ <code>boolean</code>
                * [.configs()](#module_uci.cursor+configs) ⇒ <code>Array.&lt;string&gt;</code>
                * [.error()](#module_uci.cursor+error) ⇒ <code>string</code>
                * [.error()](#module_uci.cursor+error) ⇒ <code>string</code>
                * [.error()](#module_uci.cursor+error) ⇒ <code>string</code>
                * [.error()](#module_uci.cursor+error) ⇒ <code>string</code>
            * _static_
                * [.ParserFlags](#module_uci.cursor.ParserFlags) : <code>Object</code>
                * [.ChangeRecord](#module_uci.cursor.ChangeRecord) : <code>Array.&lt;string&gt;</code>
                * [.SectionObject](#module_uci.cursor.SectionObject) : <code>Object.&lt;string, (boolean\|number\|string\|Array.&lt;string&gt;)&gt;</code>
                * [.SectionCallback](#module_uci.cursor.SectionCallback) : <code>function</code>
                * [.ParserFlags](#module_uci.cursor.ParserFlags) : <code>Object</code>
                * [.ChangeRecord](#module_uci.cursor.ChangeRecord) : <code>Array.&lt;string&gt;</code>
                * [.SectionObject](#module_uci.cursor.SectionObject) : <code>Object.&lt;string, (boolean\|number\|string\|Array.&lt;string&gt;)&gt;</code>
                * [.SectionCallback](#module_uci.cursor.SectionCallback) : <code>function</code>
        * [.cursor](#module_uci.cursor)
            * _instance_
                * [.load(config)](#module_uci.cursor+load) ⇒ <code>boolean</code>
                * [.unload(config)](#module_uci.cursor+unload) ⇒ <code>boolean</code>
                * [.get(config, section, [option])](#module_uci.cursor+get) ⇒ <code>string</code> \| <code>Array.&lt;string&gt;</code>
                * [.get_all(config, [section])](#module_uci.cursor+get_all) ⇒ <code>Object.&lt;string, module:uci.cursor.SectionObject&gt;</code> \| [<code>SectionObject</code>](#module_uci.cursor.SectionObject)
                * [.get_first(config, type, [option])](#module_uci.cursor+get_first) ⇒ <code>string</code> \| <code>Array.&lt;string&gt;</code>
                * [.add(config, type)](#module_uci.cursor+add) ⇒ <code>string</code>
                * [.set(config, section, option_or_type, [value])](#module_uci.cursor+set) ⇒ <code>boolean</code>
                * [.delete(config, section, [option])](#module_uci.cursor+delete) ⇒ <code>boolean</code>
                * [.list_append(config, section, option, value)](#module_uci.cursor+list_append) ⇒ <code>boolean</code>
                * [.list_remove(config, section, option, value)](#module_uci.cursor+list_remove) ⇒ <code>boolean</code>
                * [.rename(config, section, option_or_name, [name])](#module_uci.cursor+rename) ⇒ <code>boolean</code>
                * [.reorder(config, section, index)](#module_uci.cursor+reorder) ⇒ <code>boolean</code>
                * [.save([config])](#module_uci.cursor+save) ⇒ <code>boolean</code>
                * [.commit([config])](#module_uci.cursor+commit) ⇒ <code>boolean</code>
                * [.revert([config])](#module_uci.cursor+revert) ⇒ <code>boolean</code>
                * [.changes([config])](#module_uci.cursor+changes) ⇒ <code>Object.&lt;string, Array.&lt;module:uci.cursor.ChangeRecord&gt;&gt;</code>
                * [.foreach(config, type, callback)](#module_uci.cursor+foreach) ⇒ <code>boolean</code>
                * [.configs()](#module_uci.cursor+configs) ⇒ <code>Array.&lt;string&gt;</code>
                * [.load(config)](#module_uci.cursor+load) ⇒ <code>boolean</code>
                * [.unload(config)](#module_uci.cursor+unload) ⇒ <code>boolean</code>
                * [.get(config, section, [option])](#module_uci.cursor+get) ⇒ <code>string</code> \| <code>Array.&lt;string&gt;</code>
                * [.get_all(config, [section])](#module_uci.cursor+get_all) ⇒ <code>Object.&lt;string, module:uci.cursor.SectionObject&gt;</code> \| [<code>SectionObject</code>](#module_uci.cursor.SectionObject)
                * [.get_first(config, type, [option])](#module_uci.cursor+get_first) ⇒ <code>string</code> \| <code>Array.&lt;string&gt;</code>
                * [.add(config, type)](#module_uci.cursor+add) ⇒ <code>string</code>
                * [.set(config, section, option_or_type, [value])](#module_uci.cursor+set) ⇒ <code>boolean</code>
                * [.delete(config, section, [option])](#module_uci.cursor+delete) ⇒ <code>boolean</code>
                * [.list_append(config, section, option, value)](#module_uci.cursor+list_append) ⇒ <code>boolean</code>
                * [.list_remove(config, section, option, value)](#module_uci.cursor+list_remove) ⇒ <code>boolean</code>
                * [.rename(config, section, option_or_name, [name])](#module_uci.cursor+rename) ⇒ <code>boolean</code>
                * [.reorder(config, section, index)](#module_uci.cursor+reorder) ⇒ <code>boolean</code>
                * [.save([config])](#module_uci.cursor+save) ⇒ <code>boolean</code>
                * [.commit([config])](#module_uci.cursor+commit) ⇒ <code>boolean</code>
                * [.revert([config])](#module_uci.cursor+revert) ⇒ <code>boolean</code>
                * [.changes([config])](#module_uci.cursor+changes) ⇒ <code>Object.&lt;string, Array.&lt;module:uci.cursor.ChangeRecord&gt;&gt;</code>
                * [.foreach(config, type, callback)](#module_uci.cursor+foreach) ⇒ <code>boolean</code>
                * [.configs()](#module_uci.cursor+configs) ⇒ <code>Array.&lt;string&gt;</code>
                * [.error()](#module_uci.cursor+error) ⇒ <code>string</code>
                * [.error()](#module_uci.cursor+error) ⇒ <code>string</code>
                * [.error()](#module_uci.cursor+error) ⇒ <code>string</code>
                * [.error()](#module_uci.cursor+error) ⇒ <code>string</code>
            * _static_
                * [.ParserFlags](#module_uci.cursor.ParserFlags) : <code>Object</code>
                * [.ChangeRecord](#module_uci.cursor.ChangeRecord) : <code>Array.&lt;string&gt;</code>
                * [.SectionObject](#module_uci.cursor.SectionObject) : <code>Object.&lt;string, (boolean\|number\|string\|Array.&lt;string&gt;)&gt;</code>
                * [.SectionCallback](#module_uci.cursor.SectionCallback) : <code>function</code>
                * [.ParserFlags](#module_uci.cursor.ParserFlags) : <code>Object</code>
                * [.ChangeRecord](#module_uci.cursor.ChangeRecord) : <code>Array.&lt;string&gt;</code>
                * [.SectionObject](#module_uci.cursor.SectionObject) : <code>Object.&lt;string, (boolean\|number\|string\|Array.&lt;string&gt;)&gt;</code>
                * [.SectionCallback](#module_uci.cursor.SectionCallback) : <code>function</code>

<a name="module_uci+error"></a>

### uci.error() ⇒ <code>string</code>
<p>Query error information.</p>
<p>Returns a string containing a description of the last occurred error or
<code>null</code> if there is no error information.</p>

**Kind**: instance method of [<code>uci</code>](#module_uci)  
**Example**  
```js
// Trigger error
const ctx = cursor();
ctx.set("not_existing_config", "test", "1");

// Print error (should yield "Entry not found")
print(ctx.error(), "\n");
```
<a name="module_uci+cursor"></a>

### uci.cursor([config_dir], [delta_dir], [config2_dir], Parser) ⇒ [<code>cursor</code>](#module_uci.cursor)
<p>Instantiate uci cursor.</p>
<p>A uci cursor is a context for interacting with uci configuration files. It's
purpose is to cache and hold changes made to loaded configuration states
until those changes are written out to disk or discared.</p>
<p>Unsaved and uncommitted changes in a cursor instance are private and not
visible to other cursor instances instantiated by the same program or other
processes on the system.</p>
<p>Returns the instantiated cursor on success.</p>
<p>Returns <code>null</code> on error, e.g. if an invalid path argument was provided.</p>

**Kind**: instance method of [<code>uci</code>](#module_uci)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [config_dir] | <code>string</code> | <code>&quot;/etc/config&quot;</code> | <p>The directory to search for configuration files. It defaults to the well known uci configuration directory <code>/etc/config</code> but may be set to a different path for special purpose applications.</p> |
| [delta_dir] | <code>string</code> | <code>&quot;/tmp/.uci&quot;</code> | <p>The directory to save delta records in. It defaults to the well known <code>/tmp/.uci</code> path which is used as default by the uci command line tool.</p> <p>By changing this path to a different location, it is possible to isolate uncommitted application changes from the uci cli or other processes on the system.</p> |
| [config2_dir] | <code>string</code> | <code>&quot;/var/run/uci&quot;</code> | <p>The directory to keep override config files in. Files are in the same format as in config_dir, but can individually override ones from that directory. It defaults to the uci configuration directory <code>/var/run/uci</code> but may be set to a different path for special purpose applications, or even disabled by setting this parameter to an empty string.</p> |
| Parser | [<code>ParserFlags</code>](#module_uci.cursor.ParserFlags) |  | <p>flags to change.</p> |

<a name="module_uci+error"></a>

### uci.error() ⇒ <code>string</code>
<p>Query error information.</p>
<p>Returns a string containing a description of the last occurred error or
<code>null</code> if there is no error information.</p>

**Kind**: instance method of [<code>uci</code>](#module_uci)  
**Example**  
```js
// Trigger error
const ctx = cursor();
ctx.set("not_existing_config", "test", "1");

// Print error (should yield "Entry not found")
print(ctx.error(), "\n");
```
<a name="module_uci+cursor"></a>

### uci.cursor([config_dir], [delta_dir], [config2_dir], Parser) ⇒ [<code>cursor</code>](#module_uci.cursor)
<p>Instantiate uci cursor.</p>
<p>A uci cursor is a context for interacting with uci configuration files. It's
purpose is to cache and hold changes made to loaded configuration states
until those changes are written out to disk or discared.</p>
<p>Unsaved and uncommitted changes in a cursor instance are private and not
visible to other cursor instances instantiated by the same program or other
processes on the system.</p>
<p>Returns the instantiated cursor on success.</p>
<p>Returns <code>null</code> on error, e.g. if an invalid path argument was provided.</p>

**Kind**: instance method of [<code>uci</code>](#module_uci)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [config_dir] | <code>string</code> | <code>&quot;/etc/config&quot;</code> | <p>The directory to search for configuration files. It defaults to the well known uci configuration directory <code>/etc/config</code> but may be set to a different path for special purpose applications.</p> |
| [delta_dir] | <code>string</code> | <code>&quot;/tmp/.uci&quot;</code> | <p>The directory to save delta records in. It defaults to the well known <code>/tmp/.uci</code> path which is used as default by the uci command line tool.</p> <p>By changing this path to a different location, it is possible to isolate uncommitted application changes from the uci cli or other processes on the system.</p> |
| [config2_dir] | <code>string</code> | <code>&quot;/var/run/uci&quot;</code> | <p>The directory to keep override config files in. Files are in the same format as in config_dir, but can individually override ones from that directory. It defaults to the uci configuration directory <code>/var/run/uci</code> but may be set to a different path for special purpose applications, or even disabled by setting this parameter to an empty string.</p> |
| Parser | [<code>ParserFlags</code>](#module_uci.cursor.ParserFlags) |  | <p>flags to change.</p> |

<a name="module_uci.cursor"></a>

### uci.cursor
**Kind**: static class of [<code>uci</code>](#module_uci)  
**See**: [cursor()](#module_uci+cursor)  

* [.cursor](#module_uci.cursor)
    * _instance_
        * [.load(config)](#module_uci.cursor+load) ⇒ <code>boolean</code>
        * [.unload(config)](#module_uci.cursor+unload) ⇒ <code>boolean</code>
        * [.get(config, section, [option])](#module_uci.cursor+get) ⇒ <code>string</code> \| <code>Array.&lt;string&gt;</code>
        * [.get_all(config, [section])](#module_uci.cursor+get_all) ⇒ <code>Object.&lt;string, module:uci.cursor.SectionObject&gt;</code> \| [<code>SectionObject</code>](#module_uci.cursor.SectionObject)
        * [.get_first(config, type, [option])](#module_uci.cursor+get_first) ⇒ <code>string</code> \| <code>Array.&lt;string&gt;</code>
        * [.add(config, type)](#module_uci.cursor+add) ⇒ <code>string</code>
        * [.set(config, section, option_or_type, [value])](#module_uci.cursor+set) ⇒ <code>boolean</code>
        * [.delete(config, section, [option])](#module_uci.cursor+delete) ⇒ <code>boolean</code>
        * [.list_append(config, section, option, value)](#module_uci.cursor+list_append) ⇒ <code>boolean</code>
        * [.list_remove(config, section, option, value)](#module_uci.cursor+list_remove) ⇒ <code>boolean</code>
        * [.rename(config, section, option_or_name, [name])](#module_uci.cursor+rename) ⇒ <code>boolean</code>
        * [.reorder(config, section, index)](#module_uci.cursor+reorder) ⇒ <code>boolean</code>
        * [.save([config])](#module_uci.cursor+save) ⇒ <code>boolean</code>
        * [.commit([config])](#module_uci.cursor+commit) ⇒ <code>boolean</code>
        * [.revert([config])](#module_uci.cursor+revert) ⇒ <code>boolean</code>
        * [.changes([config])](#module_uci.cursor+changes) ⇒ <code>Object.&lt;string, Array.&lt;module:uci.cursor.ChangeRecord&gt;&gt;</code>
        * [.foreach(config, type, callback)](#module_uci.cursor+foreach) ⇒ <code>boolean</code>
        * [.configs()](#module_uci.cursor+configs) ⇒ <code>Array.&lt;string&gt;</code>
        * [.load(config)](#module_uci.cursor+load) ⇒ <code>boolean</code>
        * [.unload(config)](#module_uci.cursor+unload) ⇒ <code>boolean</code>
        * [.get(config, section, [option])](#module_uci.cursor+get) ⇒ <code>string</code> \| <code>Array.&lt;string&gt;</code>
        * [.get_all(config, [section])](#module_uci.cursor+get_all) ⇒ <code>Object.&lt;string, module:uci.cursor.SectionObject&gt;</code> \| [<code>SectionObject</code>](#module_uci.cursor.SectionObject)
        * [.get_first(config, type, [option])](#module_uci.cursor+get_first) ⇒ <code>string</code> \| <code>Array.&lt;string&gt;</code>
        * [.add(config, type)](#module_uci.cursor+add) ⇒ <code>string</code>
        * [.set(config, section, option_or_type, [value])](#module_uci.cursor+set) ⇒ <code>boolean</code>
        * [.delete(config, section, [option])](#module_uci.cursor+delete) ⇒ <code>boolean</code>
        * [.list_append(config, section, option, value)](#module_uci.cursor+list_append) ⇒ <code>boolean</code>
        * [.list_remove(config, section, option, value)](#module_uci.cursor+list_remove) ⇒ <code>boolean</code>
        * [.rename(config, section, option_or_name, [name])](#module_uci.cursor+rename) ⇒ <code>boolean</code>
        * [.reorder(config, section, index)](#module_uci.cursor+reorder) ⇒ <code>boolean</code>
        * [.save([config])](#module_uci.cursor+save) ⇒ <code>boolean</code>
        * [.commit([config])](#module_uci.cursor+commit) ⇒ <code>boolean</code>
        * [.revert([config])](#module_uci.cursor+revert) ⇒ <code>boolean</code>
        * [.changes([config])](#module_uci.cursor+changes) ⇒ <code>Object.&lt;string, Array.&lt;module:uci.cursor.ChangeRecord&gt;&gt;</code>
        * [.foreach(config, type, callback)](#module_uci.cursor+foreach) ⇒ <code>boolean</code>
        * [.configs()](#module_uci.cursor+configs) ⇒ <code>Array.&lt;string&gt;</code>
        * [.error()](#module_uci.cursor+error) ⇒ <code>string</code>
        * [.error()](#module_uci.cursor+error) ⇒ <code>string</code>
        * [.error()](#module_uci.cursor+error) ⇒ <code>string</code>
        * [.error()](#module_uci.cursor+error) ⇒ <code>string</code>
    * _static_
        * [.ParserFlags](#module_uci.cursor.ParserFlags) : <code>Object</code>
        * [.ChangeRecord](#module_uci.cursor.ChangeRecord) : <code>Array.&lt;string&gt;</code>
        * [.SectionObject](#module_uci.cursor.SectionObject) : <code>Object.&lt;string, (boolean\|number\|string\|Array.&lt;string&gt;)&gt;</code>
        * [.SectionCallback](#module_uci.cursor.SectionCallback) : <code>function</code>
        * [.ParserFlags](#module_uci.cursor.ParserFlags) : <code>Object</code>
        * [.ChangeRecord](#module_uci.cursor.ChangeRecord) : <code>Array.&lt;string&gt;</code>
        * [.SectionObject](#module_uci.cursor.SectionObject) : <code>Object.&lt;string, (boolean\|number\|string\|Array.&lt;string&gt;)&gt;</code>
        * [.SectionCallback](#module_uci.cursor.SectionCallback) : <code>function</code>

<a name="module_uci.cursor+load"></a>

#### cursor.load(config) ⇒ <code>boolean</code>
<p>Explicitly reload configuration file.</p>
<p>Usually, any attempt to query or modify a value within a given configuration
will implicitly load the underlying file into memory. By invoking <code>load()</code>
explicitly, a potentially loaded stale configuration is discarded and
reloaded from the file system, ensuring that the latest state is reflected in
the cursor.</p>
<p>Returns <code>true</code> if the configuration was successfully loaded.</p>
<p>Returns <code>null</code> on error, e.g. if the requested configuration does not exist.</p>

**Kind**: instance method of [<code>cursor</code>](#module_uci.cursor)  

| Param | Type | Description |
| --- | --- | --- |
| config | <code>string</code> | <p>The name


---

<a id="ucode-module-uloop"></a>
# ucode module: `uloop`

> **Source:** [`lib/uloop.c`](https://github.com/jow-/ucode/blob/master/lib/uloop.c)
> **Live docs:** https://ucode.mein.io/module-uloop.html
> **Generated:** 2026-03-04 13:26 UTC from commit `e87be9d`

---

## Modules

<dl>
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

<a name="module_uloop"></a>

## uloop
<h1 id="openwrt-uloop-event-loop">OpenWrt uloop event loop</h1>
<p>The <code>uloop</code> binding provides functions for integrating with the OpenWrt
[uloop library](https://github.com/openwrt/libubox/blob/master/uloop.h).</p>
<p>Functions can be individually imported and directly accessed using the
[named import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#named_import)
syntax:</p>
<pre class="prettyprint source lang-javascript"><code>import { init, handle, timer, interval, process, signal, task, run } from 'uloop';

init();

handle(…);
timer(…);
interval(…);
process(…);
signal(…);
task(…);

run();
</code></pre>
<p>Alternatively, the module namespace can be imported using a wildcard import
statement:</p>
<pre class="prettyprint source lang-javascript"><code>import * as uloop from 'uloop';

uloop.init();

uloop.handle(…);
uloop.timer(…);
uloop.interval(…);
uloop.process(…);
uloop.signal(…);
uloop.task(…);

uloop.run();
</code></pre>
<p>Additionally, the uloop binding namespace may also be imported by invoking
the <code>ucode</code> interpreter with the <code>-luloop</code> switch.</p>


* [uloop](#module_uloop)
    * _instance_
        * [.error()](#module_uloop+error) ⇒ <code>string</code>
        * [.init()](#module_uloop+init) ⇒ <code>boolean</code>
        * [.run([timeout])](#module_uloop+run) ⇒ <code>number</code>
        * [.cancelling()](#module_uloop+cancelling) ⇒ <code>boolean</code>
        * [.running()](#module_uloop+running) ⇒ <code>boolean</code>
        * [.end()](#module_uloop+end) ⇒ <code>void</code>
        * [.done()](#module_uloop+done) ⇒ <code>void</code>
        * [.timer([timeout], callback)](#module_uloop+timer) ⇒ [<code>timer</code>](#module_uloop.timer)
        * [.handle(handle, callback, events)](#module_uloop+handle) ⇒ [<code>handle</code>](#module_uloop.handle)
        * [.process(executable, [args], [env], callback)](#module_uloop+process) ⇒ [<code>process</code>](#module_uloop.process)
        * [.task(taskFunction, [outputCallback], [inputCallback])](#module_uloop+task) ⇒ [<code>task</code>](#module_uloop.task)
        * [.interval([timeout], callback)](#module_uloop+interval) ⇒ [<code>interval</code>](#module_uloop.interval)
        * [.signal(signal, callback)](#module_uloop+signal) ⇒ [<code>signal</code>](#module_uloop.signal)
        * [.error()](#module_uloop+error) ⇒ <code>string</code>
        * [.init()](#module_uloop+init) ⇒ <code>boolean</code>
        * [.run([timeout])](#module_uloop+run) ⇒ <code>number</code>
        * [.cancelling()](#module_uloop+cancelling) ⇒ <code>boolean</code>
        * [.running()](#module_uloop+running) ⇒ <code>boolean</code>
        * [.end()](#module_uloop+end) ⇒ <code>void</code>
        * [.done()](#module_uloop+done) ⇒ <code>void</code>
        * [.timer([timeout], callback)](#module_uloop+timer) ⇒ [<code>timer</code>](#module_uloop.timer)
        * [.handle(handle, callback, events)](#module_uloop+handle) ⇒ [<code>handle</code>](#module_uloop.handle)
        * [.process(executable, [args], [env], callback)](#module_uloop+process) ⇒ [<code>process</code>](#module_uloop.process)
        * [.task(taskFunction, [outputCallback], [inputCallback])](#module_uloop+task) ⇒ [<code>task</code>](#module_uloop.task)
        * [.interval([timeout], callback)](#module_uloop+interval) ⇒ [<code>interval</code>](#module_uloop.interval)
        * [.signal(signal, callback)](#module_uloop+signal) ⇒ [<code>signal</code>](#module_uloop.signal)
    * _static_
        * [.timer](#module_uloop.timer)
            * [.set([timeout])](#module_uloop.timer+set) ⇒ <code>boolean</code>
            * [.remaining()](#module_uloop.timer+remaining) ⇒ <code>number</code>
            * [.cancel()](#module_uloop.timer+cancel) ⇒ <code>boolean</code>
            * [.set([timeout])](#module_uloop.timer+set) ⇒ <code>boolean</code>
            * [.remaining()](#module_uloop.timer+remaining) ⇒ <code>number</code>
            * [.cancel()](#module_uloop.timer+cancel) ⇒ <code>boolean</code>
        * [.handle](#module_uloop.handle)
            * [.fileno()](#module_uloop.handle+fileno) ⇒ <code>number</code>
            * [.handle()](#module_uloop.handle+handle) ⇒ [<code>file</code>](#module_fs.file) \| [<code>proc</code>](#module_fs.proc) \| [<code>socket</code>](#module_socket.socket)
            * [.delete()](#module_uloop.handle+delete) ⇒ <code>void</code>
            * [.fileno()](#module_uloop.handle+fileno) ⇒ <code>number</code>
            * [.handle()](#module_uloop.handle+handle) ⇒ [<code>file</code>](#module_fs.file) \| [<code>proc</code>](#module_fs.proc) \| [<code>socket</code>](#module_socket.socket)
            * [.delete()](#module_uloop.handle+delete) ⇒ <code>void</code>
        * [.process](#module_uloop.process)
            * [.pid()](#module_uloop.process+pid) ⇒ <code>number</code>
            * [.delete()](#module_uloop.process+delete) ⇒ <code>boolean</code>
            * [.pid()](#module_uloop.process+pid) ⇒ <code>number</code>
            * [.delete()](#module_uloop.process+delete) ⇒ <code>boolean</code>
        * [.pipe](#module_uloop.pipe)
            * [.send(msg)](#module_uloop.pipe+send) ⇒ <code>boolean</code>
            * [.receive()](#module_uloop.pipe+receive) ⇒ <code>\*</code>
            * [.sending()](#module_uloop.pipe+sending) ⇒ <code>boolean</code>
            * [.receiving()](#module_uloop.pipe+receiving) ⇒ <code>boolean</code>
            * [.send(msg)](#module_uloop.pipe+send) ⇒ <code>boolean</code>
            * [.receive()](#module_uloop.pipe+receive) ⇒ <code>\*</code>
            * [.sending()](#module_uloop.pipe+sending) ⇒ <code>boolean</code>
            * [.receiving()](#module_uloop.pipe+receiving) ⇒ <code>boolean</code>
        * [.task](#module_uloop.task)
            * [.pid()](#module_uloop.task+pid) ⇒ <code>number</code>
            * [.kill()](#module_uloop.task+kill) ⇒ <code>boolean</code>
            * [.finished()](#module_uloop.task+finished) ⇒ <code>boolean</code>
            * [.pid()](#module_uloop.task+pid) ⇒ <code>number</code>
            * [.kill()](#module_uloop.task+kill) ⇒ <code>boolean</code>
            * [.finished()](#module_uloop.task+finished) ⇒ <code>boolean</code>
        * [.interval](#module_uloop.interval)
            * [.set([interval])](#module_uloop.interval+set) ⇒ <code>boolean</code>
            * [.remaining()](#module_uloop.interval+remaining) ⇒ <code>number</code>
            * [.expirations()](#module_uloop.interval+expirations) ⇒ <code>number</code>
            * [.cancel()](#module_uloop.interval+cancel) ⇒ <code>boolean</code>
            * [.set([interval])](#module_uloop.interval+set) ⇒ <code>boolean</code>
            * [.remaining()](#module_uloop.interval+remaining) ⇒ <code>number</code>
            * [.expirations()](#module_uloop.interval+expirations) ⇒ <code>number</code>
            * [.cancel()](#module_uloop.interval+cancel) ⇒ <code>boolean</code>
        * [.signal](#module_uloop.signal)
            * [.signo()](#module_uloop.signal+signo) ⇒ <code>number</code>
            * [.delete()](#module_uloop.signal+delete) ⇒ <code>boolean</code>
            * [.signo()](#module_uloop.signal+signo) ⇒ <code>number</code>
            * [.delete()](#module_uloop.signal+delete) ⇒ <code>boolean</code>
        * [.timer](#module_uloop.timer)
            * [.set([timeout])](#module_uloop.timer+set) ⇒ <code>boolean</code>
            * [.remaining()](#module_uloop.timer+remaining) ⇒ <code>number</code>
            * [.cancel()](#module_uloop.timer+cancel) ⇒ <code>boolean</code>
            * [.set([timeout])](#module_uloop.timer+set) ⇒ <code>boolean</code>
            * [.remaining()](#module_uloop.timer+remaining) ⇒ <code>number</code>
            * [.cancel()](#module_uloop.timer+cancel) ⇒ <code>boolean</code>
        * [.handle](#module_uloop.handle)
            * [.fileno()](#module_uloop.handle+fileno) ⇒ <code>number</code>
            * [.handle()](#module_uloop.handle+handle) ⇒ [<code>file</code>](#module_fs.file) \| [<code>proc</code>](#module_fs.proc) \| [<code>socket</code>](#module_socket.socket)
            * [.delete()](#module_uloop.handle+delete) ⇒ <code>void</code>
            * [.fileno()](#module_uloop.handle+fileno) ⇒ <code>number</code>
            * [.handle()](#module_uloop.handle+handle) ⇒ [<code>file</code>](#module_fs.file) \| [<code>proc</code>](#module_fs.proc) \| [<code>socket</code>](#module_socket.socket)
            * [.delete()](#module_uloop.handle+delete) ⇒ <code>void</code>
        * [.process](#module_uloop.process)
            * [.pid()](#module_uloop.process+pid) ⇒ <code>number</code>
            * [.delete()](#module_uloop.process+delete) ⇒ <code>boolean</code>
            * [.pid()](#module_uloop.process+pid) ⇒ <code>number</code>
            * [.delete()](#module_uloop.process+delete) ⇒ <code>boolean</code>
        * [.pipe](#module_uloop.pipe)
            * [.send(msg)](#module_uloop.pipe+send) ⇒ <code>boolean</code>
            * [.receive()](#module_uloop.pipe+receive) ⇒ <code>\*</code>
            * [.sending()](#module_uloop.pipe+sending) ⇒ <code>boolean</code>
            * [.receiving()](#module_uloop.pipe+receiving) ⇒ <code>boolean</code>
            * [.send(msg)](#module_uloop.pipe+send) ⇒ <code>boolean</code>
            * [.receive()](#module_uloop.pipe+receive) ⇒ <code>\*</code>
            * [.sending()](#module_uloop.pipe+sending) ⇒ <code>boolean</code>
            * [.receiving()](#module_uloop.pipe+receiving) ⇒ <code>boolean</code>
        * [.task](#module_uloop.task)
            * [.pid()](#module_uloop.task+pid) ⇒ <code>number</code>
            * [.kill()](#module_uloop.task+kill) ⇒ <code>boolean</code>
            * [.finished()](#module_uloop.task+finished) ⇒ <code>boolean</code>
            * [.pid()](#module_uloop.task+pid) ⇒ <code>number</code>
            * [.kill()](#module_uloop.task+kill) ⇒ <code>boolean</code>
            * [.finished()](#module_uloop.task+finished) ⇒ <code>boolean</code>
        * [.interval](#module_uloop.interval)
            * [.set([interval])](#module_uloop.interval+set) ⇒ <code>boolean</code>
            * [.remaining()](#module_uloop.interval+remaining) ⇒ <code>number</code>
            * [.expirations()](#module_uloop.interval+expirations) ⇒ <code>number</code>
            * [.cancel()](#module_uloop.interval+cancel) ⇒ <code>boolean</code>
            * [.set([interval])](#module_uloop.interval+set) ⇒ <code>boolean</code>
            * [.remaining()](#module_uloop.interval+remaining) ⇒ <code>number</code>
            * [.expirations()](#module_uloop.interval+expirations) ⇒ <code>number</code>
            * [.cancel()](#module_uloop.interval+cancel) ⇒ <code>boolean</code>
        * [.signal](#module_uloop.signal)
            * [.signo()](#module_uloop.signal+signo) ⇒ <code>number</code>
            * [.delete()](#module_uloop.signal+delete) ⇒ <code>boolean</code>
            * [.signo()](#module_uloop.signal+signo) ⇒ <code>number</code>
            * [.delete()](#module_uloop.signal+delete) ⇒ <code>boolean</code>
    * _inner_
        * [~Event Mode Constants](#module_uloop..Event Mode Constants)
        * [~Event Mode Constants](#module_uloop..Event Mode Constants)

<a name="module_uloop+error"></a>

### uloop.error() ⇒ <code>string</code>
<p>Retrieves the last error message.</p>
<p>This function retrieves the last error message generated by the uloop event loop.
If no error occurred, it returns <code>null</code>.</p>

**Kind**: instance method of [<code>uloop</code>](#module_uloop)  
**Returns**: <code>string</code> - <p>Returns the last error message as a string, or <code>null</code> if no error occurred.</p>  
**Example**  
```js
// Retrieve the last error message
const errorMessage = uloop.error();

if (errorMessage)
    printf(`Error message: ${errorMessage}\n`);
else
    printf("No error occurred\n");
```
<a name="module_uloop+init"></a>

### uloop.init() ⇒ <code>boolean</code>
<p>Initializes the uloop event loop.</p>
<p>This function initializes the uloop event loop, allowing subsequent
usage of uloop functionalities. It takes no arguments.</p>
<p>Returns <code>true</code> on success.
Returns <code>null</code> if an error occurred during initialization.</p>

**Kind**: instance method of [<code>uloop</code>](#module_uloop)  
**Returns**: <code>boolean</code> - <p>Returns <code>true</code> on success, <code>null</code> on error.</p>  
**Example**  
```js
// Initialize the uloop event loop
const success = uloop.init();

if (success)
    printf("uloop event loop initialized successfully\n");
else
    die(`Initialization failure: ${uloop.error()}\n`);
```
<a name="module_uloop+run"></a>

### uloop.run([timeout]) ⇒ <code>number</code>
<p>Runs the uloop event loop.</p>
<p>This function starts running the uloop event loop, allowing it to handle
scheduled events and callbacks. If a timeout value is provided and is
non-negative, the event loop will run for that amount of milliseconds
before returning. If the timeout is omitted or negative, the event loop
runs indefinitely until explicitly stopped.</p>

**Kind**: instance method of [<code>uloop</code>](#module_uloop)  
**Returns**: <code>number</code> - <p>Returns a signal number or 0 on success, <code>null</code> on error.</p>  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [timeout] | <code>number</code> | <code>-1</code> | <p>Optional. The timeout value in milliseconds for running the event loop. Defaults to -1, indicating an indefinite run.</p> |

**Example**  
```js
// Run the uloop event loop indefinitely
const success = uloop.run();
if (rc == null)
    die(`Error occurred during uloop execution: ${uloop.error()}\n`);
else if (rc != 0)
    printf("uloop event loop was interrupted by a signal: %d\n", rc);

// Run the uloop event loop for 1000 milliseconds
const success = uloop.run(1000);
if (rc == null)
    die(`Error occurred during uloop execution: ${uloop.error()}\n`);
else if (rc != 0)
    printf("uloop event loop was interrupted by a signal: %d\n", rc);
```
<a name="module_uloop+cancelling"></a>

### uloop.cancelling() ⇒ <code>boolean</code>
<p>Checks if the uloop event loop is currently shutting down.</p>
<p>This function checks whether the uloop event loop is currently in the process
of shutting down.</p>

**Kind**: instance method of [<code>uloop</code>](#module_uloop)  
**Returns**: <code>boolean</code> - <p>Returns <code>true</code> if uloop is currently shutting down, <code>false</code> otherwise.</p>  
**Example**  
```js
// Check if the uloop event loop is shutting down
const shuttingDown = uloop.cancelling();
if (shuttingDown)
    printf("uloop event loop is currently shutting down\n");
else
    printf("uloop event loop is not shutting down\n");
```
<a name="module_uloop+running"></a>

### uloop.running() ⇒ <code>boolean</code>
<p>Checks if the uloop event loop is currently running.</p>
<p>This function checks whether the uloop event loop is currently started
and running.</p>

**Kind**: instance method of [<code>uloop</code>](#module_uloop)  
**Returns**: <code>boolean</code> - <p>Returns <code>true</code> if the event loop is currently running, <code>false</code> otherwise.</p>  
**Example**  
```js
// Check if the uloop event loop is running
const isRunning = uloop.running();
if (isRunning)
    printf("uloop event loop is currently running\n");
else
    printf("uloop event loop is not running\n");
```
<a name="module_uloop+end"></a>

### uloop.end() ⇒ <code>void</code>
<p>Halts the uloop event loop.</p>
<p>This function halts the uloop event loop, stopping its execution and
preventing further processing of scheduled events and callbacks.</p>
<p>Expired timeouts and already queued event callbacks are still run to
completion.</p>

**Kind**: instance method of [<code>uloop</code>](#module_uloop)  
**Returns**: <code>void</code> - <p>This function does not return any value.</p>  
**Example**  
```js
// Halt the uloop event loop
uloop.end();
```
<a name="module_uloop+done"></a>

### uloop.done() ⇒ <code>void</code>
<p>Stops the uloop event loop and cancels pending timeouts and events.</p>
<p>This function immediately stops the uloop event loop, cancels all pending
timeouts and events, unregisters all handles, and deallocates associated
resources.</p>

**Kind**: instance method of [<code>uloop</code>](#module_uloop)  
**Returns**: <code>void</code> - <p>This function does not return any value.</p>  
**Example**  
```js
// Stop the uloop event loop and clean up resources
uloop.done();
```
<a name="module_uloop+timer"></a>

### uloop.timer([timeout], callback) ⇒ [<code>timer</code>](#module_uloop.timer)
<p>Creates a timer instance for scheduling callbacks.</p>
<p>This function creates a timer instance for scheduling callbacks to be
executed after a specified timeout duration. It takes an optional timeout
parameter, which defaults to -1, indicating that the timer is initially not
armed and can be enabled later by invoking the <code>.set(timeout)</code> method on the
instance.</p>
<p>A callback function must be provided to be executed when the timer expires.</p>

**Kind**: instance method of [<code>uloop</code>](#module_uloop)  
**Returns**: [<code>timer</code>](#module_uloop.timer) - <p>Returns a timer instance for scheduling callbacks.
Returns <code>null</code> when the timeout or callback arguments are invalid.</p>  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [timeout] | <code>number</code> | <code>-1</code> | <p>Optional. The timeout duration in milliseconds. Defaults to -1, indicating the timer is not initially armed.</p> |
| callback | <code>function</code> |  | <p>The callback function to be executed when the timer expires.</p> |

**Example**  
```js
// Create a timer with a callback to be executed after 1000 milliseconds
const myTimer = uloop.timer(1000, () => {
    printf("Timer expired!\n");
});

// Later enable the timer with a timeout of 500 milliseconds
myTimer.set(500);
```
<a name="module_uloop+handle"></a>

### uloop.handle(handle, callback, events) ⇒ [<code>handle</code>](#module_uloop.handle)
<p>Creates a handle instance for monitoring file descriptor events.</p>
<p>This function creates a handle instance for monitoring events on a file
descriptor, file, or socket. It takes the file or socket handle, a callback
function to be invoked when the specified IO events occur, and bitwise OR-ed
flags of IO events (<code>ULOOP_READ</code>, <code>ULOOP_WRITE</code>) that the callback should be
invoked for.</p>

**Kind**: instance method of [<code>uloop</code>](#module_uloop)  
**Returns**: [<code>handle</code>](#module_uloop.handle) - <p>Returns a handle instance for monitoring file descriptor events.
Returns <code>null</code> when the handle, callback or signal arguments are invalid.</p>  

| Param | Type | Description |
| --- | --- | --- |
| handle | <code>number</code> \| [<code>file</code>](#module_fs.file) \| [<code>proc</code>](#module_fs.proc) \| [<code>socket</code>](#module_socket.socket) \| [<code>handle</code>](#module_io.handle) | <p>The file handle (descriptor number, file or socket instance).</p> |
| callback | <code>function</code> | <p>The callback function to be invoked when the specified IO events occur.</p> |
| events | <code>number</code> | <p>Bitwise OR-ed flags of IO events (<code>ULOOP_READ</code>, <code>ULOOP_WRITE</code>) that the callback should be invoked for.</p> |

**Example**  
```js
// Create a handle for monitoring read events on file descriptor 3
const myHandle = uloop.handle(3, (events) => {
    if (events & ULOOP_READ)
        printf("Read event occurred!\n");
}, uloop.ULOOP_READ);

// Check socket for writability
const sock = socket.connect("example.org", 80);
uloop.handle(sock, (events) => {
    sock.send("GET / HTTP/1.0\r\n\r\n");
}, uloop.ULOOP_WRITE)
```
<a name="module_uloop+process"></a>

### uloop.process(executable, [args], [env], callback) ⇒ [<code>process</code>](#module_uloop.process)
<p>Creates a process instance for executing external programs.</p>
<p>This function creates a process instance for executing external programs.
It takes the executable path string, an optional string array as the argument
vector, an optional dictionary describing environment variables, and a
callback function to be invoked when the invoked process ends.</p>

**Kind**: instance method of [<code>uloop</code>](#module_uloop)  
**Returns**: [<code>process</code>](#module_uloop.process) - <p>Returns a process instance for executing external programs.
Returns <code>null</code> on error, e.g. due to <code>exec()</code> failure or invalid arguments.</p>  

| Param | Type | Description |
| --- | --- | --- |
| executable | <code>string</code> | <p>The path to the executable program.</p> |
| [args] | <code>Array.&lt;string&gt;</code> | <p>Optional. An array of strings representing the arguments passed to the executable.</p> |
| [env] | <code>Object.&lt;string, \*&gt;</code> | <p>Optional. A dictionary describing environment variables for the process.</p> |
| callback | <code>function</code> | <p>The callback function to be invoked when the invoked process ends.</p> |

**Example**  
```js
// Create a process instance for executing 'ls' command
const myProcess = uloop.process("/bin/ls", ["-l", "/tmp"], null, (code) => {
    printf(`Process exited with code ${code}\n`);
});
```
<a name="module_uloop+task"></a>

### uloop.task(taskFunction, [outputCallback], [inputCallback]) ⇒ [<code>task</code>](#module_uloop.task)
<p>Creates a task instance for executing background tasks.</p>
<p>This function creates a task instance for executing background tasks.
It takes the task function to be invoked as a background process,
an optional output callback function to be invoked when output is received
from the task, and an optional input callback function to be invoked
when input is required by the task.</p>

**Kind**: instance method of [<code>uloop</code>](#module_uloop)  
**Returns**: [<code>task</code>](#module_uloop.task) - <p>Returns a task instance for executing background tasks.
Returns <code>null</code> on error, e.g. due to fork failure or invalid arguments.</p>  

| Param | Type | Description |
| --- | --- | --- |
| taskFunction | <code>function</code> | <p>The task function to be invoked as a background process.</p> |
| [outputCallback] | <code>function</code> | <p>Optional. The output callback function to be invoked when output is received from the task. It is invoked with the output data as the argument.</p> |
| [inputCallback] | <code>function</code> | <p>Optional. The input callback function to be invoked when input is required by the task. It is invoked with a function to send input to the task as the argument.</p> |

**Example**  
```js
// Create a task instance for executing a background task
const myTask = uloop.task(
    (pipe) => {
        // Task logic
        pipe.send("Hello from the task\n");
        const input = pipe.receive();
        printf(`Received input from main thread: ${input}\n`);
    },
 


---

<a id="ucode-module-zlib"></a>
# ucode module: `zlib`

> **Source:** [`lib/zlib.c`](https://github.com/jow-/ucode/blob/master/lib/zlib.c)
> **Live docs:** https://ucode.mein.io/module-zlib.html
> **Generated:** 2026-03-04 13:26 UTC from commit `e87be9d`

---

## Modules

<dl>
<dt><a href="#module_zlib">zlib</a></dt>
<dd><h1 id="zlib-bindings">Zlib bindings</h1>
<p>The <code>zlib</code> module provides single-call and stream-oriented functions for interacting with zlib data.</p></dd>
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

<a name="module_zlib"></a>

## zlib
<h1 id="zlib-bindings">Zlib bindings</h1>
<p>The <code>zlib</code> module provides single-call and stream-oriented functions for interacting with zlib data.</p>


* [zlib](#module_zlib)
    * _instance_
        * [.deflate(str_or_resource, [gzip], [level])](#module_zlib+deflate) ⇒ <code>string</code>
        * [.inflate(str_or_resource)](#module_zlib+inflate) ⇒ <code>string</code>
        * [.deflater([gzip], [level])](#module_zlib+deflater) ⇒ [<code>deflate</code>](#module_zlib.deflate)
        * [.inflater()](#module_zlib+inflater) ⇒ [<code>inflate</code>](#module_zlib.inflate)
        * [.deflate(str_or_resource, [gzip], [level])](#module_zlib+deflate) ⇒ <code>string</code>
        * [.inflate(str_or_resource)](#module_zlib+inflate) ⇒ <code>string</code>
        * [.deflater([gzip], [level])](#module_zlib+deflater) ⇒ [<code>deflate</code>](#module_zlib.deflate)
        * [.inflater()](#module_zlib+inflater) ⇒ [<code>inflate</code>](#module_zlib.inflate)
    * _static_
        * [.deflate](#module_zlib.deflate)
            * [.write(src, [flush])](#module_zlib.deflate+write) ⇒ <code>boolean</code>
            * [.read()](#module_zlib.deflate+read) ⇒ <code>string</code>
            * [.error()](#module_zlib.deflate+error) ⇒ <code>string</code>
            * [.write(src, [flush])](#module_zlib.deflate+write) ⇒ <code>boolean</code>
            * [.read()](#module_zlib.deflate+read) ⇒ <code>string</code>
            * [.error()](#module_zlib.deflate+error) ⇒ <code>string</code>
        * [.inflate](#module_zlib.inflate)
            * [.write(src, [flush])](#module_zlib.inflate+write) ⇒ <code>boolean</code>
            * [.read()](#module_zlib.inflate+read) ⇒ <code>string</code>
            * [.write(src, [flush])](#module_zlib.inflate+write) ⇒ <code>boolean</code>
            * [.read()](#module_zlib.inflate+read) ⇒ <code>string</code>
            * [.error()](#module_zlib.inflate+error) ⇒ <code>string</code>
            * [.error()](#module_zlib.inflate+error) ⇒ <code>string</code>
            * [.error()](#module_zlib.inflate+error) ⇒ <code>string</code>
            * [.error()](#module_zlib.inflate+error) ⇒ <code>string</code>
        * [.deflate](#module_zlib.deflate)
            * [.write(src, [flush])](#module_zlib.deflate+write) ⇒ <code>boolean</code>
            * [.read()](#module_zlib.deflate+read) ⇒ <code>string</code>
            * [.error()](#module_zlib.deflate+error) ⇒ <code>string</code>
            * [.write(src, [flush])](#module_zlib.deflate+write) ⇒ <code>boolean</code>
            * [.read()](#module_zlib.deflate+read) ⇒ <code>string</code>
            * [.error()](#module_zlib.deflate+error) ⇒ <code>string</code>
        * [.inflate](#module_zlib.inflate)
            * [.write(src, [flush])](#module_zlib.inflate+write) ⇒ <code>boolean</code>
            * [.read()](#module_zlib.inflate+read) ⇒ <code>string</code>
            * [.write(src, [flush])](#module_zlib.inflate+write) ⇒ <code>boolean</code>
            * [.read()](#module_zlib.inflate+read) ⇒ <code>string</code>
            * [.error()](#module_zlib.inflate+error) ⇒ <code>string</code>
            * [.error()](#module_zlib.inflate+error) ⇒ <code>string</code>
            * [.error()](#module_zlib.inflate+error) ⇒ <code>string</code>
            * [.error()](#module_zlib.inflate+error) ⇒ <code>string</code>
    * _inner_
        * [~Compression levels](#module_zlib..Compression levels)
        * [~flush options](#module_zlib..flush options)
        * [~Compression levels](#module_zlib..Compression levels)
        * [~flush options](#module_zlib..flush options)

<a name="module_zlib+deflate"></a>

### zlib.deflate(str_or_resource, [gzip], [level]) ⇒ <code>string</code>
<p>Compresses data in Zlib or gzip format.</p>
<p>If the input argument is a plain string, it is directly compressed.</p>
<p>If an array, object or resource value is given, this function will attempt to
invoke a <code>read()</code> method on it to read chunks of input text to incrementally
compress. Reading will stop if the object's <code>read()</code> method returns
either <code>null</code> or an empty string.</p>
<p>Throws an exception on errors.</p>
<p>Returns the compressed data.</p>

**Kind**: instance method of [<code>zlib</code>](#module_zlib)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| str_or_resource | <code>string</code> |  | <p>The string or resource object to be compressed.</p> |
| [gzip] | <code>boolean</code> | <code>false</code> | <p>Add a gzip header if true (creates a gzip-compliant output, otherwise defaults to Zlib)</p> |
| [level] | <code>number</code> | <code>Z_DEFAULT_COMPRESSION</code> | <p>The compression level (0-9).</p> |

**Example**  
```js
// deflate content using default compression
const deflated = deflate(content);

// deflate content using fastest compression
const deflated = deflate(content, Z_BEST_SPEED);
```
<a name="module_zlib+inflate"></a>

### zlib.inflate(str_or_resource) ⇒ <code>string</code>
<p>Decompresses data in Zlib or gzip format.</p>
<p>If the input argument is a plain string, it is directly decompressed.</p>
<p>If an array, object or resource value is given, this function will attempt to
invoke a <code>read()</code> method on it to read chunks of input text to incrementally
decompress. Reading will stop if the object's <code>read()</code> method returns
either <code>null</code> or an empty string.</p>
<p>Throws an exception on errors.</p>
<p>Returns the decompressed data.</p>

**Kind**: instance method of [<code>zlib</code>](#module_zlib)  

| Param | Type | Description |
| --- | --- | --- |
| str_or_resource | <code>string</code> | <p>The string or resource object to be parsed as JSON.</p> |

<a name="module_zlib+deflater"></a>

### zlib.deflater([gzip], [level]) ⇒ [<code>deflate</code>](#module_zlib.deflate)
<p>Initializes a deflate stream.</p>
<p>Returns a stream handle on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>zlib</code>](#module_zlib)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [gzip] | <code>boolean</code> | <code>false</code> | <p>Add a gzip header if true (creates a gzip-compliant output, otherwise defaults to Zlib)</p> |
| [level] | <code>number</code> | <code>Z_DEFAULT_COMPRESSION</code> | <p>The compression level (0-9).</p> |

**Example**  
```js
// initialize a Zlib deflate stream using default compression
const zstrmd = deflater();

// initialize a gzip deflate stream using fastest compression
const zstrmd = deflater(true, Z_BEST_SPEED);
```
<a name="module_zlib+inflater"></a>

### zlib.inflater() ⇒ [<code>inflate</code>](#module_zlib.inflate)
<p>Initializes an inflate stream. Can process either Zlib or gzip data.</p>
<p>Returns a stream handle on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>zlib</code>](#module_zlib)  
**Example**  
```js
// initialize an inflate stream
const zstrmi = inflater();
```
<a name="module_zlib+deflate"></a>

### zlib.deflate(str_or_resource, [gzip], [level]) ⇒ <code>string</code>
<p>Compresses data in Zlib or gzip format.</p>
<p>If the input argument is a plain string, it is directly compressed.</p>
<p>If an array, object or resource value is given, this function will attempt to
invoke a <code>read()</code> method on it to read chunks of input text to incrementally
compress. Reading will stop if the object's <code>read()</code> method returns
either <code>null</code> or an empty string.</p>
<p>Throws an exception on errors.</p>
<p>Returns the compressed data.</p>

**Kind**: instance method of [<code>zlib</code>](#module_zlib)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| str_or_resource | <code>string</code> |  | <p>The string or resource object to be compressed.</p> |
| [gzip] | <code>boolean</code> | <code>false</code> | <p>Add a gzip header if true (creates a gzip-compliant output, otherwise defaults to Zlib)</p> |
| [level] | <code>number</code> | <code>Z_DEFAULT_COMPRESSION</code> | <p>The compression level (0-9).</p> |

**Example**  
```js
// deflate content using default compression
const deflated = deflate(content);

// deflate content using fastest compression
const deflated = deflate(content, Z_BEST_SPEED);
```
<a name="module_zlib+inflate"></a>

### zlib.inflate(str_or_resource) ⇒ <code>string</code>
<p>Decompresses data in Zlib or gzip format.</p>
<p>If the input argument is a plain string, it is directly decompressed.</p>
<p>If an array, object or resource value is given, this function will attempt to
invoke a <code>read()</code> method on it to read chunks of input text to incrementally
decompress. Reading will stop if the object's <code>read()</code> method returns
either <code>null</code> or an empty string.</p>
<p>Throws an exception on errors.</p>
<p>Returns the decompressed data.</p>

**Kind**: instance method of [<code>zlib</code>](#module_zlib)  

| Param | Type | Description |
| --- | --- | --- |
| str_or_resource | <code>string</code> | <p>The string or resource object to be parsed as JSON.</p> |

<a name="module_zlib+deflater"></a>

### zlib.deflater([gzip], [level]) ⇒ [<code>deflate</code>](#module_zlib.deflate)
<p>Initializes a deflate stream.</p>
<p>Returns a stream handle on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>zlib</code>](#module_zlib)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [gzip] | <code>boolean</code> | <code>false</code> | <p>Add a gzip header if true (creates a gzip-compliant output, otherwise defaults to Zlib)</p> |
| [level] | <code>number</code> | <code>Z_DEFAULT_COMPRESSION</code> | <p>The compression level (0-9).</p> |

**Example**  
```js
// initialize a Zlib deflate stream using default compression
const zstrmd = deflater();

// initialize a gzip deflate stream using fastest compression
const zstrmd = deflater(true, Z_BEST_SPEED);
```
<a name="module_zlib+inflater"></a>

### zlib.inflater() ⇒ [<code>inflate</code>](#module_zlib.inflate)
<p>Initializes an inflate stream. Can process either Zlib or gzip data.</p>
<p>Returns a stream handle on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>zlib</code>](#module_zlib)  
**Example**  
```js
// initialize an inflate stream
const zstrmi = inflater();
```
<a name="module_zlib.deflate"></a>

### zlib.deflate
**Kind**: static class of [<code>zlib</code>](#module_zlib)  
**See**: [module:zlib#deflater()](module:zlib#deflater())  

* [.deflate](#module_zlib.deflate)
    * [.write(src, [flush])](#module_zlib.deflate+write) ⇒ <code>boolean</code>
    * [.read()](#module_zlib.deflate+read) ⇒ <code>string</code>
    * [.error()](#module_zlib.deflate+error) ⇒ <code>string</code>
    * [.write(src, [flush])](#module_zlib.deflate+write) ⇒ <code>boolean</code>
    * [.read()](#module_zlib.deflate+read) ⇒ <code>string</code>
    * [.error()](#module_zlib.deflate+error) ⇒ <code>string</code>

<a name="module_zlib.deflate+write"></a>

#### deflate.write(src, [flush]) ⇒ <code>boolean</code>
<p>Writes a chunk of data to the deflate stream.</p>
<p>Input data must be a string, it is internally compressed by the zlib <code>deflate()</code> routine,
the end result is buffered according to the requested <code>flush</code> mode until read via
[module:zlib.zstrmd#read](module:zlib.zstrmd#read).
Valid <code>flush</code>values are <code>Z_NO_FLUSH</code> (the default),
<code>Z_SYNC_FLUSH, Z_PARTIAL_FLUSH, Z_FULL_FLUSH, Z_FINISH</code>.
If <code>flush</code> is <code>Z_FINISH</code> then no more data can be written to the stream.
Refer to the [Zlib manual](https://zlib.net/manual.html) for details
on each flush mode.</p>
<p>Returns <code>true</code> on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>deflate</code>](#module_zlib.deflate)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| src | <code>string</code> |  | <p>The string of data to deflate.</p> |
| [flush] | <code>number</code> | <code>Z_NO_FLUSH</code> | <p>The zlib flush mode.</p> |

<a name="module_zlib.deflate+read"></a>

#### deflate.read() ⇒ <code>string</code>
<p>Reads a chunk of compressed data from the deflate stream.</p>
<p>Returns the current content of the deflate buffer, fed through
[write](#module_zlib.deflate+write).</p>
<p>Returns compressed chunk on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>deflate</code>](#module_zlib.deflate)  
<a name="module_zlib.deflate+error"></a>

#### deflate.error() ⇒ <code>string</code>
<p>Queries error information.</p>
<p>Returns a string containing a description of the last occurred error or
<code>null</code> if there is no error information.</p>

**Kind**: instance method of [<code>deflate</code>](#module_zlib.deflate)  
<a name="module_zlib.deflate+write"></a>

#### deflate.write(src, [flush]) ⇒ <code>boolean</code>
<p>Writes a chunk of data to the deflate stream.</p>
<p>Input data must be a string, it is internally compressed by the zlib <code>deflate()</code> routine,
the end result is buffered according to the requested <code>flush</code> mode until read via
[module:zlib.zstrmd#read](module:zlib.zstrmd#read).
Valid <code>flush</code>values are <code>Z_NO_FLUSH</code> (the default),
<code>Z_SYNC_FLUSH, Z_PARTIAL_FLUSH, Z_FULL_FLUSH, Z_FINISH</code>.
If <code>flush</code> is <code>Z_FINISH</code> then no more data can be written to the stream.
Refer to the [Zlib manual](https://zlib.net/manual.html) for details
on each flush mode.</p>
<p>Returns <code>true</code> on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>deflate</code>](#module_zlib.deflate)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| src | <code>string</code> |  | <p>The string of data to deflate.</p> |
| [flush] | <code>number</code> | <code>Z_NO_FLUSH</code> | <p>The zlib flush mode.</p> |

<a name="module_zlib.deflate+read"></a>

#### deflate.read() ⇒ <code>string</code>
<p>Reads a chunk of compressed data from the deflate stream.</p>
<p>Returns the current content of the deflate buffer, fed through
[write](#module_zlib.deflate+write).</p>
<p>Returns compressed chunk on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>deflate</code>](#module_zlib.deflate)  
<a name="module_zlib.deflate+error"></a>

#### deflate.error() ⇒ <code>string</code>
<p>Queries error information.</p>
<p>Returns a string containing a description of the last occurred error or
<code>null</code> if there is no error information.</p>

**Kind**: instance method of [<code>deflate</code>](#module_zlib.deflate)  
<a name="module_zlib.inflate"></a>

### zlib.inflate
**Kind**: static class of [<code>zlib</code>](#module_zlib)  
**See**: [module:zlib#inflater()](module:zlib#inflater())  

* [.inflate](#module_zlib.inflate)
    * [.write(src, [flush])](#module_zlib.inflate+write) ⇒ <code>boolean</code>
    * [.read()](#module_zlib.inflate+read) ⇒ <code>string</code>
    * [.write(src, [flush])](#module_zlib.inflate+write) ⇒ <code>boolean</code>
    * [.read()](#module_zlib.inflate+read) ⇒ <code>string</code>
    * [.error()](#module_zlib.inflate+error) ⇒ <code>string</code>
    * [.error()](#module_zlib.inflate+error) ⇒ <code>string</code>
    * [.error()](#module_zlib.inflate+error) ⇒ <code>string</code>
    * [.error()](#module_zlib.inflate+error) ⇒ <code>string</code>

<a name="module_zlib.inflate+write"></a>

#### inflate.write(src, [flush]) ⇒ <code>boolean</code>
<p>Writes a chunk of data to the inflate stream.</p>
<p>Input data must be a string, it is internally decompressed by the zlib <code>inflate()</code> routine,
the end result is buffered according to the requested <code>flush</code> mode until read via
[read](#module_zlib.inflate+read).
Valid <code>flush</code> values are <code>Z_NO_FLUSH</code> (the default), <code>Z_SYNC_FLUSH, Z_FINISH</code>.
If <code>flush</code> is <code>Z_FINISH</code> then no more data can be written to the stream.
Refer to the [Zlib manual](https://zlib.net/manual.html) for details
on each flush mode.</p>
<p>Returns <code>true</code> on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>inflate</code>](#module_zlib.inflate)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| src | <code>string</code> |  | <p>The string of data to inflate.</p> |
| [flush] | <code>number</code> | <code>Z_NO_FLUSH</code> | <p>The zlib flush mode.</p> |

<a name="module_zlib.inflate+read"></a>

#### inflate.read() ⇒ <code>string</code>
<p>Reads a chunk of decompressed data from the inflate stream.</p>
<p>Returns the current content of the inflate buffer, fed through
[write](#module_zlib.inflate+write).</p>
<p>Returns decompressed chunk on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>inflate</code>](#module_zlib.inflate)  
<a name="module_zlib.inflate+write"></a>

#### inflate.write(src, [flush]) ⇒ <code>boolean</code>
<p>Writes a chunk of data to the inflate stream.</p>
<p>Input data must be a string, it is internally decompressed by the zlib <code>inflate()</code> routine,
the end result is buffered according to the requested <code>flush</code> mode until read via
[read](#module_zlib.inflate+read).
Valid <code>flush</code> values are <code>Z_NO_FLUSH</code> (the default), <code>Z_SYNC_FLUSH, Z_FINISH</code>.
If <code>flush</code> is <code>Z_FINISH</code> then no more data can be written to the stream.
Refer to the [Zlib manual](https://zlib.net/manual.html) for details
on each flush mode.</p>
<p>Returns <code>true</code> on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>inflate</code>](#module_zlib.inflate)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| src | <code>string</code> |  | <p>The string of data to inflate.</p> |
| [flush] | <code>number</code> | <code>Z_NO_FLUSH</code> | <p>The zlib flush mode.</p> |

<a name="module_zlib.inflate+read"></a>

#### inflate.read() ⇒ <code>string</code>
<p>Reads a chunk of decompressed data from the inflate stream.</p>
<p>Returns the current content of the inflate buffer, fed through
[write](#module_zlib.inflate+write).</p>
<p>Returns decompressed chunk on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>inflate</code>](#module_zlib.inflate)  
<a name="module_zlib.inflate+error"></a>

#### inflate.error() ⇒ <code>string</code>
<p>Queries error information.</p>
<p>Returns a string containing a description of the last occurred error or
<code>null</code> if there is no error information.</p>

**Kind**: instance method of [<code>inflate</code>](#module_zlib.inflate)  
<a name="module_zlib.inflate+error"></a>

#### inflate.error() ⇒ <code>string</code>
<p>Queries error information.</p>
<p>Returns a string containing a description of the last occurred error or
<code>null</code> if there is no error information.</p>

**Kind**: instance method of [<code>inflate</code>](#module_zlib.inflate)  
<a name="module_zlib.inflate+error"></a>

#### inflate.error() ⇒ <code>string</code>
<p>Queries error information.</p>
<p>Returns a string containing a description of the last occurred error or
<code>null</code> if there is no error information.</p>

**Kind**: instance method of [<code>inflate</code>](#module_zlib.inflate)  
<a name="module_zlib.inflate+error"></a>

#### inflate.error() ⇒ <code>string</code>
<p>Queries error information.</p>
<p>Returns a string containing a description of the last occurred error or
<code>null</code> if there is no error information.</p>

**Kind**: instance method of [<code>inflate</code>](#module_zlib.inflate)  
<a name="module_zlib.deflate"></a>

### zlib.deflate
**Kind**: static class of [<code>zlib</code>](#module_zlib)  
**See**: [module:zlib#deflater()](module:zlib#deflater())  

* [.deflate](#module_zlib.deflate)
    * [.write(src, [flush])](#module_zlib.deflate+write) ⇒ <code>boolean</code>
    * [.read()](#module_zlib.deflate+read) ⇒ <code>string</code>
    * [.error()](#module_zlib.deflate+error) ⇒ <code>string</code>
    * [.write(src, [flush])](#module_zlib.deflate+write) ⇒ <code>boolean</code>
    * [.read()](#module_zlib.deflate+read) ⇒ <code>string</code>
    * [.error()](#module_zlib.deflate+error) ⇒ <code>string</code>

<a name="module_zlib.deflate+write"></a>

#### deflate.write(src, [flush]) ⇒ <code>boolean</code>
<p>Writes a chunk of data to the deflate stream.</p>
<p>Input data must be a string, it is internally compressed by the zlib <code>deflate()</code> routine,
the end result is buffered according to the requested <code>flush</code> mode until read via
[module:zlib.zstrmd#read](module:zlib.zstrmd#read).
Valid <code>flush</code>values are <code>Z_NO_FLUSH</code> (the default),
<code>Z_SYNC_FLUSH, Z_PARTIAL_FLUSH, Z_FULL_FLUSH, Z_FINISH</code>.
If <code>flush</code> is <code>Z_FINISH</code> then no more data can be written to the stream.
Refer to the [Zlib manual](https://zlib.net/manual.html) for details
on each flush mode.</p>
<p>Returns <code>true</code> on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>deflate</code>](#module_zlib.deflate)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| src | <code>string</code> |  | <p>The string of data to deflate.</p> |
| [flush] | <code>number</code> | <code>Z_NO_FLUSH</code> | <p>The zlib flush mode.</p> |

<a name="module_zlib.deflate+read"></a>

#### deflate.read() ⇒ <code>string</code>
<p>Reads a chunk of compressed data from the deflate stream.</p>
<p>Returns the current content of the deflate buffer, fed through
[write](#module_zlib.deflate+write).</p>
<p>Returns compressed chunk on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>deflate</code>](#module_zlib.deflate)  
<a name="module_zlib.deflate+error"></a>

#### deflate.error() ⇒ <code>string</code>
<p>Queries error information.</p>
<p>Returns a string containing a description of the last occurred error or
<code>null</code> if there is no error information.</p>

**Kind**: instance method of [<code>deflate</code>](#module_zlib.deflate)  
<a name="module_zlib.deflate+write"></a>

#### deflate.write(src, [flush]) ⇒ <code>boolean</code>
<p>Writes a chunk of data to the deflate stream.</p>
<p>Input data must be a string, it is internally compressed by the zlib <code>deflate()</code> routine,
the end result is buffered according to the requested <code>flush</code> mode until read via
[module:zlib.zstrmd#read](module:zlib.zstrmd#read).
Valid <code>flush</code>values are <code>Z_NO_FLUSH</code> (the default),
<code>Z_SYNC_FLUSH, Z_PARTIAL_FLUSH, Z_FULL_FLUSH, Z_FINISH</code>.
If <code>flush</code> is <code>Z_FINISH</code> then no more data can be written to the stream.
Refer to the [Zlib manual](https://zlib.net/manual.html) for details
on each flush mode.</p>
<p>Returns <code>true</code> on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>deflate</code>](#module_zlib.deflate)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| src | <code>string</code> |  | <p>The string of data to deflate.</p> |
| [flush] | <code>number</code> | <code>Z_NO_FLUSH</code> | <p>The zlib flush mode.</p> |

<a name="module_zlib.deflate+read"></a>

#### deflate.read() ⇒ <code>string</code>
<p>Reads a chunk of compressed data from the deflate stream.</p>
<p>Returns the current content of the deflate buffer, fed through
[write](#module_zlib.deflate+write).</p>
<p>Returns compressed chunk on success.</p>
<p>Returns <code>null</code> if an error occurred.</p>

**Kind**: instance method of [<code>deflate</code>](#module_zlib.deflate)  
<a name="module_zlib.deflate+error"></a>

#### deflate.error() ⇒ <code>string</c


---

