## To build with PhysX:

Copy the folder:
```
Build/dependencies/physx (Updated 09/01/18)
```
and CMakeLists files:
```
Build/dependencies/CMakeLists.txt (Updated 09/01/18)
Build/calvr_plugins/calit2/SpatialViz/CMakeLists.txt (Updated 09/01/18)
Build/AndroidProject/app/CMakeLists-dependencies.txt (Updated 09/01/18)
```
to the corresponding path.

## Update detail (May not related to PhysX):

1. Modify `_LIBRARY` variables in CMakeLists files.
2. Add and statically import all PhysX libraries (ARM architecture, SDK version 3.4), and setup corresponding variables manually (`PHYSX_LIBRARY`, `PHYSX_INCLUDE_DIR`, `PHYSX_FOUND`)
3. Add check to build SpatialViz statically for Android
4. Add preprocessor macro to deal with different version of PhysX SDK. 

## Update detail (09/01/18):

1. Modify PhysX makefile provided by Nvidia to build PhysX with newest NDK and clang (instead of gcc and g++) to prevent many possible weird errors when linking libraries built by different compilers and standards (Modified makefiles are in PhysX/android26/)
2. Build cpufeatures and figure out correct linking order for PhysX
3. Move PhysX import to parent cmakelists to avoid weird scope problem.
4. Update SpatialViz and MenuBasics's CMakeLists for Android.

## Current Progress (09/01/18):

SpatialViz menu displays correctly and can create something:
![Screenshot](https://github.com/WeichenLiu/CalVR_for_Android/blob/PhysX/Note/Screenshot_2.jpg)

## Problem (09/01/18):

Created puzzles are incorrect. It can be some problems related to either rendering, or physics scaling/parameters. (Sometimes I can see a cube flying around)
