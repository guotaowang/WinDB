# 🌟 **WinDB: HMD-free and Distortion-free Panoptic Video Fixation Learning (TPAMI2025)** 🌟

[Guotao Wang](https://scholar.google.com/citations?user=eJIysC8AAAAJ), [Chenglizhao Chen](http://chenglizhaochen.cn/), [Aimin Hao](https://dblp.org/pid/94/5679.html), [Hong Qin](https://scholar.google.com/citations?hl=en&user=NOcejj8AAAAJ&view_op=list_works&sortby=pubdate), [Deng-Ping Fan](https://dengpingfan.github.io/)

📄 [**Arxiv**](https://arxiv.org/pdf/2305.13901) | 🌐 [**中文**]()

---

## 📖 Table of Contents
- [Requirements](#requirements)
- [Tobii Installation](#tobii-installation)
- [Main Steps](#main-steps)
- [Detailed Procedure of Eye Tracking Data](#detailed-procedure-of-eye-tracking-data)
  * [1. WinDB Generation](#1-windb-generation)
  * [2. Fixation Collection](#2-fixation-collection)
  * [3. Fixation Generation](#3-fixation-generation)
- [Citation](#citation)

---

## 🛠️ Requirements
- **Visual Studio 2019**
- **Matlab2016b**
- **Python 3.6.4**
- **PyTorch 1.10.0**
- **CUDA 10.2**
- **OpenCV (Python and C++)**
- **Tobii Eye Tracking installation packages**:
  - `TobiiGhost.1.7.0-Setup.exe`
  - `Tobii_Eye_Tracking_Core_v2.16.8.214_x86.exe`

**WinDB** provides a lightweight and efficient way to read **Tobii fixation data** using a pure C++ implementation. All you need is a **Tobii device**, with no extra paid software or complex configurations required. Running **WinDB** is as simple as it gets 😄.

---

## 🖥️ Tobii Installation
1. Install the following packages:
   - `Tobii_Eye_Tracking_Core_v2.16.8.214_x86.exe`
   - `TobiiGhost.1.7.0-Setup.exe`  
   > See the detailed `License.pdf`.  
   ![License](https://github.com/cvpr-submission/WinDB/blob/main/Figs/License.gif)  
2. Start the Tobii Eye Tracking software ![Tobii](https://github.com/cvpr-submission/WinDB/blob/main/Figs/TobiiL.GIF) and complete the calibration.

---

## 📂 Main Steps  
### **1. WinDB Generation → 2. Fixation Collection → 3. Fixation Generation**

---

## 🧐 Detailed Procedure of Eye Tracking Data

### 1. WinDB Generation  
![Pipeline](https://github.com/guotaowang/WinDB/blob/main/Figs/pip.gif)  
*Figure 1. The overall pipeline of our new HMD-free fixation collection approach for panoptic data. Compared to the widely-used HMD-based method, our WinDB approach is more economical, comfortable, and reasonable.*

1. Generate the **longitude (lon.txt)** and **latitude (lat.txt)** of WinDB:  
   ```bash
   python ERP2WinDBLonLat.py
    ```
2. Convert ERP to WinDB using **LonLat (lon.txt, lat.txt)**:  
   ```bash
   python ERP2WinDB.py
   ```

---

### 2. Fixation Collection  
1. Open the solution file `start.sln` with Visual Studio 2019:  
   ![start.sln](https://github.com/cvpr-submission/WinDB/blob/main/Figs/start.sln.gif)  
2. Configure property pages for `start.sln`.  
3. Run `start.spp` to save fixation locations **(x, y)** in `PeopleID.txt`:  
   ![start](https://github.com/cvpr-submission/WinDB/blob/main/Figs/start.gif)

---

### 3. Fixation Generation  
1. Convert the **fixation location (x, y)** of WinDB to ERP:  
   - Fixation location (x, y) → WinDB location (θ, φ) → ERP Location (m, n).  
   ```bash
   python Location2WinDB.py
   ```
2. Smooth the fixation data on the sphere:  
   - ERP Location (m, n) → Sphere Location (θ, φ) → Sphere Smooth → Saliency.  
   ```bash
   python SphereSmooth.py
   ```

---

## 🌟 Highlights of WinDB  
**WinDB** uses C++ to directly read Tobii fixation data, requiring only a **Tobii device** with minimal setup. Unlike the traditional approach for panoramic video fixation collection, which involves complex setups (Unity, Steam, VIVEPort, etc.) and expensive hardware (HMDs, high-end GPUs), **WinDB** is simpler, more cost-effective, and more user-friendly. 😄  

---


## 🌍 PanopticVideo-300 Dataset

<div align="center">
  <img width="400" height="400" src="https://github.com/cvpr-submission/WinDB/blob/main/Figs/class.gif"/>
</div>

<p align="center"><b>Fig.</b> The semantic categories of PanopticVideo-300 dataset. All fixations in our set are collected by <b>WinDB</b>.</p>   

### 📁 Video Clips (300)
- **Training Set**: [240 clips](https://pan.baidu.com/s/1LeiX-p9YsAhrqTd2jq0Dfw)  
- **Testing Set**: [60 clips](https://pan.baidu.com/s/1LeiX-p9YsAhrqTd2jq0Dfw)


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
