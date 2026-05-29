# AI 变更记录：beta-release-0.3.3-beta.1

## 2026-05-29 发布测试版本 v0.3.3-beta.1

- 变更摘要：按内部单包发布流程准备 `0.3.3-beta.1` 测试版本。
- 涉及文件/模块：`package.json`、`pnpm-lock.yaml`、`.gitignore`、`README.md`、`internal/cli/package_json_test.go`、`dist/release-assets`、内部 npm beta 发布链路、GitLab `dev` 分支与 `v0.3.3-beta.1` tag。
- 关键逻辑/决策：严格按内部单包发布文档在项目根目录创建本地 `.npmrc`，指向内部 Nexus npm-hosted registry；`.npmrc` 含鉴权信息，仅保留在本地并通过 `.gitignore` 防止误提交；`publishConfig.registry` 同步切到内部 Nexus，避免发布命令被历史 npmjs 配置覆盖；通过 Corepack 固定 pnpm 版本，保证文档中的 `pnpm` 命令可复现；从当前 GitLab `dev` 分支发布，本次只推送 GitLab tag 并发布内部 npm `beta` dist-tag，不创建 GitHub 或 GitLab Release 页面；发布前执行完整检查，并通过 `make release-assets` 生成 npm 包内携带的多平台二进制资产。
- 验证策略：发布前按文档校验 `pnpm install`、`pnpm test`、`pnpm build`、`npm pack --dry-run --ignore-scripts`，并保留项目完整 `make release-check`；构建后检查 release assets 文件名与数量；发布后验证内部 npm `beta` dist-tag、临时安装、`contract-cli --version`、`skills list`、`skills install` 以及 GitLab 远端分支/tag。
