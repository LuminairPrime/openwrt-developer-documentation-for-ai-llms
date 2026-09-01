# OpenWrt Buildroot: `firmware` packages

> **Source:** https://github.com/openwrt/openwrt/tree/master/package/firmware
> **Generated:** 2026-09-01 02:28 UTC from commit `0c0d6dd`

---

## `ath10k-ct-firmware`

| Field | Value |
|---|---|
| Version | 2023.04.04 |

> Source: https://github.com/openwrt/openwrt/tree/master/package/firmware/ath10k-ct-firmware

---

## `ath11k-firmware`

| Field | Value |
|---|---|
| Maintainer | Robert Marko <robimarko@gmail.com> include $(INCLUDE_DIR)/[package.mk](/openwrt-buildroot-docs/openwrt-buildroot-include-mk.md) |
| Source URL | https://git.codelinaro.org/clo/ath-firmware/ath11k-firmware.git |

> Source: https://github.com/openwrt/openwrt/tree/master/package/firmware/ath11k-firmware

---

## `broadcom-sprom`

| Field | Value |
|---|---|
| Maintainer | Álvaro Fernández Rojas <noltari@gmail.com> include $(INCLUDE_DIR)/[package.mk](/openwrt-buildroot-docs/openwrt-buildroot-include-mk.md) define Package/broadcom-sprom-default SECTION:=firmware CATEGORY:=Firmware endef define Build/Compile true endef # BCM4306  |
| Source URL | https://github.com/openwrt/broadcom-sprom.git |

> Source: https://github.com/openwrt/openwrt/tree/master/package/firmware/broadcom-sprom

---

## `cypress-firmware`

| Field | Value |
|---|---|
| Maintainer | Álvaro Fernández Rojas <noltari@gmail.com> |
| Source URL | https://github.com/Infineon/ifx-linux-firmware/ |

> Source: https://github.com/openwrt/openwrt/tree/master/package/firmware/cypress-firmware

---

## `cypress-nvram`

| Field | Value |
|---|---|
| Maintainer | Álvaro Fernández Rojas <noltari@gmail.com> include $(INCLUDE_DIR)/[package.mk](/openwrt-buildroot-docs/openwrt-buildroot-include-mk.md) define Package/cypress-nvram-default SECTION:=firmware CATEGORY:=Firmware endef define Build/Compile true endef # Cypress 4 |

> Source: https://github.com/openwrt/openwrt/tree/master/package/firmware/cypress-nvram

---

## `firmware-imx`

| Field | Value |
|---|---|
| Version | 8.28-994fa14 |
| License | LA_OPT_NXP_Software_License |
| Source URL | https://www.nxp.com/lgfiles/NMG/MAD/YOCTO/ |

> Source: https://github.com/openwrt/openwrt/tree/master/package/firmware/firmware-imx

---

## `intel-microcode`

| Field | Value |
|---|---|
| Version | 20260227 |
| Source URL | @DEBIAN/pool/non-free-firmware/i/intel-microcode/ |

> Source: https://github.com/openwrt/openwrt/tree/master/package/firmware/intel-microcode

---

## `ipq-wifi`

> Source: https://github.com/openwrt/openwrt/tree/master/package/firmware/ipq-wifi

---

## `linux-firmware`

| Field | Value |
|---|---|
| Version | 20260810 |
| Maintainer | Felix Fietkau <nbd@nbd.name> |
| Source URL | @KERNEL/linux/kernel/firmware |

> Source: https://github.com/openwrt/openwrt/tree/master/package/firmware/linux-firmware

---

## `mipi-dbi`

| Field | Value |
|---|---|
| License | GPL-2.0-or-later |
| Maintainer | Matt Eaton <linux@divinehawk.com> include $(INCLUDE_DIR)/[package.mk](/openwrt-buildroot-docs/openwrt-buildroot-include-mk.md) define Package/mipi-dbi-default SECTION:=firmware CATEGORY:=Firmware endef define Build/Compile endef # From https://github.com/notr |

> Source: https://github.com/openwrt/openwrt/tree/master/package/firmware/mipi-dbi

---

## `murata-firmware`

| Field | Value |
|---|---|
| Maintainer | Thomas Richard <thomas.richard@bootlin.com> |
| Source URL | https://github.com/murata-wireless/cyw-fmac-fw.git |

> Source: https://github.com/openwrt/openwrt/tree/master/package/firmware/murata-firmware

---

## `murata-nvram`

| Field | Value |
|---|---|
| Maintainer | Thomas Richard <thomas.richard@bootlin.com> |
| Source URL | https://github.com/murata-wireless/cyw-fmac-nvram.git |

> Source: https://github.com/openwrt/openwrt/tree/master/package/firmware/murata-nvram

---

## `omnia-mcu-firmware`

| Field | Value |
|---|---|
| Version | 4.1 |
| License | GPL-3.0-or-later |
| Maintainer | Marek Mojik <marek.mojik@nic.cz> |
| Source URL | https://gitlab.nic.cz/turris/hw/$(PKG_DISTNAME)/-/releases/v$(PKG_VERSION)/downloads/ |

> Source: https://github.com/openwrt/openwrt/tree/master/package/firmware/omnia-mcu-firmware

---

## `prism54-firmware`

> Source: https://github.com/openwrt/openwrt/tree/master/package/firmware/prism54-firmware

---

## `rtl826x-firmware`

| Field | Value |
|---|---|
| License | GPL-2.0-only include $(INCLUDE_DIR)/[package.mk](/openwrt-buildroot-docs/openwrt-buildroot-include-mk.md) define Build/Compile (set -e; cd $(PKG_BUILD_DIR); $(HOSTCC) rtl8261n_rtl8264b.c phy_patch.c -o phy_patch; ./phy_patch ) endef define Package/rtl826x-fir |
| Maintainer | Balázs Triszka <info@balika011.hu> |
| Source URL | https://github.com/balika011/realtek_phy_firmware |

> Source: https://github.com/openwrt/openwrt/tree/master/package/firmware/rtl826x-firmware

---

## `wireless-regdb`

| Field | Value |
|---|---|
| Version | 2026.05.30 |
| License | ISC |
| Maintainer | Felix Fietkau <nbd@nbd.name> include $(INCLUDE_DIR)/[package.mk](/openwrt-buildroot-docs/openwrt-buildroot-include-mk.md) define Package/wireless-regdb PKGARCH:=all SECTION:=firmware CATEGORY:=Firmware URL:=https://git.kernel.org/pub/scm/linux/kernel/git/wens |
| Source URL | @KERNEL/software/network/wireless-regdb/ |

> Source: https://github.com/openwrt/openwrt/tree/master/package/firmware/wireless-regdb

---

