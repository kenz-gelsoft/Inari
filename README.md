# Firefox on Haiku

This project is my experiment to build Firefox web browser on Haiku OS.

## Approach

Official Build Instruction pulls the (partially-) pre built binaries to build the browser.

But, there is such a pre-built binaries to use, because Haiku has not been a supported build environment yet.

We should follow build process of a tier-3 build target, here I'll look in FreeSBD's one.

## Checking prerequisites

Currently, FreeBSD port targets the 112.0 version of firefox.

But we'll target the current ESR version(111.0.1) (or older releases) if there is only old ports of prerequisites.

### 112.0 prerequisites

Build dependencies

* [ ] nspr>=4.32 : devel/nspr
* [ ] nss>=3.89 : security/nss
* [ ] icu>=72.1 : devel/icu
* [ ] libevent>=2.1.8 : devel/libevent
* [ ] harfbuzz>=7.1.0 : print/harfbuzz
* [ ] graphite2>=1.3.14 : graphics/graphite2
* [ ] png>=1.6.39 : graphics/png
* [ ] dav1d>=1.0.0 : multimedia/dav1d
* [ ] libvpx>=1.13.0 : multimedia/libvpx
* [ ] py39-sqlite3>0 : databases/py-sqlite3@py39
* [ ] v4l_compat>0 : multimedia/v4l_compat
* [ ] autoconf2.13 : devel/autoconf2.13
* [ ] nasm : devel/nasm
* [ ] yasm : devel/yasm
* [ ] zip : archivers/zip
* [ ] libc++abi.a : devel/wasi-libcxx
* [ ] libc.a : devel/wasi-libc
* [ ] libclang_rt.builtins-wasm32.a : devel/wasi-compiler-rt13
* [ ] llvm13>0 : devel/llvm13
* [ ] rust-cbindgen>=0.24.3 : devel/rust-cbindgen
* [ ] rust>=1.68.0 : lang/rust
* [ ] node : www/node
* [ ] libnotify>0 : devel/libnotify
* [ ] jack.h : audio/jack
* [ ] pulseaudio.h : audio/pulseaudio
* [ ] sndio.h : audio/sndio
* [ ] gmake>=4.3 : devel/gmake
* [ ] pkgconf>=1.3.0_1 : devel/pkgconf
* [ ] python3.9 : lang/python39
* [ ] update-desktop-database : devel/desktop-file-utils
* [ ] xorgproto>=0 : x11/xorgproto
* [ ] x11.pc : x11/libX11
* [ ] xcb.pc : x11/libxcb
* [ ] xcomposite.pc : x11/libXcomposite
* [ ] xdamage.pc : x11/libXdamage
* [ ] xext.pc : x11/libXext
* [ ] xfixes.pc : x11/libXfixes
* [ ] xrandr.pc : x11/libXrandr
* [ ] xrender.pc : x11/libXrender
* [ ] xt.pc : x11-toolkits/libXt
* [ ] xtst.pc : x11/libXtst
* [ ] perl5>=5.32.r0<5.33 : lang/perl5.32

Runtime dependencies:

* [ ] libpci.so : devel/libpci
* [ ] ffmpeg>=0.8,1 : multimedia/ffmpeg
* [ ] update-desktop-database : devel/desktop-file-utils
* [ ] x11.pc : x11/libX11
* [ ] xcb.pc : x11/libxcb
* [ ] xcomposite.pc : x11/libXcomposite
* [ ] xdamage.pc : x11/libXdamage
* [ ] xext.pc : x11/libXext
* [ ] xfixes.pc : x11/libXfixes
* [ ] xrandr.pc : x11/libXrandr
* [ ] xrender.pc : x11/libXrender
* [ ] xt.pc : x11-toolkits/libXt
* [ ] xtst.pc : x11/libXtst

Library dependencies:

* [ ] libdrm.so : graphics/libdrm
* [ ] libepoll-shim.so : devel/libepoll-shim
* [ ] libfontconfig.so : x11-fonts/fontconfig
* [ ] libfreetype.so : print/freetype2
* [ ] libaom.so : multimedia/aom
* [ ] libdav1d.so : multimedia/dav1d
* [ ] libevent.so : devel/libevent
* [ ] libffi.so : devel/libffi
* [ ] libgraphite2.so : graphics/graphite2
* [ ] libharfbuzz.so : print/harfbuzz
* [ ] libicui18n.so : devel/icu
* [ ] libnspr4.so : devel/nspr
* [ ] libnss3.so : security/nss
* [ ] libpng.so : graphics/png
* [ ] libpixman-1.so : x11/pixman
* [ ] libvpx.so : multimedia/libvpx
* [ ] libwebp.so : graphics/webp
* [ ] libdbus-1.so : devel/dbus
* [ ] libdbus-glib-1.so : devel/dbus-glib
* [ ] libGL.so : graphics/libglvnd
* [ ] libatk-1.0.so : accessibility/at-spi2-core
* [ ] libcairo.so : graphics/cairo
* [ ] libgdk_pixbuf-2.0.so : graphics/gdk-pixbuf2
* [ ] libglib-2.0.so : devel/glib20
* [ ] libintl.so : devel/gettext-runtime
* [ ] libgtk-3.so : x11-toolkits/gtk30
* [ ] libpango-1.0.so : x11-toolkits/pango
* [ ] libjpeg.so : graphics/jpeg-turbo

## References

* Official Linux Build Instruction
  * https://firefox-source-docs.mozilla.org/setup/linux_build.html
* FreeBSD ports
  * https://www.freshports.org/www/firefox/
