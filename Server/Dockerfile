FROM envoyproxy/envoy-dev:2f99e0c9f83b6c91b42d215a148ed49ce0f174fd
RUN apt-get update
COPY envoy.yaml /etc/envoy.yaml
CMD /usr/local/bin/envoy -c /etc/envoy.yaml