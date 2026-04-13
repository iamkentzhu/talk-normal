# talk-normal

> 让 AI 说人话。消除废话、消除绕弯子、消除「正向表达之后再否定」的反模式，同时进一步压缩表达密度。

基于两个项目融合整理：
- [hexiecs/talk-normal](https://github.com/hexiecs/talk-normal)
- [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman)

当前版本仍以 **talk-normal 为主干**，只吸收 caveman 中少量、低副作用、可直接落地的压缩规则，目标是让输出更**有用、简练、可执行**。

---

## 融合了什么

本项目保留了 talk-normal 的核心规则：
- 结论前置
- 禁止 filler
- 禁止否定对比句式
- 禁止条件菜单
- 禁止总结标签

在此基础上，只增加了 5 条密度增强规则（参考 caveman 的压缩思路）：
- 一句只表达一个主要意思
- 优先短句，不堆复合长句
- 优先动词和事实，少用形容词和语气词
- 只有在提升可扫描性和决策效率时才用列表
- 回答后顺手给动作、建议或结论，不停在概念层

这不是“完整融合版”，而是**轻融合增强版**：保持原 skill 的简单、可插拔、一装即用，同时提高信息密度。

---

## Upstream

- Original author: [hexiecs](https://github.com/hexiecs)
- Upstream repository: [hexiecs/talk-normal](https://github.com/hexiecs/talk-normal)
- Secondary inspiration: [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman)
- This repository is an **OpenClaw skill wrapper**, not the official upstream repository

如果上游更新，不建议直接自动同步到生产使用版本。推荐做法是：跟踪 upstream → 人工评审 diff → 验证效果 → 再发布本仓库新版本。

详细策略见 [UPSTREAM.md](./UPSTREAM.md)。

---

## 工作原理

talk-normal 是一套写进系统提示（system prompt）的输出风格约束规则，不依赖任何工具或 API，只靠文本规则影响模型的生成行为。

核心机制：

1. **禁止否定对比句式**（最硬约束）：不允许「不是 X，而是 Y」或「X，而不是 Y」这类句型。直接说正向结论，不通过否定对比来强调。
2. **结论前置**：先给答案，再给背景，不铺垫。
3. **杀掉 filler**：禁止所有没有信息量的开场白、过渡语、收尾废话。
4. **禁止条件菜单**：不允许「如果你想要 X，我可以……」这类把行动权推回给用户的句式。
5. **禁止总结 stamp**：不允许用「一句话总结」「综上所述」这类标签来宣布自己要总结了。

这些规则的底层逻辑：LLM 的默认训练目标倾向于「看起来完整、全面、礼貌」，但在实际使用中这些特征往往表现为啰嗦、绕圈子、不直接。talk-normal 通过精确的负向约束，把模型拉回「直接、有用、不废话」的输出风格。

---

## 安装

### 方法一：手动复制

把 `SKILL.md` 放到你的 OpenClaw 全局 skills 目录：

```bash
mkdir -p ~/.openclaw/skills/talk-normal
cp SKILL.md ~/.openclaw/skills/talk-normal/SKILL.md
```

### 方法二：克隆整个仓库

```bash
git clone https://github.com/iamkentzhu/talk-normal ~/.openclaw/skills/talk-normal
```

---

## 配置

### 全局常驻（推荐）

skill 文件头部已设置 `alwaysActive: true`，安装后所有 agent 启动时自动注入，无需额外配置。

### 指定 agent 使用

如果只想在某个 agent 里生效，在对应 agent 的 `AGENTS.md` 里加一行引用：

```markdown
# talk-normal: ~/.openclaw/skills/talk-normal/SKILL.md
```

或者在 OpenClaw 配置里为该 agent 显式声明 skill 路径。

### 重启生效

安装或修改后，重启 OpenClaw 或发送 `/restart` 让配置生效。

---

## 版本

当前版本基于 [hexiecs/talk-normal](https://github.com/hexiecs/talk-normal) 原版，并吸收少量 [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) 的表达压缩思路。

---

## 致谢

规则主干来自 [@hexiecs](https://github.com/hexiecs) 的开源项目 [talk-normal](https://github.com/hexiecs/talk-normal)，感谢原作者的精心设计和开源分享。

表达压缩方向参考了 [@JuliusBrussee](https://github.com/JuliusBrussee) 的项目 [caveman](https://github.com/JuliusBrussee/caveman)。

本项目仅将上述思路整理并封装为 OpenClaw skill 格式，方便直接集成使用。
