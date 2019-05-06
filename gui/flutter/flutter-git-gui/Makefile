
#https://github.com/pd4d10/git-touch

GIT_FLU_BIN_NAME=git-flu
GIT_FLU_LIB_NAME=git-touch
GIT_FLU_LIB_BRANCH=master
GIT_FLU_LIB_TAG=
GIT_FLU_LIB=github.com/pd4d10/$(GIT_FLU_LIB_NAME)
GIT_FLU_LIB_FSPATH=$(GOPATH)/src/$(GIT_FLU_LIB)


git-flu-print:
	@echo 
	@echo GIT_FLU_BIN_NAME :$(GIT_FLU_BIN_NAME)
	@echo GIT_FLU_LIB_NAME :$(GIT_FLU_LIB_NAME)
	@echo GIT_FLU_LIB_BRANCH :$(GIT_FLU_LIB_BRANCH)
	@echo GIT_FLU_LIB_TAG :$(GIT_FLU_LIB_TAG)
	@echo GIT_FLU_LIB  : $(GIT_FLU_LIB)
	@echo GIT_FLU_LIB_FSPATH  : $(GIT_FLU_LIB_FSPATH)
	@echo

git-flu-git-clone:
	# cen flutter-chat
	mkdir -p $(GIT_FLU_LIB_FSPATH)
	cd $(GIT_FLU_LIB_FSPATH) && cd .. && rm -rf $(GIT_FLU_LIB_NAME) && git clone ssh://git@$(GIT_FLU_LIB).git

	# no upstream for now

git-flu-git-clean:
	# removes everything
	rm -rf $(GIT_FLU_LIB_FSPATH)
	#rm -rf $(CENF_LIB_FSPATH__FORK)

run:
	cd $(GIT_FLU_LIB_FSPATH) && flutter run -d all
