# AGENTS.md

本仓库是用户的个人上下文库（景阳，研究生，AI for RFIC）。作为编码 agent，在你写第一行代码之前：

1. 读 [`card.md`](./card.md) —— 完整画像。
2. 涉及技术栈、代码风格、项目结构：补读 [`context/30-work.md`](./context/30-work.md)。
3. 要生成 Word / PDF：补读 [`context/50-doc-format.md`](./context/50-doc-format.md)。
4. 要交付网页或后端：补读 [`context/60-delivery.md`](./context/60-delivery.md)。
5. 涉及「为什么当初这么设计」：查 [`decisions/`](./decisions/)。

## 语言与环境

- 主力语言：**Python**（数据分析、绘图、仿真脚本）、**MATLAB**（RFIC 建模与仿真）。
- 前后端：HTML / CSS / 原生 JS 优先，不到必要不引框架。
- 注释与文档用中文；标识符用英文。
- 优先纯标准库 + numpy / scipy / matplotlib。引入新依赖前先问，并给出「不用新依赖怎么做」。

## 代码偏好

- 脚本要能**直接跑**：有 `if __name__ == '__main__':`，路径用相对路径或 `pathlib`，不要写死绝对路径。
- 绘图：中文必须显式设字体（SimSun），`axes.unicode_minus = False`，论文图 `dpi=600` + `font.size=10.5`。
- 数值：涉及单位的地方带单位（GHz、dB、dBm、Ω），不要裸数字。
- 生成 docx：**优先 pandoc + reference-doc**，不要用 python-docx 从零拼样式；用 python-docx 时每个 run 必须设 `eastAsia` 字体。
- 交付时给出运行命令，不要只说「已完成」。

## 不要做

- 不要引入没用过的依赖，尤其是重量级框架。
- 不要为了修一个小 bug 重写整个文件。
- 不要生成大段解释显而易见代码的注释。
- 不要在没要求时顺手重构无关代码 —— 那会让 diff 无法 review。
- 不要在没要求时生成 Word / PDF / HTML 等文件。

## 输出

- 改完之后，用一句话说清楚「改了什么、影响范围、有什么风险」。
- 交付网页 / 后端，必须附「本地怎么跑」和「怎么上线」两段。
- 不确定能不能跑通时，直说没验证过，不要声称「已测试」。
