PROJECT_NAME=core-personal-site
VERSION=0.0.1
TAG=

include .env
SHELL := /bin/bash

.PHONY: all
all: build run

.PHONY: deploy
deploy: build push

.PHONY: docker-login
docker-login: docker-login
	docker login --username=$(ACR_USER) --password=$(ACR_PASSWORD) $(ACR_NAME)

.PHONY: build
build: docker-login
	docker build --platform linux/amd64 \
	--build-arg PROJECT_NAME=$(PROJECT_NAME) --build-arg VERSION=$(VERSION) . --tag $(ACR_NAME)/$(PROJECT_NAME):$(VERSION)$(TAG)

.PHONY: run
run: docker-login
	docker run -it $(ACR_NAME)/$(PROJECT_NAME):$(VERSION)$(TAG)

.PHONY: push
push:
	docker push $(ACR_NAME)/$(PROJECT_NAME):$(VERSION)$(TAG)
