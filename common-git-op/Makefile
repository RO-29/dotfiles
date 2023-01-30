ALL_DIR=cd $(dir) && (ls -d -1 * | grep -v golang-libraries | grep -v sib_go-*.code-workspace)
ALL_COMMAND=$(ALL_DIR) | xargs -n 1 -I {} $(1)
ALL_RUN=$(call ALL_COMMAND,sh -c 'echo {} && cd {} && $(1)')
.PHONY: all-git-commit
all-git-commit:
	$(call ALL_RUN,git add go.mod go.sum Makefile* .github/ ruleguard/ Dockerfile .dockerignore .gitignore .golangci.yaml && git commit -m "update dependencies")
all-git-commit-del:
	$(call ALL_RUN,git add .golangci.yml && git commit -m "update dependencies")
all-git-checkout:
	$(call ALL_RUN,git checkout go.mod go.sum)
all-git-rebase-dev:
	$(call ALL_RUN,git pull --rebase origin dev)
all-git-pull-push:
	$(call ALL_RUN,git pull && git push)
all-git-pull:
	$(call ALL_RUN,git pull)
all-git-push:
	$(call ALL_RUN,git push)
all-git-rebase-master:
	$(call ALL_RUN,git checkout master && git pull --rebase origin master && git checkout dev)
all-git-commit-common-files:
	$(call ALL_RUN,git add .github/ ruleguard/ Dockerfile .gitignore .dockerignore .golangci.yaml Makefile* && git commit -m "update common files")
all-git-commit-golang-lib:
	$(call ALL_RUN,git add go.mod go.sum && git commit -m "update golang libraries")
all-fix-kafka:
	$(call ALL_RUN,go get -v -u -d github.com/segmentio/kafka-go@latest && git add go.mod go.sum && git commit -m "update kafka version" && git pull && git push)

all-fix-k:
	$(call ALL_RUN,go get -v -u -d github.com/segmentio/kafka-go@latest && git add go.mod go.sum && git commit -m "update kafka version" && git pull && git push)

all-checkout-common:
	$(call ALL_RUN,git checkout Makefile-common.mk Makefile-project.mk .gitignore .github .dockerignore .golangci.yaml ruleguard)

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
	$(call ALL_COMMAND,cp -r Makefile-common.mk Makefile-project.mk .gitignore .github .dockerignore .golangci.yaml ruleguard .travis .golangci.yaml {})

all-github-action-commit:
	$(call ALL_RUN,git add .github && git commit -m "fix cd.yaml use main from remote" && git pull && git push )
.PHONY: all-common-file-update
all-common-file-update:
	$(call ALL_RUN,git add Makefile-common.mk Makefile-project.mk .gitignore .github .dockerignore .golangci.yaml ruleguard && git commit -m "copy common files")

all-find-common:
	$(call ALL_RUN,ls .github/workflows )

all-rm-common-yml:
	$(call ALL_RUN, rm -f .github/workflows/centralise-deployment.yaml .github/workflows/release.yaml .github/workflows/staging-auto-deployment.yaml  && ls .github/workflows )

all-git-pull-checkout-push:
	$(call ALL_RUN,git pull && git checkout -b feature/go-19.5-upgrade && git push )

all-mod-update-lint:
	$(call ALL_RUN, make lint)

all-del-DS-STORE:
	$(call ALL_RUN, find . -name .DS_Store -print0 | xargs -0 rm )

all-git-pr-:
	$(call ALL_RUN,export GITHUB_TOKEN="" && sleep 5 && git add . && git commit -m "lint changes for go1.19.5" && git push && gh pr create --title "STFFENG-000: GO 1.19.5 upgrade" --body "Go 1.19.x upgrade && lint 1.50.x upgrade" )

all-git-pr-create:
	$(call ALL_RUN,export GITHUB_TOKEN="" && sleep 10 && gh pr create --title "STFFENG-000: GO 1.19.5 upgrade" --body "Go 1.19.x upgrade && lint 1.50.x upgrade" )

all-git-fix:
	$(call ALL_RUN,rm .github/workflows/doc-publishing.yaml && git add . && git commit -m "fix lint changes" && git push )

all-ls:
	$(call ALL_RUN, ls .github/workflows )

.PHONY: all-mod-update
all-mod-update:
	$(call ALL_RUN,make mod-update)
