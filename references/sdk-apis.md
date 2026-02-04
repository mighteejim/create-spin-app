# Spin SDK Main APIs (Rust)

Use this as the local, no-web reference for common Spin SDK calls.
Examples are Rust; translate for JS/TS/Python/TinyGo as needed.

## HTTP Inbound

Entry point:
```rust
use spin_sdk::http::{IntoResponse, Request, Response};
use spin_sdk::http_component;

#[http_component]
fn handler(req: Request) -> anyhow::Result<impl IntoResponse> {
    let method = req.method();
    let path = req.path();
    let body = req.body();
    Ok(Response::builder().status(200).body("ok").build())
}
```

Routing:
```rust
use spin_sdk::http::{Request, Response, Router};

fn handler(req: Request) -> Response {
    let mut router = Router::new();
    router.get("/", |_req, _params| Response::new(200, "ok"));
    router.handle(req)
}
```

## HTTP Outbound

```rust
use spin_sdk::http::{Method, Request, Response};

let req = Request::builder()
    .method(Method::Get)
    .uri("https://example.com/data")
    .build();
let res: Response = spin_sdk::http::send(req).await?;
```

Manifest:
```toml
allowed_outbound_hosts = ["https://example.com"]
```

## Variables (Config)

```rust
let region = spin_sdk::variables::get("region_id")?;
```

Manifest:
```toml
[component.my-component.variables]
region_id = "{{ app.region_id }}"
```

Local run:
`spin up --variable region_id=us-west-2`

Cloud:
`spin cloud variables set --app <app> region_id=us-west-2`

## Key/Value Store

```rust
use spin_sdk::key_value::Store;

let store = Store::open_default()?;
store.set("message", b"hello")?;
let value = store.get("message")?;
store.delete("message")?;
```

Manifest:
```toml
key_value_stores = ["default"]
```

Local seed:
`spin up --key-value message=hello`

## SQLite

```rust
use spin_sdk::sqlite::{Connection, Value};

let db = Connection::open_default()?;
db.execute("CREATE TABLE IF NOT EXISTS todos (id INTEGER PRIMARY KEY, title TEXT)", &[])?;
db.execute("INSERT INTO todos (title) VALUES (?)", &[Value::Text("task".into())])?;
```

Manifest:
```toml
sqlite_databases = ["default"]
```

Local migration:
`spin up --sqlite @migrations.sql`

## MySQL

```rust
use spin_sdk::mysql::{Connection, ParameterValue};

let db = Connection::open("mysql://user:pass@host/db")?;
let rows = db.query("SELECT * FROM users WHERE id = ?", &[ParameterValue::Int32(1)])?;
db.execute("DELETE FROM users WHERE id = ?", &[ParameterValue::Int32(1)])?;
```

Notes:
- Provide a full connection string.
- Ensure outbound access to the DB host is allowed by the runtime.

## Postgres

```rust
use spin_sdk::pg4::Connection;

let db = Connection::open("host=localhost user=postgres password=secret dbname=mydb")?;
let rows = db.query("SELECT * FROM users WHERE id = $1", &[1.into()])?;
db.execute("DELETE FROM users WHERE id = $1", &[1.into()])?;
```

Notes:
- Provide a full connection string.
- Ensure outbound access to the DB host is allowed by the runtime.

## Redis (Outbound)

```rust
use spin_sdk::redis::Connection;

let conn = Connection::open("redis://127.0.0.1:6379")?;
conn.set("key", b"value")?;
let value = conn.get("key")?;
conn.del(&["key".to_owned()])?;
```

## MQTT (Outbound)

```rust
use spin_sdk::mqtt::{Connection, Qos};

let conn = Connection::open("mqtt://localhost:1883?client_id=client1", "user", "pass", 30)?;
conn.publish("topic", b"payload", Qos::AtLeastOnce)?;
```

## LLM (Serverless AI)

```rust
use spin_sdk::llm::{self, EmbeddingModel, InferencingModel};

let result = llm::infer(InferencingModel::Llama2Chat, "Summarize this")?;
let embeddings = llm::generate_embeddings(
    EmbeddingModel::AllMiniLmL6V2,
    &[String::from("hello")]
)?;
```

Manifest:
```toml
ai_models = ["llama2-chat", "codellama-instruct", "all-minilm-l6-v2"]
```

## If Permissions Fail

Run `spin doctor` and follow the missing-permission hints in the error output.
