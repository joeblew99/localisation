
.DEFAULT_GOAL:=help
SHELL:=/bin/bash
GO111MODULE=on




FLU_LIB_NAME=flutter_i18n_complete
FLU_LIB=github.com/ashour/$(FLU_LIB_NAME)
FLU_LIB_PATH=$(GOPATH)/src/$(FLU_LIB)
FLU_LIB_EX_PATH=$(FLU_LIB_PATH)/example/test_app
FLU_LIB_DOC=https://$(FLU_LIB)

# https://github.com/bregydoc/gtranslate
GO_LIB_NAME=gtranslate
GO_LIB=github.com/bregydoc/$(GO_LIB_NAME)
GO_LIB_PATH=$(GOPATH)/src/$(GO_LIB)
GO_LIB_BUILD_PATH=$(GO_LIB_PATH)/build
GO_LIB_DOC=https://$(GO_LIB)




help:  ## Display this help
	# from: https://suva.sh/posts/well-documented-makefiles/
	@awk 'BEGIN {FS = ":.*##"; printf "\nUsage:\n  make \033[36m<target>\033[0m\n\nTargets:\n"} /^[a-zA-Z_-]+:.*?##/ { printf "  \033[36m%-10s\033[0m %s\n", $$1, $$2 }' $(MAKEFILE_LIST)


print:

	@echo
	@echo /FLU
	@echo 'FLU_LIB_NAME              $(FLU_LIB_NAME)'
	@echo 'FLU_LIB                   $(FLU_LIB)'
	@echo 'FLU_LIB_PATH              $(FLU_LIB_PATH)'
	@echo 'FLU_LIB_EX_PATH           $(FLU_LIB_EX_PATH)'
	@echo 'FLU_LIB_DOC               $(FLU_LIB_DOC)'
	@echo

	@echo
	@echo /go-l10n
	@echo 'GO_LIB_NAME              $(GO_LIB_NAME)'
	@echo 'GO_LIB                   $(GO_LIB)'
	@echo 'GO_LIB_PATH              $(GO_LIB_PATH)'
	@echo 'GO_LIB_BUILD_PATH        $(GO_LIB_BUILD_PATH)'
	@echo 'GO_LIB_DOC               $(GO_LIB_DOC)'
	@echo

git-clone: ### git-clone
	mkdir -p $(FLU_LIB_PATH)
	cd $(FLU_LIB_PATH) && cd .. && rm -rf $(FLU_LIB_NAME) && git clone ssh://git@$(FLU_LIB).git

	mkdir -p $(GO_LIB_PATH)
	cd $(GO_LIB_PATH) && cd .. && rm -rf $(GO_LIB_NAME) && git clone ssh://git@$(GO_LIB).git

	

git-clean: ### git-clean
	rm -rf $(FLU_LIB_PATH)
	rm -rf $(GO_LIB_PATH)

bin-clean:
	rm -rf $(PWD)/bin

ph-dep::
	brew tap phrase/brewed
	brew install phraseapp

phr-run:
	cd $(FLU_LIB_PATH) && phraseapp

trans:
	# Generating the Messages ARB file
	mkdir -p $(FLU_LIB_PATH)/lib/l10n
	cd $(FLU_LIB_PATH) && flutter pub pub run intl_translation:extract_to_arb --output-dir=lib/l10n lib/src/lang/sit_localizations.dart

### FLU

flu-doc: ### flu-doc
	open $(FLU_LIB_DOC)

flu-code: ### flu-code
	code $(FLU_LIB_PATH)

flu-dep:
	cd $(FLU_LIB_PATH) && flutter packages upgrade

flu-mob-run: ### flu-mob-run
	cd $(FLU_LIB_PATH) && flutter run -d all
	
flu-desk-run: ### flu-desk-run
	#cd $(FLU_LIB_PATH) && hover init $(FLU_LIB)
	cd $(FLU_LIB_PATH) && hover run

flu-desk-build: ### flu-desk-run
	cd $(FLU_LIB_PATH) && hover build
	open $(FLU_LIB_PATH)/desktop/build/outputs/darwin/$(FLU_LIB_NAME)


### LN

go-clean: ### go-web-clean
	rm -rf $(GO_LIB_BUILD_PATH)

go-code: ### go-code
	code $(GO_LIB_PATH)

go-server-run: ### go-server-run
	mkdir -p $(GO_LIB_PATH)
	mkdir -p $(GO_LIB_PATH)/db
	mkdir -p $(GO_LIB_PATH)/config

	# configs
	cp i18n-indexer.yml $(GO_LIB_PATH)
	cp bolt.db $(GO_LIB_PATH)/db
	cp projects.example.yml $(GO_LIB_PATH)/config/projects.yml

	# build to root
	go mod download
	cd $(GO_LIB_PATH) && go build -o ./server ./cmd/server/main.go 

	# run
	cd $(GO_LIB_PATH) && ./server

go-web-build:
	cd $(GO_LIB_PATH) && build/docker.sh

go-web-open: ### go-web-open
	open http://localhost:8000
	
go-bolter:
	go get -u github.com/hasit/bolter
	#bolter -f $(GO_LIB_PATH)/db/bolt.db
	bolter -f $(GO_LIB_PATH)/db/bleve/store









