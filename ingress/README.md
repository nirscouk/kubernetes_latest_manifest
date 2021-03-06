In this demo, we have added two methods to install the nginx ingress
controller.

nginx-setup file

nginx-setup: Tested and its working fine

Reference:

TLS ingress: https://kubernetes.github.io/ingress-nginx/user-guide/tls/
https://kubernetes.github.io/ingress-nginx/examples/auth/client-certs/
https://success.docker.com/article/how-to-configure-a-default-tls-certificate-for-the-kubernetes-nginx-ingress-controller

Generate TLS certificates
For this article, let's generate a self-signed certificate with openssl.
For production use, you should request a trusted, signed certificate through
a provider or your own certificate authority (CA). In the next step, you
generate a Kubernetes Secret using the TLS certificate and private key
generated by OpenSSL.

The following example generates a 2048-bit RSA X509 certificate valid
for 365 days named aks-ingress-tls.crt. The private key file is named
aks-ingress-tls.key. A Kubernetes TLS secret requires both of these files.

This article works with the demo.azure.com subject common name and doesn't
need to be changed. For production use, specify your own organizational
values for the -subj parameter:

console

Copy
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -out green-ingress-tls.crt -keyout green-ingress-tls.key -subj "/CN=green.nginx.example.com/O=green.nginx.example.com"

kubectl create secret tls green-ingress-tls --key green-ingress-tls.key --cert green-ingress-tls.crt

Curl example:
curl -v -k --resolve demo.example.com:443:192.168.0.20 https://demo.example.com

Reference:

https://docs.nginx.com/nginx-ingress-controller/

