!SLIDE[bg=_images/backgrounds/white_bg_cloud.png]


~~~SECTION:notes~~~
Lets start with the obivious advantage of Istio. Routing to the correct application.

If I refresh the site, you'll see that it's round robining between the three versions.

This is obviously bad. And the first thing we'll do is fix that.

OPEN samples/bookinfo/networking/virtual-service-all-v1.yaml

kubectl get virtualservices -o yaml
kubectl get destinationrules -o yaml
~~~ENDSECTION~~~

# All traffic to v1

    @@@ Console
        kubectl apply -f samples/bookinfo/networking/virtual-service-all-v1.yaml
        kubectl get virtualservices -o yaml
        kubectl get destinationrules -o yaml
