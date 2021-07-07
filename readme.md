# Readme
> 游戏AI训练代码运行指南

## 环境

- Windows 10
- python版本：3.8.8
- python模块： 参考文件`requirments.txt`
- 游戏：Hollow Knight《空洞骑士》
- 游戏mod：HP Bar mod(用于显示BOSS血量条，为小骑士的训练收敛提供帮助)，去除背景mod。使用的mod文件位于路径： `./hollow_knight_Data/`。将此模组复制到游戏文件夹下的mod文件夹即可。但我们已给游戏本体集成mod，使用我们提供的游戏本体无需执行该步骤。
- CUDA11.0 和cudnn7.5.0，用于tensorflow调用GPU。

## 使用说明

- 为方便训练，提供一个游戏存档，游戏位于： `/save/user3.dat` ，需将此文件复制到游戏的存档目录内，一般为`C:\user\_username_\AppData\LocalLow\Team Cherry\Hollow Knight`。
- 打开游戏，使用`shift+enter`将游戏窗口化并最大化，游戏内进入“选项-视频”，并将“分辨率”调整至“1920*1980@59HZ(@60Hz)”。
- 运行train.py函数进行训练，运行test.py函数进行测试。（运行代码前必须要求游戏已开启）
- 代码运行后，待python输出paused后，让Knight站在万神殿中BOSS"Hornet"(大黄蜂)雕像前。
- ![image-20210707101543613](C:\Users\Ne1H\AppData\Roaming\Typora\typora-user-images\image-20210707101543613.png)
- 按`F1`键开始训练，保持游戏画面位于最前，训练开始后，不要用键盘操控。若要停止训练，待本轮结束后，Knight退出boss界面，可按`F1`键暂停，也可停止python程序。


## 代码结构
- `train.py`包含主要的训练函数以及训练模型。
- `Agent.py` 控制输出Knight的动作。
- `DQN.py` 主要是深度强化学习算法。
- `Model.py` 给出模型的定义。
- `ReplayMemory.py` 用于记录和存储模型的经验池。
- `test.py` 用于测试模型。

- `./Tool` 路径下包含了以下一些功能性函数
  - `Actions` 定义小骑士的动作及自动进行新一轮训练。
  - `GetHp` 用于从内存中获取Knight和boss的血量和位置，小骑士现有的灵魂值。
  - `SendKey` 是一个API接口，用于将键盘上的指令输入到电脑中。
  - `WindowsAPI`用于截取游戏屏幕，其中的 `key_check()`函数用于调试时检测哪些键被敲击。
  - `Helper` 定义了reward函数以及其他功能函数。
