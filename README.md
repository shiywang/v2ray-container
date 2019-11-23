
# Containerized V2Ray on TLS + WebSocket

## Usage
1. Generate Certificates and keys

``` bash
pushd ./ssl
cfssl genkey -initca csr.json | cfssljson -bare ca
cfssl genkey csr.json | cfssljson -bare
cfssl sign -ca=ca.pem -ca-key=ca-key.pem cert.csr | cfssljson -bare
popd
```
2. Start server

```bash
# edit config/server/config.json for your user UUID
docker-compose up -d server nginx
```

3. Start client

``` bash
# edit config/server/config.json for your server address and user UUID
docker-compose up -d client
```
