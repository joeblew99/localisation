
.DEFAULT_GOAL:=help
SHELL:=/bin/bash
GO111MODULE=on

# https://github.com/yurykabanov/i18n-indexer
IND_LIB_NAME=i18n-indexer
IND_LIB=github.com/yurykabanov/$(IND_LIB_NAME)
IND_LIB_PATH=$(GOPATH)/src/$(IND_LIB)
IND_LIB_BUILD_PATH=$(IND_LIB_PATH)/build
IND_LIB_DOC=https://$(IND_LIB)


help:  ## Display this help
	# from: https://suva.sh/posts/well-documented-makefiles/
	@awk 'BEGIN {FS = ":.*##"; printf "\nUsage:\n  make \033[36m<target>\033[0m\n\nTargets:\n"} /^[a-zA-Z_-]+:.*?##/ { printf "  \033[36m%-10s\033[0m %s\n", $$1, $$2 }' $(MAKEFILE_LIST)

print:

	@echo
	@echo /ind-l10n
	@echo 'IND_LIB_NAME              $(IND_LIB_NAME)'
	@echo 'IND_LIB                   $(IND_LIB)'
	@echo 'IND_LIB_PATH              $(IND_LIB_PATH)'
	@echo 'IND_LIB_BUILD_PATH        $(IND_LIB_BUILD_PATH)'
	@echo 'IND_LIB_DOC               $(IND_LIB_DOC)'
	@echo

git-clone: ### git-clone
	mkdir -p $(IND_LIB_PATH)
	cd $(IND_LIB_PATH) && cd .. && rm -rf $(IND_LIB_NAME) && git clone ssh://git@$(IND_LIB).git

git-clean: ### git-clean
	rm -rf $(IND_LIB_PATH)

bin-clean:
	rm -rf $(PWD)/bin

### LOCALIZE
# https://mail.google.com/mail/u/0/#inbox/FMfcgxwCgLvrdNknvHrlqhrgLbXvKHQZ

# This quite a good Translation Server. Much simpler and easier than the others and handles ARB properly.

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

ind-clean: ### ind-web-clean
	rm -rf $(IND_LIB_BUILD_PATH)

ind-code: ### ind-code
	code $(IND_LIB_PATH)











