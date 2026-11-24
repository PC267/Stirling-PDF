# Stirling PDF Docker 部署

基于 `stirlingtools/stirling-pdf:latest`（v3.5.0）的 Docker 部署配置。

## 目录结构

```
.
├── docker-compose.yml        # Docker Compose 配置
└── config/
    ├── settings.yml          # Stirling PDF 主配置（清理敏感信息）
    └── custom_settings.yml   # 自定义覆盖配置（Free Tier 处理器额度）
```

## 快速启动

```bash
docker compose up -d
```

## 配置说明

### docker-compose.yml

- 映射端口：`1003:1003`
- 挂载目录：`./config:/configs`
- 环境变量：
  - `TZ=Asia/Shanghai`
  - `SYSTEM_DEFAULTLOCALE=zh-CN`
  - `SECURITY_ENABLELOGIN=true`
  - `SYSTEM_ENABLEANALYTICS=false`
  - `SERVER_PORT=1003`
  - `SECURITY_LOGINATTEMPTCOUNT=10`
  - `SECURITY_LOGINRESETTIMEMINUTES=30`

### custom_settings.yml（处理器额度调整）

将免费层处理器额度从默认 1000 提升至 999999：

```yaml
stirling:
  billing:
    account-link:
      free-tier-units: 999999
      enabled: true
```

## 安全说明

以下敏感内容**不会**提交到仓库：
- `credential-encryption.key` — 凭据加密密钥
- `server-certificate.p12` — 服务器证书
- `*.mv.db` — H2 数据库文件（含用户密码哈希、JWT 密钥）
- `backup/db/*.sql` — 数据库备份（含敏感数据）
- `settings.yml` 中的 `AutomaticallyGenerated` 密钥和 UUID（已替换为占位符）
