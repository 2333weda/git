# 部署脚本（deploy）

存放部署相关的脚本、容器编排与各环境配置，按「环境」和「用途」分离。

## 规划结构

```
deploy/
├── docker/           Dockerfile、docker-compose.yml
├── scripts/          构建、发布、备份等脚本
├── nginx/            反向代理与静态资源配置
├── env/              各环境变量模板（.env.example，真实值不进仓库）
└── README.md
```

## 约定

- 环境区分为 `dev` / `test` / `prod`，配置文件以环境名后缀区分，例如 `application-prod.yml`
- 只提交模板文件（`*.example`），真实的密钥、密码、证书一律通过部署平台或环境变量注入
- 脚本首行写明用途、参数与执行方式，统一使用 LF 换行

## 状态

⬜ 待后端工程落地后补充。
