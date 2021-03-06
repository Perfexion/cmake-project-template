# Build for Android
Configuring the build for the Android platform requires Qt for Android:

## Build QT for Android
```
./configure -xplatform android-clang\
 --disable-rpath -nomake tests -nomake examples\
 -android-ndk $ANDROID_NDK -android-sdk $ANDROID_SDK\
 -no-warnings-are-errors
make
```

## Configure this project to use QT from above
```
cmake \
  -DANDROID_ABI:STRING=armeabi-v7a \
  -DANDROID_NATIVE_API_LEVEL:STRING=21 \
  -DANDROID_NDK:PATH=/home/justin/workspace/android_sdk/ndk/21.1.6352462 \
  -DANDROID_SDK:PATH=/home/justin/workspace/android_sdk \
  -DANDROID_STL:STRING=c++_shared \
  -DCMAKE_BUILD_TYPE:STRING=Debug \
  -DCMAKE_CXX_COMPILER:STRING=/home/justin/workspace/android_sdk/ndk/21.1.6352462/toolchains/llvm/prebuilt/linux-x86_64/bin/clang++ \
  -DCMAKE_C_COMPILER:STRING=/home/justin/workspace/android_sdk/ndk/21.1.6352462/toolchains/llvm/prebuilt/linux-x86_64/bin/clang \
  -DCMAKE_FIND_ROOT_PATH:STRING=/opt/Qt-5.14.2-android \
  -DCMAKE_PREFIX_PATH:STRING=/opt/Qt-5.14.2-android \
  -DCMAKE_TOOLCHAIN_FILE:PATH=/home/justin/workspace/android_sdk/ndk/21.1.6352462/build/cmake/android.toolchain.cmake \
  -DQT_QMAKE_EXECUTABLE:STRING=/opt/Qt-5.14.2-android/bin/qmake \
  -DPACKAGE_TESTS=OFF \
  ..
```

For more information see: https://cmake.org/cmake/help/latest/manual/cmake-toolchains.7.html#cross-compiling-for-android-with-a-standalone-toolchain 
