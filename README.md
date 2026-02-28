以下为完整中文翻译：

---

# WiFi DensePose

一个前沿的基于 WiFi 的人体姿态估计系统，利用信道状态信息（CSI）数据和先进的机器学习技术，在无需摄像头的情况下，实现实时、保护隐私的人体姿态检测。

---

## 🚀 核心特性

* **隐私优先**：无需摄像头 —— 使用 WiFi 信号进行姿态检测
* **实时处理**：低于 50ms 延迟，支持 30 FPS 姿态估计
* **多人追踪**：可同时追踪最多 10 人
* **领域定制优化**：适用于医疗、健身、智能家居和安防等场景
* **企业级支持**：生产级 API，支持认证、限流与监控
* **硬件无关**：兼容标准 WiFi 路由器与接入点
* **全面分析能力**：跌倒检测、行为识别、人员占用监测
* **WebSocket 流式传输**：支持实时姿态数据推送
* **100% 测试覆盖率**：完整全面的测试套件

---

## 🦀 Rust 实现版本（v2）

在 `/rust-port/wifi-densepose-rs/` 提供高性能 Rust 移植版本。

### 性能基准（已验证）

| 操作             | Python (v1) | Rust (v2)    | 加速比    |
| -------------- | ----------- | ------------ | ------ |
| CSI 预处理 (4x64) | ~5ms        | **5.19 微秒**  | ~1000x |
| 相位清洗 (4x64)    | ~3ms        | **3.84 微秒**  | ~780x  |
| 特征提取 (4x64)    | ~8ms        | **9.03 微秒**  | ~890x  |
| 运动检测           | ~1ms        | **186 纳秒**   | ~5400x |
| **完整流程**       | ~15ms       | **18.47 微秒** | ~810x  |

### 吞吐量指标

| 组件      | 吞吐量              |
| ------- | ---------------- |
| CSI 预处理 | 49–66 百万元素/秒     |
| 相位清洗    | 67–85 百万元素/秒     |
| 特征提取    | 7–11 百万元素/秒      |
| 完整流程    | **约 54,000 FPS** |

### 资源对比

| 项目      | Python (v1) | Rust (v2) |
| ------- | ----------- | --------- |
| 内存占用    | ~500MB      | ~100MB    |
| WASM 支持 | ❌           | ✅         |
| 二进制大小   | N/A         | ~10MB     |
| 测试数量    | 100% 覆盖     | 107 个测试   |

---

## 🚨 WiFi-Mat：灾害救援模块

用于**搜救行动**的专用扩展模块 —— 在地震、坍塌和自然灾害中检测和定位被困幸存者。

### 核心能力

| 功能       | 描述                     |
| -------- | ---------------------- |
| 生命体征检测   | 呼吸（4–60 次/分钟）、心跳（微多普勒） |
| 三维定位     | 可穿透最多 5 米废墟进行定位        |
| START 分诊 | 自动分类为紧急 / 延迟 / 轻伤 / 死亡 |
| 实时警报     | 基于优先级的分级通知             |

### 适用场景

* 地震搜救
* 建筑坍塌响应
* 雪崩受害者定位
* 矿井塌方检测
* 洪水救援

---

## 🏗️ 系统架构

WiFi DensePose 由多个关键组件协同工作：

* **CSI 处理器**：从 WiFi 信号中提取并处理 CSI 数据
* **相位清洗模块**：去除硬件相位偏移和噪声
* **DensePose 神经网络**：将 CSI 转换为人体关键点
* **多人追踪模块**：跨帧维持人员身份一致性
* **REST API**：数据访问与系统控制接口
* **WebSocket 流**：实时姿态数据广播
* **分析引擎**：跌倒检测与行为识别等高级分析

---

## 📦 安装

### 使用 pip（推荐）

```bash
pip install wifi-densepose
```

可选依赖：

```bash
pip install wifi-densepose[gpu]   # GPU 加速
pip install wifi-densepose[dev]   # 开发环境
pip install wifi-densepose[all]   # 所有可选依赖
```

---

## 🚀 快速开始

### 1. 基础使用

```python
from wifi_densepose import WiFiDensePose

system = WiFiDensePose()
system.start()

poses = system.get_latest_poses()
print(f"检测到 {len(poses)} 人")

system.stop()
```

---

### 2. 启动 API 服务

```bash
wifi-densepose start
```

API 地址：

* 文档：[http://localhost:8000/docs](http://localhost:8000/docs)
* 健康检查：[http://localhost:8000/api/v1/health](http://localhost:8000/api/v1/health)
* 最新姿态：[http://localhost:8000/api/v1/pose/latest](http://localhost:8000/api/v1/pose/latest)

---

### 3. WebSocket 实时流

```python
ws://localhost:8000/ws/pose/stream
```

---

## 🖥 CLI 命令

```bash
wifi-densepose start      # 启动服务
wifi-densepose stop       # 停止服务
wifi-densepose status     # 查看状态
wifi-densepose config     # 配置管理
wifi-densepose db         # 数据库管理
wifi-densepose tasks      # 后台任务管理
wifi-densepose version    # 查看版本
```

---

## 🔧 硬件要求

* Python 3.8+
* Linux / macOS / Windows 10+
* 最少 4GB 内存（推荐 8GB+）
* 支持 CSI 提取的 WiFi 网卡
* 可选 NVIDIA GPU（CUDA）

### 推荐路由器

* ASUS AX6000 (RT-AX88U)
* Netgear Nighthawk AX12
* TP-Link Archer AX73
* Ubiquiti UniFi 6 Pro

---

## ⚙️ 配置

示例环境变量：

```bash
POSE_CONFIDENCE_THRESHOLD=0.7
POSE_MAX_PERSONS=10
ENABLE_AUTHENTICATION=true
ENABLE_WEBSOCKETS=true
```

支持医疗、健身等领域专用配置。

---

## 🧪 测试

```bash
pytest
pytest --cov=wifi_densepose
```

测试分类：

* 单元测试
* 集成测试
* 端到端测试
* 性能测试

---

## 🚀 部署

支持：

* Docker
* Docker Compose
* Kubernetes
* Terraform
* Ansible

---

## 📊 性能指标

* 平均处理时间：45ms
* 姿态检测准确率：94.2%
* 跌倒检测灵敏度：96.5%
* 支持 1000+ WebSocket 连接

---

## 🤝 贡献

* 遵循 PEP8
* 使用类型提示
* 保持 100% 测试覆盖
* 提交 PR 前确保测试通过

---

## 📄 许可证

MIT License

---

## 🙏 致谢

* WiFi 感知研究基础
* PyTorch、FastAPI 等开源项目
* 社区贡献者
* 硬件合作伙伴

---

## 📞 支持

* GitHub Issues
* GitHub Discussions
* PyPI 页面
* Discord 社区
* [support@wifi-densepose.com](mailto:support@wifi-densepose.com)

---

**WiFi DensePose** —— 通过保护隐私的 WiFi 技术，革新人类姿态估计方式。
