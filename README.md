# Real, Local HTTPS / SSL certificates

HTTPS / SSL Certificates for testing and development.

These certificates are valid, real certificates signed for `local.ldsconnect.org`
(which points to `127.0.0.1` and must be used in place of `localhost`).

### Add these certs to your test / demo project

```bash
git clone git@github.com:LDSorg/local.ldsconnect.org-certificates.git ./certs
```

### Examine the Certificates

```bash
tree certs
```

```
certs/
├── ca
│   ├── intermediate.crt.pem    -- RapidSSL Intermediate CA
│   └── root.crt.pem            -- GEOTrust Root CA
├── server
│   ├── my-server.crt.pem       -- RapidSSL issued cert for local.ldsconnect.org
│   └── my-server.key.pem       -- randomly generated key
└── tmp
    └── my-server.csr.pem       -- Signing Request for local.ldsconnect.org
```

### Examine more closely

Many thanks to <https://www.sslshopper.com/ssl-certificate-tools.html>

#### The Certificate Signing Request

```bash
openssl req -text -noout -in ./certs/tmp/my-server.csr.pem
```

#### The Certificates

You have info such as the name of the domain, the size of the key, the signer, etc.

```bash
openssl x509 -text -noout -in ./certs/server/my-server.crt.pem
openssl x509 -text -noout -in ./certs/ca/intermediate.crt.pem
openssl x509 -text -noout -in ./certs/ca/root.crt.pem
```

#### The Key

It's just random giberish garbage, no metadata to speak of... except key size.

```bash
openssl rsa -text -noout -in ./certs/server/my-server.key.pem
```

### Verify the key matches the cert

```
openssl x509 -noout -modulus -in ./certs/server/my-server.crt.pem | openssl md5
openssl rsa -noout -modulus -in ./certs/server/my-server.key.pem | openssl md5
openssl req -noout -modulus -in ./certs/tmp/my-server.csr.pem | openssl md5
```
