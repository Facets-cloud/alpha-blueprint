## Introduction

A Redis Instance in master/slave or reader/writer mode.

## Spec

| Property              | Type            | Required | Description                        |
|-----------------------|-----------------|----------|------------------------------------|
| `authenticated`       | boolean         | **Yes**  | Make this redis Password protected |
| `persistence_enabled` | boolean         | **Yes**  | Enable Persistence for this redis  |
| `redis_version`       | string          | **Yes**  | Version of redis e.g. 6.3          |
| `size`                | [object](../../traits/size.md) | **Yes**  |                                    |

## Outputs

| Property     | Type                  | Required | Description |
|--------------|-----------------------|----------|-------------|
| `instances`  | Map<string, [interface](../../traits/interface.md)>  | No       |             |
| `interfaces` | [object](../../traits/reader-writer-interfaces.schema.md) | No       |             |
| `spec`       | [object](#spec)       | No       |             |


## Flavors

- k8s
- elasticache
- memorystore

## Alerts

| Alert Name | Impact                | Mitigation                                           |
|------------|-----------------------|------------------------------------------------------|
| `RedisDown`  | Redis is inaccessible | Debug the instance health via metrics & logs         |
 | `RedisOutOfConfiguredMaxmemory` | Redis is running out of memory | Debug using redis dashboards in Facets control plane |
|`RedisTooManyConnections` | Redis has too many connections | Refer to client title pane in redis dashboard |