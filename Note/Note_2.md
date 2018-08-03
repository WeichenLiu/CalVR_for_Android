## Update to previous note: 
## Problem:
1. In CalVR, there are direct gl calls that are using old Opengl standard (`glBegin`, `glEnd`, `glVector3f`, `glLoadMatrix`, `glPushAttrib`, `glPopAttrib`, etc). 
GLES2/3 doesn’t support such calls. (I tried to translate `glBegin, glEnd, glVector3f`, but then I found there are no easy way to translate `glPush/PopAttrib`. So I commented them out for now)

2.  CalVR uses `std::cerr`, etc, which will be a null pointer on Android. (`std::cerr << “a”;` will trigger invalid address segfault)

3.  CalVR uses `getenv()`. Such function does exist on Android but it doesn’t seem that we have a way to set it in Android beside using `setenv()`to set environment var. Currently, `getenv()` will return Null, because no env var matches the argument.

4. CalVR sample code uses `argc, argv`. (Not sure whether they are necessary)




## Progress:
### For problem 1
`InterlacedTopBottom` screen are not intened for phones and currently we just skip the MultiViewer feature.
We use a `#ifndef __ANDROID__` to ignore them

### For problem 2, replace them with android logcat functions.

Current progress:

Implement a customized `std::streambuf` class which directs outputs to android `logcat` instead of default `/dev/null`

File name:
> `include/cvrUtil/AndroidStdio.h`
`src/cvrUtil/AndroidStdio.cpp`

Requirement:
1. define `ANDROID`
2. `std::cout.rdbuf(new androidbuf(4));` and 
`std::cerr.rdbuf(new androidbuf(6));` 
must be called before any `std::cout<<` or `std::cerr<<`
3. `AndroidStdio.h` must be included before any `std::cout<<` or `std::cerr<<` calls.

### For problem 3 

Current progress:

Implement an `Environment` class to which contains a `std::map` to store pairs of `name` and `value`.

Use macro `#define getenv(x) __android_getenv(x)` to "override" `getenv()` function in standard library.

Currently, all env are hardcoded in `AndroidGetenv.cpp`

**(TODO)** Allow to read in environment variable from file.

File name:
> `include/cvrUtil/AndroidGetenv.h`
`src/cvrUtil/AndroidGetenv.cpp`

Requirement:
1. define `ANDROID`
2. `AndroidGetenv.h` must be included after `cstdlib`/`stdlib.h` and before any `getenv()` calls.

## Solution (Todo):

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

3. Add ability to read in environment variable from file (in `src/cvrUtil/AndroidGetenv.cpp`)
