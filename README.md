# Firefox on Haiku

This project is my experiment to build Firefox web browser on Haiku OS.

## Approach

Official Build Instruction pulls the (partially-) pre built binaries to build the browser.

But, there is no such a pre-built binaries to use, because Haiku has not been a supported build environment yet.

We should follow the build process one of the tier-3 build targets, here I'll look in the FreeBSD's one.

## Checking prerequisites

Currently, the FreeBSD port targets the 112.0 version of Firefox.

But we'll target the current ESR version(111.0.1) (or older releases) if there is only old ports of prerequisites.

### 112.0 prerequisites

Build dependencies

* [x] nspr>=4.32 : devel/nspr
  * Haiku Depot: 4.34.1-3, nspr, nspr_devel
  * Installing nspr_devel also installs nspr
* [x] nss>=3.89 : security/nss
  * Haiku Depot: 3.73.1-1, nss, nss_devel
  * Older than requirement version 3.89, but maybe buildable because NSS's API doesn't change often.
  * Installing nss_devel also installs nss
* [ ] icu>=72.1 : devel/icu
  * Haiku Depot: 66.1-3, icu66, icu66_devel
  * Older than requirement version 72.1, may require packaging newer version, but try using this.
* [x] libevent>=2.1.8 : devel/libevent
  * Haiku Depot: 2.1.12-2 libeevent, libevent_devel
  * ~~Haiku Depot: 2.1.8-5 libevent21~~ (no _devel package)
  * Haiku Depot: 4.33-1 libev, libev_devel
  * FreeBSD uses libevent, but libev may be an option if it doesn't work well.
* [ ] harfbuzz>=7.1.0 : print/harfbuzz
  * Haiku Depot: 4.0.0-3 harfbuzz, harfbuzz_devel
  * Older than requirement version 7.1.0, may require packaging newer version, but try using this.
* [x] graphite2>=1.3.14 : graphics/graphite2
  * Haiku Depot: 1.3.14-2 graphite2, graphite2_devel
* [x] png>=1.6.39 : graphics/png
  * Haiku Depot: 1.6.38-2 libpng16, libpng16_devel
  * Older than requirement version 1.6.39, may require packaging newer version, but try using this.
* [x] dav1d>=1.0.0 : multimedia/dav1d
  * Haiku Depot: 1.0.0-1 dav1d, dav1d_devel
* [ ] libvpx>=1.13.0 : multimedia/libvpx
  * Haiku Depot: 1.11.0-3 libvpx, libvpx_devel
  * Older than requirement version 1.13.0, may require packaging newer version, but try using this.
* [ ] py39-sqlite3>0 : databases/py-sqlite3@py39
  * Haiku Depot: N/A
  * Haiku Depot: apsw may be a replacement. But may require build or package ourself.
* [ ] v4l_compat>0 : multimedia/v4l_compat
  * Haiku Depot: N/A
  * Used by: libyuv, mozva
* [x] autoconf2.13 : devel/autoconf2.13
  * Haiku Depot: 2.13-3 autoconf213
* [x] nasm : devel/nasm
  * Haiku Depot: 2.14.02-2 nasm
* [x] yasm : devel/yasm
  * Haiku Depot: 1.3.0-5 yasm
* [x] zip : archivers/zip
  * Haiku Depot: 3.0-4 zip
* [ ] libc++abi.a : devel/wasi-libcxx
  * Haiku Depot: wasi N/A
* [ ] libc.a : devel/wasi-libc
  * Haiku Depot: wasi N/A
* [ ] libclang_rt.builtins-wasm32.a : devel/wasi-compiler-rt13
  * Haiku Depot: wasi N/A
* [ ] llvm13>0 : devel/llvm13
  * Haiku Depot: 12.0.1-5 llvm12 
  * Older than requirement version 13, may require packaging newer version, but try using this.
* [ ] rust-cbindgen>=0.24.3 : devel/rust-cbindgen
  * Haiku Depot: 0.20.0-1 cbindgen
  * Older than requirement version 0.24.3, may require packaging newer version, but try using this.
* [ ] rust>=1.68.0 : lang/rust
  * Haiku Depot: 1.67.0-1 rust-bin
  * Older than requirement version 1.68.0, may require packaging newer version, but try using this.
* [x] node : www/node
  * Haiku Depot: 16.11.1-1 nodejs16
* [x] libnotify>0 : devel/libnotify
  * Haiku Depot: 0.8.1-2 libnotify, libnotify_devel
  * Installed with very large dependencies (including gtk3)
* [ ] jack.h : audio/jack
  * Haiku Depot: N/A
  * Used by: cubeb
* [ ] pulseaudio.h : audio/pulseaudio
  * Haiku Depot: N/A
  * Used by: libwebrtc, cubeb
* [ ] sndio.h : audio/sndio
  * Haiku Depot: N/A
  * Used by: cubeb
* [x] gmake>=4.3 : devel/gmake
  * Haiku Depot: 4.1-5 make
  * Older than requirement version, may require packaging newer version, but try using this.
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
