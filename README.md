# [WIP] cert-manager-webhook-coredns-etcd

A webhook for performaning DNS01 validation against CoreDNS backended by etcd.

### Running the test suite

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

## Links

- https://cert-manager.io/docs/configuration/acme/dns01/webhook/
- https://github.com/cert-manager/webhook-example
- https://github.com/lordofsystem/cert-manager-webhook-powerdns
- https://github.com/kubernetes-sigs/external-dns/blob/b03da005e217b2a0a5da098cb6cd669372a89799/provider/coredns/coredns.go
