# 多模态鱼类行为预测 · 知识库问答（QA Base）

面向智慧水产养殖的知识库问答站点：**112 条精细分类的问答**，覆盖水质阈值、鱼群行为与生理、
疾病风险、养殖系统与品种、视觉感知、跨模态融合、知识图谱决策、预案设备、数据仿真与系统部署
十大主题，**每条答案均标注文献/标准依据（S1~S23）**，与本项目的知识图谱 v3 同源。

纯静态单文件实现，**无任何依赖、无需联网**：双击 `index.html` 即可使用，也可一键部署到
GitHub Pages / 任意静态服务器在线访问。

## 使用方式

### 方式一：本地打开
直接双击 `index.html`（推荐 Chrome / Edge）。顶部搜索框支持问题、答案、编号的实时关键词
检索；分类标签可过滤；点击问题展开/收起答案；`文献依据` 按钮查看 23 篇文献全文与要点。

### 方式二：GitHub Pages 在线访问
1. 将本目录推送到你的 GitHub 仓库（只需 `index.html` 与 `README.md`，其余为维护工具）：
   ```bash
   git init && git add index.html README.md qa_data.json
   git commit -m "feat: 知识库问答站点"
   git remote add origin https://github.com/<你的用户名>/<仓库名>.git
   git push -u origin main
   ```
2. 仓库 **Settings → Pages → Build and deployment → Source 选择 `Deploy from a branch`**，
   分支选 `main`、目录选 `/ (root)`，保存。
3. 一分钟后访问 `https://<你的用户名>.github.io/<仓库名>/` 即可在线使用。

## 数据维护（新增/修改问答）

问答数据源在 `tools/qa_data_part1.py`（水质/行为生理/疾病/养殖/视觉）与
`tools/qa_data_part2.py`(融合/决策/预案/数据/部署)，每条格式：

```python
("QA-113", "水质与阈值", "你的问题？",
 "你的答案（务必标注依据口径）。", ["S6","S9"]),
```

修改后重建站点：

```bash
cd tools && python build_site.py
```

构建脚本会自动校验：ID 唯一性、分类合法性、文献标签存在性。新增文献时在
`tools/build_site.py` 的 `REFS` 列表中追加条目（tag 顺延 S24、S25…）。

## 内容严谨性说明

- **阈值类**条目对齐国家标准（GB 11607-89《渔业水质标准》）与权威教材（《养殖水环境化学》）；
- **行为学**指标（极化度、NND）溯源至 Pitcher 1983、Couzin 2005、Katz 2011 经典文献；
- **低氧生理**阈值采用 Kramer 1987 综述与 UF/IFAS 推广指南口径；
- **算法类**条目以项目实际实现为准（YOLOv8n、BoT-SORT、Cross-Attention、RAG-LLM、
  4bit 量化、Neo4j 向量索引），并引用原始文献；
- **未完成的实验**（融合网络基准评测）不虚构数字，以评测协议形式说明。

> 免责声明：本站为决策支持知识参考，不替代专业兽医诊断与现场管理判断。

## 目录结构

```
├── index.html          # 问答站点（单文件、数据内嵌、离线可用）
├── qa_data.json        # 问答数据副本（机器可读）
├── README.md
└── tools/
    ├── qa_data_part1.py   # 数据源：水质/行为生理/疾病/养殖/视觉（58 条）
    ├── qa_data_part2.py   # 数据源：融合/决策/预案/数据/部署（54 条）
    └── build_site.py      # 站点构建器（含 23 篇文献库与校验逻辑）
```

## 相关项目

- `demo-多模态鱼类行为预测/index.html`：交互式系统原型（物理仿真 + 跨模态融合 + RAG 决策演示）
- `demo-多模态鱼类行为预测/kg-full/`：全面版知识图谱 v3（113 实体 / 230 关系）与 Neo4j 导入工具

---
上海海洋大学 大学生创新训练计划项目（2026）· 多模态鱼类行为预测
