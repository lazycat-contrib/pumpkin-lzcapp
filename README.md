# Pumpkin for LazyCat

将 [Pumpkin](https://github.com/Pumpkin-MC/Pumpkin) 打包为 LazyCat LPK v2。Pumpkin 的目标是让每个人都能托管快速、高效的 Minecraft 服务器。

## 连接端口

| 客户端 | 协议 | 端口 |
| --- | --- | ---: |
| Minecraft Java Edition | TCP | `25565` |
| Minecraft Bedrock Edition | UDP | `19132` |

安装后打开应用可查看当前主机名，并一键复制对应的服务器地址。Pumpkin 没有 Web 管理后台，应用入口是内嵌的本地介绍页。

## 数据与运行方式

- 上游镜像：`ghcr.io/pumpkin-mc/pumpkin:0.1.0`
- 运行镜像：`ghcr.1ms.run/pumpkin-mc/pumpkin:0.1.0`
- 容器数据目录：`/pumpkin`
- LazyCat 持久化目录：`/lzcapp/var/pumpkin`
- 服务名：`pumpkin`
- 未添加健康检查，与上游 Compose 保持一致

## 本地构建

```bash
lzc-cli project release -o dist/application.lpk
lzc-cli lpk info dist/application.lpk
```

## 自动发布

`.github/workflows/lazycat.yml` 使用 `ca-x/lazycat-github-action` 检查新的稳定 SemVer 镜像标签，创建版本化 GitHub Release Asset，并只发布到喵喵私有商店。需要为仓库配置：

- `APPSTORE_URL`
- `APPSTORE_TOKEN`
- `APP_ID`，可选
- `PRIVATE_STORE_GROUP_CODES`，可选，用于私有分组

镜像使用 GHCR 默认镜像加速前缀，并在发布前校验 `linux/amd64` 源镜像与镜像加速地址的 digest 一致。

## 来源与许可

Pumpkin 由 [Pumpkin-MC](https://github.com/Pumpkin-MC) 维护，并采用 GPL-3.0 许可证。本仓库仅包含 LazyCat 打包配置、介绍页和用户提供的图标资源。
