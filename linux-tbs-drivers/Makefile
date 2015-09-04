CURRENT_DIR := $(shell pwd)
BUILD_DIR := $(CURRENT_DIR)/v4l
BITS=$(shell uname -m)
TMP ?= /tmp

ifeq ($(EDITOR),)
  ifeq ($(VISUAL),)
	EDITOR := vi
  else
	EDITOR := $(VISUAL) -w
  endif
endif

all:
	@echo "Build TBS drivers for v4l $(BITS)"
	@cd $(CURRENT_DIR) && v4l/tbs-$(BITS).sh
	$(MAKE) -C $(BUILD_DIR)

build64:
	cd $(CURRENT_DIR) && v4l/tbs-x86_64.sh	

build32:
	cd $(CURRENT_DIR) && v4l/tbs-x86.sh

build32v3:
	cd $(CURRENT_DIR) && v4l/tbs-x86_r3.sh

install:
	$(MAKE) -C $(BUILD_DIR) install

# Hmm, .PHONY does not work with wildcard rules :-(
SPECS = media-specs

.PHONY: $(SPECS)

$(SPECS):
	$(MAKE) -C $(BUILD_DIR) $(MAKECMDGOALS)

%::
	$(MAKE) -C $(BUILD_DIR) $(MAKECMDGOALS)

download untar::
	$(MAKE) -C linux/ $(MAKECMDGOALS)

dir::
	$(MAKE) -C linux/ $(MAKECMDGOALS) DIR="../$(DIR)"
