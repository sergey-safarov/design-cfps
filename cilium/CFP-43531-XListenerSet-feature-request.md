# CFP-43531: XListenerSet feature request

**SIG: SIG-NAME** ([View all current SIGs](https://docs.cilium.io/en/stable/community/community/#all-sigs))

**Begin Design Discussion:** 2026-01-01

**Cilium Release:** 1.19

**Authors:** Sergey Safarov <s.safarov@gmail.com>

**Status:** Implementable

## Summary

Many application servers in different namespaces can use the same port, such as 80 and 443.
For deployments without a load balancer, such as AWS ALB, it is necessary to share a gateway between different namespaces.
Currently, Cilium implements this by creating a gateway that contains listeners for all namespaces and accepts routes from all namespaces.
When deploying/removing software in a namespace, the gateway listeners need to be updated manually.
This is done manually because the application in the namespace does not have permission to update the gateway configuration used by multiple namespaces.

It will be fine when application in namespace declare required listeners and later Gateway controller
inject listeners into shared gateway using Listener Discovery Service ([LDS](https://www.envoyproxy.io/docs/envoy/latest/configuration/listeners/lds)).

At present time this maybe implemented using [XListenerSet](https://gateway-api.sigs.k8s.io/geps/gep-1713/) Gateway API experimental feature.

Istio implement this feature in Pull Request [#55595](https://github.com/istio/istio/pull/55595) and tiket [#56672](https://github.com/istio/istio/issues/56762).

Envoy gateway start discussion for feature implementation at ticket [#5800](https://github.com/envoyproxy/gateway/issues/5800).

Also envoy gateway has similar feature called [Merged gateways deployment](https://gateway.envoyproxy.io/v1.6/tasks/operations/deployment-mode/#merged-gateways-deployment).

## Motivation

For deployments where Gateway need to be shared between different namespaces required automated tools to add listeners configured in the namespace.
Additional motivation description available at [GEP-1713](https://gateway-api.sigs.k8s.io/geps/gep-1713/#use-cases-motivation).

## Goals

* provide a mechanism for namespace admins to generate listeners and attach them to the shared Gateway
* delegate TLS certificate management to App Owners and/or different namespaces.

## Non-Goals

* N/A

## Proposal

### Overview

Feature propasal available at https://gateway-api.sigs.k8s.io/geps/gep-1713/#yaml

## Impacts / Key Questions

Do not known.

## Future Milestones

Do not knows.
