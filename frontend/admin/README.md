# 管理端（frontend/admin）

Vue 3 + Vite + Element Plus，服务场地管理员与学院管理员。对应需求说明书 4.2 节 M-01 ~ M-06。

## 规划结构

```
admin/
├─ src/
│  ├─ views/          m01-venues ... m06-logs（与模块编号对应）
│  ├─ components/     表格、详情抽屉、图表等复用组件
│  ├─ api/            接口封装，按模块拆分
│  ├─ router/         路由与角色守卫（守卫只做体验，权限在服务端）
│  ├─ stores/         Pinia 状态
│  └─ styles/         主题变量
└─ README.md
```

## 页面与模块对应

| 路由 | 模块 | 权限范围 |
| --- | --- | --- |
| `/venues` | M-01 场地与时段 | `RESOURCE` 读写 / `COLLEGE` 读写 |
| `/approvals` | M-02 预约审批 | `RESOURCE` 写，且不得自审 |
| `/users` | M-03 用户与角色 | 仅 `COLLEGE` 可写 |
| `/failures` | M-04 爽约名单 | `RESOURCE` / `COLLEGE` 读，导出脱敏限次 |
| `/utilization` | M-05 利用率统计 | `RESOURCE` / `COLLEGE` 读 |
| `/logs` | M-06 操作日志 | 只读，导出写二次审计 |

## 约定

- 后台以"列表 → 详情抽屉"为主，不做三层以上跳转
- 前端只做展示与预校验；越权判断、数据范围过滤一律在服务端
- 前端按错误码分支处理，不解析提示文案
- `npm run dev` 默认 `http://localhost:5173`，接口代理指向后端 `http://localhost:3000`

## 状态

⬜ 尚未初始化。
