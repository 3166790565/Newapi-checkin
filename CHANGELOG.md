# 更新日志 (Changelog)

## 2026-07-31

### 🐛 修复

- README 邮件通知的 Secret 名称与代码不一致（`SMTP_*` → `EMAIL_*`），并修正 Q&A 中的字段名（`username/password` → `login_username/login_password`）
- keepalive 工作流只 echo 无法防止 GitHub 禁用定时工作流，改用 `gautamkrishnar/keepalive-workflow` 推送空提交制造仓库活动
- 控制台执行时间与通知时间不一致（GitHub Actions 的 UTC runner 上相差 8 小时），统一为北京时间

### ✨ 功能

- 签到接口增加自动重试：网络超时/连接异常、HTTP 429/5xx 时指数退避重试（最多 2 次），避免瞬时故障误报

### ♻️ 重构

- 额度格式化统一复用 `notifier.format_quota`，删除 `checkin.py` / `test_checkin.py` 中的重复实现
- `import re` 上提至模块顶部；`import pytz` 保持 `main()` 内延迟导入（避免 `from checkin import NewAPICheckin` 时强制要求 pytz）
- `_mask_url` 去重为 `cf_bypass.mask_url` 单一实现，并修复二级域名脱敏输出 `example.***.com` 的误导问题

### 📚 文档

- README 新增签到重试特性说明、`CHANGELOG.md` 文件清单条目
- `requirements.txt` 补充每行依赖用途注释
