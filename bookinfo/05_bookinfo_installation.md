!SLIDE[bg=_images/backgrounds/white_bg_cloud.png]

~~~SECTION:notes~~~
Now that we have it installed, we need to create an ingress gateway assuming
it hasn't and also put in a default routing role.

VERIFY

kubectl get gateway

export INGRESS_HOST=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export INGRESS_PORT=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="http2")].port}')
export SECURE_INGRESS_PORT=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="https")].port}')
export GATEWAY_URL=$INGRESS_HOST:$INGRESS_PORT

firefox $GATEWAY_URL/productpage

~~~ENDSECTION~~~

# Deploy Bookinfo app

    @@@ bash
         kubectl apply -f \
           samples/bookinfo/networking/bookinfo-gateway.yaml
         kubectl apply -f \
           samples/bookinfo/networking/destination-rule-all.yaml
