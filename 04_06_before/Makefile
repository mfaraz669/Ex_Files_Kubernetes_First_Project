#!/usr/bin/env make

.PHONY: run_website install_kind install_kubectl create_kind_cluster

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

