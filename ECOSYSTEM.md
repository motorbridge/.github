# Motorbridge Ecosystem Architecture

Motorbridge 致力于构建一个自底向上的、完全开源的机器人驱动平台。我们的开源矩阵分为四个核心层级：**核心基座层**、**集成层**、**产品形态层**以及**工具与文档层**。

以下是我们的核心代码仓库及其功能边界说明：

## 1. 核心基座层 (Core Infrastructure)

本层提供最底层的通信协议、跨平台驱动和固件支持。只负责处理字节、CAN 帧和电机状态，不涉及任何机器人形态逻辑。

* **`motorbridge`**
  * **定位**：核心引擎与统一 API。
  * **功能边界**：基于 Rust 开发的高性能底层驱动，提供 C ABI 和 Python/C++ 绑定。负责与各厂商（Damiao, RobStride 等）的电机进行 CAN 总线通信。暴露基础的转矩、速度、位置和状态读取接口。
* **`motorbridge-esp32`**
  * **定位**：微控制器固件网桥。
  * **功能边界**：基于 ESP-IDF 的底层固件。将 ESP32 转化为电机的直接控制器或无线/有线网桥，处理实时硬件 I/O 映射，不包含高级轨迹规划。
* **`motorbridge-smart-servo`**
  * **定位**：串行总线舵机控制栈。
  * **功能边界**：基于 Rust 的串行总线智能舵机（如 FashionStar UART）驱动。提供原生 CLI、C ABI、PyO3 Python 包和 WASM 核心模块。与 `motorbridge` 的 CAN 电机驱动互补，覆盖 UART 舵机生态。

## 2. 集成层 (Integration)

本层将 Motorbridge 的硬件能力无缝接入开发者现有的工作流和前沿技术栈。

* **`motorbridge-ros2`**
  * **定位**：标准 ROS2 通用硬件接口。
  * **功能边界**：基于 RustDDS 的原生 DDS 桥接，无需本地 ROS2 安装。通过 C ABI 调用 MotorBridge，将电机直接映射为 ROS 节点中的 Joint。充当连接单体硬件与 ROS 世界的"万能插座"。
* **`motorbridge-agent`**
  * **定位**：AI 代理与大语言模型集成。
  * **功能边界**：基于 MCP (Model Context Protocol) 协议的 MCP Server，为大语言模型（Claude、Cursor 等）提供调用底层硬件的 Tool。使 AI 能通过自然语言分析电机状态、下发动作指令，实现具身智能的基础闭环。

## 3. 产品形态层 (Product Forms)

本层面向最终用户，提供"开箱即用"的机器人子系统控制方案。

* **`motorbridge-arm`**
  * **定位**：串联机械臂完整系统级实现。
  * **功能边界**：基于 `motorbridge` Python 绑定的机械臂 SDK。包含伺服电机 ID 映射、零点标定流程、基于 Pinocchio 的运动学求解、关节空间执行和安全监护。内建完整的硬件拓扑配置。
* **`pinocchio-wasm`**
  * **定位**：WASM 刚体动力学引擎。
  * **功能边界**：面向 WASM 的刚体动力学库。提供正逆运动学 (FK/IK)、雅可比、RNEA、CRBA、ABA、碰撞检测和回归子。通过 C ABI 和 JS 绑定输出，支持 URDF/SDF/MJCF 模型加载。纯数学库，不直接操作硬件。

## 4. 工具与文档层 (Tooling & Docs)

* **`motorbridge-studio`**
  * **定位**：Web 调试与可视化面板。
  * **功能边界**：基于 React + Vite 的纯前端应用，通过 WebSocket 连接后端。提供实时可视化界面，用于单电机或多电机的参数调试、PID 整定、错误重置和数据波形监控。
* **`motorbridge-docs`**
  * **定位**：官方文档站点。
  * **功能边界**：双语（EN/ZH）文档站点。包含 API 参考、快速入门教程、CLI 指南、设备矩阵和开发指南。
* **`.github`**
  * **定位**：组织级规范。
  * **功能边界**：存放组织级别的 README、生态架构说明以及通用社区指南。
