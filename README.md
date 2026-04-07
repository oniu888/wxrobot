# 算账统计机器人（多平台版）

一套可商用的「聊天指令算账 + 自动结算 + Web 管理后台」系统，适合需要快速落地私域社群记账/开奖结算场景的团队。

> 支持多平台接入、统一账务模型、可视化后台管理，可作为源码交付项目直接二开。

---

## 项目亮点

- 多平台接入：`Telegram / QQ / 飞书 / 企业微信 / 微信相关通道`（可同时启用）
- 统一算账核心：不同平台共用同一套业务逻辑、风控与报表
- 全流程闭环：聊天收单 -> 自动结算 -> 风险预警 -> 后台审计
- Web 后台可运营：权限分级、公告推送、报表导出、数据备份
- 可二次开发：代码结构清晰，模块化 Listener 便于扩平台
 ![群聊](images/qiantai.png)
 ![后台1](images/houtai1.png)
 ![后台2](images/houtai2.png)
 ![后台3](images/houtai3.png)
---

## 功能总览

### 1) 聊天机器人能力

- 群聊/会话接收指令并解析投注文本
- 自动记录用户、平台、群号、期号等关键字段
- 开奖后自动派彩、更新会员余额与流水
- 多平台统一管理员机制（支持超级管理员）

### 2) Web 后台能力

- 首页概览：实时统计、机器人状态、开奖爬虫状态
- 投注管理：筛选查询、手动补录、批量删除、Excel 导出
- 开奖管理：录入/编辑/删除开奖结果，自动重算
- 报表分析：按时间/期号/会员/平台/群号多维分析
- 风险预警：大额投注、频繁投注、号码集中度预警
- 会员中心：余额流水、上下米审核、黑名单
- 系统管理：赔率配置、管理员管理、操作日志、数据备份

### 3) 平台协同能力

- 多平台共用同库，天然支持跨平台汇总统计
- 公告支持按平台/群号定向推送
- 自动开奖结果可广播至已配置目标群

---

## 技术架构

- 后端：Python（FastAPI + Flask + Peewee）
- 数据库：MySQL
- 前端：Vue3 + Element Plus
- 机器人入口：Listener 适配层 + Dispatcher 业务调度层

简化架构：

```text
聊天平台(多端) -> Listener适配层 -> Dispatcher算账核心 -> MySQL
                                         |
                                         +-> Web API(FastAPI) -> Vue后台
```

---

## 快速启动

### 环境要求

- Python 3.14
- MySQL 5.7+

### 1. 安装依赖

```bash
pip install -r requirements.txt
```

### 2. 配置参数

编辑 `config/config.yaml`：

- 选择 `platform` 或 `platforms`
- 填写数据库连接
- 填写对应平台的 token / key / webhook 等配置
- 生产环境务必修改 `jwt_secret`

### 3. 启动机器人

```bash
python -m src.main
```

### 4. 启动 Web 后台（可选）

```bash
python -m uvicorn web.backend.main:app --reload --port 8000
```

前端开发模式：

```bash
cd web/frontend
npm install
npm run dev
```

---

## 演示截图（建议补充）

为提升 GitHub 转化，建议你在这里放 4-6 张真实截图：

1. 聊天端下单与回复
2. 后台首页概览
3. 投注/开奖管理页
4. 报表与风险预警页
5. 多平台群推送页

示例（替换为你的图片地址）：

```md
![dashboard](docs/images/dashboard.png)
![bets](docs/images/bets.png)
![report](docs/images/report.png)
```

---

## 商业合作（源码交付）

可提供：

- 源码部署版交付（Windows / macOS / Linux）
- 指定平台接入与业务规则定制
- 后台字段/报表/权限改造
- 运维与升级支持（可选）

> 有购买或定制意向，建议通过 Issue 或邮箱沟通需求清单（预算、平台、交付时间）。

---

## 使用须知

- 本项目仅提供技术实现，不提供任何违法违规运营支持
- 使用方需自行遵守当地法律法规及平台服务协议
- 请勿将真实密钥、数据库密码、Token 等敏感信息提交到公开仓库

---

## 目录结构

```text
src/                 # 机器人核心（指令处理、结算、平台监听）
web/backend/         # Web 后端 API
web/frontend/        # Web 前端页面
config/config.yaml   # 主配置文件
tests/               # 测试用例
```

---

## License

建议你根据售卖策略二选一：

- 方案 A：仓库公开「演示版」，核心闭源（最利于商业转化）
- 方案 B：仓库开源（如 MIT），商业服务收费（部署/定制/运维）

当前可先写为：

`Copyright (c) YourName. All rights reserved.`

---

## Star 支持

如果这个项目对你有帮助，欢迎点一个 Star。  
如需私有化部署、二开接入或整套源码交付，欢迎联系。


