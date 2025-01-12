---
title: "Traefik Redis Documentation"
description: "For configuration discovery in Traefik Proxy, you can store your configurations in Redis. Read the technical documentation."
---

# Traefik & Redis

A Story of KV store & Containers
{: .subtitle }

Store your configuration in Redis and let Traefik do the rest!

## Routing Configuration

See the dedicated section in [routing](../routing/providers/kv.md).

## Provider Configuration

### `endpoints`

_Required, Default="127.0.0.1:6379"_

Defines how to access Redis.

```yaml tab="File (YAML)"
providers:
  redis:
    endpoints:
      - "127.0.0.1:6379"
```

```toml tab="File (TOML)"
[providers.redis]
  endpoints = ["127.0.0.1:6379"]
```

```bash tab="CLI"
--providers.redis.endpoints=127.0.0.1:6379
```

### `rootKey`

_Required, Default="traefik"_

Defines the root key of the configuration.

```yaml tab="File (YAML)"
providers:
  redis:
    rootKey: "traefik"
```

```toml tab="File (TOML)"
[providers.redis]
  rootKey = "traefik"
```

```bash tab="CLI"
--providers.redis.rootkey=traefik
```

### `username`

_Optional, Default=""_

Defines a username to connect with Redis.

```yaml tab="File (YAML)"
providers:
  redis:
    # ...
    username: "foo"
```

```toml tab="File (TOML)"
[providers.redis]
  # ...
  username = "foo"
```

```bash tab="CLI"
--providers.redis.username=foo
```

### `password`

_Optional, Default=""_

Defines a password to connect with Redis.

```yaml tab="File (YAML)"
providers:
  redis:
    # ...
    password: "bar"
```

```toml tab="File (TOML)"
[providers.redis]
  # ...
  password = "bar"
```

```bash tab="CLI"
--providers.redis.password=foo
```

### `tls`

_Optional_

Defines the TLS configuration used for the secure connection to Redis.

#### `ca`

_Optional_

`ca` is the path to the certificate authority used for the secure connection to Redis,
it defaults to the system bundle.

```yaml tab="File (YAML)"
providers:
  redis:
    tls:
      ca: path/to/ca.crt
```

```toml tab="File (TOML)"
[providers.redis.tls]
  ca = "path/to/ca.crt"
```

```bash tab="CLI"
--providers.redis.tls.ca=path/to/ca.crt
```

#### `caOptional`

_Optional_

The value of `caOptional` defines which policy should be used for the secure connection with TLS Client Authentication to Redis.

!!! warning ""

    If `ca` is undefined, this option will be ignored, and no client certificate will be requested during the handshake. Any provided certificate will thus never be verified.

When this option is set to `true`, a client certificate is requested during the handshake but is not required. If a certificate is sent, it is required to be valid.

When this option is set to `false`, a client certificate is requested during the handshake, and at least one valid certificate should be sent by the client.

```yaml tab="File (YAML)"
providers:
  redis:
    tls:
      caOptional: true
```

```toml tab="File (TOML)"
[providers.redis.tls]
  caOptional = true
```

```bash tab="CLI"
--providers.redis.tls.caOptional=true
```

#### `cert`

_Optional_

`cert` is the path to the public certificate used for the secure connection to Redis.
When using this option, setting the `key` option is required.

```yaml tab="File (YAML)"
providers:
  redis:
    tls:
      cert: path/to/foo.cert
      key: path/to/foo.key
```

```toml tab="File (TOML)"
[providers.redis.tls]
  cert = "path/to/foo.cert"
  key = "path/to/foo.key"
```

```bash tab="CLI"
--providers.redis.tls.cert=path/to/foo.cert
--providers.redis.tls.key=path/to/foo.key
```

#### `key`

_Optional_

`key` is the path to the private key used for the secure connection to Redis.
When using this option, setting the `cert` option is required.

```yaml tab="File (YAML)"
providers:
  redis:
    tls:
      cert: path/to/foo.cert
      key: path/to/foo.key
```

```toml tab="File (TOML)"
[providers.redis.tls]
  cert = "path/to/foo.cert"
  key = "path/to/foo.key"
```

```bash tab="CLI"
--providers.redis.tls.cert=path/to/foo.cert
--providers.redis.tls.key=path/to/foo.key
```

#### `insecureSkipVerify`

_Optional, Default=false_

If `insecureSkipVerify` is `true`, the TLS connection to Redis accepts any certificate presented by the server regardless of the hostnames it covers.

```yaml tab="File (YAML)"
providers:
  redis:
    tls:
      insecureSkipVerify: true
```

```toml tab="File (TOML)"
[providers.redis.tls]
  insecureSkipVerify = true
```

```bash tab="CLI"
--providers.redis.tls.insecureSkipVerify=true
```
