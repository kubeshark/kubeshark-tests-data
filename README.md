This repository contains data files (mainly, TCP/IP traffic dump files in PCAP format) used as part of *acceptance tests-suite* for [Mizu - Kubernetes API traffic viewer](https://github.com/up9inc/mizu)

## Kafka wire contracts

`bin/kafka/*_req.bin` and matching `*_res.bin` files feed the worker's native Kafka
dissector. `expect/kafka/summarize2` contains protobuf JSON Kafka payloads after
native analysis and a full BaseEntry protobuf binary marshal/unmarshal.

The corpus test requires populated request and response body oneofs and rejects
protobuf serialization failures before writing expectations. It does not rebuild
native payloads from JSON, which loses their concrete Go types. Conversations that
emit no complete entries have no expectation file.

Regenerate from the worker's `pkg/extensions/kafka` directory with
`KUBESHARK_TEST=1 TEST_UPDATE=1 go test . -run '^TestDissect$'`.
