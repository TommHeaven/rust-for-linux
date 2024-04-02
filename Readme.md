# rust for linux 6.9

1. 将此目录中的rustc重置为特定版本,可提前为rustup设置代理，以便加速下载过程
```
rustup override set $(scripts/min-tool-version.sh rustc)
```
2. 添加rust-src源代码
```
rustup component add rust-src
```
3. 可为cargo仓库crates.io设置使用镜像，安装bindgen工具，注意在0.60版本后，bindgen工具的命令行版本位于bindgen-cli包中
```
cargo install --force --locked --version $(scripts/min-tool-version.sh bindgen) bindgen-cli
```
4. 检查内核rust支持已经启用
```
make LLVM=1 rustavailable
```
5. 配置和编译
```
make x86_64_defconfig
make LLVM=1 menuconfig
#set the following config to yes
General setup
        ---> [*] Rust support
make LLVM=1 -j$(nproc)
```