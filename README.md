# High-Speed SDR Receiver v1.0

A high-performance SDR signal reception and acquisition system based on GNU Radio and HackRF, supporting real-time spectrum display, waveform analysis, and automatic data saving.

## 📋 Project Introduction

This project is a professional SDR (Software Defined Radio) signal reception platform specifically designed for high-speed signal acquisition and encrypted communication analysis. The system integrates SDR hardware control, real-time signal processing, serial communication, and data management functions, particularly suitable for side-channel attack and encryption algorithm signal acquisition scenarios.

**Executable File**: `High-Speed SDR Receiver v1.0.exe`

### Key Features

- 🎛️ **Complete SDR Device Control**: Supports automatic detection, parameter configuration, and real-time control of HackRF One devices
- 📊 **Real-time Signal Analysis**: Professional signal visualization tools including spectrum analysis, time-domain waveforms, IQ constellation diagrams
- 🔄 **Intelligent Trigger System**: Configurable threshold triggering, pre-trigger and post-trigger windows
- 📡 **Serial Communication Integration**: Supports communication with external encryption devices, automatic signal acquisition synchronization
- 💾 **Intelligent Data Management**: Automatically saves IQ data, trigger signals, and parameters, supporting multiple formats (.npy, .trs, .txt)
- 🎨 **Modern Interface**: Dark theme, professional PyQtGraph graphics display

## 🚀 System Requirements

### Hardware Requirements

- HackRF One SDR device (or other osmosdr-compatible devices)
- Computer (recommended 8GB+ RAM, USB 3.0 support)
- Target encryption device (for serial communication)

### Software Requirements

- Windows 7/8/10/11 (64-bit system)
- No Python environment required (packaged as standalone EXE)

## 📦 Installation Guide

### Using the Packaged EXE

1. **Download and extract the package**
   - Obtain the `High-Speed SDR Receiver v1.0.exe` executable file
   - Extract to any directory (English path recommended)
2. **Install HackRF drivers**

   **Windows System**:

   Please follow these steps to install the HackRF toolkit:
   1. Download `hackrf-YYYY.MM.PLATFORM.zip` from the [HackRF official release page](https://github.com/greatscottgadgets/hackrf/releases)
   2. Extract and place the following files in the program directory or system PATH environment variable:
      - `hackrf_info.exe`
      - `libusb-1.0.dll`
      - `hackrf.dll`
   3. Alternatively, install the complete HackRF environment (recommended to use Zadig to install drivers)
   **Detailed driver installation steps**:
   - Download [Zadig](https://zadig.akeo.ie/)
   - Connect the HackRF device
   - Open Zadig, select "HackRF" device
   - Install libusb driver
3. **Run the program**
   - Double-click `High-Speed SDR Receiver v1.0.exe` to start the program
   - The configuration file `sdr_receiver_settings.json` will be automatically generated in the program directory on first run

### HackRF Installation Instructions for Different Systems

#### Windows System

Follow these steps to install the HackRF toolkit:

1. Download `hackrf-YYYY.MM.PLATFORM.zip` from the [HackRF official release page](https://github.com/greatscottgadgets/hackrf/releases)
2. Extract and place `hackrf_info.exe` in one of the following locations:
   - Program directory (same directory as EXE)
   - Directory in system PATH environment variable
3. Or install the complete HackRF environment

#### Ubuntu/Debian System

```bash
sudo apt-get update
sudo apt-get install hackrf libhackrf-dev
```

#### Fedora System

```bash
sudo dnf install hackrf hackrf-devel
```

#### Arch Linux System

```bash
sudo pacman -S hackrf
```

#### macOS System

```bash
brew install hackrf
```

### Verification

Open the command line and run the following command to verify if HackRF tools are installed correctly:

```bash
# Windows
hackrf_info.exe

# Linux/macOS
hackrf_info
```

If HackRF device information is displayed, the installation is successful.

## 🔧 Usage Instructions

### 1. Start the Program

Double-click `High-Speed SDR Receiver v1.0.exe` to start the program.

### 2. Device Connection

#### Connect HackRF Device

1. Connect HackRF One to the computer via USB
2. Wait for the driver to install automatically (Zadig may be needed for first use)
3. Click "🔍 Detect SDR Device" in the program to detect the device
4. After confirming the device is detected, click "Open SDR Device" to open the device

#### Connect Serial Device

1. Connect the target device to the computer via serial port
2. Select the correct serial port number and baud rate in the program
3. Click "Open Serial Port" to open the serial port
4. The status bar will show the connection status

### 3. Parameter Configuration

#### SDR Parameter Settings

- **Frequency**: Set center frequency (MHz), range 1-6000 MHz
- **Sample Rate**: 2/5/10/20 MS/s selectable, affects data volume and processing load
- **Bandwidth**: 1/2/5/10/20 MHz selectable, recommended to match sample rate
- **Gain Control**:
  - RF Gain: 0-40 dB, controls RF front-end gain
  - IF Gain: 0-40 dB, controls intermediate frequency gain
  - BB Gain: 0-62 dB, controls baseband gain

#### Trigger Settings

- **Threshold**: Trigger amplitude threshold (0.01-10.0), adjust based on signal strength
- **Minimum Interval**: Minimum time interval between two triggers (milliseconds), avoid duplicate triggers
- **Trigger Window**:
  - Pre-trigger: Number of samples before trigger
  - Post-trigger: Number of samples after trigger

#### Serial Data Configuration

- **Plaintext Bytes**: Set the byte length of plaintext data (default 16 bytes)
- **Key Bytes**: Set the byte length of the key (default 16 bytes)
- **Fixed Byte Positions**: Specify byte positions in plaintext that need to be fixed (space-separated)
- **Random Mode**:
  - Check "Random" to enable random plaintext/key generation
  - In random mode, fixed position values remain unchanged

### 4. Data Acquisition Process

#### Basic Operation Flow

1. **Start Reception**: Click "Start Reception" to begin SDR signal reception
2. **Configure Data**: Configure test data in the serial control area
   - Input plaintext (hexadecimal)
   - Input key (hexadecimal)
   - Optionally enable random mode or full injection mode
3. **Send Data**: Click "Send Data" to send data to the target device
4. **Automatic Acquisition**: The system automatically detects trigger signals and saves data

#### Acquisition Modes

- **Single Acquisition**: Set acquisition count to 1, send once and acquire once
- **Batch Acquisition**: Set acquisition count > 1, automatically cycle sending and acquisition
- **Random Mode**: Automatically generate random plaintext/key before each send

### 5. Data Saving

#### Save Options

- **Save Raw IQ Data (.npy)**: Save raw IQ data for subsequent analysis
- **Save Trigger Data (.trs)**: Save trigger signal data, compatible with TRACE format
- **Save Serial Parameters (.txt)**: Save parameter metadata, including plaintext, key, etc.

#### File Naming Convention

All data files use a unified naming convention for easy data association:

```
{session_id}_{counter:06d}_{type}.extension

Example:
20250115_143025_000001_iq.npy          # IQ data
20250115_143025_000001_trigger.trs      # Trigger data
20250115_143025_000001_params.txt       # Parameter file
```

#### File Format Description

- **.npy file**: numpy binary format, contains raw IQ data (complex64 type)
- **.trs file**: TRACE format, contains signal waveform and parameter information
- **.txt file**: Text format, contains complete acquisition parameters and metadata

## 📊 Detailed Functional Modules

### SDR Device Control Module

- **Automatic Detection**: Detects connected HackRF devices through hackrf\_info tool
- **Device Management**: Supports device opening, closing, and status monitoring
- **Parameter Configuration**: Dynamically configures sample rate, frequency, gain, etc.
- **Error Handling**: Comprehensive exception handling and error prompts

### Signal Processing Module

- **Circular Buffer**: Optimized ring buffer design, supports high-throughput data streams
  - Dynamically calculates buffer size
  - Prevents data overflow
  - Supports multiple trigger event storage
- **Intelligent Trigger Detection**: Threshold-based trigger detection algorithm
  - Configurable trigger threshold
  - Minimum trigger interval control
  - Pre-trigger and post-trigger windows
- **Real-time Processing**: GNU Radio flow processing architecture, low-latency data processing

### Serial Communication Module

- **Multi-threaded Architecture**: Independent serial communication thread, does not block UI
- **Data Sending**:
  - Supports hexadecimal data format
  - Full injection mode (key + plaintext)
  - Random data generation
- **Data Receiving**:
  - Automatically reads response data
  - Data integrity check
  - Timeout handling mechanism
- **Trigger Synchronization**: Records send timestamps,关联 with SDR trigger events

### Data Management Module

- **Session Management**: Each running instance generates a unique session ID
- **Automatic Saving**: Trigger events automatically save related data
- **Association Tracking**: Records send-trigger correspondence
- **Statistics**: Real-time statistics of trigger success rate and response time

### Visualization Module

- **Spectrum Display**: Real-time FFT spectrum analysis
- **Time-domain Waveform**: I/Q channel separated display
- **IQ Constellation**: Signal modulation quality analysis
- **Trigger Data Display**: Detailed trigger waveform analysis

## 🎯 Application Scenarios

### RF Side-channel Analysis

Acquires RF leakage information during encryption device operation, used for RF side-channel security verification of nRF series Bluetooth chips

## ⚙️ Advanced Configuration

### Trigger Tracking Mechanism

The system implements a complete trigger-send association mechanism:

```python
# Trigger tracker structure
trigger_tracker = {
    'last_trigger_index': -1,        # Last trigger index
    'last_sample_index': -1,         # Last sample index
    'serial_send_counter': 0,        # Serial send counter
    'trigger_received_counter': 0,   # Trigger received counter
    'missed_triggers': 0,            # Missed trigger counter
    'trigger_map': {}                # Send-trigger mapping table
}
```

Workflow:

1. Record timestamp and data each time serial data is sent
2. Match SDR trigger events with the most recent send event
3. If successfully matched, save data and record response time
4. Provide detailed statistical reports

### Fixed Byte Positions

Supports fixing specific byte position values in random plaintext mode:

```python
# Example: Fix values at positions 0, 1, 2
Fixed positions input: 0 1 2

# Example of generated random plaintext
Fixed positions: 0: 00, 1: 01, 2: 02
Other positions: Randomly generated
Result: 00 01 02 3F 7A 8C ...
```

Uses:

- Data synchronization header
- Format verification
- Specific pattern testing

### Buffer Optimization

The system dynamically calculates buffer size based on the following factors:

- Sample rate and time window
- Trigger window size
- Minimum trigger interval
- System memory limit

```python
buffer_size = max(
    sample_rate * buffer_duration_ms / 1000,  # Time continuity requirement
    total_trigger * 10,                        # Trigger integrity requirement
    sample_rate * min_interval / 1000 * 2,     # Interval safety requirement
    1024 * 1024                                # Minimum guarantee requirement
)
```

## 🛠️ Troubleshooting

### Common Issues and Solutions

#### 1. Program Fails to Start or Crashes

**Symptoms**: No response or immediate closure after double-clicking EXE

**Solutions**:

- Check for missing necessary runtime libraries (Visual C++ Redistributable)
- Try running as administrator
- Check if error logs are generated in the program directory
- Ensure the path does not contain Chinese characters

#### 2. Cannot Detect HackRF Device

**Symptoms**: Clicking "Detect SDR Device" shows "Device not detected"

**Solutions**:

- Check if the USB cable is securely connected
- Confirm if the HackRF device indicator is lit
- Reinstall libusb driver using Zadig
- Place `hackrf_info.exe` in the same directory as the program
- Restart the computer and try again
- Open command line and run `hackrf_info.exe` to check if the device can be detected

#### 3. Serial Communication Failure

**Symptoms**: No response or timeout after clicking "Send Data"

**Solutions**:

- Confirm the serial device is not occupied by other programs (e.g., serial debug assistants)
- Check if baud rate, data bits, stop bits, etc. match the target device
- Verify serial cable connection is normal
- Try using a serial debug tool to test communication
- Check if the target device is powered on and running normally

#### 4. Program Runs Slowly or Lags

**Symptoms**: Slow interface response, high CPU usage

**Solutions**:

- Reduce sample rate (from 20 MS/s to 10 or 5 MS/s)
- Close unnecessary display tabs
- Reduce trigger window size
- Check if too many save options are enabled
- Ensure the computer meets minimum system requirements

#### 5. Signal Cannot Trigger

**Symptoms**: SDR reception runs normally, but no trigger events

**Solutions**:

- Adjust trigger threshold: lower threshold to increase sensitivity
- Check signal strength: check spectrum to confirm signal presence
- Adjust gain settings: appropriately increase RF/IF/BB gain
- Confirm frequency setting is correct
- Check antenna connection

#### 6. Data Saving Failure

**Symptoms**: Trigger events occur but data is not saved

**Solutions**:

- Confirm the save directory exists and has write permissions
- Check if disk space is sufficient
- Verify data save options are checked
- Check error messages in the log window
- Try running the program as administrator

### Performance Optimization Recommendations

#### CPU Load Optimization

- Reduce sample rate: from 20 MS/s to 10 or 5 MS/s
- Decrease FFT size: modify FFT points in code
- Reduce display refresh rate: adjust timer interval
- Close unnecessary display tabs

#### Disk I/O Optimization

- Use SSD for data storage
- Batch write data
- Regularly archive historical data

## 📄 Configuration File Description

`sdr_receiver_settings.json` contains all user configurations, automatically created on first run:

```json
{
  "frequency": 2529,
  "sample_rate": "10 MS/s",
  "bandwidth": "5 MHz",
  "rf_gain": 0,
  "if_gain": 36,
  "bb_gain": 35,
  "threshold": 0.7,
  "interval": 1.0,
  "pre_trigger": 18000,
  "post_trigger": 2000,
  "save_path": "./data",
  "save_raw": true,
  "save_trigger": true,
  "save_params": true,
  "serial_data": "00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F",
  "key": "01 23 45 67 89 ab cd ef fe dc ba 98 76 54 32 10",
  "ciphertext": "",
  "serial_port": "COM3",
  "baudrate": "115200",
  "plaintext_bytes": "16"
}
```

### Configuration Item Description

| Configuration Item | Type   | Description                   | Value Range          |
| ------------------ | ------ | ----------------------------- | -------------------- |
| frequency          | float  | Center frequency (MHz)        | 1-6000               |
| sample\_rate       | string | Sample rate                   | "2/5/10/20 MS/s"     |
| bandwidth          | string | Bandwidth                     | "1/2/5/10/20 MHz"    |
| rf\_gain           | int    | RF gain                       | 0-40                 |
| if\_gain           | int    | IF gain                       | 0-40                 |
| bb\_gain           | int    | BB gain                       | 0-62                 |
| threshold          | float  | Trigger threshold             | 0.01-10.0            |
| interval           | float  | Minimum trigger interval (ms) | 0.1-1000.0           |
| pre\_trigger       | int    | Pre-trigger samples           | 1000-50000           |
| post\_trigger      | int    | Post-trigger samples          | 1000-50000           |
| save\_path         | string | Save path                     | Valid directory path |
| plaintext\_bytes   | string | Plaintext bytes               | Any integer          |

## 🔒 Security Considerations

### Legal Compliance

- This software is for legal purposes only, not for illegal monitoring or signal interference
- Comply with local radio regulations, do not transmit signals in prohibited frequency bands
- Respect others' privacy, only collect signals from authorized devices

### Data Security

- Properly store collected data files, especially information containing keys
- Regularly clean up unnecessary data
- Encrypt sensitive data storage
- Use secure file transfer methods

### Operational Safety

- Pay attention to device heat dissipation, avoid long-term high-load operation
- Use appropriate power supply, avoid device damage due to unstable voltage
- Be careful when connecting antennas, avoid short circuits
- Pay attention to electrostatic protection during operation

## 📝 Changelog

### v1.0 (2026-03)

- Initial version release
- Complete HackRF device support
- Serial communication integration
- Automatic data saving functionality
- Real-time signal visualization
- Trigger tracking mechanism
- Random data generation
- Fixed byte position support
- Packaged as standalone EXE file

## 📧 Contact

- Email: <caijuesong@163.com>

## ⚖️ License

This project is for learning and research purposes only, without any express or implied warranty.

***

**Disclaimer**:

- This software is for educational and research purposes only
- Users assume all risks of use
- Ensure compliance with all applicable laws and regulations
- The author is not responsible for any losses caused by the use of this software

***

**Acknowledgements**:

- GNU Radio team for the powerful framework
- Great Scott Gadgets for HackRF hardware
- PyQt and pyqtgraph development communities

**Last Updated**: March 2026

# TRS File Generation and Processing Tool

## Overview

This tool is designed to process IQ data files and parameter files to generate TRS (Trace Set) files, merge multiple TRS files, and create average traces for side-channel analysis. It supports various signal types and provides a user-friendly interface for selecting different operation modes.

## Features

- **Generate TRS files from IQ data**: Convert raw IQ data (.npy files) and parameter files (.txt) into TRS files
- **Signal type selection**: Choose between In-phase (I), Quadrature (Q), or Amplitude signals
- **Parameter file processing**: Extract parameters (Plaintext, Key, Ciphertext) from text files and embed them into TRS files
- **Merge TRS files**: Combine multiple TRS files into a single merged file
- **Average trace generation**: Create average traces from multiple TRS files to improve signal-to-noise ratio

## Dependencies

- Python 3.x
- NumPy
- trsfile
- tqdm
- matplotlib
- csv\_to\_trs (custom module)
- trs\_loader (custom module)

## Usage

### Running the Tool

Execute the script to start the interactive interface:

```bash
python getfinaltrs_zh.py
```

### Operation Modes

1. **Generate TRS from IQ data and parameter files**
   - Select signal type (I, Q, or Amplitude)
   - Processes .npy IQ files and .txt parameter files to create TRS files
2. **Fill existing TRS files with parameters**
   - Reads existing TRS files and embeds parameters from .txt files
3. **Merge multiple TRS files**
   - Validates TRS files based on parameter length requirements
   - Merges valid files into a single TRS file
   - Optionally generates an average trace file
4. **Execute all operations**
   - Runs all modes sequentially

### Input File Requirements

#### Parameter Files (.txt)

Parameter files should contain the following information:

```
session_id = YYYYMMDD_HHMMSS
save_counter = 000000
plaintext = <hex_string>
key = <hex_string>
ciphertext = <hex_string>
```

#### IQ Files (.npy)

IQ files should be complex numpy arrays stored in .npy format. The expected naming convention is:

```
{session_id}_{counter:06d}_iq.npy
```

### Output

- **TRS files from IQ data**: Saved in subdirectories based on signal type (`trs_from_iq_amplitude`, `trs_from_iq_I`, `trs_from_iq_Q`)
- **TRS files with parameters**: Saved in the `with_params` directory
- **Merged TRS files**: Saved in the `merged` directory
- **Average trace files**: Saved in the `merged` directory with `average_` prefix

## Example Workflow

1. **Prepare input files**:
   - Place IQ files (.npy) and parameter files (.txt) in the same directory
2. **Run the tool**:
   - Select mode 1 to generate TRS files from IQ data
   - Select signal type (e.g., Amplitude)
   - The tool will process files and create TRS files in the appropriate subdirectory
3. **Merge TRS files**:
   - Select mode 3
   - Set parameter length requirements (e.g., AES-128: Plaintext=16, Key=16, Ciphertext=16)
   - Choose to generate an average trace if needed
   - The tool will merge valid files and save the result

## Notes

- Ensure all dependencies are installed before running the tool
- Parameter files must be properly formatted with hex strings for Plaintext, Key, and Ciphertext
- IQ files should be complex numpy arrays to ensure correct signal processing
- The tool performs validation checks to ensure TRS files meet specified parameter length requirements

## Troubleshooting

- **File not found errors**: Verify input file paths and naming conventions
- **Parameter validation failures**: Check that parameter files contain all required fields with correct hex formatting
- **TRS file opening errors**: Ensure trs\_loader and csv\_to\_trs modules are correctly installed



# High-Speed SDR Receiver v1.0

一个基于GNU Radio和HackRF的高性能SDR信号接收与采集系统，支持实时频谱显示、波形分析和自动数据保存。

## 📋 项目简介

本项目是一个专业的SDR（软件定义无线电）信号接收平台，专门设计用于高速信号采集和加密通信分析。系统集成了SDR硬件控制、实时信号处理、串口通信和数据管理功能，特别适用于侧信道攻击和加密算法的信号采集场景。

**可执行文件**：`High-Speed SDR Receiver v1.0.exe`

### 主要特性

- 🎛️ **完整的SDR设备控制**：支持HackRF One设备的自动检测、参数配置和实时控制
- 📊 **实时信号分析**：频谱分析、时域波形、IQ星座图等专业信号可视化工具
- 🔄 **智能触发系统**：可配置的阈值触发、预触发和后触发窗口
- 📡 **串口通信集成**：支持与外部加密设备通信，自动同步信号采集
- 💾 **智能数据管理**：自动保存IQ数据、触发信号和参数，支持多种格式（.npy, .trs, .txt）
- 🎨 **现代化界面**：深色主题，专业的PyQtGraph图形显示

## 🚀 系统要求

### 硬件要求

- HackRF One SDR设备（或其他兼容osmosdr的设备）
- 计算机（建议8GB以上内存，支持USB 3.0）
- 目标加密设备（用于串口通信）

### 软件要求

- Windows 7/8/10/11（64位系统）
- 无需安装Python环境（已打包为独立EXE）

## 📦 安装指南

### 直接使用打包好的EXE

1. **下载并解压程序包**
   - 获取 `High-Speed SDR Receiver v1.0.exe` 可执行文件
   - 解压到任意目录（建议英文路径）
2. **安装HackRF驱动**

   **Windows系统**：

   请按照以下步骤安装HackRF工具包：
   1. 从 [HackRF官方发布页面](https://github.com/greatscottgadgets/hackrf/releases) 下载 `hackrf-YYYY.MM.PLATFORM.zip`
   2. 解压并将以下文件放置到程序所在目录或系统PATH环境变量中：
      - `hackrf_info.exe`
      - `libusb-1.0.dll`
      - `hackrf.dll`
   3. 或者安装完整的HackRF环境（推荐使用Zadig安装驱动）
   **驱动安装详细步骤**：
   - 下载 [Zadig](https://zadig.akeo.ie/)
   - 连接HackRF设备
   - 打开Zadig，选择"HackRF"设备
   - 安装libusb驱动
3. **运行程序**
   - 双击 `High-Speed SDR Receiver v1.0.exe` 启动程序
   - 首次运行会在程序目录自动生成配置文件 `sdr_receiver_settings.json`

### 各系统HackRF安装说明

#### Windows系统

请按照以下步骤安装HackRF工具包：

1. 从 [HackRF官方发布页面](https://github.com/greatscottgadgets/hackrf/releases) 下载 `hackrf-YYYY.MM.PLATFORM.zip`
2. 解压并将 `hackrf_info.exe` 放置到以下位置之一：
   - 程序所在目录（与EXE同目录）
   - 系统PATH环境变量中的目录
3. 或者安装完整的HackRF环境

#### Ubuntu/Debian系统

```bash
sudo apt-get update
sudo apt-get install hackrf libhackrf-dev
```

#### Fedora系统

```bash
sudo dnf install hackrf hackrf-devel
```

#### Arch Linux系统

```bash
sudo pacman -S hackrf
```

#### macOS系统

```bash
brew install hackrf
```

### 验证安装

打开命令行，运行以下命令验证HackRF工具是否正确安装：

```bash
# Windows
hackrf_info.exe

# Linux/macOS
hackrf_info
```

如果显示HackRF设备信息，则表示安装成功。

## 🔧 使用说明

### 1. 启动程序

双击 `High-Speed SDR Receiver v1.0.exe` 启动程序。

### 2. 设备连接

#### 连接HackRF设备

1. 通过USB连接HackRF One到计算机
2. 等待驱动程序自动安装（首次使用可能需要Zadig安装驱动）
3. 点击程序中的"🔍 Detect SDR Device"检测设备
4. 确认检测到设备后，点击"Open SDR Device"打开设备

#### 连接串口设备

1. 将目标设备通过串口连接到计算机
2. 在程序中选择正确的串口号和波特率
3. 点击"Open Serial Port"打开串口
4. 状态栏会显示连接状态

### 3. 参数配置

#### SDR参数设置

- **频率**：设置中心频率（MHz），范围1-6000 MHz
- **采样率**：2/5/10/20 MS/s可选，影响数据量和处理负载
- **带宽**：1/2/5/10/20 MHz可选，建议与采样率匹配
- **增益控制**：
  - RF增益：0-40 dB，控制射频前端增益
  - IF增益：0-40 dB，控制中频增益
  - BB增益：0-62 dB，控制基带增益

#### 触发设置

- **阈值**：触发幅度阈值（0.01-10.0），根据信号强度调整
- **最小间隔**：两次触发的最小时间间隔（毫秒），避免重复触发
- **触发窗口**：
  - 预触发：触发前的采样点数
  - 后触发：触发后的采样点数

#### 串口数据配置

- **明文字节数**：设置明文数据的字节长度（默认16字节）
- **密钥字节数**：设置密钥的字节长度（默认16字节）
- **固定字节位置**：指定明文中需要固定的字节位置（空格分隔）
- **随机模式**：
  - 勾选"Random"可启用随机明文/密钥生成
  - 随机模式下，固定位置的值保持不变

### 4. 数据采集流程

#### 基本操作流程

1. **启动接收**：点击"Start Reception"开始SDR信号接收
2. **配置数据**：在串口控制区配置测试数据
   - 输入明文（十六进制）
   - 输入密钥（十六进制）
   - 可选开启随机模式或全注入模式
3. **发送数据**：点击"Send Data"发送数据到目标设备
4. **自动采集**：系统自动检测触发信号并保存数据

#### 采集模式

- **单次采集**：设置采集次数为1，发送一次数据采集一次
- **批量采集**：设置采集次数>1，自动循环发送和采集
- **随机模式**：每次发送前自动生成随机明文/密钥

### 5. 数据保存

#### 保存选项

- **Save Raw IQ Data (.npy)**：保存原始IQ数据，用于后续分析
- **Save Trigger Data (.trs)**：保存触发信号数据，兼容TRACE格式
- **Save Serial Parameters (.txt)**：保存参数元数据，包含明文、密钥等信息

#### 文件命名规则

所有数据文件采用统一的命名规范，便于数据关联：

```
{session_id}_{counter:06d}_{type}.extension

示例：
20250115_143025_000001_iq.npy          # IQ数据
20250115_143025_000001_trigger.trs      # 触发数据
20250115_143025_000001_params.txt       # 参数文件
```

#### 文件格式说明

- **.npy文件**：numpy二进制格式，包含原始IQ数据（complex64类型）
- **.trs文件**：TRACE格式，包含信号波形和参数信息
- **.txt文件**：文本格式，包含完整的采集参数和元数据

## 📊 功能模块详解

### SDR设备控制模块

- **自动检测**：通过hackrf\_info工具检测连接的HackRF设备
- **设备管理**：支持设备的打开、关闭和状态监控
- **参数配置**：动态配置采样率、频率、增益等参数
- **错误处理**：完善的异常处理和错误提示

### 信号处理模块

- **循环缓冲区**：优化的环形缓冲区设计，支持高吞吐量数据流
  - 动态计算缓冲区大小
  - 防止数据溢出
  - 支持多触发事件存储
- **智能触发检测**：基于阈值的触发检测算法
  - 可配置触发阈值
  - 最小触发间隔控制
  - 预触发和后触发窗口
- **实时处理**：GNU Radio流处理架构，低延迟数据处理

### 串口通信模块

- **多线程架构**：独立的串口通信线程，不阻塞UI
- **数据发送**：
  - 支持十六进制数据格式
  - 全注入模式（密钥+明文）
  - 随机数据生成
- **数据接收**：
  - 自动读取响应数据
  - 数据完整性检查
  - 超时处理机制
- **触发同步**：记录发送时间戳，与SDR触发事件关联

### 数据管理模块

- **会话管理**：每个运行实例生成唯一会话ID
- **自动保存**：触发事件自动保存相关数据
- **关联追踪**：记录发送-触发对应关系
- **统计信息**：实时统计触发成功率和响应时间

### 可视化模块

- **频谱显示**：实时FFT频谱分析
- **时域波形**：I/Q通道分离显示
- **IQ星座图**：信号调制质量分析
- **触发数据显示**：详细的触发波形分析

## 🎯 应用场景

### 射频侧信道分析

采集加密设备运行时的射频泄露信息，用于nRF系列蓝牙芯片的射频侧信道安全验证

## ⚙️ 高级配置

### 触发追踪机制

系统实现了完整的触发-发送关联机制：

```python
# 触发追踪器结构
trigger_tracker = {
    'last_trigger_index': -1,        # 最后触发索引
    'last_sample_index': -1,         # 最后采样索引
    'serial_send_counter': 0,        # 串口发送计数
    'trigger_received_counter': 0,   # 触发接收计数
    'missed_triggers': 0,            # 丢失触发计数
    'trigger_map': {}                # 发送-触发映射表
}
```

工作流程：

1. 每次串口发送时记录时间戳和数据
2. SDR触发事件发生时与最近的发送事件匹配
3. 成功匹配则保存数据，并记录响应时间
4. 提供详细的统计报告

### 固定字节位置

支持在随机明文模式中固定特定字节位置的值：

```python
# 示例：固定位置0、1、2的值
固定位置输入：0 1 2

# 生成的随机明文示例
固定位置: 0: 00, 1: 01, 2: 02
其他位置: 随机生成
结果: 00 01 02 3F 7A 8C ...
```

用途：

- 数据同步头
- 格式验证
- 特定模式测试

### 缓冲区优化

系统根据以下因素动态计算缓冲区大小：

- 采样率和时间窗口
- 触发窗口大小
- 最小触发间隔
- 系统内存限制

```python
buffer_size = max(
    sample_rate * buffer_duration_ms / 1000,  # 时间连续性要求
    total_trigger * 10,                        # 触发完整性要求
    sample_rate * min_interval / 1000 * 2,     # 间隔安全要求
    1024 * 1024                                # 最小保证要求
)
```

## 🛠️ 故障排除

### 常见问题及解决方案

#### 1. 程序无法启动或闪退

**症状**：双击EXE后无反应或立即关闭

**解决方案**：

- 检查是否缺少必要的运行库（Visual C++ Redistributable）
- 尝试以管理员身份运行
- 查看程序目录下是否生成错误日志
- 确保路径中不含中文字符

#### 2. 无法检测HackRF设备

**症状**：点击"Detect SDR Device"后显示"Device not detected"

**解决方案**：

- 检查USB连接线是否牢固
- 确认HackRF设备指示灯是否亮起
- 使用Zadig重新安装libusb驱动
- 将`hackrf_info.exe`放在程序同目录下
- 重启计算机后重试
- 打开命令行运行 `hackrf_info.exe` 检查是否能检测到设备

#### 3. 串口通信失败

**症状**：点击"Send Data"后没有响应或超时

**解决方案**：

- 确认串口设备未被其他程序（如串口调试助手）占用
- 检查波特率、数据位、停止位等参数是否与目标设备匹配
- 验证串口线缆连接是否正常
- 尝试使用串口调试工具测试通信
- 检查目标设备是否上电并正常运行

#### 4. 程序运行缓慢或卡顿

**症状**：界面响应慢，CPU占用高

**解决方案**：

- 降低采样率（从20 MS/s降低到10或5 MS/s）
- 关闭不需要的显示选项卡
- 减少触发窗口大小
- 检查是否开启了过多的保存选项
- 确保计算机满足最低系统要求

#### 5. 信号无法触发

**症状**：SDR接收运行正常，但没有触发事件

**解决方案**：

- 调整触发阈值：降低阈值提高灵敏度
- 检查信号强度：查看频谱图确认是否有信号
- 调整增益设置：适当增加RF/IF/BB增益
- 确认频率设置正确
- 检查天线连接

#### 6. 数据保存失败

**症状**：触发事件出现但数据没有保存

**解决方案**：

- 确认保存目录存在且有写入权限
- 检查磁盘空间是否充足
- 验证数据保存选项是否勾选
- 查看日志窗口的错误信息
- 尝试以管理员身份运行程序

### 性能优化建议

#### CPU负载优化

- 降低采样率：从20 MS/s降低到10或5 MS/s
- 减小FFT大小：修改代码中的FFT点数
- 降低显示刷新率：调整定时器间隔
- 关闭不需要的显示选项卡

#### 磁盘I/O优化

- 使用SSD存储数据
- 批量写入数据
- 定期归档历史数据

## 📄 配置文件说明

`sdr_receiver_settings.json` 包含所有用户配置，首次运行自动创建：

```json
{
  "frequency": 2529,
  "sample_rate": "10 MS/s",
  "bandwidth": "5 MHz",
  "rf_gain": 0,
  "if_gain": 36,
  "bb_gain": 35,
  "threshold": 0.7,
  "interval": 1.0,
  "pre_trigger": 18000,
  "post_trigger": 2000,
  "save_path": "./data",
  "save_raw": true,
  "save_trigger": true,
  "save_params": true,
  "serial_data": "00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F",
  "key": "01 23 45 67 89 ab cd ef fe dc ba 98 76 54 32 10",
  "ciphertext": "",
  "serial_port": "COM3",
  "baudrate": "115200",
  "plaintext_bytes": "16"
}
```

### 配置项说明

| 配置项              | 类型     | 说明         | 取值范围              |
| ---------------- | ------ | ---------- | ----------------- |
| frequency        | float  | 中心频率（MHz）  | 1-6000            |
| sample\_rate     | string | 采样率        | "2/5/10/20 MS/s"  |
| bandwidth        | string | 带宽         | "1/2/5/10/20 MHz" |
| rf\_gain         | int    | RF增益       | 0-40              |
| if\_gain         | int    | IF增益       | 0-40              |
| bb\_gain         | int    | BB增益       | 0-62              |
| threshold        | float  | 触发阈值       | 0.01-10.0         |
| interval         | float  | 最小触发间隔（ms） | 0.1-1000.0        |
| pre\_trigger     | int    | 预触发采样数     | 1000-50000        |
| post\_trigger    | int    | 后触发采样数     | 1000-50000        |
| save\_path       | string | 保存路径       | 有效目录路径            |
| plaintext\_bytes | string | 明文字节数      | 任意整数              |

## 🔒 安全注意事项

### 法律合规

- 本软件仅用于合法用途，不得用于非法监听或信号干扰
- 遵守当地无线电管理法规，不得在禁止频段发射信号
- 尊重他人隐私，仅采集授权设备的信号

### 数据安全

- 妥善保管采集的数据文件，特别是包含密钥的信息
- 定期清理不需要的数据
- 对敏感数据进行加密存储
- 使用安全的文件传输方式

### 操作安全

- 注意设备散热，避免长时间高负载运行
- 使用合适的电源，避免电压不稳导致设备损坏
- 天线连接时要小心，避免短路
- 操作时注意静电防护

## 📝 更新日志

### v1.0 (2026-03)

- 初始版本发布
- 完整HackRF设备支持
- 串口通信集成
- 自动数据保存功能
- 实时信号可视化
- 触发追踪机制
- 随机数据生成
- 固定字节位置支持
- 打包为独立EXE文件

## 📧 联系方式

- 电子邮件：<caijuesong@163.com>

## ⚖️ 许可证

本项目仅供学习和研究使用，不提供任何明示或暗示的担保。

***

**免责声明**：

- 本软件仅供教育和研究目的
- 使用者需自行承担使用风险
- 确保遵守所有适用的法律法规
- 作者不对因使用本软件造成的任何损失负责

***

**致谢**：

- GNU Radio团队提供的强大框架
- Great Scott Gadgets的HackRF硬件
- PyQt和pyqtgraph开发社区

**最后更新**：2026年3月

# TRS文件生成与处理工具

## 概述

本工具旨在处理IQ数据文件和参数文件，生成TRS（Trace Set）文件，合并多个TRS文件，并为侧信道分析创建平均轨迹。它支持多种信号类型，并提供用户友好的界面用于选择不同的操作模式。

## 功能特性

- **从IQ数据生成TRS文件**：将原始IQ数据（.npy文件）和参数文件（.txt）转换为TRS文件
- **信号类型选择**：可选择同相信号（I）、正交信号（Q）或幅度值信号
- **参数文件处理**：从文本文件中提取参数（明文、密钥、密文）并嵌入到TRS文件中
- **合并TRS文件**：将多个TRS文件合并为单个文件
- **平均轨迹生成**：从多个TRS文件创建平均轨迹，以提高信噪比

## 依赖项

- Python 3.x
- NumPy
- trsfile
- tqdm
- matplotlib
- csv\_to\_trs（自定义模块）
- trs\_loader（自定义模块）

## 使用方法

### 运行工具

执行脚本启动交互式界面：

```bash
python getfinaltrs_zh.py
```

### 操作模式

1. **从IQ数据和参数文件生成TRS文件**
   - 选择信号类型（I、Q或幅度值）
   - 处理.npy IQ文件和.txt参数文件，创建TRS文件
2. **为现有TRS文件填充参数**
   - 读取现有的TRS文件并嵌入来自.txt文件的参数
3. **合并多个TRS文件**
   - 根据参数长度要求验证TRS文件
   - 将有效文件合并为单个TRS文件
   - 可选生成平均轨迹文件
4. **执行所有操作**
   - 按顺序运行所有模式

### 输入文件要求

#### 参数文件（.txt）

参数文件应包含以下信息：

```
session_id = YYYYMMDD_HHMMSS
save_counter = 000000
plaintext = <十六进制字符串>
key = <十六进制字符串>
ciphertext = <十六进制字符串>
```

#### IQ文件（.npy）

IQ文件应为存储在.npy格式中的复数numpy数组。预期的命名约定是：

```
{session_id}_{counter:06d}_iq.npy
```

### 输出

- **从IQ数据生成的TRS文件**：根据信号类型保存在子目录中（`trs_from_iq_amplitude`、`trs_from_iq_I`、`trs_from_iq_Q`）
- **带参数的TRS文件**：保存在`with_params`目录中
- **合并的TRS文件**：保存在`merged`目录中
- **平均轨迹文件**：保存在`merged`目录中，带有`average_`前缀

## 示例工作流程

1. **准备输入文件**：
   - 将IQ文件（.npy）和参数文件（.txt）放在同一目录中
2. **运行工具**：
   - 选择模式1从IQ数据生成TRS文件
   - 选择信号类型（例如，幅度值）
   - 工具将处理文件并在适当的子目录中创建TRS文件
3. **合并TRS文件**：
   - 选择模式3
   - 设置参数长度要求（例如，AES-128：明文=16，密钥=16，密文=16）
   - 根据需要选择生成平均轨迹
   - 工具将合并有效文件并保存结果

## 注意事项

- 运行工具前确保安装所有依赖项
- 参数文件必须正确格式化，包含明文、密钥和密文的十六进制字符串
- IQ文件应为复数numpy数组，以确保正确的信号处理
- 工具执行验证检查，确保TRS文件满足指定的参数长度要求

## 故障排除

- **文件未找到错误**：验证输入文件路径和命名约定
- **参数验证失败**：检查参数文件是否包含所有必需字段，且格式正确
- **TRS文件打开错误**：确保正确安装了trs\_loader和csv\_to\_trs模块
