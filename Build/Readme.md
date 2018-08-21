1. ~~When building, first build with `#include(CMakeLists-jni.txt)`, so that the libraries calvr needs can be compiled before calvr. Then build again with `include(CMakeLists-jni.txt)`.~~  
> No longer needed. All libraries can be built in one pass now.
2. Add c/c++ into `CMakeLists-jni.txt`
3. The first build will take a long time.
4. If some weird errors happen(or the `CMakeLists` is modified alot), delete `AndroidProject/app/.externalNativeBuild` folder and manually sync gradle so that `CMakeCache` and other cache files can be re-generated. (Next build may take a bit longer to re-generate those files)
5. If clang++ crashes, just click Build->Make Project once more, and it will continue building the rest objects. It may be the bugs of clang++ when it tries to build too many objects at once.
