#
# Makefile fragment for Linux 2.6
# Broadcom DHD Driver
#
# Copyright (C) 1999-2010, Broadcom Corporation
# 
#      Unless you and Broadcom execute a separate written software license
# agreement governing use of this software, this software is licensed to you
# under the terms of the GNU General Public License version 2 (the "GPL"),
# available at http://www.broadcom.com/licenses/GPLv2.php, with the
# following added to such license:
# 
#      As a special exception, the copyright holders of this software give you
# permission to link this software with independent modules, and to copy and
# distribute the resulting executable under terms of your choice, provided that
# you also meet, for each linked independent module, the terms and conditions of
# the license of that module.  An independent module is a module which is not
# derived from this software.  The special exception does not apply to any
# modifications of the software.
# 
#      Notwithstanding the above, under no circumstances may you combine this
# software in any way with any other Broadcom software provided under a license
# other than the GPL, without Broadcom's express prior written consent.
#
# $Id: makefile.26,v 1.1.144.1.108.1 2010/04/14 23:34:04 Exp $

#WIFI_ICS
SRCBASE := drivers/net/wireless/bcm4329_presto

WLANCFLAGS = -DLINUX -DSRCBASE=\"$(SRCBASE)\" -DBCMDRIVER -DBCMDONGLEHOST      \
	-DDHDTHREAD -DBCMWPA2 -DUNRELEASEDCHIP -DDHD_GPL -DDHD_SCHED -DBDC     \
	-DTOE -DDHD_BCMEVENTS -DSHOW_EVENTS -DBCMSDIO -DBCMLXSDMMC             \
	-DBCMPLATFORM_BUS -DEMBEDDED_PLATFORM -DOOB_INTR_ONLY -DHW_OOB         \
	-DMMC_SDIO_ABORT -DCUSTOM_OOB_GPIO_NUM=$(CONFIG_BCM4329_OOB_GPIO)      \
	-DARP_OFFLOAD_SUPPORT -DPKT_FILTER_SUPPORT -DPNO_SUPPORT               \
	-DGET_CUSTOM_MAC_ENABLE -DCUSTOMER_HW_PT                               \
	-fshort-wchar -Wall -Wstrict-prototypes 
#-Werror # CONFIG_PANTECH_WIFI_BROADCOM_BCM4329 //20100826 thkim_wifi for wifi

WLANCFLAGS += -I$(SRCBASE)/dhd/sys \
	-I$(SRCBASE)/dongle  \
	-I$(SRCBASE)/include \
	-I$(SRCBASE)/include/proto \
	-I$(SRCBASE)/shared \
	-I$(SRCBASE)/wl/sys

WLANOFILES := \
	bcmsdio/sys/bcmsdh.o \
	bcmsdio/sys/bcmsdh_linux.o \
	bcmsdio/sys/bcmsdh_sdmmc.o \
	bcmsdio/sys/bcmsdh_sdmmc_linux.o \
	dhd/sys/dhd_cdc.o \
	dhd/sys/dhd_common.o \
	dhd/sys/dhd_custom_gpio.o \
	dhd/sys/dhd_linux.o \
	dhd/sys/dhd_linux_sched.o \
	dhd/sys/dhd_sdio.o \
	shared/aiutils.o \
	shared/bcmutils.o \
	shared/bcmwifi.o \
	shared/hndpmu.o \
	shared/linux_osl.o \
	shared/sbutils.o \
	shared/siutils.o \
	wl/sys/wl_iw.o


ifeq ($(CONFIG_BCM4329_DEBUG),y)
WLANCFLAGS += -DDHD_DEBUG -DSDTEST
endif

ifeq ($(CONFIG_BCM4329_SOFTAP),y)
WLANCFLAGS += -DSOFTAP
endif

ifeq ($(CONFIG_WIFI_CONTROL_FUNC),y)
WLANCFLAGS +=  -DCUSTOMER_HW2 -DCONFIG_MACH_MAHIMAHI
ifeq ($(CONFIG_WIFI_MEM_PREALLOC),y)
WLANCFLAGS += -DDHD_USE_STATIC_BUF
endif
endif

ifeq ($(CONFIG_BCM4329_USE_CSCAN),y)
WLANCFLAGS += -DCSCAN
endif

ifeq ($(CONFIG_MMC_MSM7X00A),y)
WLANCFLAGS += -Dlinux
WLANCFLAGS += -DDHD_SDALIGN=64 -DMAX_HDR_READ=64 -DDHD_FIRSTREAD=64
endif

#PS11_WIFI added for sending CIQ events
#WLANCFLAGS += -DATT_CIQ_SUPPORT

#PS11_WIFI added for AP certification
#WLANCFLAGS += -DAP_CERT_FOR_BG

#PS11_WIFI added for sending station block event
WLANCFLAGS += -DATT_SOFTAP_EVENT

obj-$(CONFIG_BCM4329) += wlan.o
wlan-objs = $(WLANOFILES)
EXTRA_CFLAGS = $(WLANCFLAGS)
EXTRA_LDFLAGS += --strip-debug
