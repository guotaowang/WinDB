### This repository contains the code for submission paper   
# WinDB: HMD-free and Distortion-free Panoptic Video Fixation Learning.  

<img width="15" height="15" src="https://github.com/cvpr-submission/WinDB/blob/main/Figs/star.gif"/><img width="15" height="15" src="https://github.com/cvpr-submission/WinDB/blob/main/Figs/star.gif"/><img width="15" height="15" src="https://github.com/cvpr-submission/WinDB/blob/main/Figs/star.gif"/> It should be emphasized that our proposed **WinDB** uses C++ to read Tobii **fixation** data, so you only need to prepare a **Tobii device** without any additional charging software and with a **simple** configuration to very **easily** run WinDB <img width="15" height="15" src="https://github.com/cvpr-submission/WinDB/blob/main/Figs/smile.gif"/>.
However, the current way of collecting fixation for panoramic video data based on HMD is very ***complicated***, requiring the installation of a ***large amount of software***, such as Unity, Steam, VIVEPort..., and even ***expensive*** HMD and computer hosts equipped with high-end GPU cards.

## Table of Contents
- [Requirements](#requirements)
- [Tobii Installation](#tobii-installation)
- [Main Steps](#main-steps)
- [Detailed Procedure of Eye Tracking Data:](#detailed-procedure-of-eye-tracking-data)
  * [1. WinDB Generation](#1-windb-generation)
  * [2. Fixation Collection](#2-fixation-collection)
  * [3. Fixation Generation](#3-fixation-generation)

## Requirements.  
* Visual Studio 2019   
* Matlab2016b     
* python3.6.4   
* pytorch1.10.0   
* CUDA10.2    
* Opencv python and C++  
* Tobii Eye Tracking installation package (TobiiGhost.1.7.0-Setup.exe, Tobii_Eye_Tracking_Core_v2.16.8.214_x86.exe)  

## Tobii Installation
  * 1 Install Tobii_Eye_Tracking_Core_v2.16.8.214_x86.exe and TobiiGhost.1.7.0-Setup.exe (**License.pdf**<img width="300" height="15" src="https://github.com/cvpr-submission/WinDB/blob/main/Figs/License.gif"/>).  
  * 2 Start the Tobii Eye Tracking <img width="25" height="25" src="https://github.com/cvpr-submission/WinDB/blob/main/Figs/TobiiL.GIF"/> and calibration.  

## Main Steps  
### 1. WinDB Generation -> 2. Fixation Collection -> 3. Fixation Generation

## Detailed Procedure of Fixation Learning Data:  

### 1. WinDB Generation  
<div align=center><img width="900" height="380" src="https://github.com/guotaowang/WinDB/blob/main/Figs/pip.gif"/></div>
<p align="center">Figure 1. The overall pipeline of our new HMD-free fixation collection approach for panoptic data. Compared to the widely-used HMDbased method, our WinDB approach is more economical, comfortable, and reasonable. </p>    

  * 1) Generate the **longitude (lon.txt)** and **latitude (lat.txt)** of WinDB;  
  ```python ERP2WinDBLonLat.py``` 
  * 2) From ERP to WinDB based on **LonLat (lon.txt, lat.txt)** of WinDB.  
  ```python ERP2WinDB.py```
  
### 2. Fixation Collection  
  * 1) Open the ```start.sln```<img width="75" height="25" src="https://github.com/cvpr-submission/WinDB/blob/main/Figs/start.sln.gif"/> with Visual Studio 2019;  
  * 2) Config property pages of ```start.sln```<img width="75" height="25" src="https://github.com/cvpr-submission/WinDB/blob/main/Figs/start.sln.gif"/>;    
  * 3) run the ```start.spp```<img width="90" height="30" src="https://github.com/cvpr-submission/WinDB/blob/main/Figs/start.gif"/> and the **fixation location(x, y)** will be saved in PeopleID.txt.  

### 3. Fixation Generation  
  * 1) Convert the **fixation location(x, y)** of WinDB to ERP;   
     fixation location(x, y)->WinDB location(theta, phi)->ERP Location(m, n)  
     ```python Location2WinDB.py```   
  * 2) Smooth the **fixation** of ERP on the Sphere.   
     ERP Location(m, n)->Sphere Location(theta, phi)->Sphere Smooth->saliency  
     ```python SphereSmooth.py```   
