# cae_skill

[中文](#中文) · [English](#english)

## 中文

`cae_skill` 帮助仿真工程师把工程需求整理成一份**可以在求解前核对的分析方案**。你可以直接给 Codex 一份项目书、一张标注图，也可以从一句话开始。AI 先整理已有资料，只补问那些会改变模型或结论的问题。

安装后，你可以在 Codex 中发送这样的请求。

> 用 $cae_skill 帮我规划一块带孔板的拉伸分析。我想看满载时孔边的应力分布，以及测点 P 在整个加载过程中的位移曲线。

这两个问题需要不同的数据。技能会在预览中分别列出满载时要保存的应力场，以及 P 点位移历程的方向和采样频率。它还会说明孔周拟用什么单元、哪里需要加密、怎样检查峰值对网格的敏感性。工程师可以直接修改其中一项，也可以一次确认整份方案。

你会收到两份可编辑的文档。

- **CAE 项目任务书**整理分析目的、对象、工况和判据。材料牌号已知时，AI 可查找相关物性，列出来源、单位和适用条件，并标明哪些取值待确认。[Markdown 模板](assets/CAE项目任务书.md) · [Word 模板](assets/CAE项目任务书.docx)
- **求解前方案预览**列出建模假设、单元类型、网格计划、场输出和历史输出。每个报告指标都关联到需要保存的数据。[预览模板](assets/仿真方案预览.md) · [Abaqus 与 Ansys Mechanical 设置示例](references/单元与输出设置.md)

随包的网格经验包含局部加密、粗细过渡、共享界面和扫掠案例，也记录了反复补划后如何查清哪些实体仍然没有体单元。[网格经验与配图](references/mesh/abaqus_cae经验.md)

## English

`cae_skill` is a Codex skill for simulation engineers. It turns a project brief, an annotated drawing, or a short conversation into a **simulation plan you can review before a solver run**. It reads the available information first and asks follow-up questions when the answer would change the model or the conclusion.

Once installed, you can start with a request like this in Codex.

> Use $cae_skill to plan a tensile analysis of a plate with a hole. I need the stress distribution around the hole at full load and the displacement history at point P throughout loading.

Those questions call for different output requests. The preview identifies the stress field to save at full load and the displacement component and sampling frequency to use at P. It also explains the proposed element type, where to refine the mesh, and how to check whether the peak stress changes with refinement. You can revise an individual setting or confirm the plan as a whole.

The skill produces two editable documents. The bundled templates and reference notes are in Chinese.

- **CAE project specification.** Records the objective, geometry, operating conditions, and acceptance criteria. When a material grade is known, the skill can look up relevant properties and record their sources, units, and applicable conditions for review. [Markdown template](assets/CAE项目任务书.md) · [Word template](assets/CAE项目任务书.docx)
- **Pre-solve plan.** Sets out modeling assumptions, element choices, meshing strategy, and field and history output requests. Each requested result is linked to the data the solver needs to save. [Preview template](assets/仿真方案预览.md) · [Abaqus and Ansys Mechanical examples](references/单元与输出设置.md)

The mesh notes cover local refinement, transitions between fine and coarse meshes, shared interfaces, and sweep meshing. One worked case shows how to identify solid regions that still contain no volume elements after repeated meshing attempts. [Mesh notes and diagrams](references/mesh/abaqus_cae经验.md)
