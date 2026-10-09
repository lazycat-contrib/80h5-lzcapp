# 80h5-lzcapp

网页版 NES 模拟器 **80h5**（`ghcr.io/liangminmx/80h5`）的懒猫微服打包：**只发喵喵商店，镜像模式**。

- **镜像**：`ghcr.io/liangminmx/80h5:latest`（nginx 静态站，644 个 FC 游戏，容器内监听 **3080**）。镜像模式只做只读校验，manifest 里的镜像行已写成 `ghcr.1ms.run/...` 加速地址。
- **可变 tag**：上游只有 `latest`，按 skill 的标准形状处理——`bump: patch` + `channel: custom` + `sort: created` + `tag_regex: '^latest$'` + `require_digest_match: true`；**镜像行带摘要（digest-pinned）**，那串摘要就是 bump 的基线，没有基线时 Action 会 fail closed。
- **路由**：`/` → `app-80h5:3080`（服务名沿用 compose 里的 `app-80h5`），`public_path: [/]`，手机/平板打开即玩。
- **无数据卷**，`user: root`（镜像默认 root），健康检查 `wget :3080/`。
- 图标：用户提供的 `game.png`（实心手柄）铺红底。
