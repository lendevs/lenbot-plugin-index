# LenBot 社区插件目录

LenBot 随附的插件目录只收录官方插件，其他插件收录在这里。在 LenBot 面板的**插件 → 发现插件 → 目录来源**填入下面的地址，就能浏览和安装这里的插件：

```text
https://raw.githubusercontent.com/lendevs/lenbot-plugin-index/main/catalog.json
```

## 收录条件

- 插件是一个独立的公开 Git 仓库，仓库根目录有 `plugin.toml`、`__init__.py`、README 和许可证文件。
- 条目的 `ref` 是完整的 40 位提交号。更新插件时把 `ref` 和 `version` 改到新的提交。
- 条目的 `name`、`version`、`interface` 与这个提交中的 `plugin.toml` 一致；写了 `permissions` 和 `requires_lenbot` 时也要一致。
- 插件名在目录中唯一，不与官方插件重名。

## 提交条目

在 `catalog.json` 的 `entries` 中加一项，提交 Pull Request。条目格式和各字段的含义见 LenBot 文档站的[发布到插件目录](https://lendevs.github.io/LenBot/develop/plugin-catalog)。

CI 用 LenBot 仓库中的 `scripts/check_plugin_catalog.py` 逐项取出 `ref` 指向的提交，核对清单和文件，不导入、不运行插件代码。提交前可以在本机检查（LenBot 仓库与本仓库放在同一目录下）：

```sh
uv venv --python 3.13
uv pip install ../LenBot
uv run --no-project python ../LenBot/scripts/check_plugin_catalog.py catalog.json --only <插件名>
```
