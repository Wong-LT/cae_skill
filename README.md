<img src="docs/images/nailong.png" alt="Nailong in a kung fu stance in front of a campus hall" width="168" align="right">

# cae_skill

[中文](#中文) · [English](#english)

## 中文

`cae_skill` 是面向仿真工程师的开放技能，负责把工程需求整理成项目任务书和求解前方案。它服务于下面这条完整的 CAE 工作流。

**项目文件（输入） → 工程处理流程（系统） → 分析报告（输出）**

几何建模 → 几何清理与理想化 → 网格划分 → 物理建模 → 核对最终求解输入 → 求解 → 结果处理与报告

工具选择由工程师按环节指定。简单几何和小型验证算例默认在 Abaqus 中建模，复杂结构或多零件装配默认推荐 SOLIDWORKS，其余未指定环节默认用 Abaqus。例如，已有 AutoCAD 图纸可作为几何输入，也可指定 HyperMesh 划网。

项目文件记录对象、工况和报告要回答的问题。按这套设计，CAE 软件依据同一份输入设置模型、网格和求解输出，再从计算结果中提取各项指标，形成分析报告。求解前，工程师可核对建模选择、输出请求和计划交付的原生图件。Abaqus 结果报告先展示从 ODB 导出的原生云图和变形动画，再用曲线和统计解释结果。

### 文献如何进入方案

每个项目的预览都呈现“问题 → 检索 → 适用性比较 → 建模选择 → 验证”。AI 从已有资料和可靠来源查找依据，说明材料、工况及边界条件与当前项目的关系，再给出拟采用的方法与验证计划。依据摘要保留原文链接或 DOI、实际阅读范围和待补信息，便于工程师核对。常规分析可以复用适用的已知依据，复杂问题按缺口深入检索。

研究文献以 JCR Q1 的 SCI 论文为主，Q2 仅作补充。优秀硕博论文以博士论文为主，院校在相关学科的 THE、U.S. News、软科或 QS 任一世界榜单前 100 即可，研究院校众多的热门专业可放宽至前 150。两类来源满足任一渠道即可进入候选。硕博论文优先参考论文奖项，结合导师在相关方向的学术贡献，再通过全文判断研究问题、方法、证据与结论的逻辑衔接及验证支持，记录判断依据。JCR 优先采用论文发表同年的指标，尚未发布时暂用最新可查分区，并注明年份与学科。

### 默认后台计算

AI 在提交前按实际求解器自行核对最终输入和生效的模型设置。额外诊断作业（如 Abaqus `datacheck`）可按需建议，仅在工程师明确要求时运行。

**提交前先确认计算资源。** AI 会列出执行机器的物理核心数、逻辑线程数、总内存和当前可用内存，给出本次 CPU 数与内存推荐值及依据，等待工程师确认后提交。

**提交 job 默认采用无窗口后台计算。** Windows 用户可以在任务管理器中查看对应求解进程的运行情况、CPU 和内存占用。具体分析步、增量和完成状态可从作业日志查看，提交后会给出作业与日志位置。

**需要打开软件界面或实时可视化时，请单独说明。** 例如“这次请打开界面查看变形”。报告所需的原生云图和动画仍按任务要求导出。

### 中断后继续

对已有项目说“继续”，AI 根据已确认方案、项目记录、当前进程和日志识别进度。运行中的 job 继续跟踪，完成的 job 进入结果处理；停止的 job 根据原因及可用重启动数据提出续算或重算方案。项目记录保留作业、输入、结果及下一步的位置。

### 两种输入方式

1. **有现成项目书**　把文件、路径或正文交给 AI，也可以附上图纸和材料表。AI 先读资料，代填标准任务书，只追问会改变建模或判断的缺项。
2. **没有项目书**　从分析对象和工程目标谈起，已有描述可直接用于任务书。例如，知道材料牌号后，AI 可查取所需物性，列出建议值和来源，交工程师一次核对。

两种方式生成同一格式的项目文件。第一部分用工程语言概述需求，第二部分把条件、假设和输出要求整理成结构化记录。

下面是 Codex 中的一种调用方式。其他智能体可通过各自的技能加载方式使用同一套说明和模板。

> 用 $cae_skill 帮我规划一块带孔板的拉伸分析。我想看满载时孔边的应力分布，以及测点 P 在整个加载过程中的位移曲线。

这两个问题需要不同的数据。技能会在预览中分别列出满载时要保存的应力场，以及 P 点位移历程的方向和采样频率。它还会说明孔周拟用什么单元、哪里需要加密、怎样检查峰值对网格的敏感性。工程师可以直接修改其中一项，也可以一次确认整份方案。

你会收到两份可编辑的文档。

- **CAE 项目任务书**整理分析目的、对象、工况和判据。材料牌号已知时，AI 可查找相关物性，列出来源、单位和适用条件，并标明哪些取值待确认。[Markdown 模板](assets/CAE项目任务书.md) · [Word 模板](assets/CAE项目任务书.docx)
- **求解前方案预览**列出建模假设、单元类型、网格计划、场输出和历史输出。每个报告指标都关联到需要保存的数据。[预览模板](assets/仿真方案预览.md) · [Abaqus 与 Ansys Mechanical 设置示例](references/单元与输出设置.md)

工程师可以直接说“先比较哪种方案更硬”或“判断位移是否超限”。AI 据此拟定各指标的首轮精度。报告末尾指出哪些位置值得加密、哪些区域可以尝试粗化、分别影响什么结果，以及重算可能花费的时间。工程师决定是否继续。

随包的网格经验包含局部加密、粗细过渡、共享界面和扫掠案例，也记录了反复补划后如何查清哪些实体仍然没有体单元。[网格经验与配图](references/mesh/abaqus_cae经验.md)

## English

`cae_skill` is an open skill for simulation engineers. It prepares the project specification and pre-solve plan for the following CAE workflow.

**Project file (input) → Engineering workflow (system) → Analysis report (output)**

Geometry creation → Geometry cleanup and idealization → Meshing → Physics definition → Check final solver input → Solution → Postprocessing and reporting

Engineers can choose tools for individual stages. Simple geometry and small verification models default to Abaqus modeling. Complex structures and multi-part assemblies default to SOLIDWORKS. The other stages default to Abaqus unless specified. Existing AutoCAD drawings can serve as geometry inputs, and HyperMesh can be selected for meshing.

The project file defines the model scope, operating conditions, and questions the report should answer. In this design, the CAE software uses the same specification to build and mesh the model, run the analysis, and extract the requested results for the report. Before the run, engineers can review the model choices, output requests, and planned native figures. Abaqus reports open with native contour plots and deformation animations exported from the ODB. Derived curves and statistics follow where they help explain the results.

### How evidence informs the plan

Every project preview follows “question → research → applicability comparison → modeling choice → validation.” The agent reviews existing material and reliable sources, compares their materials, operating conditions, and boundaries with the current problem, and proposes methods and validation steps. The evidence summary includes source links or DOIs, the content actually reviewed, and remaining gaps. Routine analyses can reuse applicable evidence; complex problems call for further research where it affects the decision.

Research papers primarily come from SCI journals in JCR Q1, with Q2 used only as supplementary evidence. Strong graduate theses, especially doctoral dissertations, are also eligible when the institution ranks in the relevant subject within the global top 100 in any one of THE, U.S. News, ShanghaiRanking, or QS. For popular disciplines studied at many institutions, this can extend to the top 150. Either route qualifies a source for consideration. Thesis awards receive priority in screening, alongside the academic contributions of the supervisor in the relevant field. Full-text assessment examines the logical connection between the research question, assumptions, methods, evidence, and conclusions, including validation and applicability. The assessment records its supporting sources. Prefer the JCR metric year matching the paper publication year. If that year is not yet released, use the latest verifiable quartile and record its year and subject category.

### Background calculation by default

Before submission, the agent checks the selected solver’s final input and active model settings against the agreed plan. It may suggest a separate diagnostic job, such as Abaqus `datacheck`, and runs it only at the engineer’s explicit request.

**Review computing resources before submission.** The agent reports the execution machine's physical cores, logical threads, total RAM, and currently available RAM. It recommends a CPU allocation and memory budget with a brief rationale, then waits for the engineer's confirmation before submitting the job.

**Jobs are submitted for background calculation without opening a window.** On Windows, Task Manager shows the solver process and its CPU and memory usage. Solver logs provide the analysis step, increment, and completion status. The submission response identifies the job and its log location.

**Explicitly request a visible interface or live visualization when needed.** For example, “Open the interface so I can inspect the deformation.” Native contour plots and animations requested for the report are still exported as planned.

### Resume a project

Ask to continue an existing project. The agent uses the confirmed plan, saved project records, current processes, and solver logs to identify progress. Running jobs remain under observation, completed jobs proceed to postprocessing, and stopped jobs are assessed for restart or a new run using the available restart data. The project record identifies the inputs, job, results, and next action.

### Two ways to provide input

1. **Start from an existing brief.** Share a file, its path, or the text, along with any relevant drawings or material sheets. The AI reads these first, fills in the standard specification, and asks only about gaps that could change a modeling decision or conclusion.
2. **Start with a guided interview.** Describe what you want to analyze and what you need to find out. The agent follows up on gaps that affect the analysis. For example, give it the material grade and it can look up relevant properties, cite its sources, and present the proposed values for review.

Both routes produce the same project file. The first part summarizes the engineering request in plain language. The second records conditions, assumptions, and output requests in a structured format.

In Codex, you can invoke the skill as shown below. Other agents can use the same instructions and templates through their own skill loaders.

> Use $cae_skill to plan a tensile analysis of a plate with a hole. I need the stress distribution around the hole at full load and the displacement history at point P throughout loading.

Those questions call for different output requests. The preview identifies the stress field to save at full load and the displacement component and sampling frequency to use at P. It also explains the proposed element type, where to refine the mesh, and how to check whether the peak stress changes with refinement. You can revise an individual setting or confirm the plan as a whole.

The skill produces two editable documents. The bundled templates and reference notes are in Chinese.

- **CAE project specification.** Records the objective, geometry, operating conditions, and acceptance criteria. When a material grade is known, the skill can look up relevant properties and record their sources, units, and applicable conditions for review. [Markdown template](assets/CAE项目任务书.md) · [Word template](assets/CAE项目任务书.docx)
- **Pre-solve plan.** Sets out modeling assumptions, element choices, meshing strategy, and field and history output requests. Each requested result is linked to the data the solver needs to save. [Preview template](assets/仿真方案预览.md) · [Abaqus and Ansys Mechanical examples](references/单元与输出设置.md)

An engineer can ask which design is stiffer or whether displacement exceeds a limit. The skill uses that intent to propose an initial accuracy target for each quantity of interest. The report identifies where refinement or coarsening could help, which results it may affect, and the expected cost of another run. The engineer chooses whether to rerun.

The mesh notes cover local refinement, transitions between fine and coarse meshes, shared interfaces, and sweep meshing. One worked case shows how to identify solid regions that still contain no volume elements after repeated meshing attempts. [Mesh notes and diagrams](references/mesh/abaqus_cae经验.md)
