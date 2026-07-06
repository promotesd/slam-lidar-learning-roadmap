# Visual Odometry(VO)
- preliminaries
    - struct from motion(SFM)运动结构恢复
    - Epipolar Geometry对极几何
    - 针孔相机模型
    - PnP问题求解

- visual odometry is a technique that estimates a camera's motion by analyzing consecutive images, enabling robots and vehicles to track their position and rotation in real time.
1. Principle: 
    1. 特征匹配与跟踪：从连续帧中提取提取特征点，并在相邻帧之间进行匹配，追踪这些点点运动轨迹
    2. 几何约束与位姿估计：利用特征点的匹配关系，通过几何约束计算相机的相对位姿变化。
2. Local-only VO
    - local-only VO estimates camera motion incrementally from recent frame or a local window, without global map correction.
    - robust motion estimation->triangulation->camera pose estimation->re-triangulation->repeat
3. Local-only VO without loop closure
    - loop closure detection is a SLAM component that identifies revisited places and enables constraints that correct accumulated drift.
4. Fundamental Matrix基础矩阵
    - Fundamental matrix represents the epipolar geometry between two images which maps a point from one image to an epipolar line in the other image.
    - 3*3 matrix
    - 在对极几何中，对于一对同名点$p$和$p^‘$，它们满足极线约束：$p^{'T}Fp=0$,表明左图像对应的点p在右图像对应的点必定位于由F定义的极线上。
    - This paper uses calibrated geometry and 5-point algorithm for relative pose estimation.
5. Essential Matrix本质矩阵
    - 描述两个相机归一化坐标系下匹配点的对极约束关系。它由相机的相对旋转 R 和平移 t 决定，公式为： E = [t]× R，其中 [t]× 是由平移向量构造的反对称矩阵。
6. Triangulation三角化
    - 在单目SLAM中，仅通过单张图像无法获取像素点的深度信息，需要通过三角测量或三角化的方法来确定地图点的深度信息。Triangulation reconstructs 3D points from their observations in 2 or more images.
7. Perspective-n-Point (PnP)
    - PnP问题是通过已知n个3D点及其对应的2D图像点的方法，求解相机在世界坐标系的位姿。解决PnP问题主流方法包括：DLT，P3P，EPnP，BA。
8. Reprojection Error重投影误差
    - Reprojection error is the difference between observed image point and the projected image point predicted by the estimated camera pose and 3D point.
9.  Bundle Adjustment光束法平差/束调整
    - BA是一种通过最小化重投影误差，联合优化相机参数和三维点坐标的非线性最小二乘优化方法。
  
# MonoSLAM Real-Time Single Camera SLAM

- preliminaries
    - 卡尔曼滤波 and 扩展卡尔曼滤波
    - 

1. SLAM and MonoSLAM
   - SLAM is defined as the problem of a moving sensor platform constructing the representation of its environment while concurrently estimate the its geo-motion.
   - MonoSLAM 是使用单目摄像头的实时定位和建图方法。
2. EKF-based扩展卡尔曼滤波