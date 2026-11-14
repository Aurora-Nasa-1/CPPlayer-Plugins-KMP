# CPPlayer-Plugins-KMP

CPPlayer KMP（Kotlin Multiplatform）专用插件市场与分发仓库。

## 概述
本仓库专为遵循 `kmp-sdk-v1` 契约规范的新一代 CPPlayer 音源插件及歌词插件提供索引清单与分发支持。

- 目录清单地址: `https://raw.githubusercontent.com/Aurora-Nasa-1/CPPlayer-Plugins-KMP/main/index.json`
- 规范文档参考: [CPPlayer-KMP 仓库文档](https://github.com/Aurora-Nasa-1/CPPlayer-KMP)

旧版本客户端继续使用 `CPPlayer-Plugins`（网易云 1.1.1）；本仓库只服务新版本客户端。

发布前运行：

```text
python scripts/validate_catalog.py --verify-packages
```

目录中的 `version`、`apiVersion`、`minHostApiVersion`、`runtime` 必须与包内
`manifest.json` 完全一致；缺省字段按 `1` 处理。

## Windows 原生构建（GraalVM Native Image）

从网易云 `1.3.0` / 酷狗 `0.3.0` 起，两个音源除了 JNI 还导出一套 C ABI v1
（`cpp_abi_version` / `cpp_create` / `cpp_invoke` / `cpp_cancel` / `cpp_close`），
宿主按符号直调，因此**原生构建的客户端也能导入这两个音源**。

- 新发布的目录条目使用 `runtime: "native"`，包内 `manifest.json` 的 `type` 也必须是
  `native`。C ABI 是同一个 DLL 里的追加导出，包格式与校验方式不变。
- `runtime: "jni"` 仅保留给已发布的旧包。1.8.7 及更早的宿主忽略 `contract`，
  会把 `type: "jni"` 的 SDK 包当成旧 JNI Provider；新条目改用 `native` 后，
  旧宿主会明确拒绝，而不是静默走旧协议。
- 需要宿主 `>= 1.9.0`（首个带 C ABI 桥的版本）。更早的原生构建客户端导入这两个包
  会明确提示「该音源只导出了 JNI 符号」，不会留下半装状态。
- 规范（内存所有权、返回码、线程与生命周期约束）见 CPPlayer-KMP 仓库的
  `docs/dev/PROVIDER_NATIVE_ABI.md`。
