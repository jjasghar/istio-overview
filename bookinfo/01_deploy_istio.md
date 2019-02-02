!SLIDE[bg=_images/backgrounds/white_bg_cloud.png]

~~~SECTION:notes~~~
First thing first. We need to actually deploy Istio. I'm going to run this in another window, but in essence its the following.

I should mention this assumes you have Isito already installed on your local machine.

VERIFY installation.

kubectl get pods && kubctl get svc && kubectl get ingress
istio puts everything in it's own namespace....
kubectl get svc -n istio-system
kubectl get pods -n istio-system

~~~ENDSECTION~~~

# Deploy Istio

    @@@ bash
        curl -L https://git.io/getLatestIstio | sh -
        cd istio-1.0.5
        export PATH=$PWD/bin:$PATH
        kubectl apply -f install/kubernetes/helm/helm-service-account.yaml
        helm init --service-account tiller
        helm install install/kubernetes/helm/istio --name istio --namespace istio-system

# Note: Istio installation

<https://github.com/istio/istio/releases>

* I suggest you use the `Stable` release until you are comfortable with the software.
