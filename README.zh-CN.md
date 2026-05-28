# Awesome VLA Benchmarks [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

[English](README.md) | 简体中文

面向机器人 **Vision-Language-Action (VLA)** 模型的基准、评测框架和数据集整理。

VLA 模型以视觉观测和语言指令为输入，并输出机器人动作。本列表主要整理用于评估这类模型的基准、数据集和相关平台。

**欢迎贡献！** 提交 pull request 前，请先阅读 [贡献指南](CONTRIBUTING.md)。

---

## 目录

- [VLA 模型](#vla-models)
- [仿真基准 - 操作任务](#simulation-benchmarks---manipulation)
- [仿真基准 - 具身智能 / 导航](#simulation-benchmarks---embodied-ai--navigation)
- [人形机器人基准](#humanoid-benchmarks)
- [真实世界数据集与基准](#real-world-datasets--benchmarks)
- [Sim-to-Real 评测](#sim-to-real-evaluation)
- [VLA 专用评测框架](#vla-specific-evaluation-frameworks)
- [鲁棒性与安全基准](#robustness--safety-benchmarks)
- [统一平台](#unified-platforms)
- [综述论文](#survey-papers)
- [相关 Awesome 列表](#related-awesome-lists)

---

<a id="vla-models"></a>
## VLA 模型

按时间倒序整理已发布的 Vision-Language-Action 模型，最新模型放在前面。

- **VLM 骨干**：VLA 所基于的预训练视觉语言模型；若未使用预训练 VLM，则标注为 "from-scratch"。
- **动作头**：连续机器人动作的生成方式，例如离散动作 token、扩散模型、flow matching 等。
- **开放情况**：✓ 表示权重/代码已公开；◐ 表示部分公开（仅代码或权重受限）；✗ 表示闭源。

| 模型 | 日期 | 机构 | VLM 骨干 | 动作头 | 参数量 | 开放 | 链接 |
|------|------|------|----------|--------|--------|------|------|
| **ProgVLA** | 2026-05 | Samsung / KU Leuven | 紧凑多模态编码器 | 进度感知 flow matching + RL heads | 0.1B | ✗ | [Paper](https://arxiv.org/abs/2605.28231) |
| **X-DiffVLA** | 2026-05 | Peking Univ. et al. | VLA backbone | 跨 embodiment 扩散动作头 | - | ✗ | [Paper](https://arxiv.org/abs/2605.25044) |
| **HEX** | 2026-04 | Tsinghua / Huawei et al. | VLM + 本体感知专家 | Flow matching 全身动作头 | - | ✗ | [Paper](https://arxiv.org/abs/2604.07993) |
| **MMaDA-VLA** | 2026-03 | DAMO / Zhejiang Univ. et al. | MMaDA 扩散骨干 | 面向语言/图像/动作 token 的原生离散扩散 | - | ✗ | [Paper](https://arxiv.org/abs/2603.25406) |
| **AR-VLA** | 2026-03 | INSAIT / KU Leuven | 模块化 VLA 感知骨干 | 自回归连续动作专家 | - | ✓ | [Paper](https://arxiv.org/abs/2603.10126) / [Site](https://arvla.insait.ai/) |
| **DAM-VLA** | 2026-03 | Yonsei Univ. et al. | VLM 推理模块 | 路由式动态扩散动作模型 | - | ✗ | [Paper](https://arxiv.org/abs/2603.00926) |
| **LAP-3B** | 2026-02 | Princeton / Physical Intelligence | Large VLM | Language-action 预训练 | 3B | ✓ | [Paper](https://arxiv.org/abs/2602.10556) / [Site](https://lap-vla.github.io/) |
| **LingBot-VLA** | 2026-01 | Ant Group / Robbyant | Qwen2.5-VL + depth features | 双臂动作解码器 | 4B | ✓ | [Paper](https://arxiv.org/abs/2601.18692) / [Code](https://github.com/Robbyant/lingbot-vla) |
| **ACoT-VLA** | 2026-01 | AgiBot | 预训练 VLM 骨干 | Action Chain-of-Thought + flow matching | - | ✓ | [Paper](https://arxiv.org/abs/2601.11404) / [Code](https://github.com/AgibotTech/ACoT-VLA) |
| **Green-VLA** | 2026-01 | Sber Robotics Center | GreenVLA 2B / 5B | 分阶段多 embodiment 策略 + RL 对齐 | 2B / 5B | ✓ | [Paper](https://arxiv.org/abs/2602.00919) / [Code](https://github.com/greenvla/GreenVLA) |
| **AVA-VLA** | 2025-11 | Li Auto DSR | VLA backbone + recurrent state | 主动视觉注意力动作策略 | 8B | ◐ | [Paper](https://arxiv.org/abs/2511.18960) / [Site](https://liauto-dsr.github.io/AVA-VLA-Page) |
| **X-VLA** | 2025-10 | Tsinghua AIR et al. | Soft-prompted Transformer | Flow matching 跨 embodiment 动作头 | 0.9B | ✗ | [Paper](https://arxiv.org/abs/2510.10274) / [Site](https://thu-air-dream.github.io/X-VLA/) |
| **Discrete Diffusion VLA** | 2025-08 | Shanghai AI Lab et al. | Single Transformer VLM | 离散扩散动作解码器 | - | ✗ | [Paper](https://arxiv.org/abs/2508.20072) |
| **MolmoAct** | 2025-08 | Allen AI (AI2) | Molmo VLM | 动作推理 + 分块动作 token | 7B | ✓ | [Paper](https://arxiv.org/abs/2508.07917) / [Code](https://github.com/allenai/MolmoAct) |
| **Gemini Robotics On-Device** | 2025-06 | Google DeepMind | Gemini Nano family | 端侧动作解码器 | - | ✗ | [Site](https://deepmind.google/discover/blog/gemini-robotics-on-device-brings-ai-to-local-robotic-devices/) |
| **WorldVLA** | 2025-06 | Alibaba DAMO | Chameleon | 统一世界模型 + 动作自回归 | 7B | ✓ | [Paper](https://arxiv.org/abs/2506.21539) / [Code](https://github.com/alibaba-damo-academy/WorldVLA) |
| **GR00T N1.5** | 2025-06 | NVIDIA | Eagle-2 VLM | DiT 动作头（改进后训练） | 2B | ✓ | [Code](https://github.com/NVIDIA/Isaac-GR00T) |
| **SmolVLA** | 2025-06 | Hugging Face | SmolVLM-2 | Flow matching 动作专家 | 450M | ✓ | [Paper](https://arxiv.org/abs/2506.01844) / [Code](https://github.com/huggingface/lerobot) |
| **NORA** | 2025-04 | SUTD | Qwen2.5-VL | FAST token | 3B | ✓ | [Paper](https://arxiv.org/abs/2504.19854) / [Code](https://github.com/declare-lab/nora) |
| **π0.5** | 2025-04 | Physical Intelligence | π0 + open-world co-training | Flow matching，泛化到未见过的家庭环境 | 3B | ✗ | [Paper](https://arxiv.org/abs/2504.16054) / [Site](https://www.physicalintelligence.company/blog/pi05) |
| **GO-1** | 2025-03 | AgiBot | InternVL backbone | 潜变量规划器 + 动作专家 (ViLLA) | - | ◐ | [Site](https://agibot-world.com/blog/go1) / [Code](https://github.com/OpenDriveLab/AgiBot-World) |
| **Gemini Robotics** | 2025-03 | Google DeepMind | Gemini 2.0 | 动作解码器（闭源） | - | ✗ | [Paper](https://arxiv.org/abs/2503.20020) / [Site](https://deepmind.google/discover/blog/gemini-robotics-brings-ai-into-the-physical-world/) |
| **GR00T N1** | 2025-03 | NVIDIA | Eagle-2 VLM | DiT 动作头（System 1+2 设计） | 2B | ✓ | [Paper](https://arxiv.org/abs/2503.14734) / [Code](https://github.com/NVIDIA/Isaac-GR00T) |
| **OpenVLA-OFT** | 2025-02 | Stanford | OpenVLA | 并行解码 + 连续动作 + L1 回归 | 7B | ✓ | [Paper](https://arxiv.org/abs/2502.19645) / [Code](https://github.com/moojink/openvla-oft) |
| **Hi Robot** | 2025-02 | Physical Intelligence | π0 backbone + high-level VLM | 分层结构（指令 → 动作） | 3B | ✗ | [Paper](https://arxiv.org/abs/2502.19417) / [Site](https://www.physicalintelligence.company/research/hirobot) |
| **Helix** | 2025-02 | Figure AI | S2 (VLM, ~7B) + S1 (80M visuomotor) | 双系统，S1 以 200Hz 运行 | ~7B (S2) | ✗ | [Site](https://www.figure.ai/news/helix) |
| **Magma** | 2025-02 | Microsoft | LLaVA-style | Set-of-marks + action traces | 8B | ✓ | [Paper](https://arxiv.org/abs/2502.13130) / [Code](https://github.com/microsoft/Magma) |
| **DexVLA** | 2025-02 | Midea | Qwen2-VL | 扩散动作专家（灵巧操作） | 1B+ | ✓ | [Paper](https://arxiv.org/abs/2502.05855) / [Site](https://dex-vla.github.io/) |
| **SpatialVLA** | 2025-01 | Shanghai AI Lab et al. | PaliGemma2 | Ego3D 位置感知动作 token | 4B | ✓ | [Paper](https://arxiv.org/abs/2501.15830) / [Code](https://github.com/SpatialVLA/SpatialVLA) |
| **π0-FAST** | 2025-01 | Physical Intelligence | PaliGemma | FAST (DCT) 动作 token | 3B | ✓ | [Paper](https://arxiv.org/abs/2501.09747) / [Site](https://www.physicalintelligence.company/research/fast) |
| **CogACT** | 2024-11 | Microsoft Research Asia | OpenVLA-style (DINOv2+SigLIP+Llama2) | DiT 动作专家（认知/动作解耦） | 7B+ | ✓ | [Paper](https://arxiv.org/abs/2411.19650) / [Code](https://github.com/microsoft/CogACT) |
| **π0 (Pi-Zero)** | 2024-10 | Physical Intelligence | PaliGemma | Flow-matching 动作专家 | 3B | ✓ | [Paper](https://arxiv.org/abs/2410.24164) / [Code](https://github.com/Physical-Intelligence/openpi) |
| **RDT-1B** | 2024-10 | Tsinghua AIR | SigLIP + T5-XXL | Diffusion Transformer | 1B | ✓ | [Paper](https://arxiv.org/abs/2410.07864) / [Code](https://github.com/thu-ml/RoboticsDiffusionTransformer) |
| **TinyVLA** | 2024-09 | Midea / ECNU | Small VLM (Pythia-based) | 扩散动作头 | <1B | ✓ | [Paper](https://arxiv.org/abs/2409.12514) / [Site](https://tiny-vla.github.io/) |
| **OpenVLA** | 2024-06 | Stanford / UC Berkeley | Llama-2-7B + DINOv2 + SigLIP | 离散动作 token（自回归） | 7B | ✓ | [Paper](https://arxiv.org/abs/2406.09246) / [Code](https://github.com/openvla/openvla) |
| **Octo** | 2024-05 | UC Berkeley / Stanford | Transformer (from-scratch) | 扩散动作头 | 27M / 93M | ✓ | [Paper](https://arxiv.org/abs/2405.12213) / [Code](https://github.com/octo-models/octo) |
| **3D-VLA** | 2024-03 | UMass / MIT | 3D-LLM | 生成式 3D 目标 + 动作 | - | ✓ | [Paper](https://arxiv.org/abs/2403.09631) / [Code](https://github.com/UMass-Foundation-Model/3D-VLA) |
| **RoboFlamingo** | 2023-11 | ByteDance / Berkeley | OpenFlamingo | LSTM 动作头 | ~3B | ✓ | [Paper](https://arxiv.org/abs/2311.01378) / [Code](https://github.com/RoboFlamingo/RoboFlamingo) |
| **RT-2-X / RT-X** | 2023-10 | Open X-Embodiment collab | PaLI-X | 离散动作 token，跨 embodiment | 55B | ✗ | [Paper](https://arxiv.org/abs/2310.08864) / [Site](https://robotics-transformer-x.github.io/) |
| **RT-2** | 2023-07 | Google DeepMind | PaLI-X / PaLM-E | 离散动作 token（与网页数据联合微调） | 5B / 55B | ✗ | [Paper](https://arxiv.org/abs/2307.15818) / [Site](https://robotics-transformer2.github.io/) |
| **PaLM-E** | 2023-03 | Google | PaLM + ViT | LLM 驱动规划（文本动作） | up to 562B | ✗ | [Paper](https://arxiv.org/abs/2303.03378) / [Site](https://palm-e.github.io/) |
| **RT-1** | 2022-12 | Google | EfficientNet + Universal Sentence Encoder | 离散动作 token (Transformer) | 35M | ✓ | [Paper](https://arxiv.org/abs/2212.06817) / [Code](https://github.com/google-research/robotics_transformer) |

---

<a id="simulation-benchmarks---manipulation"></a>
## 仿真基准 - 操作任务

| 基准 | 年份 | 仿真器 | 任务 | 关注重点 | 链接 |
|------|------|--------|------|----------|------|
| **DOMINO** | 2026 | - | 35 tasks, 110K+ trajs | 动态操作泛化 | [Paper](https://arxiv.org/abs/2603.15620) / [Code](https://github.com/H-EmbodVis/DOMINO) |
| **LiLo-VLA (LIBERO-Long++ / Ultra-Long)** | 2026 | robosuite | 21 tasks | 基于物体中心链接的组合式长时程操作 | [Paper](https://arxiv.org/abs/2602.21531) |
| **InstructVLA** | 2026 | - | Instruction-tuning suite | 从理解到操作的指令微调套件（ICLR 2026） | [Code](https://github.com/InternRobotics/InstructVLA) |
| **GenManip** | 2025 | - | 200 scenarios | LLM 驱动的指令泛化 | [Paper](https://arxiv.org/abs/2501.03327) / [Code](https://github.com/InternRobotics/GenManip) |
| **PerAct2** | 2024 | CoppeliaSim | 18 bimanual tasks | 双臂 6-DoF 协作 | [Paper](https://arxiv.org/abs/2407.00278) / [Code](https://github.com/markusgrotz/peract_bimanual) |
| **ManiSkill3** | 2024 | SAPIEN | 12 domains | GPU 并行，最快仿真（30K+ FPS） | [Paper](https://arxiv.org/abs/2410.00425) / [Code](https://github.com/haosulab/ManiSkill) |
| **ManiSkill-HAB** | 2024 | SAPIEN | Home rearrangement | 面向家庭场景的低层操作 | [Paper](https://arxiv.org/abs/2410.07889) / [Site](https://arth-shukla.github.io/mshab/) |
| **COLOSSEUM** | 2024 | CoppeliaSim | 20 tasks x 14 perturbations | 系统化泛化测试 | [Paper](https://arxiv.org/abs/2402.08191) / [Code](https://github.com/robot-colosseum/robot-colosseum) |
| **VLABench** | 2024 | - | 100 categories, 2000+ objects | 长时程推理 | [Paper](https://arxiv.org/abs/2412.18477) / [Code](https://github.com/OpenMOSS/VLABench) |
| **GemBench** | 2024 | CoppeliaSim | 7 primitives x 4 levels | 不同泛化层级 | [Paper](https://arxiv.org/abs/2410.18084) / [Code](https://github.com/vlc-robot/robot-3dlotus) |
| **ClevrSkills** | 2024 | ManiSkill2 | 33 tasks, 330K trajs | 组合式推理 | [Paper](https://arxiv.org/abs/2404.09187) |
| **RoboCasa** | 2024 | robosuite | 100-365 tasks | 厨房任务，通用机器人 | [Paper](https://arxiv.org/abs/2406.02523) / [Code](https://github.com/robocasa/robocasa) |
| **BiGym** | 2024 | MuJoCo | 40 tasks | 双臂移动操作 | [Paper](https://arxiv.org/abs/2407.07788) / [Code](https://github.com/chernyadev/bigym) |
| **RoboTwin** | 2024 | - | 50 tasks, 5 embodiments | 生成式数字孪生中的双臂任务 | [Paper](https://arxiv.org/abs/2409.02920) / [Code](https://github.com/RoboTwin-Platform/RoboTwin) |
| **LIBERO** | 2023 | robosuite | 130 tasks, 4 suites | 终身学习、知识迁移 | [Paper](https://arxiv.org/abs/2306.03310) / [Code](https://github.com/Lifelong-Robot-Learning/LIBERO) |
| **VIMA** | 2023 | PyBullet | 17 task types, 600K+ trajs | 多模态 prompt 条件任务 | [Paper](https://arxiv.org/abs/2210.03094) / [Code](https://github.com/vimalabs/VimaBench) |
| **ARNOLD** | 2023 | Isaac Sim | 8 tasks, 40 objects | 真实感 3D 场景中的连续状态 | [Paper](https://arxiv.org/abs/2304.04321) / [Code](https://github.com/arnold-benchmark/arnold) |
| **LoHoRavens** | 2023 | PyBullet | 10 tasks | 无逐步指令的长时程任务 | [Paper](https://arxiv.org/abs/2310.12020) / [Code](https://github.com/Shengqiang-Zhang/LoHo-Ravens) |
| **FurnitureBench** | 2023 | Isaac Gym | 8 IKEA-style tasks | 长时程家具组装 | [Paper](https://arxiv.org/abs/2305.12821) / [Code](https://github.com/clvrai/furniture-bench) |
| **DexArt** | 2023 | SAPIEN | Multiple | 灵巧手操作铰接物体 | [Paper](https://arxiv.org/abs/2305.05706) / [Code](https://github.com/Kami-code/dexart-release) |
| **CALVIN** | 2022 | PyBullet | 34 tasks, 4 envs | 长时程语言条件操作 | [Paper](https://arxiv.org/abs/2112.03227) / [Code](https://github.com/mees/calvin) |
| **Ravens / CLIPort** | 2020/22 | PyBullet | 10 tasks | Transporter / 语言条件重排 | [Paper](https://arxiv.org/abs/2109.12098) / [Code](https://github.com/google-research/ravens) |
| **BEHAVIOR-1K** | 2022 | OmniGibson | 1000 activities | 完整家庭活动 | [Paper](https://arxiv.org/abs/2403.09227) / [Code](https://github.com/StanfordVL/BEHAVIOR-1K) |
| **Bi-DexHands** | 2022 | Isaac Gym | Thousands | 双手灵巧操作 | [Paper](https://arxiv.org/abs/2206.08686) / [Code](https://github.com/PKU-MARL/DexterousHands) |
| **RoboMimic** | 2021 | MuJoCo | 5 sim + 3 real tasks | 从人类演示进行模仿学习 | [Paper](https://arxiv.org/abs/2108.03298) / [Code](https://github.com/ARISE-Initiative/robomimic) |
| **RLBench** | 2020 | CoppeliaSim | 100 tasks | 视觉引导操作（RL、IL、few-shot） | [Paper](https://arxiv.org/abs/1909.12271) / [Code](https://github.com/stepjam/RLBench) |
| **robosuite** | 2020 | MuJoCo | 9 tasks, 10 robots | 模块化操作任务框架 | [Paper](https://arxiv.org/abs/2009.12293) / [Code](https://github.com/ARISE-Initiative/robosuite) |
| **Meta-World** | 2019 | MuJoCo | 50 tasks | 多任务 / 元强化学习 | [Paper](https://arxiv.org/abs/1910.10897) / [Code](https://github.com/Farama-Foundation/Metaworld) |
| **Franka Kitchen** | 2019 | MuJoCo | 4 subtasks | 多任务离线强化学习 | [Paper](https://arxiv.org/abs/1910.11956) |

<a id="simulation-benchmarks---embodied-ai--navigation"></a>
## 仿真基准 - 具身智能 / 导航

| 基准 | 年份 | 仿真器 | 任务 | 关注重点 | 链接 |
|------|------|--------|------|----------|------|
| **EmbodiedBench** | 2025 | Multi-env | 1,128 instances | 基于 MLLM 的具身智能体 | [Paper](https://arxiv.org/abs/2504.01850) / [Code](https://github.com/EmbodiedBench/EmbodiedBench) |
| **Habitat 2.0** | 2021 | Habitat Sim | Thousands of envs | 导航 + 重排 | [Paper](https://arxiv.org/abs/2106.14405) / [Site](https://aihabitat.org/) |
| **AI2-THOR / ManipulaTHOR** | 2017 | Unity | 120+ rooms | 导航 + 操作 | [Paper](https://arxiv.org/abs/1712.05474) / [Code](https://github.com/allenai/ai2thor) |

<a id="humanoid-benchmarks"></a>
## 人形机器人基准

| 基准 | 年份 | 仿真器 | 任务 | 关注重点 | 链接 |
|------|------|--------|------|----------|------|
| **SIMPLE** (Psi-0) | 2026 | MuJoCo + Isaac Sim | 6+ loco-manip tasks | 开放的人形机器人 VLA 基准仿真器 | [Paper](https://arxiv.org/abs/2603.12263) / [Code](https://github.com/physical-superintelligence-lab/Psi0) |
| **LeVERB** | 2025 | Isaac Lab | 150+ tasks, 10 categories | 视觉语言人形机器人全身控制 | [Paper](https://arxiv.org/abs/2506.13751) |
| **Ego Humanoid Manipulation** | 2025 | Isaac Lab | 12 tasks | 第一视角人形机器人操作 | [Code](https://github.com/quincy-u/Ego_Humanoid_Manipulation_Benchmark) |
| **HumanoidGen (HGen-Bench)** | 2025 | SAPIEN | 20 tasks | LLM 驱动的双臂灵巧任务生成 | [Paper](https://arxiv.org/abs/2507.00833) / [Code](https://github.com/TeleHuman/HumanoidGen) |
| **Humanoid Everyday** | 2025 | Real-world | 260 tasks, 10.3K trajs | 大规模真实人形机器人操作 | [Paper](https://arxiv.org/abs/2510.08807) / [Data](https://huggingface.co/datasets/USC-GVL/humanoid-everyday) |
| **HumanoidBench** | 2024 | MuJoCo | 27 (15 manip + 12 loco) | 全身运动与操作 | [Paper](https://arxiv.org/abs/2403.10506) / [Code](https://github.com/carlosferrazza/humanoid-bench) |
| **OmniH2O** | 2024 | Isaac Gym | 6 tasks | 人到人形机器人的遥操作与自主化 | [Paper](https://arxiv.org/abs/2406.08858) / [Code](https://github.com/LeCAR-Lab/human2humanoid) |
| **Mimicking-Bench** | 2024 | - | 6 tasks, 23K sequences | 人到人形机器人的场景交互模仿 | [Paper](https://arxiv.org/abs/2412.17730) / [Site](https://mimicking-bench.github.io/) |

<a id="real-world-datasets--benchmarks"></a>
## 真实世界数据集与基准

| 基准 | 年份 | Embodiment | 规模 | 关注重点 | 链接 |
|------|------|------------|------|----------|------|
| **RoboMIND** | 2025 | 4 embodiments | 107K trajs, 479 tasks | 多 embodiment，并包含失败数据 | [Paper](https://arxiv.org/abs/2412.13877) / [Site](https://x-humanoid-robomind.github.io/) |
| **AgiBot World** | 2025 | Dual-arm | 1M+ trajs, 217 tasks | 大规模双臂数据（4000 m² 设施） | [Paper](https://arxiv.org/abs/2503.18899) / [Code](https://github.com/OpenDriveLab/AgiBot-World) |
| **DROID** | 2024 | 18 Frankas | 76K trajs, 564 scenes | 野外真实操作 | [Paper](https://arxiv.org/abs/2403.12945) / [Code](https://github.com/droid-dataset/droid_policy_learning) |
| **FMB** | 2024 | Franka | 22.5K demos | 功能性操作（抓取、装配） | [Paper](https://arxiv.org/abs/2401.08553) / [Site](https://functional-manipulation-benchmark.github.io/) |
| **RoboVQA** | 2024 | 3 embodiments | 829K pairs | 面向机器人推理的 VQA | [Paper](https://arxiv.org/abs/2311.00899) / [Site](https://robovqa.github.io/) |
| **Open X-Embodiment** | 2023 | 22 robots | 1M+ trajs, 527 skills | 跨 embodiment 迁移 | [Paper](https://arxiv.org/abs/2310.08864) / [Code](https://github.com/google-deepmind/open_x_embodiment) |
| **BridgeData V2** | 2023 | WidowX 250 | 60K trajs, 24 envs | 多任务、跨环境 | [Paper](https://arxiv.org/abs/2308.12952) / [Site](https://rail-berkeley.github.io/bridgedata/) |
| **RoboSet** | 2023 | Franka | 7.5K trajs, 38 tasks | 厨房多任务 | [Paper](https://arxiv.org/abs/2307.01918) / [Site](https://robopen.github.io/roboset/) |
| **Language-Table** | 2023 | Custom | 600K trajs | 开放词汇推动 / 重排 | [Paper](https://arxiv.org/abs/2210.10645) / [Code](https://github.com/google-research/language-table) |
| **LHManip** | 2023 | Real robot | 200 episodes, 20 tasks | 杂乱场景中的长时程操作 | [Paper](https://arxiv.org/abs/2312.12036) / [Code](https://github.com/fedeceola/LHManip) |
| **ALOHA / Mobile ALOHA** | 2023 | Custom bimanual | 7-50 tasks | 双臂（移动）操作 | [Paper](https://arxiv.org/abs/2304.13705) / [Site](https://tonyzhaozh.github.io/aloha/) |
| **MUTEX** | 2023 | Franka | 100 sim + 50 real | 6 种模态的任务规格 | [Paper](https://arxiv.org/abs/2309.14320) |

<a id="sim-to-real-evaluation"></a>
## Sim-to-Real 评测

| 基准 | 年份 | 方法 | 关注重点 | 链接 |
|------|------|------|----------|------|
| **REALM** | 2025 | Real-validated sim | 15 个扰动因素，与真实结果显著相关（p<0.001） | [Paper](https://arxiv.org/abs/2502.02538) / [Code](https://github.com/martin-sedlacek/REALM) |
| **RobotArena Infinity** | 2025 | Real-to-sim translation | VLM 评分 + 人类偏好 | [Paper](https://arxiv.org/abs/2504.04603) / [Site](https://robotarenainf.github.io/) |
| **RoboArena** | 2025 | Distributed real eval | 众包式 ELO 排名评测 | [Paper](https://arxiv.org/abs/2504.08659) |
| **RoboChallenge** | 2025 | Remote real robots | 30 个任务，10 台机器人组成的远程评测平台 | [Paper](https://arxiv.org/abs/2504.01783) / [Site](https://robochallenge.ai/) |
| **SimplerEnv (SIMPLER)** | 2024 | Sim-as-real proxy | 在仿真中评估真实世界策略 | [Paper](https://arxiv.org/abs/2405.05941) / [Code](https://github.com/simpler-env/SimplerEnv) |

<a id="vla-specific-evaluation-frameworks"></a>
## VLA 专用评测框架

| 框架 | 年份 | 类型 | 关注重点 | 链接 |
|------|------|------|----------|------|
| **vla-eval** | 2026 | Unified harness | 17 个基准、500+ 模型，基于 Docker | [Code](https://github.com/allenai/vla-evaluation-harness) |
| **Eval-Actions + AutoEval** | 2026 | Automated eval | 可信机器人操作评测协议 | [Paper](https://arxiv.org/abs/2601.18723) |
| **VLA-Arena** | 2025 | Systematic eval | 170 个任务，4 个维度 x 3 个难度等级 | [Paper](https://arxiv.org/abs/2504.14064) / [Code](https://github.com/PKU-Alignment/VLA-Arena) |
| **ManipBench** | 2025 | MCQ-based | 面向低层操作的 VLM 推理评测 | [Paper](https://arxiv.org/abs/2504.02452) / [Site](https://manipbench.github.io/) |
| **RoboBench** | 2025 | MCQ/VQA-based | 将 MLLM 作为具身大脑，从 5 个认知维度评估 | [Paper](https://arxiv.org/abs/2503.19827) / [Site](https://robo-bench.github.io/) |
| **LADEV** | 2024 | Language-driven eval | 从自然语言描述自动生成场景 | [Paper](https://arxiv.org/abs/2410.05613) |

<a id="robustness--safety-benchmarks"></a>
## 鲁棒性与安全基准

| 基准 | 年份 | 扩展自 | 关注重点 | 链接 |
|------|------|--------|----------|------|
| **LIBERO-X** | 2026 | LIBERO | 分层鲁棒性 litmus test | - |
| **LIBERO-Para** | 2026 | LIBERO | 释义鲁棒性（22-52% 性能下降） | - |
| **RoboMME** | 2026 | Custom | 记忆增强 VLA 评测 | [Code](https://github.com/RoboMME/robomme_benchmark) |
| **RoboCasa-Safety (via OmniGuide)** | 2026 | RoboCasa | 安全率协议（不与静态家具碰撞）+ 3D SDF 引导 | [Paper](https://arxiv.org/abs/2603.10052) / [Site](https://omniguide.github.io/) |
| **Linguistic Red-Team** | 2026 | Multiple | 多样性感知对抗指令（SR 93% → 5.85%） | [Paper](https://arxiv.org/abs/2604.05595) |
| **VLSA / AEGIS** | 2026 | Plug-in | 即插即用 CBF 安全约束层，带理论保证 | [Paper](https://arxiv.org/abs/2512.11891) |
| **LIBERO-PRO** | 2025 | LIBERO | 4 维扰动下的鲁棒性 | [Paper](https://arxiv.org/abs/2502.18985) / [Code](https://github.com/Zxy-MLlab/LIBERO-PRO) |
| **LIBERO-Plus** | 2025 | LIBERO | 7 个维度 x 5 个等级的鲁棒性分析 | [Paper](https://arxiv.org/abs/2503.16064) / [Code](https://github.com/sylvestf/LIBERO-plus) |
| **SimX-OR** | 2025 | Plug-in | 观测鲁棒性（模糊、噪声等） | [Paper](https://arxiv.org/abs/2504.12453) / [Code](https://github.com/LiHaoHN/SimX-OR) |
| **Eva-VLA** | 2025 | LIBERO | 对抗性物理变化 | [Paper](https://arxiv.org/abs/2501.01370) |
| **VLA-Risk** | 2025 | Multiple | 296 个场景、3 个维度（物体/动作/空间）x 2 种模态的安全风险评测 | [OpenReview](https://openreview.net/forum?id=31EjDFwFEe) |
| **Safety-CHORES / SafeVLA** | 2025 | AI2-THOR / CHORES | 长时程导航+操作中的 5 类成本（corner、blind_spot、fragile、critical、danger）；通过 CMDP 进行安全 RL（NeurIPS 2025 Spotlight） | [Paper](https://arxiv.org/abs/2503.03480) / [Code](https://github.com/PKU-Alignment/SafeVLA) / [Site](https://pku-safevla.github.io/) |

<a id="unified-platforms"></a>
## 统一平台

| 平台 | 年份 | 关注重点 | 链接 |
|------|------|----------|------|
| **RoboVerse** | 2025 | 跨仿真器统一平台（MetaSim） | [Paper](https://arxiv.org/abs/2504.09837) / [Code](https://github.com/RoboVerseOrg/RoboVerse) |
| **STAR-Gen** | 2025 | 泛化分类法（视觉、语义、行为） | [Paper](https://arxiv.org/abs/2503.11106) / [Site](https://stargen-taxonomy.github.io/) |

<a id="survey-papers"></a>
## 综述论文

- **"Vision-Language-Action Models for Robotics: A Review"** - [Site](https://vla-survey.github.io/)
- **"Pure Vision Language Action (VLA) Models: A Comprehensive Survey"** - [Paper](https://arxiv.org/abs/2509.19012)
- **"A Survey on Vision-Language-Action Models for Embodied AI"** - [Paper](https://arxiv.org/abs/2405.14093)
- **"A Survey on Efficient Vision-Language-Action Models"** - [Paper](https://arxiv.org/abs/2510.24795) / [Site](https://evla-survey.github.io/)
- **"A Survey on Vision-Language-Action Models: An Action Tokenization Perspective"** - [Paper](https://arxiv.org/abs/2507.01925)
- **"Benchmarking the Generality of Vision-Language-Action Models"** - [Paper](https://arxiv.org/abs/2512.11315)

<a id="related-awesome-lists"></a>
## 相关 Awesome 列表

- [Awesome-VLA](https://github.com/LukeLIN-web/Awesome-VLA) - VLA 模型、基准、数据集
- [awesome-world-models-for-vla-agents](https://github.com/FutureTwT/awesome-world-models-for-vla-agents) - 面向 VLA agent 的世界模型
- [awesome-embodied-vla-va-vln](https://github.com/jonyzhang2023/awesome-embodied-vla-va-vln) - VLA、VA、VLN 最新进展
- [Awesome-VLA-Papers](https://github.com/Psi-Robot/Awesome-VLA-Papers) - 动作 tokenization 视角
- [awesome-physical-ai](https://github.com/keon/awesome-physical-ai) - Physical AI、VLA、世界模型
- [Awesome-VLA-Robotics](https://github.com/Jiaaqiliu/Awesome-VLA-Robotics) - 综合性 VLA 论文列表
- [Awesome-RL-VLA](https://github.com/Denghaoyuan123/Awesome-RL-VLA) - RL + VLA
- [Awesome-VLA (yueen-ma)](https://github.com/yueen-ma/Awesome-VLA) - 400+ 篇论文可视化整理
- [Awesome-Learning-for-Manipulation](https://github.com/Noietch/Awesome-Learning-for-Manipulation) - VLA、visuomotor、世界模型

---

## 贡献

请阅读 [CONTRIBUTING.md](CONTRIBUTING.md) 了解贡献方式。

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)
