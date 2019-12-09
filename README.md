# seahorse

A minimal CLI framework written in Rust

## Using

```toml
[dependencies]
seahorse = { version = "0.1.0", git = "https://github.com/KeisukeToyota/seahorse.git" }
```

## Example

```rust
use std::env;
use seahorse::{App, Command, color};

fn main() {
    let args: Vec<String> = env::args().collect();

    let command = Command {
        name: "hello".to_string(),
        usage: "cli_tool hello user".to_string(),
        action: |v: Vec<String>| println!("Hello, {:?}", v)
    };

    let mut app = App::new();

    app.name = "cli_tool".to_string();
    app.display_name = color::magenta("
     ██████╗██╗     ██╗
    ██╔════╝██║     ██║
    ██║     ██║     ██║
    ██║     ██║     ██║
    ╚██████╗███████╗██║
    ╚═════╝╚══════╝╚═╝");
    app.usage = "cli_tool [command] [arg]".to_string();
    app.version = env!("CARGO_PKG_VERSION").to_string();
    app.commands = vec![command];

    app.run(args.clone());
}
```