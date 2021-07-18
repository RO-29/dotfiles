ALL_DIR=cd $(dir) && (ls -d -1 * | grep -v golang-libraries | grep -v Makefile | grep -v sib_go-*.code-workspace)
ALL_COMMAND=$(ALL_DIR) | xargs -n 1 -I {} $(1)
ALL_RUN=$(call ALL_COMMAND,sh -c 'echo {} && cd {} && $(1)')
.PHONY: all-git-commit
all-git-commit:
	$(call ALL_RUN,git add go.mod go.sum Makefile* .github/ ruleguard/ Dockerfile && git commit -m "update dependencies")
all-git-checkout:
	$(call ALL_RUN,git checkout go.mod go.sum)
all-git-rebase-dev:
	$(call ALL_RUN,git pull --rebase origin dev)
all-git-pull-push:
	$(call ALL_RUN,git pull && git push)
all-git-rebase-master:
	$(call ALL_RUN,git checkout master && git pull --rebase origin master && git checkout dev)
all-git-commit-common-files:
	$(call ALL_RUN,git add .travis/ Makefile* && git commit -m "update common files")
all-git-commit-golang-lib:
	$(call ALL_RUN,git add go.mod go.sum && git commit -m "update golang libraries")

#GOLANG_LIBS_COMMON_OPS
.PHONY: all-run
all-run:
	$(eval COMMAND?=ls)
	$(call ALL_RUN,$(COMMAND))

.PHONY: all-build
all-build:
	$(call ALL_RUN,make build)

.PHONY: all-test
all-test:
	$(call ALL_RUN,make test)

.PHONY: all-lint
all-lint:
	$(call ALL_RUN,make lint)

.PHONY: all-golangci-lint
all-golangci-lint: install-golangci-lint
	$(call ALL_RUN,make golangci-lint)

.PHONY: all-check-rules
all-check-rules:
	$(call ALL_RUN,make check-rules)

.PHONY: all-clean
all-clean:
	$(call ALL_RUN,make clean)

.PHONY: all-mod-update
all-mod-update:
	$(call ALL_RUN,make mod-update)

.PHONY: all-mod-update-golang-libraries
all-mod-update-golang-libraries:
	$(call ALL_RUN,make mod-update-golang-libraries)

.PHONY: all-mod-tidy
all-mod-tidy:
	$(call ALL_RUN,make mod-tidy)

.PHONY: all-cloud-build-local
all-cloud-build-local:
	$(call ALL_RUN,make cloud-build-local)

.PHONY: all-copy-common
all-copy-common:
	$(call ALL_COMMAND,cp -r Makefile-common.mk Makefile-project.mk Makefile-travis.mk .travis .golangci.yml {})
.PHONY: all-common-file-update
all-common-file-update:
	$(call ALL_RUN,git add Makefile-common.mk Makefile-project.mk Makefile-travis.mk && git commit -m "copy common files [ci skip]")
