# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.



cmake_minimum_required(VERSION 3.4.1)

# for more detailed linker message
SET( GCC_COVERAGE_LINK_FLAGS    "-v")
SET( CMAKE_EXE_LINKER_FLAGS  "${CMAKE_EXE_LINKER_FLAGS} ${GCC_COVERAGE_LINK_FLAGS}" )
SET( CMAKE_SHARED_LINKER_FLAGS  "${CMAKE_SHARED_LINKER_FLAGS} ${GCC_COVERAGE_LINK_FLAGS}" )
SET( CMAKE_STATIC_LINKER_FLAGS  "${CMAKE_STATIC_LINKER_FLAGS} ${GCC_COVERAGE_LINK_FLAGS}" )

SET(KERNEL_LIBRARIES 
    cvrKernel                     # For cvr, Kernel > Menu > Util
    cvrMenu                       # The order of Input, Config, Collaborative is unsure (current order works)
    cvrUtil                       #
    cvrInput                      #
    cvrConfig                     #
    cvrCollaborative              #
    mxml                          # mxml must be included before cvr
    ${log-lib}                    #
    osgPresentation               # For osg, the dependency relations:
    osgWidget                     # osgPresentation: https://github.com/WeichenLiu/CalVR_for_Android/blob/master/Note/osgPresentation.png
    osgUI                         # osgdb_osg: https://github.com/WeichenLiu/CalVR_for_Android/blob/master/Note/osgdb_osg.png
    osgManipulator                # osgdb_serializers_osg:
    osgAnimation                  # https://github.com/WeichenLiu/CalVR_for_Android/blob/master/Note/osgdb_serializers_osg.png
    osgViewer                     # (These three are the "roots" of the trees)
    osgVolume                     #
    osgSim                        #
    osgShadow                     #
    osgTerrain                    #
    osgParticle                   #
    osgFX                         #
    z                             #
    osgText                       #
    osgGA                         #
    osgdb_tiff
    osgdb_png
    osgdb_jpeg
    osgdb_osg                     #
	osgdb_freetype
	osgdb_rgb
    osgdb_serializers_osg         #
    osgDB                         #
    osgUtil                       #
    osg                           #
    OpenThreads                   #
    tiff
    png
    jpeg
	freetype
    #zlib
    EGL                           #
    GLESv2                        #
)

# physx needs cpufeatures
include_directories(${ANDROID_NDK}/sources/android/cpufeatures)
add_library(cpufeatures ${ANDROID_NDK}/sources/android/cpufeatures/cpu-features.c)
target_link_libraries(cpufeatures dl)

# order matters
SET(PHYSX_LIBS
    PxPvdSDK
	PsFastXml
	PhysX3CharacterKinematic
	PhysX3Extensions
	PhysX3Cooking
	PhysX3Vehicle
	PhysX3
	PhysX3Common
	PxFoundation
	cpufeatures
)

# set variable for 3rd dependencies
include(CMakeLists-dependencies.txt)
# set variable for osg					   
include(CMakeLists-osg.txt)
# set variable for mxml	
include(CMakeLists-mxml.txt)
# set variable for calvr
include(CMakeLists-calvr.txt)

include(CMakeLists-jni.txt)
