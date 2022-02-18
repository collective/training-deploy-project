### Defensive settings for make:
#     https://tech.davis-hansson.com/p/make/
SHELL:=bash
.ONESHELL:
.SHELLFLAGS:=-xeu -o pipefail -O inherit_errexit -c
.SILENT:
.DELETE_ON_ERROR:
MAKEFLAGS+=--warn-undefined-variables
MAKEFLAGS+=--no-builtin-rules


# We like colors
# From: https://coderwall.com/p/izxssa/colored-makefile-for-golang-projects
RED=`tput setaf 1`
GREEN=`tput setaf 2`
RESET=`tput sgr0`
YELLOW=`tput setaf 3`

.PHONY: all
all: build

# Add the following 'help' target to your Makefile
# And add help text after each target name starting with '\#\#'
.PHONY: help
help: ## This help message
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'

.PHONY: vagrant-provision
vagrant-destroy: ../../bin/ansible ## Provision Vagrant box 
	@echo "$(GREEN)==> Provision Vagrant box $(RESET)"
	sudo vagrant destroy
	sudo rm .vagrant_private_key .vagrant

.PHONY: vagrant-provision
vagrant-provision: ../../bin/ansible ## Provision Vagrant box 
	@echo "$(GREEN)==> Provision Vagrant box $(RESET)"
	sudo vagrant up
	sudo cp .vagrant/machines/default/virtualbox/private_key .vagrant_private_key
	USER=`plone` sudo chown ${USER}: .vagrant_private_key
	ssh-keygen -f ~/.ssh/known_hosts -R "[127.0.0.1]:2222"

.PHONY: compose-pull-local
compose-pull-local: ## Run Compose pull local
	DOCKER_CONTEXT=vagrant docker-compose --project-directory project pull

.PHONY: compose-up-local
compose-up-local: ## Run Compose up local
	DOCKER_CONTEXT=vagrant docker-compose --project-directory project up -d
