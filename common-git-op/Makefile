ALL_DIR=cd $(dir) && (ls -d -1 * | grep -v golang-libraries | grep -v Makefile | grep -v sib_go-*.code-workspace)
ALL_COMMAND=$(ALL_DIR) | xargs -n 1 -I {} $(1)
ALL_RUN=$(call ALL_COMMAND,sh -c 'echo {} && cd {} && $(1)')
.PHONY: all-git-commit
all-git-commit:
	$(call ALL_RUN,git add go.mod go.sum && git commit -m "update dependencies")
all-git-checkout:
	$(call ALL_RUN,git checkout go.mod go.sum)
all-git-rebase-dev:
	$(call ALL_RUN,git pull --rebase origin dev)
all-git-push-dev:
	$(call ALL_RUN,git push -u origin dev)
