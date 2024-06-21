# OpenTelemetry Protocol (OTLP) Specification

**NOTE**

This is a modified version of the Go OpenTelemtry protobuf files to re-add deprecated/removed Metric types (IntSum, IntGuage, IntHistogram) and label type (StringKeyValue).

You should not depend on these protobuf files directly, instead use the Honeycomb fork of the [opentelemetry-proto-go](https://github.com/honeycombio/opentelemetry-proto-go) package which includes these changes.

This repo is currently pinned to [v0.19.0](https://github.com/open-telemetry/opentelemetry-proto/tree/v0.19.0) of the upstream repository.

[![Build Check](https://github.com/open-telemetry/opentelemetry-proto/workflows/Build%20Check/badge.svg?branch=main)](https://github.com/open-telemetry/opentelemetry-proto/actions?query=workflow%3A%22Build+Check%22+branch%3Amain)

This repository contains the [OTLP protocol specification](specification/otlp.md)
and the corresponding Language Independent Interface Types ([.proto files](opentelemetry/proto)).

## Language Independent Interface Types

The proto files can be consumed as GIT submodules or copied and built directly in the consumer project.

The compiled files are published to central repositories (Maven, ...) from OpenTelemetry client libraries.

See [contribution guidelines](CONTRIBUTING.md) if you would like to make any changes.

## OTLP/JSON

See additional requirements for [OTLP/JSON wire representation here](https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/protocol/otlp.md#json-protobuf-encoding).

## Generate gRPC Client Libraries

To generate the raw gRPC client libraries, use `make gen-${LANGUAGE}`. Currently supported languages are:

* cpp
* csharp
* go
* java
* objc
* openapi (swagger)
* php
* python
* ruby

## Maturity Level

Component                            | Maturity                                                                                                                                |
-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
**Binary Protobuf Encoding**         |                                                                                                                                         |
common/*                             | Stable                                                                                                                                  |
metrics/\*<br>collector/metrics/*    | Stable                                                                                                                                  |
resource/*                           | Stable                                                                                                                                  |
trace/trace.proto<br>collector/trace/* | Stable                                                                                                                                  |
trace/trace_config.proto             | Alpha                                                                                                                                   |
logs/\*<br>collector/logs/*          | Stable                                                                                                                                  |
**JSON encoding**                    |                                                                                                                                         |
All messages                         | [Stable](https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/protocol/otlp.md#json-protobuf-encoding) |

(See [maturity-matrix.yaml](https://github.com/open-telemetry/community/blob/47813530864b9fe5a5146f466a58bd2bb94edc72/maturity-matrix.yaml#L57)
for definition of maturity levels).

## Stability Definition

Components marked `Stable` provide the following guarantees:

- Field types, numbers and names will not change.
- Service names and service package names will not change.
- Service method names will not change.
- Service method parameter names will not change.
- Service method parameter types and return types will not change.
- Service method kind (unary vs streaming) will not change.
- Names of messages and enums will not change.
- Names of enum choices and numbers assigned to enum choices will not change.
- The location of messages and enums, i.e. whether they are declared at the top lexical
  scope or nested inside another message will not change.
- Package names and directory structure will not change.
- `optional` and `repeated` declarators of existing fields will not change.
- No existing symbol will be deleted.

The following additive changes are allowed:

- Adding new fields to existing messages.
- Adding new messages or enums.
- Adding new choices to existing enums.
- Adding new choices to existing oneof fields.
- Adding new services.
- Adding new methods to existing services.

All the additive changes above must be accompanied by an explanation about how
new and old senders and receivers that implement the version of the protocol
before and after the change interoperate.

No guarantees are provided whatsoever about the stability of the code that
is generated from the .proto files by any particular code generator.

## Experiments

In some cases we are trying to experiment with different features. In this case,
we recommend using an "experimental" sub-directory instead of adding them to any
protocol version. These protocols should not be used, except for
development/testing purposes.

Another review must be conducted for experimental protocols to join the main project.
