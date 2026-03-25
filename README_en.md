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

