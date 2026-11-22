# 前端工程（frontend）

按端分离，两端互不共享构建配置：

| 目录 | 端 | 技术选型 | 页面编号 |
| --- | --- | --- | --- |
| `miniprogram/` | 学生端 | 微信小程序（原生） | S-01 ~ S-06 |
| `admin/` | 管理端 | Vue 3 + Vite + Element Plus | M-01 ~ M-06 |

两端的低保真稿见 [docs/prototypes/html/](../docs/prototypes/html/)，线框与页面编号以需求说明书第 7 章为准。

## 约定

- 组件文件名用大驼峰 `SlotCard.vue`，页面 / 目录用小写短横线 `slot-list/`
- 接口请求统一收口到各自 `src/api/`，不在页面里直接写 `fetch` / `axios`
- 环境变量只暴露非敏感项；真实密钥一律通过部署环境注入
- 构建产物 `dist/`、依赖 `node_modules/` 已在 `.gitignore` 中排除

## 状态

⬜ 尚未初始化，待后端接口契约确定后建脚手架。
