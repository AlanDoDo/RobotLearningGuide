- 开源教程学习(从数采→后训练→部署详细指导)
- [教程链接](https://ldgl0ghbka.feishu.cn/wiki/MZNSwUT88i8ijokrEMPcgYF5nIb)
- [Github地址](https://github.com/Robbyant/lingbot-vla/)

## Install

```shell
conda create -n lingbotvla python=3.12 -y
conda activate lingbotvla
```

```shell
git clone https://github.com/Robbyant/lingbot-vla.git
```

```shell
cd lingbot-vla
bash install.sh
```

```shell
sudo apt-get update
sudo apt-get install -y ffmpeg libavdevice-dev libavfilter-dev libavformat-dev libavcodec-dev libswr  esample-dev libswscale-dev libavutil-dev
```


## Download Model

### Lingbot-VLA预训练权重（必须）

LingBot-VLA 的预训练权重，包含两种配置：无深度（depth-free）版本和深度蒸馏（depth-distilled）版本。
```Plain
python3 scripts/download_hf_model.py --repo_id robbyant/lingbot-vla-4b --local_dir /data/models
#从modelscope下载模型
pip install modelscope
modelscope download --model Robbyant/lingbot-vla-4b --local_dir /data/models/lingbot-vla-4b
```

### Qwen2.5-VL-3B-Instruct模型（必须）

LingBot-VLA 使用 Qwen2.5-VL-3B-Instruct 模型作为视觉语言基座。训练或推理均需要准备 Qwen2.5-VL-3B-Instruct 模型，同样使用脚本下载

```Plain
python3 scripts/download_hf_model.py --repo_id Qwen/Qwen2.5-VL-3B-Instruct --local_dir /data/models
# 或使用modelscope下载
modelscope download --model Qwen/Qwen2.5-VL-3B-Instruct --local_dir /data/models/Qwen2.5-VL-3B-Instruct
```

## 训练数据准备

[Lerobot快速上手指南](https://ldgl0ghbka.feishu.cn/wiki/MRyDwqbKtiXxH4kyLP0cbYYPnAg?from=from_copylink)

```Python
# lerobot_example脚本目录预览
lerobot_example/
├── 1_查看端口.py           # 查找可用串口
├── 2_查看摄像头.py          # 查找可用摄像头
├── 3_摄像头测试.py          # 摄像头实时预览测试
├── 4_机械臂校准标定.py       # 机械臂零点校准
├── 5_遥操作.py             # 单臂遥操作
├── 5_2_双臂遥操作.py        # 双臂遥操作
├── 6_数据采集.py            # 单臂数据采集
├── 6_2_双臂数据采集.py       # 双臂数据采集
├── 7_回放数据集.py          # 回放已采集的数据集
├── 8_数据可视化.py          # 数据集可视化
├── 9_训练.py               # 策略训练
├── 10_推理.py              # 本地策略推理
├── lingbot-vla推理.py       # WebSocket 云端 VLA 推理（RTC 实时分块）
├── scripts/                # 支持库目录
│   ├── Params.py           # 全局硬件参数配置
│   ├── cli_utils.py        # CLI 命令执行工具
│   ├── image_tools.py      # 图像处理工具
│   ├── lerobot_robot_client.py  # WebSocket 机器人客户端核心（含 RTC）
│   ├── websocket_client_policy.py # WebSocket 策略通信封装
│   └── msgpack_numpy.py    # NumPy 数组序列化
└── README.md               # 本文档
```

## 开始训练及评估

```Bash
bash train.sh tasks/vla/train_lingbotvla.py ./configs/vla/my_vla_task.yaml
```

## 真机部署

```Python
# ==================== 机器人硬件配置（从 Params.py 导入） ====================
# 单臂机器人配置示例（如使用 so100_follower / koch_follower 等，请取消下方注释并注释掉双臂配置）
# ROBOT_TYPE = "so100_follower"
# ROBOT_PORT_CFG = f'--robot.port={ROBOT_PORT}'
# ROBOT_ID_CFG = f'--robot.id={ROBOT_ID}'

# 双臂机器人配置示例（bi_so102_follower / bi_so100_follower / bi_so101_follower 等）
ROBOT_TYPE = "bi_so102_follower"
ROBOT_LEFT_ARM_PORT = f'--robot.left_arm_port={LEFT_ROBOT_PORT}'
ROBOT_LEFT_ARM_ID = f'--robot.left_arm_id={LEFT_ROBOT_ID}'
ROBOT_RIGHT_ARM_PORT = f'--robot.right_arm_port={RIGHT_ROBOT_PORT}'
ROBOT_RIGHT_ARM_ID = f'--robot.right_arm_id={RIGHT_ROBOT_ID}'

# ==================== 推理服务器配置 ====================
# 服务器使用 HTTPS，对应 WebSocket 应使用 wss://
SERVER_HOST = "wss://fg68n6zezsnym8omakea100.funhpc.com"
SERVER_PORT = 30499
SERVER_PATH = ""          # WebSocket 端点路径，如服务器要求特定路径请填写，例如: "ws" 或 "infer"
USE_SSL = True            # 启用 wss://（host 已带 wss:// 前缀时此参数不影响实际协议，但建议保持 True）

# ==================== LingBot-VLA 配置 ====================
ROBOT_CONFIG_NAME = "bi_so102"      # configs/robot_configs/<name>.yaml
ACTIONS_PER_CHUNK = 25              # 每块推理动作数（对应 LingBot-VLA 的 --use_length）
FPS = 15                            # 控制循环频率 (Hz)
TASK = "pick up a tape and put it into a drawer"       # 自然语言任务指令

# 反归一化配置（如服务器返回归一化 action 则需要；当前服务器已返回反归一化结果，可不填）
NORM_STATS_PATH = ""  # e.g. Path(__file__).parent / "biso102.json"
NORM_TYPE = "meanstd"

# ==================== RTC (Real-Time Chunking) 配置 ====================
# RTC 用于让机器人动作更平滑流畅，默认开启。如关闭则回退到传统固定阈值模式。
RTC_ENABLED = True
RTC_LOOKAHEAD_RATIO = 0.4           # 触发比例：剩余动作 <= 40% chunk 时触发下一次推理（越高越提前）
RTC_BLEND_STEPS = 5                 # chunk 重叠区渐进混合步数（0 = 关闭混合）
RTC_ACTION_EMA_ALPHA = 0.4          # 执行层 EMA 平滑因子（0=极平滑，1=无平滑）
RTC_SAFETY_MARGIN_STEPS = 2         # 安全余量步数
RTC_LATENCY_WINDOW = 5              # 推理延迟滑动窗口大小

# ==================== 相机配置 ====================
# 单前视相机配置示例（单臂场景）
# CAMERAS = (
#     f'{{front: {{type: opencv, index_or_path: {FRONT_CAM_ID}, width: 640, height: 480, fps: 30}}}}'
# )

# 双臂相机配置示例（顶置 + 左右手腕相机，参考 6_2_双臂数据采集.py）
CAMERAS = (
    f'{{observation.images.top: {{type: opencv, index_or_path: {FRONT_CAM_ID}, width: 640, height: 480, fps: 30}},'
    f' observation.images.left_wrist: {{type: opencv, index_or_path: {LEFT_WRIST_CAM_ID}, width: 640, height: 480, fps: 30}},'
    f' observation.images.right_wrist: {{type: opencv, index_or_path: {RIGHT_WRIST_CAM_ID}, width: 640, height: 480, fps: 30}}}}'
)
```

```Bash
# 运行lingbot-vla推理脚本
python lerobot_example\lingbot-vla推理.py
```