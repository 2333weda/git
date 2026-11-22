# 协作规范

> 总纲见 [README.md](README.md) 第 9 节；这里写执行细节，组内按此执行，不做额外细分。

## 1. 分支模型

```
main ────●────●────●────●────●──→  始终可演示、可联调，受保护
          \        \        \
           \        \        └─ fix/checkin-timeout   （短分支，1—3 天）
            \        └────────── feat/admin-stats
             └────────────────── feat/slot-model
```

- `main`：唯一长期分支。禁止直接 push，禁止 force push。
- 功能分支：从最新 `main` 切出，完成即合并删除。课程周期内不设 `develop` / `release` / `hotfix` 等长期分支。
- 标签：阶段交付在 `main` 上打 tag——`v0.1-需求冻结`、`v0.2-联调可用`、`v1.0-验收`。

## 2. 命名

格式 `前缀/简短说明`，全小写，单词间用连字符，不用中文、不用下划线、不用日期。

| 前缀 | 用于 | 例子 |
| --- | --- | --- |
| `feat/` | 新功能 | `feat/slot-model`、`feat/booking-api`、`feat/checkin`、`feat/miniprogram-pages`、`feat/admin-stats` |
| `fix/` | 修缺陷 | `fix/booking-overlap`、`fix/signin-window` |
| `docs/` | 文档 | `docs/requirement-ch4` |
| `chore/` | 构建、依赖、配置 | `chore/nginx`、`chore/env-sample` |

判断标准只有一条：**看名字知道大概在做什么**。`feat/booking-api` 合格，`feat/booking-api-create-endpoint-v2-20261122` 过度。

一个分支一个目的。做着做着发现要顺手改别的，另开分支，不要混在一个 MR 里。

## 3. 提交信息

```
类型(范围): 说明
```

- 类型：`feat` 新功能 / `fix` 修复 / `docs` 文档 / `style` 格式 / `refactor` 重构 / `test` 测试 / `chore` 杂项
- 范围：模块名，如 `booking`、`checkin`、`auth`、`admin`、`readme`
- 说明：动宾短语，写清做了什么，不写"更新""修改"

```text
feat(booking): 实现 C-05 重叠与 C-06 相邻间隔校验
fix(checkin): 修正签到窗口右边界，等于 +15 分钟仍可签
docs(requirement): 补第 3 章约束条目表
chore(deploy): 添加 Nginx 反向代理配置示例
```

一次提交只做一件事；提交前确保能编译、能启动，禁止把"先存一下"的半成品推到 `main`。

## 4. 日常流程

```bash
git switch main && git pull              # 1. 更新主干
git switch -c feat/booking-api           # 2. 切功能分支
#   ... 编码、自测 ...
git add . && git commit -m "feat(booking): 实现 C-03/C-04 校验"
git push -u origin feat/booking-api      # 3. 推送到远端
# 4. 平台上发起 MR → 1 人 review → squash 合并 → 删除分支
```

## 5. 合并请求（MR / PR）

1. 推分支后在平台上发起合并请求，标题与分支同义，例如「feat: 预约冲突校验」。
2. 描述写三行：改了什么、怎么验证的（跑了哪条 TC）、影响范围（是否动数据库结构）。
3. 至少 1 名组员 review；关注点：边界是否按规则卡、权限是否在服务端、错误码是否与需求说明书表 3-2 一致。
4. 通过后 **squash 合并** 到 `main`，删除源分支。

## 6. 冲突处理

- 先 `git pull --rebase origin main`，在自己分支上解决冲突，再推。
- 冲突集中在 `package-lock.json`、生成文件时不要手改，删除后重新安装 / 生成。
- 数据库结构变更（`db/schema.sql`）冲突必须两人当面确认，不能各改各的。

## 7. 提交前自检

- [ ] 代码能跑，未提交 `node_modules`、`dist`、`.env`
- [ ] 提交信息符合 `类型(范围): 说明`
- [ ] 涉及约束的改动，同步了需求说明书表 3-1 / 3-3 与用例编号
- [ ] 没有把他人手机号、真实密钥、测试账号密码写进代码或日志
