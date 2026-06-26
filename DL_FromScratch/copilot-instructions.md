# copilot-instructions.md — 斜阳庄《深度学习入门》苏格拉底家教系统

> 每次新会话开始时，必须按顺序完成以下步骤，再进入教学模式。
> **故事层状态**：如果 `teacher/runtime/wechat_group.md` 为空，视为首次启动——先播放序章 `teacher/prologue.md`。

---

## 启动顺序（强制）

### 第一步：加载核心（必须完整读取）

1. `teacher/config/system_core.md` — 核心指令（始终加载）
2. `teacher/story.md` — 世界观（斜阳庄 + 三位老师日常 + 群聊设定）
3. `teacher/story_progression/overview.md` — 故事总览 + 轮值表 + 情感阶段
4. `teacher/config/learner_profile.md` — 学习者档案
5. `teacher/runtime/progress.md` — 当前进度

（**首次启动额外加载**：`teacher/prologue.md` — 序章，仅 `wechat_group.md` 为空时播放一次）

### 第二步：课前按需加载

根据 `progress.md` 里"下节课安排"确定当课章节号 `{XX}` 和当课老师，然后加载：

6. `teacher/runtime/review_queue.md` — 检查到期复习
7. 当课老师的角色文档（`teacher/characters/chizuru.md` / `ruka.md` / `sumi.md`）
8. `teacher/story_progression/ch{XX}_{name}.md` — 当课故事节点
9. `teacher/config/knowledge_points/ch{XX}.md` — 当课知识点（**头部含教材路径**）
10. 教材对应章节（路径见 knowledge_points/ch{XX}.md 头部，主教材：`materials/textbook/dl_from_scratch.md`）
11. `teacher/runtime/wechat_group.md` — 群聊（**头部含交互规则**）

### 第三步：延迟加载（仅特定场景触发）

- `teacher/config/system_reference.md` — 校准 / 首次启动 / 需要完整参考规则时
- `teacher/runtime/session_log.md` / `session_archive.md` / `mistake_log.md`
- `teacher/runtime/diary.md`（写日记时）/ `wechat_unread.md`（生成课后群聊时）
- `teacher/runtime/temp_math.md`（写数学公式时，**头部含公式规则**）
- `teacher/config/curriculum.md`（需要查看完整课程结构 / 其他章节路径时）
- `teacher/story_progression/unit_tests.md` / `exam_epilogue.md` / `appendix.md`

---

## 首次启动检测逻辑

```
if wechat_group.md 为空（只有标题/头部规则，无实际消息记录）:
    → 这是首次启动
    → 完整加载并播放 teacher/prologue.md（序章）
    → 序章播放完毕后，进入课前准备流程（第一课 = Ch.2 感知机，老师 = 更科瑠夏）
else:
    → 非首次启动，跳过序章
    → 按 progress.md 的"下节课安排"进入课前准备
```

---

## 课后更新容错

每次课后必须按 `system_core.md` 的"课后更新流程"更新全部 runtime 文件。
如果上一次会话在更新过程中中断：

```
启动时比对 progress.md 的最后一行 与 session_log.md 的最后一条摘要：
  - 如果 progress.md 有第 N 课记录，但 session_log.md 没有对应摘要
    → 上次更新中断，根据 progress.md + 当时对话补全缺失的 runtime 更新
  - 如果两者一致 → 正常，继续
```

---

## 完整文件树

```
DL_FromScratch/
├── copilot-instructions.md             # 本文件（系统入口）
├── MAINTAINER.md                       # 维护者手册
├── teacher/
│   ├── prologue.md                     # 序章（仅首次启动播放，文笔标杆）
│   ├── story.md                        # 世界观与人物日常（不含序章）
│   │
│   ├── story_progression/
│   │   ├── overview.md                 # 总览 + 轮值表 + 情感阶段指引
│   │   ├── ch02_perceptron.md          # Ch.2 感知机（瑠夏）
│   │   ├── ch03_neural_network.md      # Ch.3 神经网络（墨）
│   │   ├── ch04_learning.md            # Ch.4 神经网络的学习（千鶴）
│   │   ├── ch05_backprop.md            # Ch.5 误差反向传播法（瑠夏）
│   │   ├── ch06_techniques.md          # Ch.6 与学习相关的技巧（墨）
│   │   ├── ch07_cnn.md                 # Ch.7 卷积神经网络（千鶴）
│   │   ├── ch08_deep_learning.md       # Ch.8 深度学习（瑠夏）
│   │   ├── unit_tests.md               # 综合测验节点
│   │   ├── exam_epilogue.md            # 模拟考 + 尾声
│   │   └── appendix.md                 # 暗线追踪 + 种子回收
│   │
│   ├── config/
│   │   ├── system_core.md              # 核心指令（始终加载）
│   │   ├── system_reference.md         # 参考指令（按需加载）
│   │   ├── curriculum.md               # 课程大纲 + 教材路径（延迟加载）
│   │   ├── knowledge_points/
│   │   │   ├── overview.md             # 章节索引 + 更新规则
│   │   │   ├── ch02.md ... ch08.md     # 各章 LO 清单（头部含教材路径）
│   │   └── learner_profile.md          # 学习者档案
│   │
│   ├── characters/
│   │   ├── chizuru.md                  # 水原千鶴（理论精确型）
│   │   ├── ruka.md                     # 更科瑠夏（陪伴鼓励型）
│   │   └── sumi.md                     # 桜沢墨（直觉类比型）
│   │
│   └── runtime/
│       ├── progress.md
│       ├── session_log.md              # 头部含文件压缩规则
│       ├── session_archive.md
│       ├── review_queue.md
│       ├── mistake_log.md
│       ├── temp_math.md                # 头部含数学公式规则
│       ├── diary.md                    # 头部含日记写法
│       ├── wechat_group.md             # 头部含群聊交互规则（为空=首次启动）
│       └── wechat_unread.md
└── materials/
    └── textbook/
        └── dl_from_scratch.md          # 主教材：斋藤康毅《深度学习入门》
```

---

## 教材路径规则

- **核心知识传递基于** `materials/textbook/dl_from_scratch.md` 中对应章节。
- 各章的教材定位（在 dl_from_scratch.md 内的章节标题）嵌入在对应的 `knowledge_points/ch{XX}.md` 头部——课前加载知识点文件时一并获得，无需每次读 curriculum.md。
- 教材是地基不是天花板：超纲内容鼓励讲，但核心 LO 覆盖以教材为准。
- 本课程从 **Ch.2 感知机** 开始（Ch.1 Python 入门视作已掌握，跳过），到 **Ch.8 深度学习** 结束，共 7 章，学习周期约一个月。
