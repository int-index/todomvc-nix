# TodoMVC-Nix Rust

After running `nix develop`, there are packages added in the `PATH` for Rust development, like `cargo`, `rustc` and `rustfmt`.

## Development

In Nix, there are couple ways to develop rust package. In this repo, [nixkgs-mozilla](https://github.com/mozilla/nixpkgs-mozilla) is selected because it is the most up to date rust environment in the Nix world.

### **Backend**

Go to backend rust folder and run the cargo command as follows:

```
$ cd rust
$ cargo run backend
```

For the backend, we use [sqlx](https://github.com/launchbadge/sqlx), [tide](https://github.com/http-rs/tide), [serde](https://github.com/serde-rs/serde) and some of common library in rust ecosystem.

### **Frontend**

To develop frontend in Rust, only `yarn` or `npm` is needed to compile Rust into WebAssembly. Before begin running the project, please run `yarn install` or `npm install` to generate `node_modules`.

Please refer to [package.json](../rust/frontend/package.json) for further reference. In short, `rollupjs` is used to compile/package rust to wasm. Run the following command to start developing:

```
$ cd rust/frontend
$ yarn todo_watch
```

In this project, we use an FRP library called [Dominator](https://github.com/pauan/rust-dominator).

## Release

For release process, we don't use `cabal.project` anymore. Instead, run the following command to build `backend` or `frontend`:

### For non-flake-nix user:

1. Frontend
```
$ nix-build -A defaultNix.legacyPackages.x86_64-linux.nix.rustFrontend
```

2. Backend
```
nix-build -A defaultNix.legacyPackages.x86_64-linux.nix.rustBackend
```


### For flake user:

1. Frontend
```
nix build .#nix.rustFrontend
```

2. Backend
```
nix build .#nix.rustBackend
```
