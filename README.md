

## Build FFmpeg For UPAVPlayerLib



__解决异常__ ：``` building armv7...
GNU assembler not found, install/update gas-preprocessor```原因是本地 gas-preprocessor未更新。删除本地gas-preprocessor（/usr/local/bin/gas-preprocessor.pl），重新运行脚本即可。	

__CONFIGURE_FLAGS__ 添加：```--disable-hwaccels```  //开启硬件加速引起videotoolbox连接的一个错误，暂时关闭处理。 错误信息如下：

```
Undefined symbols for architecture x86_64:
  "_CMBlockBufferCreateWithMemoryBlock", referenced from:
      _videotoolbox_common_end_frame in libavcodec.a(videotoolbox.o)
  "_CMSampleBufferCreate", referenced from:
      _videotoolbox_common_end_frame in libavcodec.a(videotoolbox.o)
  "_CMVideoFormatDescriptionCreate", referenced from:
      _av_videotoolbox_default_init2 in libavcodec.a(videotoolbox.o)
  "_ModPlug_GetCurrentOrder", referenced from:
 
```

__CONFIGURE_FLAGS__ 添加: ```--disable-encoders --disable-filters ```//无需编码和滤镜，关闭减小文件大小


__ARCHS__ :```ARCHS="arm64 armv7 x86_64"``` //去掉了 i386










# FFmpeg iOS build script

[![Build Status](https://travis-ci.org/kewlbear/FFmpeg-iOS-build-script.svg?branch=master)](https://travis-ci.org/kewlbear/FFmpeg-iOS-build-script)
[![Flattr this git repo](http://api.flattr.com/button/flattr-badge-large.png)](https://flattr.com/submit/auto?user_id=kewlbear&url=https://flattr.com/submit/auto?user_id=kewlbear&url=https%3A%2F%2Fgithub.com%2Fkewlbear%2FFFmpeg-iOS-build-script)

This is a shell script to build FFmpeg libraries for iOS and tvOS apps.

Tested with:

* FFmpeg 3.0
* Xcode 7.2.1

## Requirements

* https://github.com/libav/gas-preprocessor
* yasm 1.2.0

## Usage

Use build-ffmpeg-tvos.sh for tvOS.

* To build everything:

        ./build-ffmpeg.sh

* To build arm64 libraries:

        ./build-ffmpeg.sh arm64

* To build fat libraries for armv7 and x86_64 (64-bit simulator):

        ./build-ffmpeg.sh armv7 x86_64

* To build fat libraries from separately built thin libraries:

        ./build-ffmpeg.sh lipo

## Download

You can download a binary for FFmpeg 3.0 release at https://downloads.sourceforge.net/project/ffmpeg-ios/ffmpeg-ios-master.tar.bz2

## External libraries

You should link your app with

* libz.dylib
* libbz2.dylib
* libiconv.dylib

## Influences

* https://github.com/bbcallen/ijkplayer/blob/fc70895c64cbbd20f32f1d81d2d48609ed13f597/ios/tools/do-compile-ffmpeg.sh#L7
