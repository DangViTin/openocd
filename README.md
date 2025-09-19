# OpenOCD

1. Prepare **clean** MinGW, download and install MinGW at https://www.msys2.org/, download [OpenOCD_package.zip](OpenOCD_package.zip) in this Git.

2. Open MSYS2 MINGW32 terminal (the gray icon at **"C:\msys64\mingw32.exe”**), run update (terminal will close)
    
    ```bash
    pacman -Syuu
    ```
    
3. Open MSYS2 MINGW32 terminal again
    
    Go to OpenOCD package
    
    ```bash
    cd <Your_OpenOCD_Location>
    # cd /c/Data/OpenOCD_package/
    ```
    
    Install online packages
    
    ```bash
    pacman -S --disable-download-timeout --noconfirm --needed \
    git autoconf automake libtool make pkgconf unzip \
    mingw-w64-i686-toolchain \
    mingw-w64-i686-libusb-win32 \
    mingw-w64-i686-hidapi
    ```
    
    Install offline packages
    
    ```bash
    pacman -U --disable-download-timeout --noconfirm \
    mingw-w64-i686-libftdi-1.5-7-any.pkg.tar.zst \
    mingw-w64-i686-libusb-1.0.26-1-any.pkg.tar.zst \
    mingw-w64-i686-libjaylink-git-r175.cfccbc9-2-any.pkg.tar.zst
    ```
    
    Now we have 2 ways to install OpenOCD, using offline version (old version) or latest version on Github. Choose one.
    
    ```bash
    # Using offline version
    unzip openocd-0.12.0.zip
    cd openocd-0.12.0
    
    # Latest version on Git
    git clone --recursive https://github.com/DangViTin/openocd.git openocd
    cd openocd
    ./bootstrap
    ```
    
    Run full config.
    
    ```bash
    ./configure --disable-werror --disable-wextra --disable-gccwarnings --disable-doxygen-html --disable-doxygen-pdf --enable-internal-jimtcl
    ```
    
    Or fast build with only cmsis-dap support.
    
    ```bash
    ./configure --disable-werror --disable-wextra --disable-gccwarnings --disable-doxygen-html --disable-doxygen-pdf --enable-internal-jimtcl \
    --enable-cmsis-dap \
    --disable-ft232r \
    --disable-vsllink \
    --disable-ftdi \
    --disable-stlink \
    --disable-ti-icdi \
    --disable-ulink \
    --disable-usb_blaster \
    --disable-usb_blaster_2 \
    --disable-armjtagew \
    --disable-osbdm \
    --disable-opendous \
    --disable-amtjtagaccel \
    --disable-versaloon \
    --disable-usbprog \
    --disable-rlink \
    --disable-presto \
    --disable-openjtag \
    --disable-parport \
    --disable-buspirate \
    --disable-jlink \
    --disable-kitprog \
    --disable-nulink \
    --disable-xds110 \
    --disable-esp-usb-jtag \
    --disable-aice \
    --disable-remote-bitbang
    ```
    
    Then run make and install, wait for it to compile.
    
    ```bash
    make -j12 && make install
    ```
    
4. Finally, copy file into our folder
    
    ```bash
    mkdir -p ../OpenOCD_output/bin
    cp -r /c/msys64/mingw32/share/openocd/scripts/ ../OpenOCD_output/
    cp /c/msys64/mingw32/bin/openocd.exe ../OpenOCD_output/bin
    cp /c/msys64/mingw32/bin/libusb-1.0.dll ../OpenOCD_output/bin
    cp /c/msys64/mingw32/bin/libftdi1.dll ../OpenOCD_output/bin
    cp /c/msys64/mingw32/bin/libhidapi-0.dll ../OpenOCD_output/bin
    cp /c/msys64/mingw32/bin/libjaylink-0.dll ../OpenOCD_output/bin
    cp /c/msys64/mingw32/bin/libgcc_s_dw2-1.dll ../OpenOCD_output/bin
    cp /c/msys64/mingw32/bin/libwinpthread-1.dll ../OpenOCD_output/bin
    ```
    
5. If you missing any .dll file, find it at **C:\msys64\mingw32\bin** and copy it to OpenOCD_output/bin/
    
    

Useful package when needed:

[Index of /msys2/mingw/ | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/)

[Index of /msys2/mingw/mingw32/ | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/mingw32/)

[Index of /msys2/mingw/mingw64/ | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/mingw64/)