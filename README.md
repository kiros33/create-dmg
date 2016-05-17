create-dmg
==========

간단한 스크립트로 DMG 파일을 만들 수 있습니다.
이 소스는 [andreyvit/create-dmg](https://github.com/andreyvit/create-dmg) 의 forked 버전입니다.

거의 개인용으로 사용중이기에 추가 설명이 필요하면 

[ImageMagick 다운로드] (http://www.imagemagick.org/script/binary-releases.php)

##1) ImageMagick 를 사용해서 기본 이미지에 년월일 정보를 추가해서 새로운 이미지를 만들어내고

설치용 배경이미지 생성(Applications 용 화살표 이미지 없음)
```bash
convert -font "/System/Library/Fonts/Helvetica.dfont" \
-fill white \
-draw "rectangle 30,1000 270,1040" \
-fill black \
-pointsize 24 \
-draw "text 40,1030 '$(date '+%Y/%m/%d %H:%M:%S')'" \
"${HOME}/Downloads/0000-DMG/background/background-001.png" \
"${HOME}/Downloads/0000-DMG/background/background-now.png"
```

복사용 배경이미지 생성
```bash
convert -font "/System/Library/Fonts/Helvetica.dfont" \
-fill white \
-draw "rectangle 30,1000 270,1040" \
-fill black \
-pointsize 24 \
-draw "text 40,1030 '$(date '+%Y/%m/%d %H:%M:%S')'" \
"${HOME}/Downloads/0000-DMG/background/background-002.png" \
"${HOME}/Downloads/0000-DMG/background/background-now.png"
```

##2) create-dmg 로 배경과 아이콘, 앱 등을 설정해서 dmg 이미지를 생성합니다.

설치용 dmg 생성
```bash
create-dmg \
--volname "Little Snitch 3.6.3" \
--volicon "/Users/kiros33/Downloads/0001-Done/Little Snitch 3.6.3/Little Snitch Installer.app/Contents/Resources/Little Snitch Installer.icns" \
--background "${HOME}/Downloads/0000-DMG/background/background-now.png" \
--window-pos 200 120 \
--window-size 800 550 \
--icon-size 100 \
--icon "serial.txt" 650 100 \
--hide-extension "serial.txt" \
--icon "Little Snitch Installer.app" 300 400 \
--hide-extension "Little Snitch Installer.app" \
--icon "Little Snitch Uninstaller.app" 120 400 \
--hide-extension "Little Snitch Uninstaller.app" \
"${HOME}/Downloads/Little Snitch 3.6.3 [K].dmg" \
"/Users/kiros33/Downloads/0001-Done/Little Snitch 3.6.3"
```

복사용 dmg 생성
```bash
create-dmg \
--volname "VMware Fusion 8.1.1" \
--volicon "/Users/kiros33/Downloads/0001-Done/VMware Fusion 8.1.1/VMware Fusion.app/Contents/Resources/fusion.icns" \
--background "${HOME}/Downloads/0000-DMG/background/background-now.png" \
--window-pos 200 120 \
--window-size 800 550 \
--icon-size 100 \
--icon "VMware Fusion.app" 650 100 \
--hide-extension "VMware Fusion.app" \
--icon "VMware Pro 8 [K]" 120 400 \
--hide-extension "VMware Pro 8 [K]" \
--icon "unlocker208.zip" 300 400 \
--hide-extension "unlocker208.zip" \
--app-drop-link 650 400 \
"${HOME}/Downloads/VMware Fusion 8.1.1 [K].dmg" \
"/Users/kiros33/Downloads/0001-Done/VMware Fusion 8.1.1"
```

아래는 원본 github의 설명입니다.
------------------------------

A shell script to build fancy DMGs.  


Status and contribution policy
------------------------------

This project is maintained thanks to the contributors who send pull requests. The original author has no use for the project, so his only role is reviewing and merging pull requests.

I will merge any pull request that adds something useful and does not break existing things.

Starting in January 2015, everyone who gets a pull request merged gets commit access to the repository.
  
  
Installation
------------
  
By being a shell script, yoursway-create-dmg installation is very simple. Simply download and run.  
  
> git clone https://github.com/andreyvit/yoursway-create-dmg.git  
> cd yoursway-create-dmg  
> ./create-dmg [options]  
  
  
Usage
-----
  
> create-dmg [options...] [output\_name.dmg] [source\_folder]  

All contents of source\_folder will be copied into the disk image.  
  
**Options:**  
  
*   **--volname [name]:** set volume name (displayed in the Finder sidebar and window title)  
*   **--volicon [icon.icns]:** set volume icon    
*   **--background [pic.png]:** set folder background image (provide png, gif, jpg)    
*   **--window-pos [x y]:** set position the folder window    
*   **--window-size [width height]:** set size of the folder window    
*   **--text-size [text size]:** set window text size (10-16)    
*   **--icon-size [icon size]:** set window icons size (up to 128)    
*   **--icon [file name] [x y]:** set position of the file's icon    
*   **--hide-extension [file name]:** hide the extension of file    
*   **--custom-icon [file name]/[custom icon]/[sample file] [x y]:** set position and custom icon    
*   **--app-drop-link [x y]:** make a drop link to Applications, at location x, y    
*   **--eula [eula file]:** attach a license file to the dmg    
*   **--no-internet-enable:** disable automatic mount&copy    
*   **--version:** show tool version number    
*   **-h, --help:** display the help  
  
  
Example
-------
  
> \#!/bin/sh  
> test -f Application-Installer.dmg && rm Application-Installer.dmg  
> create-dmg \  
> --volname "Application Installer" \  
> --volicon "application\_icon.icns" \  
> --background "installer\_background.png" \  
> --window-pos 200 120 \  
> --window-size 800 400 \  
> --icon-size 100 \  
> --icon Application.app 200 190 \  
> --hide-extension Application.app \  
> --app-drop-link 600 185 \  
> Application-Installer.dmg \  
> source\_folder/  


Alternatives
------------

* [node-appdmg](https://github.com/LinusU/node-appdmg)
* [dmgbuild](https://pypi.python.org/pypi/dmgbuild)
* see the [StackOverflow question](http://stackoverflow.com/questions/96882/how-do-i-create-a-nice-looking-dmg-for-mac-os-x-using-command-line-tools)
