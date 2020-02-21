# Project Guidoge

* Mobile device assisted visual extension Exhibition Scheme *

* Project Name: Guidoge ｜ Kelu
* Developer: nekowink, eEhyQx.
* Project Overview: Guidoge is a set of assisted vision solutions based on ordinary smart mobile devices

## 0.Trailer

[! [GUIDOGE VIDEO] (https://s2.ax1x.com/2019/09/29/uGMrVO.png)]] (https://www.bilibili.com/video/av69334959)

👆 Click the picture above to play Kelu's 1min promotional video!

## 1. Project Introduction

Guidoge is a set of assisted vision solutions based on ordinary smart mobile devices, which is mainly targeted at visually impaired people, cycling or balance bike enthusiasts and other groups with visual assistance / expanding needs. Guidoge does not require complicated peripherals, and only one mobile phone and one Guidoge Loop can realize rich visual assistance / expansion functions.

## 2. Solution

Guidoge's only peripheral is a Guidoge Loop. After opening the Guidoge APP to complete the relevant settings, the user hangs the rear camera of the phone forward on his chest through the Guidoge Loop. Next, Guidoge Sever will complete some tasks including Depth estimation and Object Detection and provide users with navigation and obstacle avoidance As the core visual extension function.

**Avoidance**

Guidoge Sever uses the video information sent by the front end to perform the Depth estimation step to obtain the depth information of the foreground, and uses Object Detection to identify obstacles. Based on this information, the user is alerted by using interactive methods such as voice and vibration.

**navigation**

According to the preset destination and the current location information provided by the device, Guidoge uses the API of the third-party navigation service to obtain the route plan, and further converts the route plan into clear semantic vibrations and voice prompts, bringing a better navigation experience to users .

**Remote guidance**

Guidoge provides observation windows open to users' relatives and friends. Users can enable the remote guidance mode to allow relatives and friends to observe the pictures collected by Guidoge through the observation window, and provide remote guidance by relatives and friends.

**Rearview mirror mode**

Guidoge is open to the rearview mirror mode for user groups such as cycling and balance bike enthusiasts. In this mode, users need to adjust the Guidoge Loop to attach the mobile device to their back.

**No screen interaction**

Guidoge provides a complete voice user interface method, and users can achieve screenless interaction with Guidoge through voice control. Guidoge's basic feedback to users is also transmitted through vibration and voice, realizing screenless interaction.

## 3. Technology implementation
Many technologies involved in the Guidoge solution are closely related to Deep Learning and Computer Vision. Here we will briefly describe the solutions adopted by some of our current core technology points.

**Video Streaming**

Using the SDK provided by Agora (Sound Network) to complete the video streaming.

**Depth estimation**

According to the hardware support, we provide 3 Depth estimation schemes:

* Native Depth information (eg TOF)
* Binocular camera inference
* Monocular camera estimation

The former two already have more mature methods, and we will not repeat them here. In the use of a monocular camera for Depth estimation, we adopted the open-source version of the recent publication of Digging Into Self-Supervised Monocular Depth Estimation (Clément Godard, Oisin Mac Aodha, Michael Firman, Gabriel Brostow) published by ICCV2019.
  
**Object Detection**
  
Based on hardware support and environmental conditions, we provide 2 types of Object Detection solutions:
  
* Use depth information directly
* Judging by point cloud (requires internal reference of mobile device camera)

The first scheme uses Depth information and uses gradient estimation method in combination with the obstacle warning algorithm designed by the team to implement road condition description and obstacle determination; the second scheme is to restore Depth information to Point Cloud when the camera internal parameters can be obtained. Then the CVPR2019 recently published paper PointRCNN: 3D Object Proposal Generation and Detection from Point Cloud (Shi S, Wang X, Li H) open source version is combined with the obstacle early warning algorithm designed by the team to realize obstacle recognition and early warning. The two schemes can be executed at the same time if conditions permit.

## 4. Team introduction and progress

Team Name: FemtoTech

Name | Email
--- | ---
[nekowink] (https://github.com/nekowink) | eachandall@163.com
[eEhyQx] (https://github.com/eEhyQx) | qxzhang.work@gmail.com

You can contact the captain nekowink via email or QQ (61337542).

After we learned about the AI in RTC programming challenge on 9/22, we launched the project on that day and started the process of model verification, demo deployment, and production of promotional videos. We have verified the reliability of the solution in many places on the campus of Shanghai University of Science and Technology, and conducted real-time and field tests.

It is worth mentioning that in addition to the model for processing deep predictions, we also applied the latest research results of speech synthesis. You may find that the dubbing in the trailer is smooth and natural. All fragments are synthesized by a neural network.

Our team plans to design and complete a set of auxiliary applications that combine object recognition, scene description, and voice feedback before the final reply. It will be deployed on the Android and iOS platforms and finally achieve all of the above design goals. Please look forward to our results!

## 5. Compilation Guide

In order to facilitate your testing, our server runs directly locally through the Sanic framework. You can run the following instructions in the / ChallengeProject / Guidoge / directory to complete the environment configuration:

Please note: You need hardware that supports NVIDIA CUDA technology. The following commands passed the test under Windows 10 version 1903, Python 3.7, CUDA 10.0, and PyTorch 1.2.

-Install and run the dependencies needed for neural network, image processing and front end, `pip install numpy matplotlib Pillow sanic`

-Configure the deep learning PyTorch framework, you can refer to the relevant instructions on the [PyTorch] (https://pytorch.org/get-started/locally/) official website.

After completion, you can execute `python server.html` and` python -m http.server 8080` in the current directory to start the server. Enter [http: // localhost: 8080 / server.html] (http: // localhost: 8080 / server.html) in your local browser, and you can start to experience the magic of deep learning and WebRTC technology!

## 6.Demo running guide

You need a server on the public network with https enabled, and the Agora Web SDK Sample deployed on it. When you use a mobile device or a laptop / tablet with a camera to access the sample, enter the AppID, and check the Host to publish the video, you can enter the corresponding information in the local browser and connect. If successful, you can see the interface in the [Promotion Video] (https://www.bilibili.com/video/av69334959) title on the local server.

**Mark**

* Based on debugging requirements, https is not required for local access, but the WebRTC protocol requires that encrypted connections be established when accessing other servers.

* For better compatibility, Chrome and its mobile versions are recommended for testing.

* The server and client do not need to be on the same network segment (we use live reliable technology provided by Agora.io for live broadcast).

## Special Thanks

[! [AGORA.IO] (https://www.agora.io/en/wp-content/uploads/2019/06/agoralightblue-1.png)] (https://www.agora.io/)

## Reference

Godard, Clément, Mac Aodha O, Firman M, et al. Digging Into Self-Supervised Monocular Depth Estimation [J]. 2018.

Shi S, Wang X, Li H. PointRCNN: 3D Object Proposal Generation and Detection from Point Cloud [J]. 2018.
