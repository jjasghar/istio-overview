!SLIDE[bg=_images/backgrounds/white_bg_cloud.png]

~~~SECTION:notes~~~
So we know how to move traffic around, and how things look, but what about issues through the stack?
This is where tracing comes into play.

VERIFY

firefox http://localhost:16686
~~~ENDSECTION~~~

# Distributed Tracing

    @@@ Console
        kubectl port-forward -n istio-system $(kubectl get pod -n istio-system -l app=jaeger -o jsonpath='{.items[0].metadata.name}') 16686:16686
