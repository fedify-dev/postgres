<!-- deno-fmt-ignore-file -->

@fedify/postgres: PostgreSQL drivers for Fedify
===============================================

> [!IMPORTANT]
> This repository is obsolete and has been archived in favor of the monorepo
> [fedify-dev/fedify].

[![JSR][JSR badge]][JSR]
[![npm][npm badge]][npm]
[![GitHub Actions][GitHub Actions badge]][GitHub Actions]

This package provides [Fedify]'s [`KvStore`] and [`MessageQueue`]
implementations for PostgreSQL:

 -  [`PostgresKvStore`]
 -  [`PostgresMessageQueue`]

~~~~ typescript
import { createFederation } from "@fedify/fedify";
import { PostgresKvStore, PostgresMessageQueue } from "@fedify/postgres";
import postgres from "postgres";

const sql = postgres("postgresql://user:password@localhost/dbname");

const federation = createFederation({
  kv: new PostgresKvStore(sql),
  queue: new PostgresMessageQueue(sql),
});
~~~~

[fedify-dev/fedify]: https://github.com/fedify-dev/fedify
[JSR]: https://jsr.io/@fedify/postgres
[JSR badge]: https://jsr.io/badges/@fedify/postgres
[npm]: https://www.npmjs.com/package/@fedify/postgres
[npm badge]: https://img.shields.io/npm/v/@fedify/postgres?logo=npm
[GitHub Actions]: https://github.com/fedify-dev/postgres/actions/workflows/main.yaml
[GitHub Actions badge]: https://github.com/fedify-dev/postgres/actions/workflows/main.yaml/badge.svg
[Fedify]: https://fedify.dev/
[`KvStore`]: https://jsr.io/@fedify/fedify/doc/federation/~/KvStore
[`MessageQueue`]: https://jsr.io/@fedify/fedify/doc/federation/~/MessageQueue
[`PostgresKvStore`]: https://jsr.io/@fedify/postgres/doc/federation/~/PostgresKvStore
[`PostgresMessageQueue`]: https://jsr.io/@fedify/postgres/doc/federation/~/PostgresMessageQueue


Installation
------------

### Deno

~~~~ sh
deno add @fedify/postgres
~~~~

### Node.js

~~~~ sh
npm install @fedify/postgres
~~~~

### Bun

~~~~ sh
bun add @fedify/postgres
~~~~


Changelog
---------

### Version 0.4.0

To be released.

### Version 0.3.0

Released on March 28, 2025.

 -  Added `PostgresMessageQueue.enqueueMany()` method for efficiently enqueuing
    multiple messages at once.

 -  Updated *@js-temporal/polyfill* to 0.5.0 for Node.js and Bun. On Deno,
    there is no change because the polyfill is not used.

 -  Added some logging using [LogTape] for the sake of debugging.  The following
    categories are used:

     -  `["fedify", "postgres", "kv"]`
     -  `["fedify", "postgres", "mq"]`

[LogTape]: https://logtape.org/

### Version 0.2.2

Released on November 18, 2024.

 -  Fixed a bug where binding parameters have not been properly escaped with
    some settings of Postgres.js.

### Version 0.2.1

Released on November 3, 2024.

 -  Fixed a bug where some scalar values have failed to be stored in the
    database.

### Version 0.2.0

Released on November 3, 2024.

 -  Fixed a bug where JSON values are double-quoted in the database.  Since it's
    a breaking change data-wise, the default values of the following options
    are also changed:

     -  `PostgresKvStoreOptions.tableName` defaults to `"fedify_kv_v2"`.
     -  `PostgresMessageQueueOptions.tableName` defaults to
        `"fedify_message_v2"`.

### Version 0.1.0

Initial release.  Released on September 26, 2024.
