
.DEFAULT_GOAL:=help
SHELL:=/bin/bash
GO111MODULE=on


# https://github.com/bregydoc/gtranslate
GTR_LIB_NAME=gtranslate
GTR_LIB=github.com/bregydoc/$(GTR_LIB_NAME)
GTR_LIB_PATH=$(GOPATH)/src/$(GTR_LIB)
GTR_LIB_BUILD_PATH=$(GTR_LIB_PATH)/build
GTR_LIB_DOC=https://$(GTR_LIB)




help:  ## Display this help
	# from: https://suva.sh/posts/well-documented-makefiles/
	@awk 'BEGIN {FS = ":.*##"; printf "\nUsage:\n  make \033[36m<target>\033[0m\n\nTargets:\n"} /^[a-zA-Z_-]+:.*?##/ { printf "  \033[36m%-10s\033[0m %s\n", $$1, $$2 }' $(MAKEFILE_LIST)


print:


	@echo
	@echo /gtr-l10n
	@echo 'GTR_LIB_NAME              $(GTR_LIB_NAME)'
	@echo 'GTR_LIB                   $(GTR_LIB)'
	@echo 'GTR_LIB_PATH              $(GTR_LIB_PATH)'
	@echo 'GTR_LIB_BUILD_PATH        $(GTR_LIB_BUILD_PATH)'
	@echo 'GTR_LIB_DOC               $(GTR_LIB_DOC)'
	@echo

git-clone: ### git-clone
	mkdir -p $(GTR_LIB_PATH)
	cd $(GTR_LIB_PATH) && cd .. && rm -rf $(GTR_LIB_NAME) && git clone ssh://git@$(GTR_LIB).git


git-clean: ### git-clean
	rm -rf $(FLU_LIB_PATH)
	rm -rf $(GTR_LIB_PATH)

bin-clean:
	rm -rf $(PWD)/bin

### GTR

gtr-clean: ### gtr-web-clean
	rm -rf $(GTR_LIB_BUILD_PATH)

gtr-code: ### gtr-code
	code $(GTR_LIB_PATH)

gtr-server-run: ### gtr-server-run
	mkdir -p $(GTR_LIB_PATH)
	mkdir -p $(GTR_LIB_PATH)/db
	mkdir -p $(GTR_LIB_PATH)/config

	# configs
	cp i18n-indexer.yml $(GTR_LIB_PATH)
	cp bolt.db $(GTR_LIB_PATH)/db
	cp projects.example.yml $(GTR_LIB_PATH)/config/projects.yml

	# build to root
	go mod download
	cd $(GTR_LIB_PATH) && go build -o ./server ./cmd/server/main.go 

	# run
	cd $(GTR_LIB_PATH) && ./server

gtr-web-build:
	cd $(GTR_LIB_PATH) && build/docker.sh

gtr-web-open: ### gtr-web-open
	open http://localhost:8000
	
gtr-bolter:
	go get -u github.com/hasit/bolter
	#bolter -f $(GTR_LIB_PATH)/db/bolt.db
	bolter -f $(GTR_LIB_PATH)/db/bleve/store









