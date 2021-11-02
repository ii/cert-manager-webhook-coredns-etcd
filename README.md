# [WIP] cert-manager-webhook-coredns-etcd

A webhook for performing DNS01 validation against CoreDNS backended by etcd.

## TODO

- [ ] ensure that (Cluster)Issuer can talk to APIService/Service

## Building

```bash
docker build -t cert-manager-webhook-coredns-etcd .
```

## Deploying

```bash
helm upgrade --install \
  cert-manager-webhook-coredns-etcd \
  -n pair-system \
  --set image.repository=cert-manager-webhook-coredns-etcd \
  --set image.pullPolicy=Never \
  --set groupName=$SHARINGIO_PAIR_BASE_DNS_NAME \
  deploy/cert-manager-webhook-coredns-etcd/
```

## Running the test suite

All DNS providers **must** run the DNS01 provider conformance testing suite,
else they will have undetermined behaviour when used with cert-manager.

**It is essential that you configure and run the test suite when creating a
DNS01 webhook.**

An example Go test file has been provided in [main_test.go](https://github.com/jetstack/cert-manager-webhook-example/blob/master/main_test.go).

You can run the test suite with:

```bash
$ TEST_ZONE_NAME=example.com. make test
```

The example file has a number of areas you must fill in and replace with your
own options in order for tests to pass.

## Debug

Show all ClusterRoles for cert-manager (and misc)

```bash
kubectl get clusterrole $(kubectl get clusterrole | grep cert-manager | awk '{print $1}' | xargs) -o yaml | less
```

Show all keys in etcd

```bash
etcdctl --endpoints "etcd-client.pair-system:2379" get / --prefix --keys-only
```

## Testing

```bash
envsubst < ./letsencrypt-coredns-staging.yaml | kubectl apply -f -
```

## Links

- https://cert-manager.io/docs/configuration/acme/dns01/webhook/
- https://github.com/cert-manager/webhook-example
- https://github.com/lordofsystem/cert-manager-webhook-powerdns
- https://github.com/kubernetes-sigs/external-dns/blob/b03da005e217b2a0a5da098cb6cd669372a89799/provider/coredns/coredns.go
