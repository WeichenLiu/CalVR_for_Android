## To build with PhysX:

Copy the folder:
```
Build/dependencies/physx
```
and CMakeLists files:
```
Build/dependencies/CMakeLists.txt (Updated)
Build/calvr_plugins/calit2/SpatialViz/CMakeLists.txt
Build/AndroidProject/app/CMakeLists-dependencies.txt (Updated)
```
to the corresponding path.

## Update detail (May not related to PhysX):

1. Modify `_LIBRARY` variables in CMakeLists files.
2. Add and statically import all PhysX libraries (ARM architecture, SDK version 3.4), and setup corresponding variables manually (`PHYSX_LIBRARY`, `PHYSX_INCLUDE_DIR`, `PHYSX_FOUND`)
3. Add check to build SpatialViz statically for Android
4. Add preprocessor macro to deal with different version of PhysX SDK. 
