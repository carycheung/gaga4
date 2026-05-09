# gaga4 — GA4 调度器

每天北京时间 09:07,调用 GitHub API 触发 [carycheung/GA4](https://github.com/carycheung/GA4) 私有 repo 里的 `daily-report.yml`。

## 为什么单独建这个 repo

GitHub 的 schedule cron 在**私有 repo**上经常被丢/延迟数小时,但**公开 repo**稳定得多。所以拆成两个 repo:
- `gaga4`(本 repo,公开)— 只负责调度触发
- `GA4`(私有)— 真正跑 GA4 监控 + 飞书推送

## 配置

1. **Secret:** `TRIGGER_PAT` — fine-grained PAT,scope 是 `Actions: Read and write`,仅限 `carycheung/GA4`
2. **Schedule:** UTC 01:07 = 北京 09:07,错开整点

## 手动触发

Actions 页面 → Trigger GA4 Daily Report → Run workflow,可填日期。

## 故障

- 触发失败(HTTP != 204)→ 检查 PAT 是否过期
- 触发成功但 GA4 没跑 → 检查 GA4 私有 repo Actions 页面看真实运行结果
