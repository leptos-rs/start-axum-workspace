<picture>
    <source srcset="https://raw.githubusercontent.com/leptos-rs/leptos/main/docs/logos/Leptos_logo_Solid_White.svg" media="(prefers-color-scheme: dark)">
    <img src="https://raw.githubusercontent.com/leptos-rs/leptos/main/docs/logos/Leptos_logo_RGB.svg" alt="Leptos Logo">
</picture>

# Leptos Axum Starter Template

This is a template for use with the [Leptos](https://github.com/leptos-rs/leptos) web framework and the [cargo-leptos](https://github.com/leptos-rs/cargo-leptos) tool using [Axum](https://github.com/tokio-rs/axum).

## Creating your template repo

If you don't have `cargo-leptos` installed you can install it with

```bash
cargo install cargo-leptos --locked
```

Then run
```bash
cargo leptos new --git https://github.com/leptos-rs/start-axum-workspace/
```

to generate a new project template.

```bash
cd {{project-name}}
```

to go to your newly created project.  
Feel free to explore the project structure, but the best place to start with your application code is in `src/app.rs`.  
Additionally, Cargo.toml may need updating as new versions of the dependencies are released, especially if things are not working after a `cargo update`.

### Islands support

Note that for islands to work correctly, you need to have a `use app;` in your frontend `lib.rs` otherwise rustc / wasm_bindgen gets confused.
To prevent clippy from complaining, at the top of the `frontend/lib.rs` file place:
```rust
#[allow(clippy::single_component_path_imports)]
#[allow(unused_imports)]
use app;
```

## Running your project

```bash
cargo leptos watch
```

## Installing Additional Tools

By default, `cargo-leptos` uses `nightly` Rust, `cargo-generate`, and `sass`. If you run into any trouble, you may need to install one or more of these tools.

1. `rustup toolchain install nightly --allow-downgrade` - make sure you have Rust nightly
2. `rustup default nightly` - setup nightly as default, or you can use rust-toolchain file later on
3. `rustup target add wasm32-unknown-unknown` - add the ability to compile Rust to WebAssembly
4. `cargo install cargo-generate` - install `cargo-generate` binary (should be installed automatically in future)
5. `npm install -g sass` - install `dart-sass` (should be optional in future

## Compiling for Release
```bash
cargo leptos build --release
```

Will generate your server binary in target/server/release and your site package in target/site

## Testing Your Project

Cargo-leptos uses (https://playwright.dev)[Playwright] as the end-to-end test tool. 

Prior to the first run of the end-to-end tests run Playwright must be installed. 
In the project's `end2end` directory run `npm install -D playwright @playwright/test` to install playwright and browser specific APIs.

To run the tests during development in the project root run:
```bash
cargo leptos end-to-end
```

To run tests for release in the project root run:
```bash
cargo leptos end-to-end --release
```
There are some examples tests are located in `end2end/tests` directory that pass tests with the sample Leptos app.

A web-based report on tests is available by running `npx playwright show-report` in the `end2end` directory.


## Executing a Server on a Remote Machine Without the Toolchain
After running a `cargo leptos build --release` the minimum files needed are:

1. The server binary located in `target/server/release`
2. The `site` directory and all files within located in `target/site`

Copy these files to your remote server. The directory structure should be:
```text
{{project-name}}
site/
```
Set the following environment variables (updating for your project as needed):
```text
LEPTOS_OUTPUT_NAME="{{project-name}}"
LEPTOS_SITE_ROOT="site"
LEPTOS_SITE_PKG_DIR="pkg"
LEPTOS_SITE_ADDR="127.0.0.1:3000"
LEPTOS_RELOAD_PORT="3001"
```
Finally, run the server binary.

## Licensing

This template itself is released under the Unlicense. You should replace the LICENSE for your own application with an appropriate license if you plan to release it publicly.
