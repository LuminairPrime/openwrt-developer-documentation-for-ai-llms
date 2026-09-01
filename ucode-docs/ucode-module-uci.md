# ucode module: `uci`

> **Source:** [`lib/uci.c`](https://github.com/jow-/ucode/blob/master/lib/uci.c)
> **Live docs:** https://ucode.mein.io/module-uci.html
> **Generated:** 2026-09-01 02:27 UTC from commit `fa2c1bc`

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
<dt><a href="#module_ffi">ffi</a></dt>
<dd><h1 id="foreign-function-interface-(ffi)">Foreign Function Interface (FFI)</h1>
<p>The <code>ffi</code> module provides a foreign function interface for ucode, allowing
direct interaction with C libraries. It combines a C declaration parser with
libffi-based function calling to enable seamless interop between ucode and C.</p>
<p>The module can be imported using the wildcard import syntax:</p>
<pre class="prettyprint source"><code>import * as ffi from 'ffi';
</code></pre>
<h2 id="synopsis">Synopsis</h2>
<pre class="prettyprint source lang-javascript"><code>import * as ffi from 'ffi';

<p>// 1. Declare C types and functions
ffi.cdef(<code>    struct point { int x; int y; };     extern char **environ;</code>);</p>
<p>// 2. Call C functions via the global C namespace
// Primitive return values are auto-converted to ucode types
let strcmp = ffi.C.wrap(&#39;int strcmp(const char *, const char *)&#39;);
print(strcmp(&quot;hello&quot;, &quot;world&quot;), &quot;\n&quot;);  // =&gt; non-zero (number)</p>
<p>// 3. String return values remain as cdata - use ffi.string() to convert
let getenv = ffi.C.wrap(&#39;char *getenv(char <em>)&#39;);
let path_ptr = getenv(&#39;PATH&#39;);      // Returns char</em> cdata
let path_str = ffi.string(path_ptr); // Convert to ucode string</p>
<p>// 4. Create C data instances
ffi.cdef(&#39;struct point { int x; int y; };&#39;);
let p = ffi.ctype(&#39;struct point&#39;, 10, 20);
print(p.get(&#39;x&#39;), p.get(&#39;y&#39;), &quot;\n&quot;);  // =&gt; 10 20</p>
<p>// 5. Access global variables
print(ffi.C.dlsym(&#39;environ&#39;).get(0), &quot;\n&quot;);</p>
<p>// 6. Query type information
print(ffi.sizeof(&#39;int&#39;), &quot;\n&quot;);        // =&gt; 4
print(ffi.alignof(&#39;double&#39;), &quot;\n&quot;);    // =&gt; 8
print(ffi.offsetof(&#39;struct point&#39;, &#39;y&#39;), &quot;\n&quot;);  // =&gt; 4</p>
<p>// 7. Load external libraries
let libz = ffi.dlopen(&#39;z&#39;);
let zlibVersion = libz.wrap(&#39;const char *zlibVersion(void)&#39;);
print(zlibVersion().slice(), &quot;\n&quot;);  // =&gt; &quot;1.2.11&quot; (or similar)</p>
<p>// Use in callbacks (primitives auto-converted)
let qsort = ffi.C.wrap(&#39;void qsort(void <em>, size_t, size_t, int (</em>)(const void *, const void *))&#39;);
let cmp = ffi.C.wrap(&#39;int strcmp(const char *, const char *)&#39;);
let arr = ffi.ctype(&#39;char *[5]&#39;, [&quot;zebra&quot;, &quot;apple&quot;, &quot;banana&quot;, &quot;cherry&quot;, &quot;date&quot;]);
// cmp() returns ucode number directly (primitives auto-converted)
qsort(arr.ptr(), arr.length(), arr.itemsize(),
      (a, b) =&gt; cmp(a.deref(&#39;const char *&#39;), b.deref(&#39;const char *&#39;)));
</code></pre></p>
<h2 id="memory-management-for-char*-return-values">Memory Management for char* Return Values</h2>
<p>When a wrapped C function returns <code>char*</code>, the return value is a <strong>cdata pointer
object</strong>, not an auto-converted ucode string. This design prevents memory leaks
and gives you explicit control over memory management.</p>
<h3 id="converting-char*-to-ucode-strings">Converting char* to ucode Strings</h3>
<p>Use <code>ffi.string()</code> or <code>slice()</code> to convert a char* cdata to a ucode string:</p>
<pre class="prettyprint source lang-javascript"><code>let getenv = ffi.C.wrap('char *getenv(char *)');

<p>let path_ptr = getenv(&#39;PATH&#39;);    // Returns char* cdata
let path = ffi.string(path_ptr);  // Convert to ucode string
// or equivalently:
let path = path_ptr.slice();      // slice() without args = string()
</code></pre></p>
<p><strong>Note</strong>: Both <code>ffi.string()</code> and <code>slice()</code> create a <strong>copy</strong> of the C string.
The original C memory remains untouched.</p>
<h3 id="memory-ownership-patterns">Memory Ownership Patterns</h3>
<h4 id="pattern-1%3A-c-manages-memory-(no-free-required)">Pattern 1: C Manages Memory (No Free Required)</h4>
<p>Functions like <code>getenv()</code>, <code>strerror()</code> return pointers to <strong>static/internal
memory</strong> managed by the C library. Do NOT free these.</p>
<pre class="prettyprint source lang-javascript"><code>let getenv = ffi.C.wrap('char *getenv(char *)');

<p>let path_ptr = getenv(&#39;PATH&#39;);
let path = ffi.string(path_ptr);  // Copies to ucode string</p>
<p>// path_ptr points to C internal memory - DO NOT free
// path is a ucode string - managed by ucode GC
</code></pre></p>
<h4 id="pattern-2%3A-caller-must-free-(malloc'd-memory)">Pattern 2: Caller Must Free (malloc'd Memory)</h4>
<p>Functions like <code>strdup()</code>, <code>asprintf()</code>, <code>getline()</code> return <strong>malloc'd memory</strong>
that you must free to avoid leaks.</p>
<pre class="prettyprint source lang-javascript"><code>let strdup = ffi.C.wrap('char *strdup(const char *)');
let free = ffi.C.wrap('void free(void *)');

<p>let ptr = strdup(&quot;hello&quot;);      // malloc&#39;d by strdup
let str = ffi.string(ptr);      // Copies to ucode string
free(ptr);                       // NOW you can safely free</p>
<p>// str is safe - it&#39;s a ucode string copy
// ptr memory is freed - no leak
</code></pre></p>
<p><strong>Key</strong>: Keep the cdata pointer until you're done copying, then free it.</p>
<h4 id="pattern-3%3A-stack-allocated-buffers">Pattern 3: Stack-Allocated Buffers</h4>
<p>When C writes into a buffer you provide (e.g., <code>sprintf</code>), the buffer is
managed by ucode.</p>
<pre class="prettyprint source lang-javascript"><code>let sprintf = ffi.C.wrap('int sprintf(char *, const char *, ...)');

<p>let buf = ffi.ctype(&#39;char[256]&#39;);  // ucode-managed array
sprintf(buf, &quot;Hello %s&quot;, &quot;World&quot;);</p>
<p>let msg = ffi.string(buf);  // Copies to ucode string</p>
<p>// buf is managed by ucode GC - no manual free needed
</code></pre></p>
<h3 id="substring-operations-with-slice()">Substring Operations with slice()</h3>
<p>For char* pointers, <code>slice()</code> supports substring extraction:</p>
<pre class="prettyprint source lang-javascript"><code>let getenv = ffi.C.wrap('char *getenv(char *)');
let ptr = getenv('PATH');

<p>// From start to end (same as ffi.string())
let full = ptr.slice();</p>
<p>// From start index to end
let rest = ptr.slice(5);</p>
<p>// Specific range
let part = ptr.slice(0, 10);</p>
<p>// Negative indices (from end)
let last = ptr.slice(-5);
</code></pre></p>
<h3 id="common-functions-reference">Common Functions Reference</h3>
<table>
<thead>
<tr>
<th>Function</th>
<th>Memory Owner</th>
<th>Pattern</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>getenv()</code></td>
<td>C (static)</td>
<td>No free needed</td>
</tr>
<tr>
<td><code>strerror()</code></td>
<td>C (static)</td>
<td>No free needed</td>
</tr>
<tr>
<td><code>strdup()</code></td>
<td>Caller</td>
<td>Must <code>free()</code></td>
</tr>
<tr>
<td><code>asprintf()</code></td>
<td>Caller</td>
<td>Must <code>free()</code></td>
</tr>
<tr>
<td><code>getline()</code></td>
<td>Caller</td>
<td>Must <code>free()</code></td>
</tr>
<tr>
<td><code>sprintf()</code></td>
<td>Caller (buffer)</td>
<td>Buffer managed by you</td>
</tr>
<tr>
<td><code>strtok()</code></td>
<td>C (static)</td>
<td>No free needed</td>
</tr>
</tbody>
</table>
<h3 id="best-practices">Best Practices</h3>
<ol>
<li><strong>Always use <code>ffi.string()</code> or <code>slice()</code></strong> when you need a ucode string from <code>char*</code></li>
<li><strong>Track ownership</strong>: Does C manage the memory or do you?</li>
<li><strong>Free after copying</strong>: Call <code>free(ptr)</code> only after <code>ffi.string(ptr)</code> or <code>ptr.slice()</code></li>
<li><strong>Never free static memory</strong>: <code>getenv()</code>, <code>strerror()</code> return static pointers</li>
</ol>
<h2 id="limitations">Limitations</h2>
<ul>
<li><strong>No vararg closures</strong>: <code>wrap()</code> cannot create closures with variable arguments</li>
<li><strong>Fixed ABI</strong>: Calling convention determined at closure creation time</li>
<li><strong>Platform constraints</strong>: Some architectures have limited support for certain type combinations</li>
</ul>
<h2 id="the-ffi.c-namespace">The <code>ffi.C</code> Namespace</h2>
<p><code>ffi.C</code> is a special CLib instance representing the process's global symbol table.
It provides access to standard C library functions without explicit <code>dlopen()</code>:</p>
<pre class="prettyprint source lang-javascript"><code>// These are equivalent:
let strlen1 = ffi.C.wrap('size_t strlen(const char *)');

<p>ffi.cdef(&#39;size_t strlen(const char *);&#39;);
let strlen2 = ffi.C.wrap(&#39;strlen&#39;);
</code></pre></p>
<p>Functions declared via <code>cdef()</code> are automatically registered in <code>ffi.C</code>'s symbol table.</p>
<h2 id="pointer-arithmetic-and-memory-access">Pointer Arithmetic and Memory Access</h2>
<p>C data objects (cdata) provide methods for pointer arithmetic and memory access:</p>
<h3 id="creating-pointers-with-ptr()">Creating Pointers with ptr()</h3>
<p>Use <code>ptr()</code> to get a pointer to a cdata value:</p>
<pre class="prettyprint source lang-javascript"><code>let x = ffi.ctype('int', 42);
let px = x.ptr();  // int* pointer to x

<p>// Pass to C functions expecting pointers
ffi.cdef(&#39;int atoi(const char *)&#39;);
let num = ffi.ctype(&#39;char[4]&#39;, &quot;123&quot;);
let result = atoi(num.ptr());  // =&gt; 123
</code></pre></p>
<h3 id="array-indexing-with-get()-and-set()">Array Indexing with get() and set()</h3>
<p>Access array elements using <code>get(index)</code> and <code>set(index, value)</code>:</p>
<pre class="prettyprint source lang-javascript"><code>let arr = ffi.ctype('int[5]', [10, 20, 30, 40, 50]);

<p>// Read elements
let first = arr.get(0);  // =&gt; 10 (ucode number)
let third = arr.get(2);  // =&gt; 30 (ucode number)</p>
<p>// Modify elements
arr.set(0, 100);
arr.set(4, 200);</p>
<p>// Negative indices work too
let last = arr.get(-1);  // =&gt; 200 (ucode number)
</code></pre></p>
<h3 id="understanding-get()-vs-index()">Understanding get() vs index()</h3>
<p><strong><code>get()</code> returns converted ucode values</strong>, while <strong><code>index()</code> returns
raw cdata references</strong>. This is the key distinction between the two methods.</p>
<h4 id="get()---converted-values">get() - Converted Values</h4>
<p>The <code>get()</code> method immediately converts C values to ucode types:</p>
<pre class="prettyprint source lang-javascript"><code>let arr = ffi.ctype('int[5]', [10, 20, 30, 40, 50]);

<p>// Returns ucode number directly
let val1 = arr.get(0);      // =&gt; 10 (number)
let val2 = arr.get(2);      // =&gt; 30 (number)</p>
<p>// Struct field access - returns converted value
ffi.cdef(&#39;struct point { int x; int y; };&#39;);
let p = ffi.ctype(&#39;struct point&#39;, 10, 20);
p.get(&#39;x&#39;);      // =&gt; 10 (number)
p.get(&#39;y&#39;);      // =&gt; 20 (number)
</code></pre></p>
<h4 id="index()---raw-cdata-references">index() - Raw cdata References</h4>
<p>The <code>index()</code> method returns a cdata reference for further manipulation:</p>
<pre class="prettyprint source lang-javascript"><code>let arr = ffi.ctype('int[5]', [10, 20, 30, 40, 50]);

<p>// Returns cdata reference (unconverted)
let ref1 = arr.index(0);    // =&gt; cdata (int)
let ref2 = arr.index(2);    // =&gt; cdata (int)</p>
<p>// Convert to ucode value explicitly
ref1.get();     // =&gt; 10 (number)</p>
<p>// Or modify through the reference
arr.index(0).set(100);  // Set arr[0] = 100
</code></pre></p>
<h4 id="pointer-arithmetic">Pointer Arithmetic</h4>
<p>Both methods work with pointers, but return different types:</p>
<pre class="prettyprint source lang-javascript"><code>let ptr = ffi.ctype('int *', arr.ptr());

<p>// index() returns cdata reference
ptr.index(0);   // =&gt; cdata at ptr[0]
ptr.index(1);   // =&gt; cdata at ptr[1]
ptr.index(0).get();  // =&gt; 10 (number)</p>
<p>// get() returns converted value
ptr.get(0);     // =&gt; 10 (number)
ptr.get(1);     // =&gt; 20 (number)
</code></pre></p>
<h4 id="path-syntax-support">Path Syntax Support</h4>
<p>Both methods support path notation for nested access:</p>
<pre class="prettyprint source lang-javascript"><code>ffi.cdef('struct rect { struct point min; struct point max; };');
let r = ffi.ctype('struct rect', {
    min: {x: 0, y: 0},
    max: {x: 100, y: 100}
});

<p>// get() returns converted value
r.get(&#39;min.x&#39;);       // =&gt; 0 (number)</p>
<p>// index() returns cdata reference
r.index(&#39;min.x&#39;);     // =&gt; cdata (int)
r.index(&#39;min.x&#39;).get() // =&gt; 0 (number)
</code></pre></p>
<h4 id="practical-guidance">Practical Guidance</h4>
<p><strong>Use <code>get()</code> when:</strong></p>
<ul>
<li>You need the value immediately as a ucode type</li>
<li>Reading values for computation: <code>let x = arr.get(i)</code></li>
<li>Accessing struct fields: <code>let y = struct.get('field')</code></li>
<li>Most common use cases</li>
</ul>
<p><strong>Use <code>index()</code> when:</strong></p>
<ul>
<li>You need a reference for further manipulation</li>
<li>Chaining operations: <code>arr.index(i).set(val)</code></li>
<li>Pointer arithmetic with cdata: <code>ptr.index(n).deref()</code></li>
<li>Passing references to other C functions</li>
</ul>
<p><strong>For writing values:</strong></p>
<ul>
<li>Use <code>set()</code> for both arrays and structs: <code>arr.set(i, val)</code>, <code>struct.set('f', val)</code></li>
</ul>
<p><strong>For getting pointers (not values):</strong></p>
<ul>
<li>Use <code>ptr()</code> on scalars: <code>x.ptr()</code> gives you <code>int*</code></li>
<li>Arrays are already pointers: <code>arr</code> can be passed to C functions</li>
</ul>
<h3 id="pointer-arithmetic-via-get()-and-index()">Pointer Arithmetic via get() and index()</h3>
<p>Both <code>get(n)</code> and <code>index(n)</code> work for pointer arithmetic on pointer types:</p>
<pre class="prettyprint source lang-javascript"><code>ffi.cdef('char *strdup(const char *)');
let strdup = ffi.C.wrap('char *strdup(const char *)');

<p>let ptr = strdup(&quot;hello world&quot;);</p>
<p>// get() returns converted value (number for char)
let first_char = ptr.get(0);    // &#39;h&#39; (number 104)
let sixth_char = ptr.get(6);    // &#39;w&#39; (number 119)</p>
<p>// index() returns cdata reference
ptr.index(6);       // =&gt; cdata (char)
ptr.index(6).get()  // =&gt; 119 (number)</p>
<p>// Get substring from offset
let substring = ffi.string(ptr.get(6));  // &quot;world&quot;</p>
<p>free(ptr);
</code></pre></p>
<h3 id="path-based-access-for-nested-structures">Path-Based Access for Nested Structures</h3>
<p>Use dot notation and array indexing in paths for complex access:</p>
<pre class="prettyprint source lang-javascript"><code>ffi.cdef(`
    struct point { int x; int y; };
    struct rect { struct point min; struct point max; };
`);

<p>let r = ffi.ctype(&#39;struct rect&#39;, {
    min: {x: 0, y: 0},
    max: {x: 100, y: 100}
});</p>
<p>// Nested field access
r.get(&#39;min.x&#39;);    // =&gt; 0
r.set(&#39;max.y&#39;, 50);</p>
<p>// Array of structs
ffi.cdef(&#39;struct point points[3];&#39;);
let arr = ffi.ctype(&#39;struct point[3]&#39;, [
    {x: 1, y: 2},
    {x: 3, y: 4},
    {x: 5, y: 6}
]);</p>
<p>arr.get(&#39;[1].x&#39;);  // =&gt; 3
arr.set(&#39;[2].y&#39;, 10);
</code></pre></p>
<h3 id="dereferencing-pointers-with-deref()">Dereferencing Pointers with deref()</h3>
<p>Use <code>deref(type)</code> to read the value pointed to:</p>
<pre class="prettyprint source lang-javascript"><code>let x = ffi.ctype('int', 42);
let px = x.ptr();

<p>let value = px.deref(&#39;int&#39;);  // =&gt; 42</p>
<p>// With char* pointers
ffi.cdef(&#39;char *strdup(const char *)&#39;);
let strdup = ffi.C.wrap(&#39;char *strdup(const char *)&#39;);</p>
<p>let ptr = strdup(&quot;hello&quot;);
let first_byte = ptr.deref(&#39;char&#39;);  // =&gt; &#39;h&#39; (as number 104)</p>
<p>free(ptr);
</code></pre></p>
<h3 id="querying-array-properties">Querying Array Properties</h3>
<p>Use <code>length()</code> and <code>itemsize()</code> for array information:</p>
<pre class="prettyprint source lang-javascript"><code>let arr = ffi.ctype('int[10]');

<p>arr.length();   // =&gt; 10 (number of elements)
arr.itemsize(); // =&gt; 4 (size of each element in bytes)</p>
<p>// Calculate total size
let total = arr.length() * arr.itemsize();  // =&gt; 40 bytes
</code></pre></p>
<h3 id="working-with-byte-arrays">Working with Byte Arrays</h3>
<p>For <code>char[]</code> or <code>uint8_t[]</code>, use <code>slice()</code> to extract strings:</p>
<pre class="prettyprint source lang-javascript"><code>let buf = ffi.ctype('char[10]', &quot;hello&quot;);

<p>// Extract as ucode string
let str = buf.slice();        // =&gt; &quot;hello&quot;
let part = buf.slice(0, 3);   // =&gt; &quot;hel&quot;</p>
<p>// Or use ffi.string()
let str2 = ffi.string(buf);   // =&gt; &quot;hello&quot;
</code></pre></p>
<h3 id="complete-example%3A-string-manipulation">Complete Example: String Manipulation</h3>
<pre class="prettyprint source lang-javascript"><code>ffi.cdef(`
    char *strdup(const char *);
    void free(void *);
    size_t strlen(const char *);
`);

<p>let strdup = ffi.C.wrap(&#39;char *strdup(const char *)&#39;);
let free = ffi.C.wrap(&#39;void free(void *)&#39;);
let strlen = ffi.C.wrap(&#39;size_t strlen(const char *)&#39;);</p>
<p>// Create a duplicatable string
let ptr = strdup(&quot;hello world&quot;);</p>
<p>// Get length
let len = strlen(ptr).get();  // =&gt; 11</p>
<p>// Access individual characters via indexing
let first = ptr.get(0);       // &#39;h&#39;
let sixth = ptr.get(6);       // &#39;w&#39;</p>
<p>// Extract substrings
let hello = ptr.slice(0, 5);  // &quot;hello&quot;
let world = ptr.slice(6);     // &quot;world&quot;</p>
<p>// Modify in place
ptr.set(5, 0);  // Null-terminate at space</p>
<p>let str = ffi.string(ptr);  // =&gt; &quot;hello&quot;</p>
<p>// Clean up
free(ptr);
</code></pre></p>
</dd>
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
<code>ucode</code> interpreter with the <code>-lmath</code> switch.</p>
<p>It should be noted that when the ucode interpreter is run as <code>-p &quot;...&quot;</code>,
values involving Infinity are returned as the max double precision value
+/-1e309 (JSON), whereas when run as <code>-e &quot;print(...)&quot;</code> Infinity is
represented by the string <code>Infinity</code>. The boolean check <code>isinf()</code> is
available to determine Infinity values.</p></dd>
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
<p>The core namespace is not an actual module but refers to
