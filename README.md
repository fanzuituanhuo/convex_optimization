# Convex Optimization 学习笔记

> 基于 Stephen Boyd & Lieven Vandenberghe《Convex Optimization》整理的章节笔记，采用 LaTeX + XeLaTeX 撰写，支持中文与数学公式。

## 项目结构

```
.
├── src/                                  # LaTeX 源代码
│   ├── chapter2_convex_sets_notes.tex
│   ├── chapter3_convex_functions_notes.tex
│   └── chapter4_convex_optimization_notes.tex
├── pdf/                                  # 编译生成的笔记 PDF
│   ├── chapter2_convex_sets_notes.pdf
│   ├── chapter3_convex_functions_notes.pdf
│   └── chapter4_convex_optimization_notes.pdf
├── assets/                               # 笔记中引用的图片素材
├── template/                             # 笔记模板（来自 deep_generative_model）
├── Convex Optimization By StephenBoyd/   # 参考书、课件与题解 PDF
└── README.md
```

- **`src/`** 只放可编辑的 LaTeX 源码；不要在这里留下编译产物。
- **`pdf/`** 只放从 `src/` 编译出来的最终 PDF；不要手动把参考书 PDF 放进来。
- **`assets/`** 放笔记需要的插图；源码中引用时使用相对路径 `../assets/...`。
- **`template/`** 放笔记模板，来自 [`fanzuituanhuo/deep_generative_model`](https://github.com/fanzuituanhuo/deep_generative_model)；新增章节时可参考 `template/main.tex` 的样式。
- **`Convex Optimization By StephenBoyd/`** 放外部参考材料（教材、幻灯片、题解），不纳入编译流程。

## 环境要求

- XeLaTeX（本项目使用 `ctex`、`fontspec` 等宏包，必须用 XeLaTeX 编译）
- 常用宏包：`geometry`、`amsmath`、`amssymb`、`amsthm`、`mathtools`、`tikz`、`tcolorbox`、`hyperref` 等

macOS 上可通过 Homebrew 安装：

```bash
brew install texlive
```

## 编译

进入 `src/` 目录，使用 `-output-directory=../pdf` 将产物输出到 `pdf/`：

```bash
cd src

for f in chapter2_convex_sets_notes.tex \
         chapter3_convex_functions_notes.tex \
         chapter4_convex_optimization_notes.tex; do
    xelatex -interaction=nonstopmode -output-directory=../pdf "$f"
    xelatex -interaction=nonstopmode -output-directory=../pdf "$f"
done
```

通常需要编译两次以正确生成交叉引用与书签。

## 新增章节

1. 在 `src/` 下新建 `chapterN_xxx_notes.tex`。
2. 参考现有文件或 `template/main.tex` 使用统一的导言区与样式。
3. 如需引用图片，放入 `assets/` 并在源码中使用 `../assets/图片文件名`。
4. 编译后将生成的 PDF 放入 `pdf/`。
5. 更新本 README 的进度列表。

## 当前进度

- [x] 第 2 章 Convex Sets
- [x] 第 3 章 Convex Functions
- [x] 第 4 章 Convex Optimization Problems
- [ ] 第 5 章 Duality（待补充）

## 参考资料

- Stephen Boyd & Lieven Vandenberghe, *Convex Optimization*, Cambridge University Press, 2004.
- 配套课件与题解见 `Convex Optimization By StephenBoyd/`。
