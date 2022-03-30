---
tags:
  - configuration
  - sample
---

# Sample Configuration

```
version: 1.1

app:
  env: development
  mode: debug
  port: 8080
  trackerDomain: trck.slvrtnio.com
  health:
    enabled: true
    path: /health
  stats:
    enabled: true
    path: /stats

middleware:
  timeout:
    enabled: false
    ms: 2000
  rateLimiter:
    enabled: false
    period: S
    limit: 10
  cookie:
    enabled: true
    name: nuid
    secure: false
    ttlDays: 365
    domain: slvrtnio.com
    path: /
    sameSite: Lax
  cors:
    enabled: true
    allowOrigin:
      - "*"
    allowCredentials: true
    allowMethods:
      - POST
      - OPTIONS
      - GET
    maxAge: 86400
  requestLogger:
    enabled: true
  yeet:
    enabled: false

inputs:
  snowplow:
    enabled: true
    standardRoutesEnabled: true
    openRedirectsEnabled: true
    getPath: /plw/g
    postPath: /plw/p
    redirectPath: /plw/r
    anonymize:
      ip: false
      userId: false
  cloudevents:
    enabled: true
    path: /ce/p
  generic:
    enabled: true
    path: /gen/p
    contexts:
      rootKey: contexts
      schemaKey: schema
      dataKey: data
    payload:
      rootKey: payload
      schemaKey: schema
      dataKey: data
  webhook:
    enabled: true
    path: /wb/hk
  relay:
    enabled: true
    path: /relay

schemaCache:
  schemaCacheBackend:
    type: fs
    path: ./schemas
  ttlSeconds: 300
  maxSizeBytes: 104857600 # 100mb -> 100 * 1024 * 1024
  purge:
    enabled: true
    path: /c/purge
  schemaEndpoints:
    enabled: true

manifold:
  bufferRecordThreshold: 1
  bufferByteThreshold: 1024
  bufferTimeThreshold: 60

sinks:
  - name: primary
    type: kafka
    kafkaBrokers:
      - redpanda-1:29092
      - redpanda-2:29093
      - redpanda-3:29094
    invalidEventTopic: hpt-invalid
    validEventTopic: hpt-valid
  - name: console
    type: stdout
  - name: adios
    type: blackhole

squawkBox:
  enabled: true
  cloudeventsPath: /sqwk/ce
  snowplowPath: /sqwk/sp
  genericPath: /sqwk/gen

tele:
  enabled: true
  heartbeatMs: 3000

```