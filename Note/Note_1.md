## Current Progress:
I fixed the linking error by reordering dependencies in `CMakeLists` and cleaning up the `CMakeCache`.
Right now, I am not sure whether the built library can handle font/texture or not, since I haven’t tested those function yet. Hopefully it can.
I will upload the `CMakeLists` files (with comments and also other files I modified to build) here later.
## Current problem:
1. In CalVR, there are direct gl calls that are using old Opengl standard (`glBegin`, `glEnd`, `glVector3f`, `glLoadMatrix`, `glPushAttrib`, `glPopAttrib`, etc). 
GLES2/3 doesn’t support such calls. (I tried to translate `glBegin, glEnd, glVector3f`, but then I found there are no easy way to translate `glPush/PopAttrib`. So I commented them out for now)

2.  CalVR uses `std::cerr`, etc, which will be a null pointer on Android. (`std::cerr << “a”;` will trigger invalid address segfault)

3.  CalVR uses `getenv()`. Such function does exist on Android but it doesn’t seem that we have a way to set it in Android beside using `setenv()`to set environment var. Currently, `getenv()` will return Null, because no env var matches the argument.

4. CalVR sample code uses `argc, argv`. (Not sure whether they are necessary)

## Possible solution (Todo):

1. For problem 1, maybe rewrite those codes using new Opengl
>I only found 5 functions that prevent it from compiling:
>ScreenMVStencil.h:
> `fullscreenQuad()`
> `fullscreenTriangle()`
> ScreenMVStencil.cpp: 
> `ScreenMVStencil::setupZones()`
> ScreenInterlacedTopBottom.cpp:
> `ScreenInterlacedTopBottom::InterlaceCallback::operator()`
> ScreenMVShader.cpp: 
> `ScreenMVShader::PreDrawCallback::operator()`

2. For problem 2, replace them with android logcat functions.
> For example, `__android_log_write()`

3. For problem 3 (and maybe 4):
>a. Hardcode env variables and set them using `setenv()` at the very beginning of application (Not sure if Android allows an app to do this)
>b. Wrap all `getenv()` calls with `#ifndef Android`, and feed in hardcoded path instead.