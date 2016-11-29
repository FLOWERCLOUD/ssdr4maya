
This code is a sample of plug-in implementation for Maya 2016 of the article Smooth Skinning Decomposition with Rigid Bones by Binh Huy Le and Zhigang Deng.

Binh Huy Le and Zhigang Deng, Smooth Skinning Decomposition with Rigid Bones, ACM Transactions on Graphics, 31 (6), (2012), 199: 1-199: 10.
Binh Huy Le and Zhigang Deng, Robust and Accurate Skeletal Rigging from Mesh Sequences, ACM Transactions on Graphics, 33 (4), (2014), 84: 1-84: 10.
Tomohiko Mukai, skinning decomposition, Computer Graphics Gems JP 2015 Chapter 7: Skinning decomposition (Born Digital), 2015.
Installation method

Place the complete set of packages in the bin folder in the folder that Maya's plugin path (MAYA_PLUG_IN_PATH) passes.
how to use

This plugin approximates the shape of each frame with skin + bone attitude. Adjacent frames do not necessarily need to change smoothly. In other words, it is possible to process even a sequence in which each frame of pause is recorded frame by frame.

We are only testing with baker animation basket to nCloth simulation, public data of Mesh Data from Deformation Transfer for Triangle Meshes, and a few data such as Maya Muscle.

Procedure for use

Specify the animation start time and end time.
Only the specified time range is processed.
If an extra range where animation is not set is also selected, problems such as longer computation time or unstable calculation will occur.
Select the shape to be processed.
Processing starts from [MukaiLab] -> [SSDR] in the menu.
When processing is done, the approximation error (RMSE) and the number of bones used (# Bones) are displayed on the command line.
Calculation parameters such as minimum bone count and maximum influence number can be changed by editing mlSsdrBuilder.py directly.
The converted skin and bones are grouped into "SsdrResult" group.
It is displayed at the same position as the shape before conversion.
All bones are always placed at the origin of the world coordinate system in the bind pose. This is the image where movement (displacement) of the origin center acts on the shape.
Please refer to the YouTube videos below for usage images.

SSDR4Maya

Adjustment of calculation parameters

The calculation parameters of SSDR are summarized at the beginning of the ssdrBuildCmd class in mlSsdrBuilder.py.

NumMaxInfluences: maximum number of bones allocated per vertex
NumMinBones: Minimum number of bones used for vertex animation approximation
NumMaxIterations: maximum number of iterations
By changing these three parameters, I think that you can see the change in the calculation result accordingly. Currently, it is confirmed that the calculation fails if a large value is given to the minimum bone number.

Build and run method

The extension library ssdr.pyd is created as a Visual Studio 2012 Professional Update 4 project (※ solution file is created on VS 2013). Build requires Eigen, QuadProg ++, Boost, and Maya 2016.3 Developer Kit as external libraries. Eigen 3.2.8, QuadProg ++ 1.2.1, and Boost 1.55.0 were used for the build and execution tests.

Build procedure

Pass the include path to the Eigen installation folder.
Pass the include path to the installation folder of Boost.
// Pass the include path to the MAYA_LOCATION / include and // MAYA_LOCATION / include / python 2.7 folders.
Download QuadProg ++ and copy the following four files to the ssdr folder.
QuadProg ++. Hh
QuadProg ++. Cc
Array.hh
Array.cc
Build & run on Visual Studio
Development & test environment

Windows 10 Pro
Maya 2016 SP 6
Visual Studio 2012 Update 4
Maya 2016.3 Developer kit
Eigen 3.2.8
QuadProg ++ 1.2.1
Boost 1.55.0
change history

2016/09/24 Alpha release

Compliant with Maya 2016 standard development environment
Visual Studio 2012 Update 4
Boost 1.55.0
Replace math library in ssdr.pyd module with OpenMaya
Modification of menu generation related python code
2016/07/06 Initial publication

