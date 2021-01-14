<div align="center">
<h1>Salvo</h1>
<p>

[![build status](https://github.com/kenorld/salvo/workflows/CI%20(Linux)/badge.svg?branch=master&event=push)](https://github.com/kenorld/salvo/actions)
[![build status](https://github.com/kenorld/salvo//workflows/CI%20(macOS)/badge.svg?branch=master&event=push)](https://github.com/kenorld/salvo/actions)
[![build status](https://github.com/kenorld/salvo/workflows/CI%20(Windows)/badge.svg?branch=master&event=push)](https://github.com/kenorld/salvo/actions)
<br>
[![codecov](https://codecov.io/gh/kenorld/salvo/branch/master/graph/badge.svg)](https://codecov.io/gh/kenorld/salvo)
[![crates.io](https://img.shields.io/crates/v/salvo)](https://crates.io/crates/salvo)
[![Download](https://img.shields.io/crates/d/salvo.svg)](https://crates.io/crates/salvo)
![License](https://img.shields.io/crates/l/salvo.svg)
</p>
<h3>Salvo is a simple web framework written by rust.</h3>
</div>

## Features
  * Base on hyper, tokio.
  * Tree-like routing system.

## Quick start
You can view samples [here](https://github.com/kenorld/salvo/tree/master/examples) or read docs [here](https://docs.rs/salvo/).

Create a new rust project:
```bash
cargo new hello_salvo --bin
```

Add this to `Cargo.toml`
```toml
[dependencies]
salvo = "0.4"
tokio = { version = "1.0", features = ["full"] }
```

Create a simple function handler in the main.rs file, we call it `hello_world`, this function just render plain text "Hello World".

```rust
use salvo::prelude::*;

#[fn_handler]
async fn hello_world(_req: &mut Request, _depot: &mut Depot, res: &mut Response) {
    res.render_plain_text("Hello World");
}
```

In the main function, we need to create a root Router first, and then create a server and call it's serve function:

```rust
use salvo::prelude::*;

#[fn_handler]
async fn hello_world(_req: &mut Request, _depot: &mut Depot, res: &mut Response) {
    res.render_plain_text("Hello World");
}

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error + Send + Sync>> {
    let router = Router::new().get(hello_world);
    let server = Server::new(router);
    server.serve().await?;
    Ok(())
}
```

## License

Salvo is licensed under MIT License ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)