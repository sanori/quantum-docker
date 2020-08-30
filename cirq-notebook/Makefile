.PHONY: help build dev test test-env

# Docker image name and tag
IMAGE:=sanori/cirq-notebook
TAG?=latest
CIRQ_VERSION?=$(shell ./pipver cirq)
VERSION:=$(CIRQ_VERSION)
# Shell that make should use
SHELL:=bash

help:
# http://marmelab.com/blog/2016/02/29/auto-documented-makefile.html
	@grep -E '^[a-zA-Z0-9_%/-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | \
	awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'

clean: ## Make clean the build environment
	docker image prune

build: DARGS?=--build-arg cirq_version=$(CIRQ_VERSION)
build: ## Make the latest build of the image
	docker build $(DARGS) --rm --force-rm -t $(IMAGE):$(TAG) -t $(IMAGE):$(VERSION) .

dev: ARGS?=
dev: DARGS?=-v $(PWD)/work:/home/jovyan/work
dev: PORT?=8888
dev: ## Make a container from a tagged image
	docker run -it --rm -p $(PORT):8888 $(DARGS) $(IMAGE):$(TAG) $(ARGS)