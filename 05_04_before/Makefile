#!/usr/bin/env make

.PHONY: run_website install_kind install_kubectl create_kind_cluster \
	create_docker_registry

run_website:
	docker build -t explorecalifornia.com . && \
		docker run -p 5000:80 -d --name explorecalifornia.com --rm explorecalifornia.com

install_kubectl:
	brew install kubectl || true;

install_kind:
	curl -o ./kind https://github.com/kubernetes-sigs/kind/releases/download/v0.11.1/kind-darwin-arm64

create_kind_cluster: install_kind install_kubectl
	kind create cluster --name explorecalifornia.com --config ./kind_config.yaml || true
	kubectl get nodes

create_docker_registry:
	if ! docker ps | grep -q 'local-registry'; \
	then docker run -d -p 5000:5000 --name local-registry --restart=always registry:2; \
	else echo "---> local-registry is already running. There's nothing to do here."; \
	fi

