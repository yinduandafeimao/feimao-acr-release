# feimao ACR 公开发布仓内容

本目录**仅含发布物**（JSON + zip），不含 C# 源码。同步到公开仓库：

https://github.com/yinduandafeimao/feimao-acr-release

## 玩家添加作者源

HiAuRo → **ACR 源管理** → 添加并启用：

```text
https://raw.githubusercontent.com/yinduandafeimao/feimao-acr-release/main/publisher.json
```

然后在 **ACR 列表** → 刷新 → 下载「feimao 机工」。

安装目录（自动）：`pluginConfigs/HiAuRo/ACR/feimao.mch/feimao.mch.dll`

## 作者发布新版本（在私有源码仓根目录）

```powershell
.\scripts\Pack-Release.ps1 -Version 1.0.1 -Changelog "修复说明"
```

脚本会：编译 Release → 打 zip → 更新 `release/feimao.mch.manifest.json` 的 `sha256` 与 `packageUrl`。

然后：

```powershell
# 1. 推 manifest / publisher 到公开仓 main
cd release
git add publisher.json feimao.mch.manifest.json README.md
git commit -m "release: v1.0.1"
git push

# 2. 在公开仓创建 GitHub Release 并上传 zip（路径见脚本输出）
gh release create v1.0.1 ..\dist\feimao.mch.zip --repo yinduandafeimao/feimao-acr-release --title "v1.0.1" --notes "修复说明"
```

## 与手动安装的区别

| 方式 | 目录 |
|------|------|
| 手动拷贝（旧） | `ACR/feimao/feimao.dll` |
| 作者源下载（新） | `ACR/feimao.mch/feimao.mch.dll` |

设置分别保存在 `setting/ACR/feimao/` 与 `setting/ACR/feimao.mch/`。
