## Progress:

1. Built osg plugins: osgdb_jpeg, osgdb_png, osgdb_tiff and corresponding third party dependencies. (Codes and cmakefiles for dependencies are available on `dependencies` branch)
2. Fix a problem in previous cmakefiles that prevents the whole library from being built in one pass.
3. Built calvr plugins: MenuBasics (Modification to calvr plugin codes and cmakefiles are available on `dependencies` branch)
4. To use osg plugins statically, add these macros right after osg includes. Otherwise, osg will try to use loadLibrary to find plugins dynamically.
```
USE_OSGPLUGIN(rgb)
USE_OSGPLUGIN(tiff)
USE_OSGPLUGIN(png)
USE_OSGPLUGIN(jpeg)
USE_OSGPLUGIN(freetype)
```
5. Default path to icons and font seems to be incorrect. If the codes fail to load icons or fonts, double check the path.

Menu with icons and font loaded:
![Screenshot](https://github.com/WeichenLiu/CalVR_for_Android/blob/denpendencies/Note/Screenshot_1.jpg)
