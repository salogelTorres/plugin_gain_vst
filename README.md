# plugin_gain_vst


1. Run
```bash
cargo new gain_vst
```
2. Run
```bash
cd  gain_vst
```
3. In Cargo.toml replace:
```toml
[package]
name = "gain_vst"
version = "0.1.0"
edition = "2021"

[dependencies]
nih-plug = { git = "https://github.com/robbert-vdh/nih-plug.git", package = "nih_plug", features = ["assert_process_allocs", "standalone"] }
parking_lot = "0.12"

[lib]
crate-type = ["cdylib"]
```
4. Now, let's create xtask. Run:
```bash
mkdir xtask
mkdir xtask\src
```
Create a new Cargo.toml inside xtask directory:
```toml
[package]
name = "xtask"
version = "0.1.0"
edition = "2021"

[dependencies]
nih_plug_xtask = { git = "https://github.com/robbert-vdh/nih-plug.git" }
```
Add this content to xtask/src/main.rs:
```rust
fn main() -> nih_plug_xtask::Result<()> {
    nih_plug_xtask::main()
}
```
Finally, update your root Cargo.toml to include the workspace configuration:
```toml
...existing code...
[workspace]
members = ["xtask"]
```
5. Now we can code our GainPlugin in src/lib.rs
6. Then run:
```bash
cargo run -p xtask -- bundle gain_vst --release
```
7. Your VST3 plugin is located in /target/bundled/gain_vst.vst3.
