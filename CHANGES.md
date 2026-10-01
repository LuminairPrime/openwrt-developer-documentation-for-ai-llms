# Documentation Changes — 2026-10-01 08:41 UTC

> Summary of changes detected in this run compared to the
> previous committed version. Shows added, removed, and
> modified entries in each documentation index.

---

## Changes in `ucode-docs/llms.txt`

```diff
diff --git a/ucode-docs/llms.txt b/ucode-docs/llms.txt
index 6122751..a13862c 100644
--- a/ucode-docs/llms.txt
+++ b/ucode-docs/llms.txt
@@ -1,7 +1,7 @@
 # ucode Documentation Index
-# Source: https://github.com/jow-/ucode (commit: fa2c1bc)
+# Source: https://github.com/jow-/ucode (commit: cef095d)
 # Live docs: https://ucode.mein.io/
-# Generated: 2026-09-01 02:27 UTC
+# Generated: 2026-10-01 08:40 UTC
 #
 # ucode is a tiny ECMAScript-like scripting language for OpenWrt.
 # Provides bindings for ubus, uci, uloop, netlink, and other OpenWrt APIs.
@@ -13,7 +13,9 @@
 ## Files in this directory
 
 - [ucode-module-debug.md](/ucode-docs/ucode-module-debug.md): ucode `debug` module — 1 documented members
-- [ucode-module-digest.md](/ucode-docs/ucode-module-digest.md): ucode `digest` module — 2 documented members
+- [ucode-module-debug_proto.md](/ucode-docs/ucode-module-debug_proto.md): ucode `debug_proto` module — 1 documented members
+- [ucode-module-debug_remote.md](/ucode-docs/ucode-module-debug_remote.md): ucode `debug_remote` module — 1 documented members
+- [ucode-module-digest.md](/ucode-docs/ucode-module-digest.md): ucode `digest` module — 1 documented members
 - [ucode-module-fs.md](/ucode-docs/ucode-module-fs.md): ucode `fs` module — 1 documented members
 - [ucode-module-io.md](/ucode-docs/ucode-module-io.md): ucode `io` module — 1 documented members
 - [ucode-module-log.md](/ucode-docs/ucode-module-log.md): ucode `log` module — 1 documented members
@@ -21,10 +23,10 @@
 - [ucode-module-nl80211.md](/ucode-docs/ucode-module-nl80211.md): ucode `nl80211` module — 1 documented members
 - [ucode-module-resolv.md](/ucode-docs/ucode-module-resolv.md): ucode `resolv` module — 1 documented members
 - [ucode-module-rtnl.md](/ucode-docs/ucode-module-rtnl.md): ucode `rtnl` module — 1 documented members
-- [ucode-module-serial.md](/ucode-docs/ucode-module-serial.md): ucode `serial` module — 2 documented members
+- [ucode-module-serial.md](/ucode-docs/ucode-module-serial.md): ucode `serial` module — 1 documented members
 - [ucode-module-socket.md](/ucode-docs/ucode-module-socket.md): ucode `socket` module — 1 documented members
 - [ucode-module-struct.md](/ucode-docs/ucode-module-struct.md): ucode `struct` module — 1 documented members
 - [ucode-module-ubus.md](/ucode-docs/ucode-module-ubus.md): ucode `ubus` module — 1 documented members
 - [ucode-module-uci.md](/ucode-docs/ucode-module-uci.md): ucode `uci` module — 1 documented members
 - [ucode-module-uloop.md](/ucode-docs/ucode-module-uloop.md): ucode `uloop` module — 1 documented members
-- [ucode-module-zlib.md](/ucode-docs/ucode-module-zlib.md): ucode `zlib` module — 2 documented members
+- [ucode-module-zlib.md](/ucode-docs/ucode-module-zlib.md): ucode `zlib` module — 1 documented members
```

## Changes in `luci-docs/llms.txt`

```diff
diff --git a/luci-docs/llms.txt b/luci-docs/llms.txt
index 7296719..fa75b4f 100644
--- a/luci-docs/llms.txt
+++ b/luci-docs/llms.txt
@@ -1,7 +1,7 @@
 # LuCI JS API Documentation Index
-# Source: https://github.com/openwrt/luci (commit: 4c0a4ed)
+# Source: https://github.com/openwrt/luci (commit: 32775cf)
 # Live docs: https://openwrt.github.io/luci/jsapi/
-# Generated: 2026-09-01 02:28 UTC
+# Generated: 2026-10-01 08:41 UTC
 #
 # LuCI is the OpenWrt web configuration interface.
 # This index covers its complete client-side JavaScript API.
```

## Changes in `openwrt-buildroot-docs/llms.txt`

```diff
diff --git a/openwrt-buildroot-docs/llms.txt b/openwrt-buildroot-docs/llms.txt
index 1fdd37b..5764001 100644
--- a/openwrt-buildroot-docs/llms.txt
+++ b/openwrt-buildroot-docs/llms.txt
@@ -1,6 +1,6 @@
 # OpenWrt Buildroot Documentation Index
-# Source: https://github.com/openwrt/openwrt (commit: 0c0d6dd)
-# Generated: 2026-09-01 02:28 UTC
+# Source: https://github.com/openwrt/openwrt (commit: c1b3943)
+# Generated: 2026-10-01 08:41 UTC
 #
 # Package metadata and README files from the OpenWrt buildroot.
 #
@@ -10,6 +10,6 @@
 - [openwrt-buildroot-firmware.md](/openwrt-buildroot-docs/openwrt-buildroot-firmware.md): OpenWrt buildroot `firmware` — 16 packages
 - [openwrt-buildroot-kernel.md](/openwrt-buildroot-docs/openwrt-buildroot-kernel.md): OpenWrt buildroot `kernel` — 28 packages
 - [openwrt-buildroot-libs.md](/openwrt-buildroot-docs/openwrt-buildroot-libs.md): OpenWrt buildroot `libs` — 47 packages
-- [openwrt-buildroot-system.md](/openwrt-buildroot-docs/openwrt-buildroot-system.md): OpenWrt buildroot `system` — 20 packages
+- [openwrt-buildroot-system.md](/openwrt-buildroot-docs/openwrt-buildroot-system.md): OpenWrt buildroot `system` — 21 packages
 - [openwrt-buildroot-utils.md](/openwrt-buildroot-docs/openwrt-buildroot-utils.md): OpenWrt buildroot `utils` — 49 packages
-- [openwrt-buildroot-include-mk.md](/openwrt-buildroot-docs/openwrt-buildroot-include-mk.md): Build system .mk files — 31 documented
+- [openwrt-buildroot-include-mk.md](/openwrt-buildroot-docs/openwrt-buildroot-include-mk.md): Build system .mk files — 32 documented
```

## Changes in `openwrt-examples/llms.txt`

```diff
diff --git a/openwrt-examples/llms.txt b/openwrt-examples/llms.txt
index 0de452e..cd96877 100644
--- a/openwrt-examples/llms.txt
+++ b/openwrt-examples/llms.txt
@@ -1,6 +1,6 @@
 # OpenWrt Curated LuCI Application Examples
 # Source: https://github.com/openwrt/luci/tree/master/applications
-# Generated: 2026-09-01 02:28 UTC from LuCI commit 4c0a4ed
+# Generated: 2026-10-01 08:41 UTC from LuCI commit 32775cf
 #
 # Four apps selected for distinct pedagogical value. Together they cover the
 # full range of modern LuCI development patterns. All files are raw upstream
```

