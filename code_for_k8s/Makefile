SHELL=/bin/bash

INGRESS_H=$(shell kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
INGRESS_P=$(shell kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="http2")].port}')
SECURE_INGRESS=$(shell kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="https")].port}')
SERVICE_GRAPH=$(shell kubectl -n istio-system get pod -l app=servicegraph -o jsonpath='{.items[0].metadata.name}')
DISTRIBUTED_GRAPH=$(shell kubectl get pod -n istio-system -l app=jaeger -o jsonpath='{.items[0].metadata.name}')

.PHONY: help print

help:
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'

# make target: <dependancies> ## comment for the self documenting
istio: ## Deploy Istio
	@kubectl apply -f https://git.io/fxlAR
	@kubectl apply -f /home/jj/repo/workshops/istio-workshop/istio-1.0.2/install/kubernetes/istio-demo.yaml

# make target: <dependancies> ## comment for the self documenting
istio_verify: ## Verify Istio
	@kubectl get pods && kubectl get svc
	@echo ''
	@echo ''
	@kubectl get svc -n istio-system
	@echo ''
	@echo ''
	@kubectl get pods -n istio-system

# make target: <dependancies> ## comment for the self documenting
bookinfo: ## Deploy bookinfo
	@kubectl apply -f <(istioctl kube-inject -f /home/jj/repo/workshops/istio-workshop/istio-1.0.2/samples/bookinfo/platform/kube/bookinfo.yaml)

# make target: <dependancies> ## comment for the self documenting
bookinfo_verify: ## Verify bookinfo
	@kubectl get pods
	@echo ''
	@echo ''
	@kubectl get svc

# make target: <dependancies> ## comment for the self documenting
bookinfo_default: ## Default routing bookinfo
	@kubectl apply -f /home/jj/repo/workshops/istio-workshop/istio-1.0.2/samples/bookinfo/networking/bookinfo-gateway.yaml
	@kubectl apply -f /home/jj/repo/workshops/istio-workshop/istio-1.0.2/samples/bookinfo/networking/destination-rule-all.yaml

# make target: <dependancies> ## comment for the self documenting
bookinfo_view: ## Open bookinfo in firefox
	@firefox $(INGRESS_H):$(INGRESS_P)/productpage

# make target: <dependancies> ## comment for the self documenting
bookinfo_version_one: ## v1 routing bookinfo
	@kubectl apply -f /home/jj/repo/workshops/istio-workshop/istio-1.0.2/samples/bookinfo/networking/virtual-service-all-v1.yaml

# make target: <dependancies> ## comment for the self documenting
bookinfo_version_one_verify: ## verify v1 routing bookinfo
	@cat /home/jj/repo/workshops/istio-workshop/istio-1.0.2/samples/bookinfo/networking/virtual-service-all-v1.yaml

# make target: <dependancies> ## comment for the self documenting
bookinfo_version_two: ## v2 routing bookinfo
	@kubectl apply -f /home/jj/repo/workshops/istio-workshop/istio-1.0.2/samples/bookinfo/networking/virtual-service-reviews-test-v2.yaml

# make target: <dependancies> ## comment for the self documenting
bookinfo_version_two_verify: ## verify v2 routing bookinfo
	@cat /home/jj/repo/workshops/istio-workshop/istio-1.0.2/samples/bookinfo/networking/virtual-service-reviews-test-v2.yaml

# make target: <dependancies> ## comment for the self documenting
service_graph: ## enable the service graph
	@kubectl -n istio-system port-forward $(SERVICE_GRAPH) 8088:8088 &

# make target: <dependancies> ## comment for the self documenting
service_graph_verify: ## verify the service graph
	@firefox http://localhost:8088/force/forcegraph.html

# make target: <dependancies> ## comment for the self documenting
distributed_graph: ## enable the distributed graph
	@kubectl port-forward -n istio-system $(DISTRIBUTED_GRAPH)  16686:16686 &

# make target: <dependancies> ## comment for the self documenting
distributed_graph_verify: ## verify the service graph
	@firefox http://localhost:16686

# make target: <dependancies> ## comment for the self documenting
fault_injection: ## Inject some faults
	@kubectl apply -f /home/jj/repo/workshops/istio-workshop/istio-1.0.2/samples/bookinfo/networking/virtual-service-ratings-test-delay.yaml

# make target: <dependancies> ## comment for the self documenting
fault_injection_fifty: ## Fix it 50/50
	@kubectl apply -f /home/jj/repo/workshops/istio-workshop/istio-1.0.2/samples/bookinfo/networking/virtual-service-reviews-50-v3.yaml

# make target: <dependancies> ## comment for the self documenting
fault_injection_fix: ## Fix it
	@kubectl apply -f /home/jj/repo/workshops/istio-workshop/istio-1.0.2/samples/bookinfo/networking/virtual-service-reviews-v3.yaml
	@cat /home/jj/repo/workshops/istio-workshop/istio-1.0.2/samples/bookinfo/networking/virtual-service-reviews-v3.yaml


# If you want to have it at the bottom of the file:
# .DEFAULT_GOAL := help
