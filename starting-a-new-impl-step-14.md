# Step 13. HTTP Proxy Server mode of operation

See "Web proxy servers" within [https://en.wikipedia.org/wiki/Proxy_server](https://en.wikipedia.org/wiki/Proxy_server)

This one varies per language and the HTTP request initiation available. Client calls to an arbitrary server, can be run through a proxy server on the way there. Some commercial Service Virtualization techs like HoverFly work this way by design. For Servirtium it is an option.  If mounted as a HTTP Proxy Server technologies that would call over the wire may not be specifically configured for it.

# Notes on prior implementations

If you're making a new impl, you don't actually have to understand the architecture of previous implementations. Indeed, your impl may be better for **not** being educated on prior implementations.

