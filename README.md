<h1 align="center">🌟WinDB🌟 HMD-Free and Distortion-Free Panoptic Video Fixation Learning (TPAMI 2025)</h1>

<div align='center'>
    <a href='https://scholar.google.com/citations?user=eJIysC8AAAAJ' target='_blank'><strong>Guotao Wang</strong></a><sup> 1</sup>,&thinsp;
    <a href='http://chenglizhaochen.cn/' target='_blank'><strong>Chenglizhao Chen</strong></a><sup> 2, 6</sup>,&thinsp;
    <a href='https://dblp.org/pid/94/5679.html' target='_blank'><strong>Aimin Hao</strong></a><sup> 1</sup>,&thinsp;
    <a href='https://scholar.google.com/citations?hl=en&user=NOcejj8AAAAJ&view_op=list_works&sortby=pubdate' target='_blank'><strong>Hong Qin</strong></a><sup> 3</sup>,&thinsp;
    <a href='https://dengpingfan.github.io/' target='_blank'><strong>Deng-Ping Fan</strong></a><sup> 4, 5</sup>,&thinsp;
</div>

<div align='center'>
    <sup>1 </sup>Beihang University&ensp;  <sup>2 </sup>China University of Petroleum&ensp;  <sup>3 </sup>Stony Brook University&ensp; <sup>4 </sup>Nankai University&ensp; 
    <br />
    <sup>5 </sup>Nankai International Advanced Research Institute (SHENZHEN FUTIAN)&ensp;  <sup>6 </sup>Sichuan Provincial Key Laboratory of Criminal Examination&ensp; 
</div>

   

📄 [**Arxiv**](https://arxiv.org/pdf/2305.13901) | 🌐 [**中文**]()

<div align="center">
  <img width="1000" height="210" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732611209391.gif"/>
</div>

The existing HMD-based fixation collection method for panoptic data has a critical limitation --- **blind zoom**, results in the collected fixations being insufficient to train deep models to accurately predict which regions in a given panoptic are most important.   

## News :newspaper:
* **`Nov 29, 2024`:**  We uploaded the FishNet model [Baidu Netdisk](https://pan.baidu.com/s/16Q5aFhYVGu81Ig5wnv4j9A?pwd=48a5), [Google Netdisk](https://drive.google.com/file/d/1M78YHnyVDdvFh1bjJxAaaerhZmovujfS/view?usp=sharing).
* **`Nov 23, 2024`:** Our WinDB is now officially released [online](https://pan.baidu.com/s/1zugJ-HxiM7LZRoq-9baMdg?pwd=vgjo) on TPAMI journal.
* **`Nov 27, 2024`:** We released and uploaded the Chinese version of our paper to my [Baidu Netdisk](https://pan.baidu.com/s/1PonoZTmK-Xlw4hSD-9-2Bw?pwd=agci).
* **`Mar 7, 2024`:**  We released FishNet codes, [Code](https://github.com/guotaowang/FishNet).
* **`Mar 7, 2024`:**  We released PanopticVideo-300 dataset, [Code](https://github.com/guotaowang/PanopticVideo-300).
* **`Sep 27, 2023`:**  We released WinDB codes, [Code](https://github.com/guotaowang/WinDB).
* **`May 23, 2023`:**  We released our paper on [arXiv](https://arxiv.org/abs/2305.13901).

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

### 🖥️ Tobii Installation
1. **Install Packages**:
   - `Tobii_Eye_Tracking_Core_v2.16.8.214_x86.exe`
   - `TobiiGhost.1.7.0-Setup.exe`  
   > See the detailed `License.pdf`.  
   ![License](https://github.com/cvpr-submission/WinDB/blob/main/Figs/License.gif)  
2. **Calibration**: Start the Tobii Eye Tracking software ![Tobii](https://github.com/cvpr-submission/WinDB/blob/main/Figs/TobiiL.GIF) and complete the calibration.

### 📂 Main Steps  
**1. WinDB Generation → 2. Fixation Collection → 3. Fixation Generation**


### 🧐 Detailed Procedure of Eye Tracking Data

#### 1. WinDB Generation  
<div align="center">
  <img width="800" height="310" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732611610575.gif"/>
</div>
<p align="center"><b>Fig.</b> The overall pipeline of our HMD-free fixation collection approach for panoptic data.</p>   

- **Generate Longitude & Latitude**:  
   ```bash
   python ERP2WinDBLonLat.py
   ```
- **Convert ERP to WinDB using LonLat**:  
   ```bash
   python ERP2WinDB.py
   ```
#### 2. Fixation Collection  
1. **Open the Solution File**: Use Visual Studio 2019 to open `start.sln`.  
   ![start.sln](https://github.com/cvpr-submission/WinDB/blob/main/Figs/start.sln.gif)  
2. **Configure Property Pages**: Ensure `start.sln` has been configured correctly.
3. **Run Fixation Collection**: Execute `start.spp` to save fixation locations **(x, y)** in `PeopleID.txt`.  
   ![start](https://github.com/cvpr-submission/WinDB/blob/main/Figs/start.gif)

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

## 🌟 Key Highlights of WinDB  
**WinDB** revolutionizes panoramic video fixation data collection by eliminating the cumbersome and expensive traditional setups involving HMDs, Unity, Steam, and more. Leveraging a straightforward C++ interface with Tobii devices, **WinDB** stands out for being simple, cost-effective, and extremely easy to use. 😄  

---

## 🌍 PanopticVideo-300 Dataset

<div align="center">
  <img width="500" height="260" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732611645555.gif"/>
</div>

<p align="center"><b>Fig.</b> Statistics on the types of fixation shifts and the semantic categories. All fixation data in our set is collected using <b>WinDB</b>.</p>   

### 📁 Video Clips (300)
- **Training Set**: [240 clips](https://pan.baidu.com/s/17Awqc_1uZd2e8XmYylag-Q?pwd=aqhy)  
- **Testing Set**: [60 clips](https://pan.baidu.com/s/17Awqc_1uZd2e8XmYylag-Q?pwd=aqhy)

<div align="center">
  <img width="1000" height="170" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732611280138.gif"/>
</div>

<p align="center"><b>Fig.</b> Qualitative demonstration of the differences between the datasets collected by our WinDB method and the VR-Eye Tracking.</p>   

---

## 🎣 FishNet Architecture  

<div align="center">
  <img width="1000" height="480" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732611673627.gif"/>
</div>

<p align="center"><b>Fig.</b> The detailed network architecture of our FishNet.</p>   

**A** focuses on performing ERP-based global feature embedding to achieve panoptic perception and avoid visual distortion.  
**B** catches fixation shifting by refocusing the network to avoid the compression problem of shifted fixations in SOTA models.  
**C** makes the network fully aware of the fixation shifting mechanism to ensure that the network is sensitive to fixation shifting.  

<div align="center">
<img width="400" height="250" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732614599303.gif"/> <img width="400" height="170" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732614640036.gif"/>
</div>

<p align="center"><b>Fig.</b> Detailed calculation of the spherical distance. <b>Fig.</b> Visualizing of the ``shifting-aware feature enhancing''.</p>  

### 🛠️ Key Steps for FishNet (CODE: https://github.com/guotaowang/FishNet/tree/main)

1. **Training Process**  
   ```bash
   python train.py
   ```

2. **Inference Process**  
   ```bash
   python test.py
   ```

3. **Model Weight**  
   - [Model.pt](https://pan.baidu.com/s/11YoqCtI7iT1ZHw3NhpzgzQ?pwd=j5ap) (97.9 MB) 

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
  <img width="600" height="290" src="https://github.com/guotaowang/WinDB/blob/main/Figs/1732611752777.gif"/>
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
