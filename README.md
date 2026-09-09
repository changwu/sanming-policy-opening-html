# 三明市人民政府政务公开 - 网站公开内容爬取归档

公开内容爬取与自动存档仓库(礼貌爬取:随机延时 + 退避重试,全程未触发反爬)。

## 站点

| 站点子目录 | 站点 | 状态 |
|---|---|---|
| [sanming/](sanming/) | 三明市人民政府政务公开(https://www.sm.gov.cn/zw/ 及直接链接的政府信息公开/解读回应子板块与 *.sm.gov.cn 子站文章) | ✅ 已归档 |

## 数据规模(sanming/)

- 文章页 done: 37,175(死链 404: 153,持续失败: 2)
- 附件下载成功: 7,708(失败死链: 149;CMS 元数据误报跳过: 12)
- 栏目/频道: 385 个(全部按 TRS 平台 API 枚举,无遗漏)
- 站外链接记录: 136
- 本地完整副本约 10.4GB;本仓库站点子目录约 3.9GB(受 GitHub 仓库 5GB 硬性上限约束)

## 内容与结构(每个文章目录)

```
<栏目路径>/<年月>/<文档ID>/
    page.txt      # 标题/发布时间/文号/发布机构/栏目/原始链接/本地目录/正文
    links.tsv     # 页内 attachment/image/link 链接记录
    attachments/  # 同域下载的附件
```

- 全站索引: `sanming/_index.tsv` / `_attachments.tsv` / `_outbound_links.tsv`
- 失败清单: `sanming/_failed_pages.txt` / `_failed_attachments.txt`
- 目录结构(含未入库文件): `sanming/_directory_tree.txt`

## 过滤规则(见各清单)

1. 单文件 >25MB:不入库(规格要求),本地完整保留 —— `_filtered_over_25mb.txt`(69 个,3.36GB)
2. GitHub 仓库 5GB 硬性上限守卫:原始网页存档 `page.html` 与视频媒体(mp4/flv/mpg 等)不入库,本地 output 完整保留 —— `_filtered_repo_size_guard.txt`(37,259 个,3.14GB)

> 正文文本(page.txt)、附件(文档/图片,≤25MB)、列表接口 JSON 均完整入库。

## 技术说明

- 来源: TRS 统一内容平台,频道枚举接口 `GET /fjdzapp/data`(channelid=100000,classsql=chnlid=…,prepage=100),比静态翻页更完整
- 断点续爬: SQLite 状态库(state.db),中断后重跑自动跳过已完成项
- 双模板正文抽取(TRS_Editor 等),抽取质量抽查 1200 样本:正文缺失 0 / 标题缺失 0 / 编码错误 0

_生成于 2026-09-09,由 dsh-crawl-agent 礼貌爬取_
