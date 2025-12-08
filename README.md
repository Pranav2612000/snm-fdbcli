# 📦 snm-fdbcli  
### A Modern Interactive CLI & Library for FoundationDB (Directory + Tuple Layer)

[![Crates.io](https://img.shields.io/crates/v/snm-fdbcli)](https://crates.io/crates/snm-fdbcli)
[![Documentation](https://docs.rs/snm-fdbcli/badge.svg)](https://docs.rs/snm-fdbcli)
[![License](https://img.shields.io/crates/l/snm-fdbcli)](LICENSE)
[![Downloads](https://img.shields.io/crates/d/snm-fdbcli)](https://crates.io/crates/snm-fdbcli)
[![Recent Downloads](https://img.shields.io/crates/dr/snm-fdbcli)](https://crates.io/crates/snm-fdbcli)

![SnmFDBCLI](https://srotas-suite-space.s3.ap-south-1.amazonaws.com/srotas-space.png)

### 🧩 Built on the Official FoundationDB Rust Crate

This project is powered by the official FoundationDB Rust bindings:

```CMD
foundationdb = { version = "0.10.0", features = ["embedded-fdb-include", "fdb-7_3"] }
```


`snm-fdbcli` is a powerful **FoundationDB Directory/Tuple explorer**, providing:

- ✔️ CLI commands (`dircreate`, `dirlist`, `pack`, `unpack`, `range`, `clearprefix`)  
- ✔️ A REPL / interactive shell (`snm-fdbcli repl`)  
- ✔️ High-level Rust APIs for directory management  
- ✔️ Tuple pack/unpack helpers  
- ✔️ Range queries, prefix queries, deletion  
- ✔️ Dump entire subspaces  
- ✔️ Works with any FoundationDB cluster (local or remote)  

---

## 🚀 Features

### Directory Layer  
- Create directories at any depth  
- List subdirectories  
- Open existing directories  

### Tuple Layer  
- Pack `(a, 1, "demo")` into FDB key  
- Unpack bytes back to tuple  
- Automatic prefix-range generation  

### Data Operations  
- Read range  
- Query tuple ranges  
- Delete prefix ranges  
- Dump entire directories  

---

# 📥 Installation

### Build the CLI
```bash
cargo install snm-fdbcli
```

---

# 🔧 Configuration

Export your cluster file path:

```bash
export SNM_FDBCLI_DB_PATH="/usr/local/etc/foundationdb/fdb.cluster"
```

If not set, `Database::default()` is used.

---


### Interactive Shell

```bash
$ snm-fdbcli repl
snm-fdbcli> help
snm-fdbcli> dircreate srotas users
snm-fdbcli> dirlist
snm-fdbcli> dirlist srotas
snm-fdbcli> seed user-1
snm-fdbcli> show-user user-1
snm-fdbcli> show-wallet user-1
snm-fdbcli> logins user-1
snm-fdbcli> orders user-1
snm-fdbcli> pack (user-1, 1)
snm-fdbcli> unpack 0167757365722d31000000000000000100
snm-fdbcli> range srotas logins (user-1)
snm-fdbcli> clearprefix srotas logins (user-1)
snm-fdbcli> dump-all
snm-fdbcli> exit
```


# 🖥️ CLI Usage

```bash
snm-fdbcli init
snm-fdbcli seed --user user-1
snm-fdbcli show-user user-1
snm-fdbcli show-wallet user-1
snm-fdbcli show-logins user-1
snm-fdbcli show-orders user-1
snm-fdbcli dump-all
snm-fdbcli repl
```

---

# 🐚 REPL MODE

Commands:

```
init
seed <user>
show-user <user>
show-wallet <user>
logins <user>
orders <user>
dump-all
dircreate <path>
dirlist <path>
pack (tuple)
unpack <hex>
range <dir> (tuple)
clearprefix <dir> (tuple)
help
exit
```

---

# 🔑 Tuple Pack / Unpack

```
snm-fdbcli> pack (user-1, 1)
snm-fdbcli> unpack 01677573...
```

---

# 📚 Range Queries

```
snm-fdbcli> range srotas/logins (user-1)
snm-fdbcli> clearprefix srotas/logins (user-1)
```

---

# 🧪 Tests

### Unit tests (no DB required)
```bash
cargo test
```

### Full end-to-end (requires running FDB)
```bash
cargo test -- --ignored
```

---

# 📘 Library API Examples

```rust
let db = snm_fdbcli::connect_db()?;
let dir = snm_fdbcli::dir_create(&trx, &["srotas", "users"]).await?;
let key = snm_fdbcli::tuple_pack_from_string("(user-1,1)")?;
```

---

Made with ❤️ by the [Srotas Space] (https://srotas.space/open-source)


---

## 👥 Contributors

- **[Snm Maurya](https://github.com/xsmmaurya)** - Creator & Lead Developer
  <img src="https://srotas-suite-space.s3.ap-south-1.amazonaws.com/snm.jpeg" alt="Snm Maurya" width="80" height="80" style="border-radius: 50%;">
  [LinkedIn](https://www.linkedin.com/in/xsmmaurya/)


[![GitHub stars](https://img.shields.io/github/stars/srotas-space/snm-fdbcli?style=social)](https://github.com/srotas-space/snm-fdbcli)



---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
