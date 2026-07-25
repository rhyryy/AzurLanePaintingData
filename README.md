# AzurLanePaintingData

《碧蓝航线》国服客户端立绘数据，供
[`AzurLaneTools`](https://github.com/Pelom777/AzurLaneTools)
等项目读取。

数据从 Android 游戏资源提取并转换，不包含游戏程序本体。

## 目录

```text
data/
├─ ship.json
└─ skin.json
painting/<皮肤名>/
├─ <图层>.png
├─ <图层>-mesh.obj
└─ <皮肤名>.json
paintingface/<皮肤名>/
└─ <表情编号>.png
```

- `data/ship.json`：舰船基础信息。
- `data/skin.json`：舰船皮肤信息。
- `painting`：立绘碎片、Mesh 和图层位置 JSON。
- `paintingface`：表情差分图片，文件名按数字编号。

## 在 AzurLaneTools 中使用

可以将本仓库的 `data`、`painting`、`paintingface` 放入
AzurLaneTools 的 `public` 目录，保持上述目录结构不变。

也可以使用 GitHub Raw：

```text
https://raw.githubusercontent.com/rhyryy/AzurLanePaintingData/master/
```

例如：

```text
https://raw.githubusercontent.com/rhyryy/AzurLanePaintingData/master/paintingface/<皮肤名>/<编号>.png
```

## 提交新版本皮肤

推荐使用 `AzurLanePaintingUpdater`。需要 Windows、uv、ADB、Git、
GitHub CLI，以及一台已开启 USB 调试并安装国服《碧蓝航线》的 Android 手机。

首次准备：

```powershell
gh auth login
gh repo fork rhyryy/AzurLanePaintingData --clone
cd AzurLanePaintingUpdater
uv sync
```

以下示例假定 `AzurLanePaintingUpdater` 和 clone 下来的
`AzurLanePaintingData` 两个目录同级；路径不同时请替换为实际路径。

生成新增皮肤：

```powershell
uv run azur-lane-update prepare ..\AzurLanePaintingData
```

检查结果后提交 Pull Request：

```powershell
uv run azur-lane-update submit ..\AzurLanePaintingData
```

如果需要重新导出已有皮肤：

```powershell
uv run azur-lane-update prepare ..\AzurLanePaintingData --painting changfeng_3
```

请只提交以下内容：

- `data/ship.json`
- `data/skin.json`
- `painting/`
- `paintingface/`

不要手工修改生成的 Mesh、图层 JSON 或表情编号。导出失败时，请先查看
Updater 的 `logs/`，不要提交不完整资源。
