# cae_skill

[中文](#中文) · [English](#english)

## 中文

`cae_skill` 是面向仿真工程师的开放技能，负责把工程需求整理成项目任务书和求解前方案。它服务于下面这条完整的 CAE 工作流。

**项目文件（输入） → 工程处理流程（系统） → 分析报告（输出）**

几何建模 → 几何清理与理想化 → 网格划分 → 物理建模 → 求解 → 结果处理与报告

工具选择由工程师按环节指定。需要新建几何时默认推荐 SOLIDWORKS，其余未指定环节默认用 Abaqus。例如，已有 AutoCAD 图纸可作为几何输入，也可指定 HyperMesh 划网。

项目文件记录对象、工况和报告要回答的问题。按这套设计，CAE 软件依据同一份输入设置模型、网格和求解输出，再从计算结果中提取各项指标，形成分析报告。求解前，工程师可核对建模选择、输出请求和计划交付的原生图件。Abaqus 结果报告先展示从 ODB 导出的原生云图和变形动画，再用曲线和统计解释结果。

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

Geometry creation → Geometry cleanup and idealization → Meshing → Physics definition → Solution → Postprocessing and reporting

Engineers can choose tools for individual stages. SOLIDWORKS is the default recommendation for new geometry. The other stages default to Abaqus unless specified. Existing AutoCAD drawings can serve as geometry inputs, and HyperMesh can be selected for meshing.

The project file defines the model scope, operating conditions, and questions the report should answer. In this design, the CAE software uses the same specification to build and mesh the model, run the analysis, and extract the requested results for the report. Before the run, engineers can review the model choices, output requests, and planned native figures. Abaqus reports open with native contour plots and deformation animations exported from the ODB. Derived curves and statistics follow where they help explain the results.

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
