
.DEFAULT_GOAL:=help
SHELL:=/bin/bash
GO111MODULE=on


# github.com/ashour/flutter_i18n_complete
# blog: https://phraseapp.com/blog/posts/how-to-internationalize-a-flutter-app/


FLU_LIB_NAME=flutter_i18n_complete
FLU_LIB=github.com/ashour/$(FLU_LIB_NAME)
FLU_LIB_PATH=$(GOPATH)/src/$(FLU_LIB)
FLU_LIB_EX_PATH=$(FLU_LIB_PATH)/example/test_app
FLU_LIB_TRANS_PATH=$(FLU_LIB_PATH)/lib/l10n
FLU_LIB_DOC=https://$(FLU_LIB)

# https://github.com/yurykabanov/i18n-indexer
GO_LIB_NAME=i18n-indexer
GO_LIB=github.com/yurykabanov/$(GO_LIB_NAME)
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
	@echo 'FLU_LIB_TRANS_PATH        $(FLU_LIB_TRANS_PATH)'
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

### LOCALIZE
# https://mail.google.com/mail/u/0/#inbox/FMfcgxwCgLvrdNknvHrlqhrgLbXvKHQZ

loc-open:
	open https://localise.biz/dashboard/project/init?p=67430

loc-push:
	curl https://localise.biz/api/import/arb?locale=en --data-binary $(FLU_LIB_PATH)/lib/l10n/messages_en.dart

loc-pull:
	 curl https://localise.biz/api/export/locale/en.arb


### TRANS
tran-build: ### tran-build
	go build -o $(GOPATH)/bin/tran main.go

tran-ls:
	cd $(FLU_LIB_PATH)/lib/l10n && ls -al

tran-send:
	go run main.go

	# Now open each in Compare mode :)
	#/Users/apple/workspace/go/src/github.com/ashour/flutter_i18n_complete/lib/l10n/intl_messages_en.arb
	#/Users/apple/workspace/go/src/github.com/ashour/flutter_i18n_complete/lib/l10n/intl_messages_de.arb
	#File: Compare Active File With ...
tran-diff:
	cd $(FLU_LIB_PATH)/lib/l10n && code -d intl_messages_en.arb intl_messages_ar.arb

tran-extract:
	# Generating the Messages ARB file
	mkdir -p $(FLU_LIB_PATH)/lib/l10n
	cd $(FLU_LIB_PATH) && flutter pub pub run intl_translation:extract_to_arb --output-dir=lib/l10n lib/src/lang/sit_localizations.dart

tran-gen:
	# copy exisiting just in case we screw up
	rm -rf $(FLU_LIB_PATH)/lib/l10n_temp
	mkdir -p $(FLU_LIB_PATH)/lib/l10n_temp

	cp -r $(FLU_LIB_PATH)/lib/l10n $(FLU_LIB_PATH)/lib/l10n_temp
	cd $(FLU_LIB_PATH) && flutter pub pub run intl_translation:generate_from_arb lib/src/lang/sit_localizations.dart lib/l10n/*.arb --output-dir=lib/l10n
### GO Indexer

go-clean: ### go-web-clean
	rm -rf $(GO_LIB_BUILD_PATH)

go-code: ### go-code
	code $(GO_LIB_PATH)











