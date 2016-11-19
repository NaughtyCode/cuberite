# Configure command (from the current directory):
# cmake . -DCMAKE_SYSTEM_NAME=Android -DCMAKE_SYSTEM_VERSION=16 -DCMAKE_BUILD_TYPE=Release -DCMAKE_ANDROID_ARCH_ABI=armeabi -DNATIVE_TOLUA_GENERATOR="" -DCMAKE_ANDROID_NDK=""
# -G "MinGW Makefiles" -DCMAKE_MAKE_PROGRAM="" may also be required on Windows

# Build command (from the current directory):
# cmake --build .

Users should obtain the latest copy of the Android NDK from https://developer.android.com/ndk/downloads and set the paramter CMAKE_ANDROID_NDK to the root directory of the downloaded NDK folder.

For additional ABI options, visit https://cmake.org/cmake/help/latest/variable/CMAKE_ANDROID_ARCH_ABI.html

The parameter NATIVE_TOLUA_GENERATOR should be a recognised CMake compiler, installed on the current system. It is used to compile a native (rather than Android) version of tolua which is used to generate bindings.

Windows users may make use of Visual Studio to compile for Android, but CMake requires the presence of Nvidia CodeWorks/Nsight Tegra, which can be a hassle to install. The easiest generator to use seems to be the NDK-bundled Make, to be specified as shown in the configure command above. This executable may be found under the 'prebuilt/windows-*/bin' subdirectory in the NDK folder.

The minimum API level is 16 in the verbatim copy of this folder, due to the inclusion of position independent compilation. This can be changed.

If the build succeeded, an Android-launchable binary will have been generated under the Server directory. However, since this directory does not have any supporting files, they must be copied from the parent folder's Server directory. The Android executable is now ready to use.

On Linux, one may make use of one Compile.sh, which will insert these parameters into the configuration command and perform builds. Please note that this script will behave differently if asked to build for all ABIs; it will instead package a complete folder, inclusive of both binary and supporting files, in a zipped folder. Singular ABI builds will behave the same as specified in the above paragraph.