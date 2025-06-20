# 极域(jiyu)电子教室 UDP 重放攻击工具

[![GitHub stars](https://img.shields.io/github/stars/NULL11034/jiyufucker.svg?style=flat)](https://github.com/NULL11034/jiyufucker/stargazers)  
[![GitHub downloads](https://img.shields.io/github/downloads/NULL11034/jiyufucker/total.svg?style=flat)](https://github.com/NULL11034/jiyufucker/releases)

**版本：1.4**  
**作者：NULL11034**

## 概述

本工具基于 Python3 开发，利用 UDP 数据包重放漏洞实现对目标机器的远程命令执行与控制。工具最初针对极域电子教室的学生端漏洞开发，现已扩展出多项功能模块，支持：
- **消息发送与命令执行**：通过预设模板（-msg / -c）构造数据包，支持单条及批量命令执行。
- **内网扫描**：利用 UDP Ping 扫描指定网段内的在线主机，并以进度条方式实时显示扫描进度。
- **反弹 Shell**：构造反弹 shell 命令，使目标机器连接到攻击者预设的监听端口。
- **强制结束进程**：使用 NT API（NtTerminateProcess）实现对目标进程（如 StudentMain.exe）的强制终止。
- **磁盘共享**：让目标机器共享其本地磁盘（例如执行 `net share MyC=C:\ /grant:everyone,full`），并自动在本机打开共享目录。
- **解除锁定**：直接执行 `sc stop TDFileFilter` 和 `sc stop TDNetFilter` 命令，解除目标机器的文件、键盘、应用及网络锁定。
- **多网卡检测与进度显示**：自动检测本机所有私有 IP 所在的 /24 网段，并通过进度条显示操作状态。

> **注意**  
> 本工具仅供授权测试和研究用途，严禁用于非法攻击。使用该工具可能触犯法律，作者对由此引发的任何后果不承担责任。

## 功能模块

- **消息发送 / 命令执行**  
  - 使用 `-msg` 模块发送自定义消息。
  - 使用 `-c` 模块执行指定命令（例如 `calc.exe` 或 `cmd.exe /c ipconfig`）。
  - 支持批量命令执行，每行一条命令。

- **内网扫描**  
  - 输入目标网段（支持单个 IP、IP 范围及 /24 格式），扫描在线主机，并显示扫描进度。

- **反弹 Shell**  
  - 选择 `nc` 模块，工具会随机生成监听端口，并构造反弹 shell 命令。
  - 目标机器收到命令后会连接到攻击者预设的监听端口。

- **磁盘共享**  
  - 选择 `map` 模块，在“消息/命令内容”中输入共享参数，例如 `MyC=C:\`。
  - 目标机器执行命令后，将共享其 C 盘（共享名称为 MyC），并自动在本机打开共享目录（如 `\\目标IP\MyC`）。

- **解除锁定**  
  - 点击后执行接触命令命令，解除目标机器的锁定状态。

- **强制结束进程**  
  - 选择 `kill` 模块，利用 NT API 强制结束目标进程（如 StudentMain.exe）。

- **多网卡自动检测**  
  - 自动检测本机网卡并获取对应的 /24 网段，便于用户选择合适的网段进行操作。

## 使用方法

1. **配置目标**  
   在 `-ip` 输入框中填写目标机器的 IP 地址（例如 `192.168.1.101`）。

2. **设置端口**  
   在 `-p` 输入框中填写目标机器监听 UDP 数据包的端口（默认 `4705`）。

3. **选择操作模式**  
   - **消息发送 / 命令执行**：选择命令类型（`-msg` 或 `-c`）并在消息/命令内容中输入相应内容。
   - **批量命令**：勾选“批量命令执行”，每行输入一条命令。
   - **磁盘共享**：选择额外选项 `map`，在消息/命令内容中输入共享参数（例如 `MyC=C:\`），目标机器将共享其 C 盘，随后自动打开 UNC 路径 `\\192.168.1.101\MyC`。
   - **解除锁定**：点击“解除锁定”大按钮，目标机器将停止相关锁定服务。
   - **反弹 Shell**、**强制结束进程**：分别选择 `nc` 和 `kill` 模块。

4. **执行操作**  
   点击“开始执行”按钮，程序将构造 UDP 数据包并发送至目标机器，根据选定的模块执行相应操作。

5. **查看结果**  
   - 操作日志会在界面下方显示操作过程和结果。
   - 若为磁盘共享操作，程序在发送完共享命令后会自动打开目标机器的共享目录。

## 环境要求

- Windows 操作系统  
- Python 3.x  
- 依赖模块：  
  - pywin32  
  - PyQt6

## 安全与免责声明

本工具仅供授权测试和研究使用，严禁用于非法攻击。使用本工具攻击或未经授权控制他人计算机属于违法行为。作者对使用该工具造成的任何后果概不负责。请在合法环境下进行测试。


## 🚫 项目状态 / Project Status

### 🇨🇳 中文说明：
本项目已进入归档状态。由于受到某些个人（尤其是袁白痴）的恶意干扰与陷害，开发工作无法继续推进。为了避免更大的误解和麻烦，决定暂停维护，归档处理。

项目的全部代码和成果仍将保留供学习与参考，若将来时机成熟，不排除重新启动的可能。

### 🇬🇧 English Notice:
This project has been archived. Due to targeted sabotage and malicious interference from certain individuals (notably "Yuan Idiot"), active development has been halted.

### ⚠️ 附加声明 / Additional Statement

### 🇨🇳 中文：
所谓的“袁白痴”本名疑似为“袁继平”。鉴于其恶意行为已对项目造成实质性破坏，特此声明，以正视听。希望所有开发者警惕此人，并保护自己的创作空间不受无端干扰。

本声明仅为事件记录，不构成对其人身攻击，亦欢迎其自行澄清。

### 🇬🇧 English:
The individual referred to as “Yuan Idiot” is believed to be Yuan Jiping. Due to their malicious actions which directly damaged the project, this statement is made to clarify the situation.

This is a factual record of events, not a personal attack. The individual is welcome to clarify their position if desired.

To avoid further misunderstanding and trouble, the project is now suspended and archived. All code and past work will remain accessible for learning and reference purposes. A restart may be considered in the future.
