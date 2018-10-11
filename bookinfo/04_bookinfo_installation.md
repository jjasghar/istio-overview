!SLIDE[bg=_images/backgrounds/white_bg_cloud.png]

~~~SECTION:notes~~~
The following command is what i'm going to run to install bookinfo.


VERIFY

kubectl get services && kubectl get pods

As you con see here we now have services and pods running bookinfo. including our v1,v2,v3

~~~ENDSECTION~~~

# Deploy Bookinfo app

    @@@ Console
        kubectl apply -f <(istioctl kube-inject -f samples/bookinfo/platform/kube/bookinfo.yaml)
