# 

.DEFAULT_GOAL:=help
SHELL:=/bin/bash
GO111MODULE=off

# https://github.com/empirefox/protoc-gen-dart-ext
DET_LIB_NAME=protoc-gen-dart-ext
DET_LIB_BRANCH=master
DET_LIB_TAG=v1.0.0
DET_LIB=github.com/empirefox/$(DET_LIB_NAME)
DET_LIB_UPSTREAM=github.com/empirefox/$(DET_LIB_NAME)
DET_LIB_FSPATH=$(GOPATH)/src/$(DET_LIB)


# https://github.com/lyft/protoc-gen-star
GENSTAR_LIB_NAME=protoc-gen-star
GENSTAR_LIB_BRANCH=master
GENSTAR_LIB_TAG=v1.0.0
GENSTAR_LIB=github.com/lyft/$(GENSTAR_LIB_NAME)
GENSTAR_LIB_UPSTREAM=github.com/lyft/$(GENSTAR_LIB_NAME)
GENSTAR_LIB_FSPATH=$(GOPATH)/src/$(GENSTAR_LIB)


help:  ## Display this help
	# from: https://suva.sh/posts/well-documented-makefiles/
	@awk 'BEGIN {FS = ":.*##"; printf "\nUsage:\n  make \033[36m<target>\033[0m\n\nTargets:\n"} /^[a-zA-Z_-]+:.*?##/ { printf "  \033[36m%-10s\033[0m %s\n", $$1, $$2 }' $(MAKEFILE_LIST)

print: ### print

	@echo 	
	@echo DET_LIB_NAME :      $(DET_LIB_NAME)
	@echo DET_LIB_BRANCH :    $(DET_LIB_BRANCH)
	@echo DET_LIB_TAG :       $(DET_LIB_TAG)
	@echo DET_LIB :           $(DET_LIB)
	@echo DET_LIB_FSPATH  :   $(DET_LIB_FSPATH)
	@echo 

	@echo 	
	@echo GENSTAR_LIB_NAME :      $(GENSTAR_LIB_NAME)
	@echo GENSTAR_LIB_BRANCH :    $(GENSTAR_LIB_BRANCH)
	@echo GENSTAR_LIB_TAG :       $(GENSTAR_LIB_TAG)
	@echo GENSTAR_LIB :           $(GENSTAR_LIB)
	@echo GENSTAR_LIB_FSPATH  :   $(GENSTAR_LIB_FSPATH)
	@echo 

git-clone: ### git-clone

	mkdir -p $(DET_LIB_FSPATH)
	cd $(DET_LIB_FSPATH) && cd .. && rm -rf $(DET_LIB_NAME) && git clone ssh://git@$(DET_LIB).git
	cd $(DET_LIB_FSPATH) && git fetch --all --tags --prune
	#cd $(DET_LIB_FSPATH) && git checkout tags/$(DET_LIB_TAG)

git-clean: ### git-clean
	rm -rf $(DET_LIB_FSPATH)


genstar-git-clone:
	# gen-star
	mkdir -p $(GENSTAR_LIB_FSPATH)
	cd $(GENSTAR_LIB_FSPATH) && cd .. && rm -rf $(GENSTAR_LIB_NAME) && git clone ssh://git@$(GENSTAR_LIB).git
	cd $(GENSTAR_LIB_FSPATH) && git fetch --all --tags --prune

	cd $(GENSTAR_LIB_FSPATH) && make vendor

	# subs dependent on genstart
	#go get -u github.com/empirefox/protoc-gen-validate
	#go get -u github.com/TheThingsIndustries/protoc-gen-fieldmask

genstar-git-clean:
	rm -rf $(GENSTAR_LIB_FSPATH)


code-open: ### code-open
	code $(DET_LIB_FSPATH)

### DEPS

dep-modules:
	# Use GOMODULES
	cd $(DET_LIB_FSPATH) && GO111MODULE=on go get ./...

dep-nomodules: 
	# Not using go modules because some of these libs are not able to use it yet.
	go get -u github.com/Masterminds/sprig
	go get -u github.com/hashicorp/go-multierror
	go get -u github.com/lynn9388/supsub
	go get -u github.com/relvacode/iso8601
	go get -u github.com/stoewer/go-strcase
	go get -u github.com/thoas/go-funk

	go get -u github.com/elliotchance/pie
	
	go get -u github.com/empirefox/messageformat

# NOTE: MESSAGE_LIB depends on PLURAL_LIB
PLURAL_LIB=github.com/empirefox/makeplural
PLURAL_LIB_FSPATH=$(GOPATH)/src/$(PLURAL_LIB)
dep-sub-plural:
	# TODO: Currently busted.

	# print
	echo $(PLURAL_LIB_FSPATH)

	# clean
	rm -rf $(PLURAL_LIB_FSPATH)

	# build
	GO111MODULE=on go get -u $(PLURAL_LIB)
	cd $(PLURAL_LIB_FSPATH) && GO111MODULE=on go run make-plural.go
	cd $(PLURAL_LIB_FSPATH)/plural && GO111MODULE=on go test


MESSAGE_LIB=github.com/empirefox/messageformat
MESSAGE_LIB_FSPATH=$(GOPATH)/src/$(MESSAGE_LIB)
dep-sub-message:

	# print
	echo $(MESSAGE_LIB_FSPATH)
	
	# clean
	rm -rf $(MESSAGE_LIB_FSPATH)

	# build
	GO111MODULE=off go get -u $(MESSAGE_LIB)
	cd $(MESSAGE_LIB_FSPATH) && GO111MODULE=on go test

### GEN

gen-proto:
	# These core ones used seldom.

gen: ### gen
	# Currently staged. Order matters !

	# TO DO: Differentiates between Design time and Build Time in the workflow.
	# See here for Ordering hints: https://github.com/empirefox/protoc-gen-dart-ext/issues/1
	cd $(DET_LIB_FSPATH) && make gen_atom
	cd $(DET_LIB_FSPATH) && make gen_currency
	cd $(DET_LIB_FSPATH) && make gen_prefix
	cd $(DET_LIB_FSPATH) && make protoc
	cd $(DET_LIB_FSPATH) && make gen_golang
	cd $(DET_LIB_FSPATH) && make gen_plural

	# ZIP from ? https://physics.nist.gov/cuu/Units/units.html
	cd $(DET_LIB_FSPATH) && make gen_gtt_to_dart

gen-other:
	# Needs zip !
	#cd $(DET_LIB_FSPATH) && make gen_units_gtt

	# does nothing
	cd $(DET_LIB_FSPATH) && make gen_proto
	
	cd $(DET_LIB_FSPATH) && make gen_golang
	cd $(DET_LIB_FSPATH) && make gen_dart
	
	cd $(DET_LIB_FSPATH) && make gen_exports
	cd $(DET_LIB_FSPATH) && make gen_exports_go

go-run: ### go-run
	cd $(DET_LIB_FSPATH) && GO111MODULE=on go run main.go

flu-fix: ### flu-fix

	#code $(DET_LIB_FSPATH)/dart/pubspec.lock
	# then change all references from "flutter.cn" to "pub.dartlang.org"

	cd $(DET_LIB_FSPATH)/dart && flutter pub get

flu-run: ### flu-run
	cd $(DET_LIB_FSPATH)/dart && flutter run -d all

	
	
	
	

	
	
	


	
	