# OpenWrt Buildroot: Build System Include Files

> **Source:** https://github.com/openwrt/openwrt/tree/master/include
> **Generated:** 2026-04-01 03:15 UTC from commit `cd0f6dd`

Core build system Makefile fragments.

---

## `autotools.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2007-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/autotools.mk

---

## `debug.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2007-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/debug.mk

---

## `depends.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2007-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/depends.mk

---

## `download.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2006-2012 OpenWrt.org
Copyright (C) 2016 LEDE project
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/download.mk

---

## `feeds.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2014 OpenWrt.org
Copyright (C) 2016 LEDE Project
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/feeds.mk

---

## `hardening.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2015-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/hardening.mk

---

## `host-build.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2006-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/host-build.mk

---

## `image.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2006-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/image.mk

---

## `kernel-build.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2006-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/kernel-build.mk

---

## `kernel-defaults.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2006-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/kernel-defaults.mk

---

## `kernel.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2006-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/kernel.mk

---

## `meson.mk`

```
To build your package using meson:
include $(INCLUDE_DIR)/meson.mk
MESON_ARGS+=-Dfoo -Dbar=baz
To pass additional environment variables to meson:
MESON_VARS+=FOO=bar
Default configure/compile/install targets are provided, but can be
overwritten if required:
define Build/Configure
$(call Build/Configure/Meson)
...
endef
same for Build/Compile and Build/Install
Host packages are built in the same fashion, just use these vars instead:
MESON_HOST_ARGS+=-Dfoo -Dbar=baz
MESON_HOST_VARS+=FOO=bar
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/meson.mk

---

## `netfilter.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2006-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/netfilter.mk

---

## `nls.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2011-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/nls.mk

---

## `openssl-module.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2022-2023 Enéas Ulir de Queiroz
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/openssl-module.mk

---

## `package-bin.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2007-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/package-bin.mk

---

## `package-defaults.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2006-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/package-defaults.mk

---

## `package-dumpinfo.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2006-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/package-dumpinfo.mk

---

## `package-pack.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2006-2022 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/package-pack.mk

---

## `package-seccomp.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2015-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/package-seccomp.mk

---

## `package.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2006-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/package.mk

---

## `prereq-build.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2006-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/prereq-build.mk

---

## `prereq.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2006-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/prereq.mk

---

## `quilt.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2007-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/quilt.mk

---

## `subdir.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2007-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/subdir.mk

---

## `target.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2007-2008 OpenWrt.org
Copyright (C) 2016 LEDE Project
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/target.mk

---

## `toolchain-build.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2009-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/toolchain-build.mk

---

## `toplevel.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2007-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/toplevel.mk

---

## `unpack.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2006-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/unpack.mk

---

## `verbose.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2006-2020 OpenWrt.org
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/verbose.mk

---

## `version.mk`

```
SPDX-License-Identifier: GPL-2.0-only
Copyright (C) 2012-2015 OpenWrt.org
Copyright (C) 2016 LEDE Project
```

> Source: https://github.com/openwrt/openwrt/blob/master/include/version.mk

---

