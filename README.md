
# 🌟 **WinDB: HMD-Free and Distortion-Free Panoptic Video Fixation Learning (TPAMI 2025)** 🌟

### Authors: 
[Guotao Wang](https://scholar.google.com/citations?user=eJIysC8AAAAJ), [Chenglizhao Chen](http://chenglizhaochen.cn/), [Aimin Hao](https://dblp.org/pid/94/5679.html), [Hong Qin](https://scholar.google.com/citations?hl=en&user=NOcejj8AAAAJ&view_op=list_works&sortby=pubdate), [Deng-Ping Fan](https://dengpingfan.github.io/)

📄 [**Arxiv**](https://arxiv.org/pdf/2305.13901) | 🌐 [**中文**]()

<div align="center">
  <img width="1000" height="220" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732611209391.gif"/>
</div>

---

## 📖 Table of Contents
- [WinDB Overview](#windb-overview)
  - [Requirements](#requirements)
  - [Tobii Installation](#tobii-installation)
  - [Main Steps](#main-steps)
  - [Detailed Procedure of Eye Tracking Data](#detailed-procedure-of-eye-tracking-data)
- [PanopticVideo-300 Dataset](#panopticvideo-300-dataset)
- [FishNet Architecture](#fishnet-architecture)
- [Citation](#citation)

---

## 🛠️ WinDB Overview

### 📋 Requirements
- **Visual Studio 2019**
- **Matlab 2016b**
- **Python 3.6.4**
- **PyTorch 1.10.0**
- **CUDA 10.2**
- **OpenCV (Python and C++)**
- **Tobii Eye Tracking installation packages**:
  - `TobiiGhost.1.7.0-Setup.exe`
  - `Tobii_Eye_Tracking_Core_v2.16.8.214_x86.exe`

**WinDB** provides a lightweight and efficient method for collecting Tobii fixation data using a C++ implementation. With a simple **Tobii device**, there is no need for additional paid software or complex setups. It’s as simple as it gets 😄.

---

### 🖥️ Tobii Installation
1. **Install Packages**:
   - `Tobii_Eye_Tracking_Core_v2.16.8.214_x86.exe`
   - `TobiiGhost.1.7.0-Setup.exe`  
   > See the detailed `License.pdf`.  
   ![License](https://github.com/cvpr-submission/WinDB/blob/main/Figs/License.gif)  
2. **Calibration**: Start the Tobii Eye Tracking software ![Tobii](https://github.com/cvpr-submission/WinDB/blob/main/Figs/TobiiL.GIF) and complete the calibration.

---

### 📂 Main Steps  
**1. WinDB Generation → 2. Fixation Collection → 3. Fixation Generation**

---

### 🧐 Detailed Procedure of Eye Tracking Data

#### 1. WinDB Generation  
<div align="center">
  <img width="800" height="300" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732611610575.gif"/>
</div>
*Figure 1. The overall pipeline of our HMD-free fixation collection approach for panoptic data.*

- **Generate Longitude & Latitude**:  
   ```bash
   python ERP2WinDBLonLat.py
   ```
- **Convert ERP to WinDB using LonLat**:  
   ```bash
   python ERP2WinDB.py
   ```

---

#### 2. Fixation Collection  
1. **Open the Solution File**: Use Visual Studio 2019 to open `start.sln`.  
   ![start.sln](https://github.com/cvpr-submission/WinDB/blob/main/Figs/start.sln.gif)  
2. **Configure Property Pages**: Ensure `start.sln` has been configured correctly.
3. **Run Fixation Collection**: Execute `start.spp` to save fixation locations **(x, y)** in `PeopleID.txt`.  
   ![start](https://github.com/cvpr-submission/WinDB/blob/main/Figs/start.gif)

---

#### 3. Fixation Generation  
- **Convert Fixation to ERP**:
  - Fixation location (x, y) → WinDB location (θ, φ) → ERP Location (m, n).  
   ```bash
   python Location2WinDB.py
   ```
- **Smooth Fixation Data**:
  - ERP Location (m, n) → Sphere Location (θ, φ) → Sphere Smooth → Saliency.  
   ```bash
   python SphereSmooth.py
   ```

---

## 🌟 Key Highlights of WinDB  
**WinDB** revolutionizes panoramic video fixation data collection by eliminating the cumbersome and expensive traditional setups involving HMDs, Unity, Steam, and more. Leveraging a straightforward C++ interface with Tobii devices, **WinDB** stands out for being simple, cost-effective, and extremely easy to use. 😄  

---

## 🌍 PanopticVideo-300 Dataset

<div align="center">
  <img width="800" height="400" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732611645555.gif"/>
</div>

<p align="center"><b>Fig.</b> The semantic categories of PanopticVideo-300 dataset. All fixation data in our set is collected using <b>WinDB</b>.</p>   

### 📁 Video Clips (300)
- **Training Set**: [240 clips](https://pan.baidu.com/s/1LeiX-p9YsAhrqTd2jq0Dfw)  
- **Testing Set**: [60 clips](https://pan.baidu.com/s/1LeiX-p9YsAhrqTd2jq0Dfw)

<div align="center">
  <img width="1000" height="170" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732611280138.gif"/>
</div>

---

## 🎣 FishNet Architecture  

<div align="center">
  <img width="1000" height="450" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732611673627.gif"/>
</div>

<p align="center"><b>Fig.</b> Detailed architecture of our Fixation Shifting Network (FishNet), which comprises three core components:</p>

1. **Component A**: Focuses on ERP-based global feature embedding, achieving comprehensive perception while mitigating visual distortions.  
2. **Component B**: Tracks fixation shifts in PanopticVideo-300, ensuring that compression issues in existing SOTA models are addressed effectively.  
3. **Component C**: Fully comprehends and learns the mechanisms behind fixation shifting, making the network highly sensitive to fixation changes.

<div align="center">
  <img width="450" height="250" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732614599303.gif"/>
</div>
<div align="center">
  <img width="400" height="180" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732614640036.gif"/>
</div>

---

### 🛠️ Key Steps for FishNet

1. **Training Process**  
   ```bash
   python train.py
   ```

2. **Inference Process**  
   ```bash
   python test.py
   ```

3. **Model Weight**  
   - `Model.pt` (97.9 MB)

4. **Results**  
   - Results are stored in the output directory.

<div align="center">
  <img width="800" height="350" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732611730375.gif"/>
</div>

---

### 📊 Evaluation

1. **Score of Each Testing Set Clip**  
   ```bash
   MatricsOfMyERP.m
   ```

2. **Score of Entire Testing Set**  
   ```bash
   MatricsOfMyALLERP.m
   ```

<div align="center">
  <img width="600" height="300" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732611752777.gif"/>
</div>

---

## 📜 Citation  
If you use **WinDB**, please cite the following paper:

```bibtex
@article{wang2023windb,
  title={WinDB: HMD-free and Distortion-free Panoptic Video Fixation Learning},
  author={Wang, Guotao and Chen, Chenglizhao and Hao, Aimin and Qin, Hong and Fan, Deng-Ping},
  journal={arXiv preprint arXiv:2305.13901},
  year={2023}
}
```
