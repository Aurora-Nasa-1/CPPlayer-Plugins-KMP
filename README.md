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
