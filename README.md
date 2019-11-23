
# Containerized V2Ray on TLS + WebSocket

## Prerequisite

You must have the following components installed:

- Docker
- docker-compose
- uuidgen
- [cfssl](https://github.com/cloudflare/cfssl)

## Usage
1. Setup

Generate client UUID and keep a note:

``` bash
uuidgen
```

Generate Certificates and keys:

``` bash
pushd ./ssl
cfssl genkey -initca csr.json | cfssljson -bare ca
cfssl genkey csr.json | cfssljson -bare
cfssl sign -ca=ca.pem -ca-key=ca-key.pem cert.csr | cfssljson -bare
popd
```

3. Start server

```bash
# edit config/server/config.json for your user UUID
docker-compose up -d server nginx
```

4. Start client

``` bash
# edit config/server/config.json for your server address and user UUID
docker-compose up -d client
```
