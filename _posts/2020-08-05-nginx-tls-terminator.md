---
layout: post
title: "Nginx TLS terminator"
date: 2020-08-05 13:37:00 +0100
categories: nginx tls https openssl security docker kubernetes
---

<img src="/assets/nginx_logo.svg" width="300">

Sometimes you'll want/need to use TLS for connections to internal kubernetes services where TLS isn't supported or used by the original application, or where you'd normally terminate TLS in the ingress but don't want to have internal kubernetes traffic routed through that. Cases like that are a great fit for the [sidecar pattern](https://docs.microsoft.com/en-us/azure/architecture/patterns/sidecar), injecting a small proxy inside a pod to terminate TLS and forward the requests to the original application. Having configured a few of these sidecars for various projects, I started to compile a common configuration for nginx which I could reuse for this purpose. Hence the [nginx-tls-terminator](https://github.com/anderseknert/nginx-tls-terminator) project was born.

From the project's decription:

>Single-purpose TLS terminating nginx proxy.
>
>Primary function is to run as a sidecar container in kubernetes pods where the app running in the main container either does not support TLS, or it's inconvenient to add it - such as for legacy apps or where the code is not under your control. Another common use case is when external traffic has TLS terminated by the ingress controller, but some internal services need to reach the same services from the inside on the same URL. One example of this is the issuer URL provided in OAuth2 and OpenID Connect, where both external and internal applications will need to query the same endpoints over a secure channel.

>Features:

> * Small single-purpose container at ~9 MB with minimal configuration needed.
> * Does not require root privileges and runs as non-root user by default. Runs with strictest securityContext configured on the container.
> * Running with a read-only root filesystem as easy as mounting a volume on /tmp.
> * Exposed TLS port as well as target upstream port configurable through environment variables.

Check it out on [Github](https://github.com/anderseknert/nginx-tls-terminator) and [Docker Hub](https://hub.docker.com/r/eknert/nginx-tls-terminator).