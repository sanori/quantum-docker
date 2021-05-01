.PHONY: help build push dev test test-env

# Docker image name and tag
IMAGE:=sanori/qiskit-notebook
TAG?=latest
QISKIT_VERSION?=$(shell ./pipver qiskit)
VERSION:=$(QISKIT_VERSION)
# Shell that make should use
SHELL:=bash

help:
# http://marmelab.com/blog/2016/02/29/auto-documented-makefile.html
	@grep -E '^[a-zA-Z0-9_%/-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'

clean: ## Make clean the build environment
	docker image prune

build: DARGS?=--pull --build-arg qiskit_version=$(QISKIT_VERSION)
build: ## Make the latest build of the image
	docker build $(DARGS) --rm --force-rm -t $(IMAGE):$(TAG) -t $(IMAGE):$(VERSION) .

push: ## Push the latest image
	docker push $(IMAGE):$(VERSION)
	docker push $(IMAGE):latest

dev: ARGS?=
dev: DARGS?=-v $(PWD)/work:/home/jovyan/work
dev: PORT?=8888
dev: ## Make a container from a tagged image
	docker run -it --rm -p $(PORT):8888 $(DARGS) $(IMAGE):$(VERSION) $(ARGS)

test: ## Make a test run against the latest image
	pytest tests

test-env: ## Make a test environment by installing test dependencies with pip
	pip install -r requirements-test.txt
