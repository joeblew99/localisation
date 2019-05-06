# https://github.com/empirefox/protoc-gen-dart-ext

.DEFAULT_GOAL:=help
SHELL:=/bin/bash
#GO111MODULE=on

# protoc-gen-dart-ext(DET)
DET_LIB_NAME=protoc-gen-dart-ext
DET_LIB_BRANCH=master
DET_LIB_TAG=v1.0.0
DET_LIB=github.com/empirefox/$(DET_LIB_NAME)
DET_LIB_UPSTREAM=github.com/empirefox/$(DET_LIB_NAME)
DET_LIB_FSPATH=$(GOPATH)/src/$(DET_LIB)




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

git-clone: ### git-clone

	mkdir -p $(DET_LIB_FSPATH)
	cd $(DET_LIB_FSPATH) && cd .. && rm -rf $(DET_LIB_NAME) && git clone ssh://git@$(DET_LIB).git
	cd $(DET_LIB_FSPATH) && git fetch --all --tags --prune
	#cd $(DET_LIB_FSPATH) && git checkout tags/$(DET_LIB_TAG)

git-clean: ### git-clean
	
	rm -rf $(DET_LIB_FSPATH)

code-open: ### code-open
	code $(DET_LIB_FSPATH)

flutter-fix:
	code $(DET_LIB_FSPATH)/dartpubspec.lock
	# then change all references from "flutter.cn" to "pub.dartlang.org"

dep:
	# Not using go modules because some of these libs are not able to use it yet.
	go get -u github.com/Masterminds/sprig
	go get -u github.com/hashicorp/go-multierror
	go get -u github.com/lynn9388/supsub
	go get -u github.com/relvacode/iso8601
	go get -u github.com/stoewer/go-strcase

	go get -u github.com/thoas/go-funk
	go get -u github.com/empirefox/messageformat
	
	go get -u github.com/lyft/protoc-gen-star

dep-clean:
	
	