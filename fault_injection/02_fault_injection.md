!SLIDE[bg=_images/backgrounds/white_bg_cloud.png]

~~~SECTION:notes~~~
So now we can see the health of our app, manipulatiate the traffic, lets cause some problems.

Lets force some failures and look at jaeger to see the errors.

VERIFY

firefox $GATEWAY_URL/productpage  # login as jason

As you can see we are erroring!
You’ve found a bug. There are hard-coded timeouts in the microservices that have caused the
reviews service to fail.
The timeout between the productpage and the reviews service is 6 seconds - coded as 3s + 1
retry for 6s total. The timeout between the reviews and ratings service is hard-coded at
10 seconds. Because of the delay we introduced, the /productpage times out prematurely and
throws the error.
Bugs like this can occur in typical enterprise applications where different teams develop
different microservices independently. Istio’s fault injection rules help you identify
such anomalies without impacting end users.

DON'T FORGET TO LOG OUT HERE

~~~ENDSECTION~~~

# Fault Injection

## Create the Delay

    @@@ Console
        kubectl apply -f samples/bookinfo/networking/virtual-service-all-v1.yaml
        kubectl apply -f samples/bookinfo/networking/virtual-service-reviews-test-v2.yaml
        kubectl apply -f samples/bookinfo/networking/virtual-service-ratings-test-delay.yaml

## Start up jaeger

    @@@ Console
        kubectl port-forward -n istio-system $(kubectl get pod -n istio-system -l app=jaeger -o jsonpath='{.items[0].metadata.name}') 16686:16686
        firefox http://localhost:1668
