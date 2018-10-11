!SLIDE[bg=_images/backgrounds/white_bg_cloud.png]
~~~SECTION:notes~~~
Now I'm going to now cut the traffic for a user named "Jason."

Imagine the ability to put out a pre-release version of your microservice and
only have one user use it. It's all done via HTTP headers and in this case we
have the following

~~~ENDSECTION~~~

# Some traffic to v2

    @@@ Console
        kubctl apply -f samples/bookinfo/networking/virtual-service-reviews-test-v2.yaml
