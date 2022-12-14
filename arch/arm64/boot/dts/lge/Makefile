# Per Platform
ifeq ($(CONFIG_MACH_MSM8998_LUCY),y)
DTS_PROJECT := msm8998-lucy
endif
ifeq ($(CONFIG_MACH_MSM8998_JOAN),y)
DTS_PROJECT := msm8998-joan
endif

# phoenix_sb_jp & lgu_kr use CONFIG_BUILD_ARM64_DT_OVERLAY(DTBO)
ifeq ($(CONFIG_MACH_MSM8998_PHOENIX),y)
ifeq ($(CONFIG_BUILD_ARM64_DT_OVERLAY),y)
DTS_PROJECT := msm8998-phoenix_overlay
else
DTS_PROJECT := msm8998-phoenix
endif
endif

# Per Device
ifeq ($(CONFIG_MACH_MSM8998_LUCY_KR),y)
DTS_TARGET := msm8998-lucy_kr
endif
ifeq ($(CONFIG_MACH_MSM8998_LUCY_DCM_JP),y)
DTS_TARGET := msm8998-lucy_dcm_jp
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_KR),y)
DTS_TARGET := msm8998-joan_kr
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_VZW),y)
DTS_TARGET := msm8998-joan_vzw
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_ATT_US),y)
DTS_TARGET := msm8998-joan_att_us
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_SPR_US),y)
DTS_TARGET := msm8998-joan_spr_us
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_NAO_US),y)
DTS_TARGET := msm8998-joan_nao_us
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_TMO_US),y)
DTS_TARGET := msm8998-joan_tmo_us
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_CLR_PR),y)
DTS_TARGET := msm8998-joan_tmo_us
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_GLOBAL_COM),y)
DTS_TARGET := msm8998-joan_global_com
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_GLOBAL_CA),y)
DTS_TARGET := msm8998-joan_global_ca
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_ACG_US),y)
DTS_TARGET := msm8998-joan_acg_us
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_KDDI_JP),y)
DTS_TARGET := msm8998-joan_kddi_jp
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_DCM_JP),y)
DTS_TARGET := msm8998-joan_dcm_jp
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_GLOBAL_LDU),y)
DTS_TARGET := msm8998-joan_global_ldu
endif

ifeq ($(CONFIG_MACH_MSM8998_PHOENIX_LAO_COM),y)
DTS_TARGET := msm8998-phoenix_lao_com
endif

ifeq ($(CONFIG_MACH_MSM8998_PHOENIX_SB_JP),y)
DTS_TARGET := msm8998-phoenix_sb_jp_overlay
endif

ifeq ($(CONFIG_MACH_MSM8998_PHOENIX_LGU_KR),y)
DTS_TARGET := msm8998-phoenix_lgu_kr_overlay
endif

ALL_DTS := $(notdir $(wildcard echo $(srctree)/$(src)/$(DTS_PROJECT)/$(DTS_TARGET)/*.dts))
ifeq ($(CONFIG_BUILD_ARM64_DT_OVERLAY),y)
dtbo-y += $(patsubst %.dts,%.dtbo,$(ALL_DTS))

DTB_NAMES := $(subst $\",,$(CONFIG_BUILD_ARM_APPENDED_DTB_IMAGE_NAMES))
ifneq ($(DTB_NAMES),)
DTB_LIST := $(addsuffix .dtbo,$(DTB_NAMES))
else
DTB_LIST := $(dtbo-y)
endif

always  := $(dtbo-y)

$(obj)/%.dtbo: $(src)/$(DTS_PROJECT)/$(DTS_TARGET)/%.dts FORCE
	$(call if_changed_dep,dtc)
	$(call if_changed,dtbo_verify)
else
dtb-y += $(patsubst %.dts,%.dtb,$(ALL_DTS))

DTB_NAMES := $(subst $\",,$(CONFIG_BUILD_ARM_APPENDED_DTB_IMAGE_NAMES))
ifneq ($(DTB_NAMES),)
DTB_LIST := $(addsuffix .dtb,$(DTB_NAMES))
else
DTB_LIST := $(dtb-y)
endif

always  := $(addprefix ../,$(DTB_LIST))

$(obj)/../%.dtb: $(src)/$(DTS_PROJECT)/$(DTS_TARGET)/%.dts FORCE
	$(call if_changed_dep,dtc)
endif
clean-files := *.dtbo *.dtb
