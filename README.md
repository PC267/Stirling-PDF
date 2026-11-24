# Stirling PDF 配置文件

当前 Stirling PDF v3.5.0 Docker 部署的配置文件。

## 文件说明

- `settings.yml` — Stirling PDF 主配置
- `custom_settings.yml` — 自定义覆盖配置（Free Tier 处理器额度调整）

## 自定义配置

`custom_settings.yml` 将免费层处理器额度从默认 1000 提升至 999999：

```yaml
stirling:
  billing:
    account-link:
      free-tier-units: 999999
      enabled: true
```

## 敏感信息

`settings.yml` 中的 `AutomaticallyGenerated` 密钥和 UUID 已替换为占位符，请勿将实际值提交到公开仓库。
