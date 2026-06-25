# Feynman Listener Skill

> A patient AI listener for the Feynman learning method: you explain first, AI asks evidence-bound questions, then coaches you into a clearer retell.

**Feynman Listener** 是一个 Codex skill，用来把 AI 从“直接讲课的老师”切换成“聪明、耐心、会追问的听众”。它适合用来学习数学、工程、物理、计算机、生命科学、历史、文学等主题。

它的核心不是套一个固定提问模板，而是：

1. 先听你用自己的话讲一遍；
2. 从你的原话、公式、白板、代码或参考资料里找理解裂缝；
3. 只问少量关键追问；
4. 等你回答后，AI 再给出直接讲解和纠偏；
5. 最后要求你重新完整讲一遍，并生成可复习的学习报告。

## Why this exists

很多 AI 学习工具会一上来就解释概念，学习者很容易变成“听懂了”的错觉。费恩曼学习法真正有价值的地方，是让你先把理解外化出来，然后检查：

- 概念有没有定义清楚；
- 因果链有没有跳步；
- 是否能举具体例子；
- 边界和反例是否知道；
- 是否和参考资料一致。

这个 skill 的设计目标是让 AI 先闭嘴听完，再精准追问，最后再教。

## What the skill does

- Listens to a learner's first explanation.
- Generates up to three evidence-bound probes.
- Avoids generic questions that could fit any topic.
- Gives direct coaching after each learner answer.
- Helps the learner produce a second, clearer retell.
- Produces a learning report with review questions.
- Can prepare Obsidian-style Markdown notes.

## Install

Clone this repository into your Codex skills directory.

Windows PowerShell:

```powershell
git clone https://github.com/Mashiachers/feynman-listener_skill.git "$env:USERPROFILE\.codex\skills\feynman-listener"
```

macOS / Linux:

```bash
git clone https://github.com/Mashiachers/feynman-listener_skill.git ~/.codex/skills/feynman-listener
```

Then restart Codex so the skill can be discovered.

## Usage

Invoke it explicitly:

```text
Use $feynman-listener to help me understand why gradient descent can find a minimum.
```

More examples:

```text
Use $feynman-listener. I want to explain distortionless transmission in Signals and Systems. After I explain, ask me only the most important gaps.
```

```text
Use $feynman-listener. I am learning transaction isolation in databases. Let me explain first, then challenge my explanation with concrete concurrent examples.
```

```text
Use $feynman-listener. Help me study Lu Xun's A Madman's Diary. I want the AI to ask textual-evidence-based questions, not generic literature prompts.
```

## Example interaction

Learner:

```text
梯度下降就是看当前位置斜率往哪里上升最快，然后往反方向走一点。
这样函数值会下降，重复很多次就会靠近最小值。
学习率太大时会跳过最低点。
```

AI using this skill:

```markdown
我听到的理解：你已经抓住了“负梯度方向让函数下降”的直觉，但还没有区分“每步下降”“收敛到最小值”和“只到局部低点”。

我想追问的地方：
1. [机制] 证据：“这样函数值会下降，重复很多次就会靠近最小值”
   问题：对一维函数 f(x)=x^2，如果 x=3、学习率 α=0.1，下一步 x 会变成多少？这个数字怎样说明“负梯度方向让函数值下降”？

2. [边界] 证据：“靠近最小值”
   问题：如果函数不是凸的，梯度下降为什么可能只找到局部最小值，而不是全局最小值？
```

After the learner answers, the AI switches from questioning to coaching:

```markdown
判断：基本正确

直接答案：对 f(x)=x^2，梯度是 2x。若 x=3 且 α=0.1，则 x_new = 3 - 0.1*6 = 2.4，函数值从 9 降到 5.76。

需要修正/补强：你说“会靠近最小值”时要加条件：步长合适、函数形状较好，例如凸函数；非凸时可能卡在局部最小或鞍点附近。

下一轮可以这样讲：梯度下降每次用当前位置的斜率做一个局部下降决策，例如 f(x)=x^2 从 3 走到 2.4，函数值变小；但它能否收敛取决于步长和函数形状。
```

## Subject examples

Concrete examples are included in [references/examples.md](references/examples.md), covering:

- Math / optimization: gradient descent
- Engineering: distortionless transmission
- Physics: Gauss's law
- Computer science: transaction isolation
- Biology / biochemistry: Michaelis-Menten kinetics
- History: Treaty of Versailles and World War II
- Literature: Lu Xun's *A Madman's Diary*

Each example includes:

- a learner's first explanation;
- a good AI probe response;
- a good AI coaching response after the learner answers.

## Repository structure

```text
.
├── SKILL.md                 # Codex skill entry point
├── agents/openai.yaml        # UI metadata
├── references/examples.md    # subject-specific examples
└── LICENSE
```

## Related project

This skill was extracted from the product workflow behind **Feynman Listener / 讲明白**, a voice-first Feynman learning web app:

[Mashiachers/work](https://github.com/Mashiachers/work)

## License

MIT License.
