<!SLIDE center full-page background-fit >
!SLIDE[bg=_images/backgrounds/white_bg_cloud.png]

~~~SECTION:notes~~~
Lets fix this by moving all the traffic to version 3 which we know works

First we'll move it 50/50 to verify that we aren't crazy

Ok, good that's looking better

~~~ENDSECTION~~~

# Fault Injection

## Set traffic to 50/50

    @@@ Console
        kubectl apply -f samples/bookinfo/networking/virtual-service-reviews-50-v3.yaml

## Send all the traffic to v3

    @@@ Console
        kubectl apply -f samples/bookinfo/networking/virtual-service-reviews-v3.yaml
        kubectl get virtualservice reviews -o yaml
