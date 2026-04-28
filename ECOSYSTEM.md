# Motorbridge Ecosystem Architecture

Motorbridge 致力于构建一个自底向上的、完全开源的机器人驱动平台。为了保证架构的清晰与可扩展性，我们的开源矩阵分为四个核心层级：**核心基座层**、**算法层**、**生态系统层**以及**产品形态层**。

以下是我们的核心代码仓库及其功能边界说明：

## 1. 核心基座层 (Core Infrastructure)

本层提供最底层的通信协议、跨平台驱动和固件支持。它们是"盲"的，只负责处理字节、CAN 帧和通用电机状态，不涉及任何机器人形态逻辑。

* **`motorbridge`** (Public)
  * **定位**：核心引擎与统一 API。
  * **功能边界**：基于 Rust 开发的高性能底层驱动，提供 C ABI 和 Python/C++ 绑定。负责与各个厂商（Damiao, RobStride 等）的电机进行 CAN 总线通信。只暴露基础的转矩、速度、位置和状态读取接口。
* **`motorbridge-esp32`** (Public)
  * **定位**：微控制器固件网桥。
  * **功能边界**：使用 C/C++ 编写的底层固件。将 ESP32 转化为电机的直接控制器或无线/有线网桥，处理实时硬件 I/O 映射，不包含高级轨迹规划。

## 2. 工具与生态层 (Tooling & Ecosystem)

本层旨在将 Motorbridge 的硬件能力无缝接入开发者现有的工作流和前沿技术栈。

* **`motorbridge-studio`** (Public)
  * **定位**：Web 调试与可视化面板。
  * **功能边界**：基于 JavaScript 开发。提供纯前端/全栈的实时可视化界面，用于单电机或多电机的参数调试、PID 整定、错误重置和数据波形监控。
* **`motorbridge-ros2`** (Public)
  * **定位**：标准 ROS2 通用硬件接口。
  * **功能边界**：提供标准的 `ros2_control` 插件。它将单一或通用电机直接映射为 ROS 节点中的 Joint。**注意**：这里不处理系统级同步或复杂机械结构逻辑，仅充当连接单体硬件与 ROS 世界的"万能插座"。
* **`motorbridge-agent`** (Public)
  * **定位**：AI 代理与大语言模型集成。
  * **功能边界**：基于 MCP (Model Context Protocol) 等标准化协议，为大语言模型（如 Claude 等）提供调用底层硬件的 Tool（工具）。它使 AI 能够通过自然语言分析电机状态、下发动作指令，实现具身智能的基础闭环。

## 3. 算法与解算层 (Algorithms)

将纯粹的数学计算与物理硬件配置解耦，确保逻辑高内聚。

* **`motorbridge-kinematics`** (Private)
  * **定位**：核心运动学与轨迹规划求解器。
  * **功能边界**：纯数学库。包含特定构型的正逆运动学 (FK/IK) 解析解/数值解、姿态插补以及 MoveJ/MoveL/MoveC 轨迹规划算法。它不直接操作硬件，而是作为核心算法依赖（Dependency）被产品层调用。

## 4. 机器人产品形态层 (Product Forms)

本层面向最终用户，提供"开箱即用"的机器人整机/子系统控制方案。产品层直接调用 `motorbridge` 和 `motorbridge-kinematics`，并内建完整的硬件拓扑配置。

* **`motorbridge-arm`** (Private)
  * **定位**：串联机械臂完整系统级实现。
  * **功能边界**：针对特定开源机械臂套件的完整代码库。包含专属的伺服电机 ID 映射、零点标定流程、独立集成的 ROS2 系统启动包 (Bringup / Launch) 以及 URDF 模型。处理多关节的底层数据级严格同步。
* **`motorbridge-humanoid`** (Private)
  * **定位**：双足/人形机器人集成框架。
  * **功能边界**：处理极其复杂的多节点 CAN 总线拓扑、预留全身动力学控制 (WBC) 接口以及相关的步态测试脚本和仿真环境（如 Isaac Gym）配置文件。

## 5. 文档与规范 (Docs & Meta)

* **`motorbridge-docs`** (Public)
  * **定位**：官方文档站点源文件。
  * **功能边界**：基于 MDX 编写的 API 参考、快速入门教程和开发指南。
* **`.github`** (Public)
  * **定位**：组织级规范。
  * **功能边界**：存放组织级别的 Issue 模板、Pull Request 规范、CI/CD 工作流配置以及通用社区指南。
