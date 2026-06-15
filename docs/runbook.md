# Console E2E Probe 运行手册

## 本地安装与启动

## 测试、构建与健康检查

记录自动测试、生产启动、health endpoint、公网浏览器关键流程、静态资源、
控制台错误和 Kimi 截图视觉验收方式。

## 环境变量

## Base Path

项目必须支持 `/projects/console-e2e-probe/`，静态资源和前端路由不得假设部署在 `/`。

公网浏览器验收时，最终 URL 和所有项目资源必须保留此前缀。

## 缓存策略

功能迭代后公网 URL 不变，必须防止老板浏览器命中缓存旧页面：

- HTML 文档响应头必须携带 `Cache-Control: no-cache`（或 `no-store`），每次重新校验；
- 所有静态资源 URL 必须携带版本令牌 `?v=<当前发布版本 0.0.N>`，且路径保留 `/projects/console-e2e-probe/` 前缀（令牌挂在已带 basePath 的 URL 上）；
- 版本令牌随 `0.0.N` 递增，于是每个交付版本自动触发缓存失效。

浏览器验收（schema v2 机器报告）会逐条重算：`static_assets` 状态码 200–399、URL 带版本令牌且在 basePath 下，`document_cache_control` 为 no-cache/no-store。

## Aliyun systemd 与 Nginx

## 日志查看

## 常见故障与恢复

## 回滚到精确 Tag
