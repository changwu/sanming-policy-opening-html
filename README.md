# Sanming Gov Crawl Archive (三明市人民政府政务公开 爬取归档)

- 数据来源: https://www.sm.gov.cn/zw/ (政务公开) + https://www.sm.gov.cn/smsrmzfbgs/smsrmzf/ (政府信息公开) + https://www.sm.gov.cn/zcjd/ (解读回应)
- 方式: 礼貌爬取(随机延时/退避重试),TRS 统一平台 /fjdzapp/data 频道枚举 + 文章/附件抓取,SQLite 断点续爬
- 站点子目录: sanming/
- 内容: 每文章 page.txt(标题/时间/文号/机构/正文)+ page.html + links.tsv + attachments/
- 全局索引: _index.tsv / _attachments.tsv / _outbound_links.tsv / _failed_pages.txt
- 过滤: 超过 25MB 附件不推入库,见 _filtered_over_25mb.txt
