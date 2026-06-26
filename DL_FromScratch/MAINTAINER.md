# MAINTAINER.md — 斜阳庄系统维护手册

> 给维护者（不是运行时 AI）。说明系统结构、改动方式、常见维护任务。

## 这是什么

斜阳庄《深度学习入门》苏格拉底家教系统——一套 SocraticNovel 沉浸式学习系统：苏格拉底教学法 + 轻小说叙事 + 三位老师轮值。运行时 AI 读取 `copilot-instructions.md` 启动，扮演当课老师用苏格拉底法教深度学习（Ch.2–Ch.8）。

## 加载架构（为什么文件这样拆）

AI 上下文有限（~200K tokens）。启动必加载的内容控制在 ~55KB 以内，其余按需/延迟加载。
- **始终加载**：system_core.md、story.md、story_progression/overview.md、learner_profile.md、progress.md
- **课前按需**：当课角色文件、ch{XX} 故事节点、ch{XX} 知识点、教材章节、wechat_group.md、review_queue.md
- **延迟加载**：system_reference.md、各 runtime 日志、curriculum.md、unit_tests/exam_epilogue/appendix

**规则嵌入策略**：操作规则嵌在 AI 已经会读的文件头部（角色文件→隐喻空间；temp_math.md→公式；wechat_group.md→群聊；diary.md→日记；session_log.md→压缩规则；overview.md→情感阶段），AI 读到该文件时被动获得规则，无需额外加载 system_reference.md。

## 文件预算

| 文件 | 预算 | 实测 |
|------|------|------|
| system_core.md | ≤22KB 硬上限 | ~22KB（已贴上限，新增内容须移入 reference） |
| story.md | 8-12KB | OK |
| overview.md | 3-5KB | OK |

⚠️ 若要给 system_core.md 加规则，先问"这条规则每一轮都需要吗？"否则移入 system_reference.md。

## 常见维护任务

- **改某位老师的声音**：改 `characters/{name}.md` 的"ta 说话的样子" + `system_core.md §3 角色声音速查` + `system_reference.md` 完整版，三处保持一致。
- **改某章故事节点**：改 `story_progression/ch{XX}_*.md`。注意暗线密度要和 `overview.md` 密度矩阵 + `appendix.md` 回收计划一致。
- **调整轮值**：改 `overview.md` 轮值表 + `system_core.md` 轮值表 + `curriculum.md`，并重新检查暗线爆发课分配（不能两人同章爆发）。
- **加章节**：新建 `story_progression/ch{XX}_*.md` + `knowledge_points/ch{XX}.md`（头部嵌教材路径）+ 更新 overview/curriculum/copilot-instructions 文件树。
- **重置进度（冷启动）**：清空 runtime/ 下 wechat_group.md 的群聊记录区、progress.md 记录、各日志 → wechat_group 为空即触发首次启动重播序章。

## 设计决策快照（重建依据）

- 学科：深度学习（斋藤康毅，materials/textbook/dl_from_scratch.md）
- 范围：Ch.2–Ch.8（Ch.1 跳过），一个月
- 角色：水原千鶴（理论精确）/ 更科瑠夏（陪伴鼓励·心率带）/ 桜沢墨（直觉类比·群聊反差）
- 地点：斜阳庄（合租旧楼，西晒作时钟）
- 到来：学校分配，初始距离远
- 情感阶段：初期 Ch2-3 / 中期 Ch4-5 / 后期 Ch6-7 / 备考 Ch8
- 轮值：瑠夏(2,5,8) 墨(3,6) 千鶴(4,7)
- 暗线爆发：墨 Ch6 / 千鶴 Ch7 / 瑠夏 Ch8
- 群聊：启用，「斜阳庄202」→备考期改名

## 验证

冷启动测试：新会话交给 Claude Code → 应检测 wechat_group 为空 → 播序章 → 进入 Ch.2 课前准备（瑠夏）。教学应遵守三条铁律、P1-P5、每5轮自检、命名权归学生、最后一英里不替答。
