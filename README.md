# ESTELA runtime (`@estela/nest`)

Enterprise Integration Patterns for NestJS, in the spirit of Spring Integration: message channels
(direct, queue, pub/sub, fanout), a flow DSL, service activators, inbound and outbound adapters
(REST, gRPC, RabbitMQ, GraphQL), tracing, idempotency, resilience policies, privacy for logs and
stores, sagas and a live topology graph.

**ESTELA is a contribution of D&DD Tech to the open-source community.** The runtime is free to use,
including in commercial products, under the [MIT License](./LICENSE).

This repository distributes the packaged runtime and explains how to install it. It does not host the
source code.

## Install

ESTELA is published as a GitHub Release asset. Pin an exact version:

```bash
npm install https://github.com/dyddtechnologies/estela-rt/releases/download/v<version>/estela-nest-<version>.tgz
```

The available versions are listed under [Releases](https://github.com/dyddtechnologies/estela-rt/releases).
Each release lists its changes.

### Requirements

| Package | Version |
|---|---|
| Node.js | 18 or later |
| `@nestjs/common`, `@nestjs/core` | 10 or 11 |
| `@nestjs/swagger` | 7 or 8 |
| `reflect-metadata` | 0.1.13 or later |
| `rxjs` | 7 |

Optional, only when you use the matching adapter: `amqplib` (RabbitMQ), `@grpc/grpc-js` (gRPC),
`@nestjs/graphql` (GraphQL).

### Entry points

- `@estela/nest`: the runtime.
- `@estela/nest/testing`: test helpers.

### Minimal setup

```ts
import { Module } from '@nestjs/common';
import { IntegrationModule } from '@estela/nest';

@Module({
  imports: [
    IntegrationModule.forRoot(
      { channels: [{ name: 'orders.place', type: 'direct' }] },
      [],
    ),
  ],
})
export class AppModule {}
```

## Upgrading

Install the new version's URL, read its release notes for anything marked as a breaking change, run your
test suite, and check that the startup log lists the same activators, inbound and outbound endpoints as before.

## Support

Questions and bug reports: open an issue in this repository. Include the ESTELA version, the Node and NestJS
versions, and a minimal reproduction.

## License

MIT. Copyright (c) 2026 D&DD Inversiones, commercially D&DD Tech. The software is provided "as is", without warranty of any kind.
