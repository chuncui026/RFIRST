# RFIRST
RFIRST: A Framework and Public Dataset for RF Side-Channel Analysis on Zephyr-Based nRF52

The RFIRST_nRF52_TinyAES dataset is the first publicly available radio frequency side-channel analysis (RF-SCA) dataset collected from modern low-power mixed-signal microcontrollers running a real-time operating system. The dataset contains RF leakage traces captured during TinyAES encryption executions on Nordic nRF52 DK development boards (PCA10040) equipped with nRF52832 chips.

Two versions of the dataset are provided, representing different generations of the nRF52 platform:

2019 Version: Collected from board PCA10040 1.2.4 (2019.8), containing 100,000 traces with relatively higher signal-to-noise ratio (SNR)
2024 Version: Collected from board PCA10040 3.0.4 (2024.34), containing 300,000 traces with reduced SNR due to low-power optimizations in the newer chip revision
All traces were acquired using a HackRF One software-defined radio connected directly to the RF test port via coaxial cable, ensuring controlled and repeatable measurements. The acquisition platform RFRST (Real-time First Intelligent acquisition platform for RF Side-channel analysis on Target devices) employs an event-driven, amplitude-based triggering mechanism that enables single-trace acquisition without averaging, closely reflecting real-world encryption scenarios.

Each trace is accompanied by its corresponding plaintext, key, and ciphertext, enabling supervised deep learning-based side-channel analysis. The dataset is provided in multiple formats (raw I/Q .npy, Riscure .trs, and metadata .txt) to support diverse research needs.

This dataset aims to foster reproducible research in RF side-channel analysis, facilitate the development of deep learning models for low-SNR scenarios, and enable quantitative studies on the security implications of low-power optimizations in modern mixed-signal chips.
