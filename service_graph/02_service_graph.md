!SLIDE[bg=_images/backgrounds/white_bg_cloud.png]

~~~SECTION:notes~~~
Ok, so we can now make sure that specific things go to specific places, but
what about our app, we think we know what it looks like, but we should verfiy right?
Luckly Istio has a built in Service graph system:


This can be extremely useful for more advanced setups. Visualizing how everything
comes together.

VERIFY

firefox http://localhost:8088/force/forcegraph.html
~~~ENDSECTION~~~

# Service Graph

    @@@ Console
        kubectl -n istio-system get svc servicegraph
        kubectl -n istio-system port-forward $(kubectl -n istio-system get pod -l app=servicegraph -o jsonpath='{.items[0].metadata.name}') 8088:8088
