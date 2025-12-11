# postgres-adapter

> **Note:** This is a fork of [casbin-rs/postgres-adapter](https://github.com/casbin-rs/postgres-adapter) with updated dependencies to support the [ponix-rs](https://github.com/ponix-dev/ponix-rs) repository.

postgres-adapter uses [tokio-postgres](https://github.com/sfackler/rust-postgres/tree/master/tokio-postgres) and [deadpool-postgres](https://github.com/bikeshedder/deadpool/tree/master/postgres) as an adapter for [Casbin-rs](https://github.com/casbin/casbin-rs). With this library, Casbin can load policy from [Postgres](https://github.com/lib/pq) or save policy to it with fully asynchronous support and prepared statements.

## Install

Add it to `Cargo.toml`

```toml
tokio-postgres-adapter = { git = "https://github.com/ponix-dev/casbin-tokio-postgres-adapter.git" }
```

## Configure

1. Set up database environment    
    ```bash
    #!/bin/bash

    docker run -itd \
        --restart always \
        -e POSTGRES_USER=casbin_rs \
        -e POSTGRES_PASSWORD=casbin_rs \
        -e POSTGRES_DB=casbin \
        -p 5432:5432 \
        -v /srv/docker/postgresql:/var/lib/postgresql \
        postgres:11;
    ```

2. Create table `casbin_rule`

    ```bash
    # PostgreSQL
    psql postgres://casbin_rs:casbin_rs@127.0.0.1:5432/casbin -c "CREATE TABLE IF NOT EXISTS casbin_rule (
        id SERIAL PRIMARY KEY,
        ptype VARCHAR NOT NULL,
        v0 VARCHAR NOT NULL,
        v1 VARCHAR NOT NULL,
        v2 VARCHAR NOT NULL,
        v3 VARCHAR NOT NULL,
        v4 VARCHAR NOT NULL,
        v5 VARCHAR NOT NULL,
        CONSTRAINT unique_key_sqlx_adapter UNIQUE(ptype, v0, v1, v2, v3, v4, v5)
        );"

## Usage

See the [casbin-rs documentation](https://github.com/casbin/casbin-rs) for usage examples with the `TokioPostgresAdapter`.
