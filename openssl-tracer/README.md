# OpenSSL Tracer using BPF

This is a basic example of how to trace the OpenSSL library using eBPF.
This tracer uses BCC to deploy the eBPF probes.
This demo was created to accompany the "Debugging with eBPF Part 3: Tracing SSL/TLS connections" [blog post](https://blog.px.dev/ebpf-openssl-tracing/).

## Prerequisites

You must have the BCC development package installed. On Ubuntu, the package can be installed as follows:

```
sudo apt install libbpfcc-dev binutils clang llvm bcc python3 openssl -y
```

Other distributions have similar commands.

## Build

To compile, execute the following command:

```
make
```

## Run Demo Application

A demo application to trace is included. It is a simple client-server written in Python, which uses OpenSSL.

First, you'll have to generate some certificates for the client and server.
To keep things simple, you can generate some self-signed certificates as follows:


To run the demo, you'll need two terminals.

In one terminal, open a secure connection to e.g. google

```
openssl s_client -connect google.com:443
```

In the second terminal, run the tracer on the ProcessID (pid) of the above connection

```
sudo ./openssl_tracer $(pgrep -f openssl)
```
Now, back in the openssl terminal
```
GET / HTTP/1.1
and press enter twice
```




