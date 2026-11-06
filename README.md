# resource

Shuyra 的 `no_std` 用户态资源机制库：孔通信、页映射、门铃与多路等待。

`src/capability.rs`、`loan.rs` 管理能力持有与派生授予；`dock.rs`、`port.rs`、
`bell.rs`、`pile.rs` 是使用入口。`kernel.rs` 与 `mapping_kernel.rs` 定义内核调用边界，
`native.rs` 提供原生实现。原始能力表查询与 token 适配集中在 `raw.rs`，不表示资源已验证。
所有权、释放和撤销条件以对应源码接口文档为准。

`tests/capability` 是独立宿主工作区，直接使用生产模块并注入 fake Env。
根库禁用测试入口；应运行能力工作区，而非将根目录零用例视为验证。

## 工具链与维护

使用 `rust-toolchain.toml` 固定的 `nightly-2026-09-04`，首次运行需要 Rustup
下载工具链及 RV64 目标。依赖版本以 Cargo 清单和锁文件为准。
下列命令从仓库根目录执行；宿主测试不代表真实内核运行验证。

```sh
cargo check --locked --target x86_64-unknown-linux-gnu
cargo build --locked --target riscv64gc-unknown-none-elf
cargo test --locked --manifest-path tests/capability/Cargo.toml --target x86_64-unknown-linux-gnu
```

## 贡献与来源

维护与 PR 规则见 [Shuyra 贡献规范](https://github.com/shuyra-arche/vanllia/blob/main/CONTRIBUTING.md)。
来源、作者与许可情况见 [PROVENANCE.md](PROVENANCE.md)。
