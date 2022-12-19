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
| `instances`  | [object](#instances)  | No       |             |
| `interfaces` | [object](#interfaces) | No       |             |
| `spec`       | [object](#spec)       | No       |             |


## Flavors

