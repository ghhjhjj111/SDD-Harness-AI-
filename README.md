# SDD规范驱动+Harness驾驭工程AI全栈开发（完结）

获课：jzit.top/25200/SDD规范驱动+Harness驾驭工程AI全栈开发（完结）

SDD规范驱动+Harness驾驭工程AI全栈开发
SDD与Harness Engineering的关系不是竞争，而是包含。 SDD是Harness前馈层（Feed Forward）的深度实践，Harness把SDD包在了里面。Harness是一个大筐，装着“模型之外的一切”：前馈（Spec、Rules、Context）+ 反馈（Test、Lint、Review、CI/CD）。SDD干的活，是把这个筐里“前馈”那块的Spec这一格做深做厚
。

从“出码率”到“交付率”的困局
出码率已从53%提升至80%—90%，但项目交付周期并未等比例缩短——编码环节仅占研发全链路的20%—30%。Vibe Coding的病理报告很扎心：METR实测，经验开发者用AI工具实际慢19%（尽管自认为快20%）；GitClear数据显示，AI协作代码重复量翻了4倍；CodeRabbit发现，AI代码“重大问题”率是人类代码的1.7倍。本质就一条：没图纸，全凭感觉，必然返工。

SDD：规范成为AI的“唯一事实来源”
SDD的核心思想是颠覆以代码为中心的权力结构：规范不服务代码——代码服务规格。产品需求文件不是实施指南，而是产生实现的来源；技术计划不是指导编码的文件，而是精确的定义，产生代码。当使用规格和实现计划来产生代码时，没有缺口——只有转换。

Microsoft Learn将SDD工作流拆解为四个阶段：Specify（定义软件“做什么”及“为什么”）→ Plan（决定“如何构建”）→ Task（拆解为离散可执行的任务）→ Implement（AI在规范指导下编写代码，每个任务依据规范验证）。每个阶段在前进之前都有一个验证步骤：规划之前检查规格完整性，生成任务之前检查计划可行性，实施开始之前验证任务覆盖性。

Harness Engineering：为AI设计“缰绳”与“反馈系统”
Harness Engineering的核心定义来自Mitchell Hashimoto（Terraform作者）：“每当发现Agent犯了一个错误，就花时间去工程化一个解决方案，让它再也不会犯同样的错误。”其核心哲学是“人类掌舵，智能体执行”。

Harness干四件事：约束、告知、验证、纠正。它拆两半：Feed Forward（前馈，写代码前引导）+ Feedback（反馈，写代码后检查）。最硬的数据来自LangChain：用GPT-5.2-Codex，模型不动，只优化Harness，Terminal Bench 2.0从52.8%干到66.5%，从Top 30外冲进Top 5。

OpenAI的标杆实践：3-5名工程师在5个月内，通过Codex Agent协作交付了超过100万行生产级代码，无一行人类手写，平均每人每日合并3.5个Pull Request，效率达到传统模式的10倍。

两者协同的落地机制
得物技术的全栈SDD实践揭示了一个关键操作原则：给AI一个已有的实现作为参照，让它照着复刻，而不是凭空创造。不推荐的提示词是“请实现一个结束语管理的CRUD接口”，推荐的提示词是“请参照现有‘场景欢迎语’功能（后端接口 /api/v1/feature/list，前端入口 FeatureTable/index.tsx:53-58）实现‘结束语’功能。数据结构、分层方式、命名风格都保持一致”。两者的差距不在于AI是否聪明，而在于你给了AI多少约束和上下文——后者将代码可用率从30%提升到80%以上。

在CI/CD环节，Harness将SDD规范转化为流水线的逻辑分支：静态安全检查调用Checkov扫描K8s规范，若检测到privileged: true违背安全规范，流水线直接失败；覆盖率门禁检查核心支付模块覆盖率是否>85%，若不足则AI助手自动分析未覆盖分支并尝试生成补充测试；API兼容性检查使用OAS-Diff检查当前PR对OpenAPI规范的修改是否破坏向后兼容性。

一个务实的判断
Harness越强，执行能力越强，Spec的质量对最终结果的影响就越大。Harness是放大器，Spec是被放大的内容。 SDD是必须而且重要的，不是因为Harness不够好，而是因为Harness把Spec的重要性放大了。从Prompt到声明式Skill，好的Prompt不应该锁在个人脑子里。在Claude Code等工具中，支持将好用的Prompt封装为.claude/skills/目录下的Skill资产，并通过Git进行版本控制。新成员克隆代码库时就能瞬间继承整个团队沉淀的AI编程能力。

