# Language Support (Spin SDKs)

Use this matrix to choose a language.

Rust
- Triggers: HTTP, Redis
- APIs: outbound HTTP, variables, KV, SQLite, MySQL, Postgres, outbound Redis, AI, MQTT
- Extensibility: custom triggers supported

JavaScript/TypeScript
- Triggers: HTTP (Redis trigger not supported)
- APIs: outbound HTTP, variables, KV, SQLite, MySQL, Postgres, outbound Redis, AI, MQTT
- Extensibility: custom triggers not supported

Python
- Triggers: HTTP, Redis
- APIs: outbound HTTP, variables, KV, SQLite, MySQL, Postgres, outbound Redis, AI
- MQTT not supported
- Extensibility: custom triggers not supported

TinyGo
- Triggers: HTTP, Redis
- APIs: outbound HTTP, variables, KV, SQLite, MySQL, Postgres, outbound Redis, AI
- MQTT not supported
- Extensibility: custom triggers not supported

Selection rules
- Need custom triggers or MQTT: choose Rust.
- Need Redis trigger: avoid JS/TS.
- If user insists on unsupported combo, propose Rust or a supported language.
