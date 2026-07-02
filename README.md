# 论文阅读室 Paper Digest

一个 [Claude Code](https://claude.com/claude-code) skill：把丢进目录里的论文 PDF 处理成中文阅读页。

- 每篇论文生成一份**总结**（摘要 / 核心思想 / 方法概述 / 亮点 / 局限与思考）+ 一份**中文全文**（外语论文忠实全译，中文论文整理排版）
- 全部汇入一个带左侧导航的单页 HTML（`paper-digest/index.html`），支持 MathJax 公式渲染
- 数据与页面分离：每篇论文的元信息、总结、全文存为独立文件，页面由脚本重建，增量收录，永不手改

## 效果

```
你的论文目录/
├── attention.pdf          ← 把 PDF 丢进来
├── some-paper.pdf
└── paper-digest/          ← skill 生成
    ├── index.html         ← 打开这个：左侧论文列表，右侧总结 + 中文全文
    └── data/<slug>/       ← 每篇论文一个目录
        ├── meta.json      ← 标题、作者、年份、标签…
        ├── summary.html   ← 总结
        └── fulltext.html  ← 中文全文
```

## 安装

**个人级**（所有项目可用）：

```bash
git clone https://github.com/hyacinthhh/paper-digest-skill.git ~/.claude/skills/paper-digest
```

**项目级**（仅当前项目可用）：

```bash
git clone https://github.com/hyacinthhh/paper-digest-skill.git <项目>/.claude/skills/paper-digest
```

依赖：`python3`（生成页面用，macOS 自带）。读取 PDF 建议安装 poppler（`brew install poppler`），
没有的话 Claude Code 也会自行想办法提取文本。

## 使用

1. 把论文 PDF 丢进任意目录
2. 在该目录启动 `claude`，说一句：

   > 处理论文 / 读论文 / 总结论文 / 翻译论文 / 更新论文库

   或直接 `/paper-digest`
3. 处理完成后打开 `paper-digest/index.html` 阅读（macOS 上 Claude 会帮你 `open`）

再往目录里丢新 PDF、再喊一次即可增量收录；已处理过的论文不会重复处理。

## 文件说明

| 文件 | 作用 |
|---|---|
| `SKILL.md` | skill 主体：工作流程与写作规范（Claude 读这个干活） |
| `scripts/build.py` | 扫描 `data/*/` 重建 `index.html` |
| `assets/template.html` | 页面模板（样式、导航、MathJax） |

## License

MIT
