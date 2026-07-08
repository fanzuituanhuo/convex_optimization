# Agent Guide

本文件为 Kimi / 其他 coding agent 提供本项目的工作约定与注意事项。

## 项目定位

这是一个个人学习笔记仓库，核心产出是三份用 LaTeX 写的《Convex Optimization》章节笔记。仓库同时存放参考 PDF 与图片素材。

## 目录约定

| 目录 | 用途 | 注意事项 |
|------|------|----------|
| `src/` | LaTeX 源码 | 可编辑；不要留 `.aux/.log/.out/.pdf` 等编译产物 |
| `pdf/` | 编译生成的笔记 PDF | 只放从 `src/` 编译出来的 PDF；不要放参考 PDF |
| `assets/` | 笔记引用的图片 | 源码中引用路径为 `../assets/文件名` |
| `template/` | 笔记模板（改编自 manifold_optimization_study_notes_chinese） | 可编辑；更新后同步到仓库 |
| `Convex Optimization By StephenBoyd/` | 外部参考 PDF（教材、课件、题解） | 只读；不要修改或删除 |

## 编译流程

必须使用 **XeLaTeX**：

```bash
cd /Users/fanzuituanhuo/note/convex_optimization/src
xelatex -interaction=nonstopmode -output-directory=../pdf chapterN_xxx_notes.tex
xelatex -interaction=nonstopmode -output-directory=../pdf chapterN_xxx_notes.tex
```

- 建议编译两次，以正确处理交叉引用、目录与 PDF 书签。
- 所有编译产物（`.aux`、`.log`、`.out`、`.synctex.gz`）应输出到 `pdf/`；完成后可清理，只保留 `.pdf`。

## 常见陷阱

1. **图片路径**
   - 源码在 `src/`，图片在 `assets/`，因此引用时必须使用 `../assets/图片名`。
   - 文件名包含空格与中文，建议用 `\detokenize{...}` 包裹，例如：
     ```latex
     \includegraphics[width=\linewidth]{\detokenize{../assets/ChatGPT Image 2026年4月26日 19_03_54.png}}
     ```

2. **编译器选择**
   - 文档使用 `ctex` + `fontspec`，只能用 `xelatex`，不要用 `pdflatex` 或 `lualatex`。

3. **大文件与 Git**
   - 仓库中已有多个 PDF 大文件；避免无意义地重复提交二进制 PDF。
   - 若只是小修文字，可不必立即重新编译 PDF。
   - 若移动或重命名大文件，注意 Git 会记录为删除+新增，尽量一次性完成。

4. **模板文件**
   - `template/` 目录样式改编自 `https://github.com/Polaris-Aeterna/manifold_optimization_study_notes_chinese`，包含 `main.tex`、`ref.bib` 及图片素材。
   - 章节笔记不再依赖 `template.zip`；如需参考模板样式，直接查看 `template/main.tex`。

## 修改建议

- 保持各章节导言区风格一致：`\documentclass[11pt,a4paper]{article}` + `ctex` + `geometry` + 常用数学/图表宏包。
- 新增定理、定义、示例时，优先复用现有 `tcolorbox` 样式，保持视觉统一。
- 不要在导言区随意增删宏包，避免不同章节之间出现样式漂移。
- 修改 `.tex` 后若涉及交叉引用或目录变化，应编译两次。

## 推荐操作顺序

1. 改源码前确认当前在 `src/` 下对应的 `.tex` 文件。
2. 修改后执行编译命令，检查 `pdf/` 中是否生成有效 PDF。
3. 若编译失败，优先查看 `pdf/*.log` 的末尾错误信息。
4. 编译成功后清理 `pdf/` 中的 `.aux/.log/.out` 等辅助文件。
5. 更新 `README.md` 中的进度列表（如新增章节）。
