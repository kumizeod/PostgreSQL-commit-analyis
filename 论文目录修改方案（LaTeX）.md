# 论文目录修改方案（LaTeX 具体执行版）

## 1. 本次修改目标

针对你“仓库已完成整合、论文使用 LaTeX 撰写”的现状，本方案不再停留在目录建议层，而是提供可直接落地的改造路径：

1. 明确主控文件与章节拆分方式；
2. 给出逐文件修改清单；
3. 统一章节命名、引用与图表编号规范；
4. 确保你可以从现有 `.md/.log/.py` 材料快速迁移到 LaTeX 论文。

---

## 2. 目录结构修改为“可编译工程”

建议将论文部分固定为以下结构（已按本仓库落地）：

```text
thesis/
├── main.tex
└── chapters/
    ├── chapter1_intro.tex
    ├── chapter2_dataset_and_identification.tex
    ├── chapter3_static_analysis.tex
    ├── chapter4_dynamic_analysis.tex
    ├── chapter5_formal_verification.tex
    ├── chapter6_discussion.tex
    └── chapter7_conclusion.tex
```

说明：目前已新增 `main.tex` 与 `chapter1_intro.tex`，其余章节按同样模式继续补齐。

---

## 3. 逐文件具体修改方案

### 3.1 `thesis/main.tex`（主控文件）

需要保留并检查以下点：

1. 文档类使用 `ctexbook`，保障中文章节与目录正常；
2. 统一加载基础宏包：`geometry`、`graphicx`、`booktabs`、`amsmath`、`hyperref`；
3. 前置部分包含：`\maketitle`、`\tableofcontents`；
4. 正文部分使用 `\input{chapters/chapterX_xxx}` 按章拆分；
5. 先保证第一章可编译，再逐章解除注释。

### 3.2 `thesis/chapters/chapter1_intro.tex`（绪论）

本章建议固定为 5 节：

- 1.1 研究背景与问题定义
- 1.2 研究目标与贡献
- 1.3 研究方法与技术路线
- 1.4 论文结构
- 1.5 本章小结

写作要求：

1. 背景中要交代 PostgreSQL 的工程复杂度与 Bug 修复研究价值；
2. 问题定义要明确“测试不足以证明正确性”，引出形式化验证；
3. 技术路线需覆盖统计、静态、动态、形式化四段证据链；
4. 小结要为第二章做承接。

### 3.3 第二至七章（待补齐文件）

按以下模板创建文件并在 `main.tex` 中 `\input`：

- `chapter2_dataset_and_identification.tex`
- `chapter3_static_analysis.tex`
- `chapter4_dynamic_analysis.tex`
- `chapter5_formal_verification.tex`
- `chapter6_discussion.tex`
- `chapter7_conclusion.tex`

每章最少包含：`\chapter` + 3 个 `\section` + `\section{本章小结}`。

---

## 4. 仓库材料到章节的迁移映射（可直接执行）

### 第二章（数据与识别）

来源：

- `bug_fix_identification_rules.md`
- `bug_fix_commit_rules_member2.md`
- `bug_fix_annotation_workflow.md`
- `bug_fix_trend_analysis.md`
- `bug_fix_trend_analysis_conclusion.md`

迁移方法：

1. 规则类文档进“2.2 识别规则”；
2. 标注流程进“2.3 标注流程与质量控制”；
3. 时间/作者/模块统计进“2.4 描述性统计”。

### 第三章（静态分析）

来源：

- `bug_fix.md`
- `bug_fix_structure_feature.md`
- `fix_example.md`

迁移方法：

1. 概念与方法写入“3.1 AST/libcst 方法”；
2. 模式总结写入“3.2/3.3 结构演化规律”；
3. 示例代码放附录或代码块环境。

### 第四章（动态分析）

来源：

- `dynamic_analyze/dynamic_analyze.md`
- `dynamic_analyze/成员四总结报告.md`
- `dynamic_analyze/异常逻辑识别报告.md`
- `dynamic_analyze/逻辑修复与验证报告.md`
- `dynamic_analyze/da_*.log` 与 `test_validation*.log`

迁移方法：

1. 异常发现、定位证据、修复回归按“问题-证据-修复-验证”组织；
2. 日志只保留关键片段，完整日志放附录。

### 第五章（形式化验证）

来源：

- `z3-solver/verify_config_logic.py`
- `z3-solver/verify_fix.py`
- `z3-solver/PostgreSQL 配置同步逻辑的形式化验证报告 (Z3-Solver).md`

迁移方法：

1. 抽象变量与规约写“5.1”；
2. SAT 反例写“5.2”；
3. UNSAT 证明写“5.3”；
4. 强调“从测试到证明”的方法价值写“5.4”。

---

## 5. LaTeX 规范（避免返工）

1. 图表统一：图 `Figure`、表 `Table`，均用 `\label`+`\ref`；
2. 公式仅在需要时使用 `equation` 环境，避免行内堆叠；
3. 代码片段建议使用 `verbatim` 或后续引入 `listings`；
4. 英文术语首次出现中英文并列：如“静默逻辑失效（Silent Failure）”；
5. 每章末尾必须有“本章小结”，保证论证连贯。

---

## 6. 一次性执行清单（按顺序）

1. 先编译 `thesis/main.tex`，确认第一章通过；
2. 逐章创建 chapter2--chapter7 文件并填最小骨架；
3. 按“第 4 节映射表”迁移已有材料；
4. 补图表编号、交叉引用与参考文献；
5. 最后统一摘要、结论、附录格式与术语。

执行完这 5 步后，你的论文将从“资料集合”升级为“可编译、可提交、可答辩”的 LaTeX 成稿框架。
