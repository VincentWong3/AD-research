# 归档规范（CONTRIBUTING）

新增论文翻译时，请严格遵守以下规则，保持仓库整洁统一。

## 结构规范

```
<论文名或代号>/
└── <论文名或代号>_中文.pdf      # 唯一的成品文件
```

- 每个论文一个文件夹，**文件夹名 = 论文名**（中文名，不加 arXiv ID 前缀）
- **经典论文优先用代号命名**，如 BEVFormer、VAD、UniAD、DETR3D、DiT、BridgeSim、Diffusion Planner 等；没有公认代号的才用中文论文名
- 文件夹内**只保留 1 个成品中文 PDF**，命名 `<论文名或代号>_中文.pdf`

## 禁止进入仓库

以下中间文件一律不提交：

- LaTeX 源码（.tex / .sty / .cls / .bib / .bst）
- `paper_source/`、`paper_cn/` 目录及其中内容
- 源码压缩包（`paper_source.tar.gz`）
- 图片/图表（figures、pics、img 等）
- 编译产物（.aux / .log / .out / .xdv / .fls / .fdb_latexmk 等）
- 技术报告（technical_report.md）
- 重复文件（同 md5 的 PDF 副本）

## 流程

1. 在本地工作目录完成翻译与编译（如 `~/arXiv_XXXX/paper_cn/main.pdf`）
2. 确认 PDF 可正常打开、页数完整
3. 在仓库创建 `<论文名>/` 文件夹，**只拷入**成品 PDF
4. 更新 README 的论文表格（论文 / 领域 / 会议 / 页数）
5. `git add -A && git commit && git push`

## 检查命令

```bash
# 确认仓库里只有 PDF 和 README
git ls-files | grep -vE '\.pdf$|^README|^\.gitignore'

# 确认无重复文件
find . -name "*.pdf" -exec md5sum {} \; | sort | awk '{print $1}' | uniq -d
```
