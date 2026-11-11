# 行间 · 私人日记与广场前端

Vue 3、Vue Router、Axios 和 Vite 实现的私人日记前端，支持个人分类、补记、广场发布及账号安全。

- 前端仓库：[wxlovex/personal_bolg_vite](https://github.com/wxlovex/personal_bolg_vite)。
- 后端仓库：[wxlovex/personal_blog](https://github.com/wxlovex/personal_blog)。
- 本地前端目录：`D:\project\personal_blog_vite`；仓库名按创建时指定保留 `personal_bolg_vite`。

## 本地开发

按 Vite 的 engines 要求安装 Node.js；配套 CI 使用 Node.js 24。

```sh
npm ci
npm run dev
```

开发页面默认地址为 `http://localhost:5173`。Vite 将 `/api` 请求转发到 `http://localhost:8080`，保留 `/api` 前缀。先按后端 README 配置并启动 Spring Boot 服务。

```sh
npm run build
npm run preview
```

生产文件输出到 `dist/`。`preview` 仅用于检查构建结果；线上由后端容器提供静态页面和同域 API。

## 后端部署快照与验证

在后端目录运行以下命令，将本仓库源码同步到后端的 `frontend/`，供现有 Docker/Render 构建使用：

```powershell
./scripts/prepare-render.ps1 -FrontendPath D:/project/personal_blog_vite
./scripts/check-frontend-snapshot.ps1 -SourcePath D:/project/personal_blog_vite
```

前端变更应同时提交到本仓库及后端的 `frontend/` 快照。后端 CI 会构建快照，并运行 `scripts/verify-review-regressions.py` 的浏览器回归。
审查与验证详情见后端的 [修复记录](https://github.com/wxlovex/personal_blog/blob/main/docs/review-fixes-2026-11-11.md)。

`node_modules/`、`dist/`、本地环境变量和 IDE 工程文件不纳入版本控制。部署所需密钥只在后端运行环境配置。
