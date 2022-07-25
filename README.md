# Ubuntu에서 Network Manager 라이브러리 사용

* for amd64

https://packages.ubuntu.com/ (Ubuntu Packages Search)

```
$getconf LONG_BIT
  > 64 or 32 bit 확인
$dpkg --print-architecture
  > amd64(x86의 64비트 확장 아키텍쳐) or arm64 확인
$lsb_release -a
  > 리눅스 버젼 확인
  > 18.04(bionic), 20.04(focal), 22.04(jammy)
  
$sudo apt-get install libnm-dev
  > libnm-dev 종속 패키지: gir1.2-nm-1.0 | libglib2.0-dev | libnm0
  > 18.04 LTS(bionic)에서만 사용 가능한 패키지: libnm-util-dev
    > libnm-util-dev 종속 패키지: gir1.2-networkmanager-1.0 | libglib2.0-dev | libdbus-glib-1-dev | libnm-util2 | network-manager-dev

$sudo apt-get install libdbus-glib-1dev
  > 필요시
$sudo apt-get install network-manager-dev
  > 필요시
  
$apt list --installed | grep [package name]
  > 설치된 패키지 확인
  
$gcc -Wall [file_name].c -o [executable_file_name] `pkg-config --cflags --libs libnm`   

$gcc -Wall [file_name].c -o [executable_file_name] `pkg-config --cflags --libs glib-2.0 dbus-glib-1 libnm-util libnm`

```

* for arm64

```
$sudo dpkg --add-architecture arm64
  > 삭제는 
    > $sudo dpkg --remove-architecture arm64
    > $sudo apt-get remove --purge `dpkg --get-selections | grep armhf | awk '{print $1}'`
$sudo dpkg --print-foreign-architectures
  > arm64 아키텍쳐 추가 확인
$sudo apt-get update
$sudo nano /etc/apt/sources.list
  deb [arch=arm64] http://ports.ubuntu.com/ focal main multiverse universe
  deb [arch=arm64] http://ports.ubuntu.com/ focal-security main multiverse universe
  deb [arch=arm64] http://ports.ubuntu.com/ focal-backports main multiverse universe
  deb [arch=arm64] http://ports.ubuntu.com/ focal-updates main multiverse universe
  > sources.list에 arm64용 주소 추가
$sudo apt-get update
$sudo apt-get install libnm-dev:arm64

$sudo apt-get install libdbus-glib-1-dev:arm64
  > 필요시  

$sudo apt install binutils-aarch64-linux-gnu gcc-aarch64-linux-gnu
  > arm64용 컴파일러 설치
$sudo aarch64-linux-gnu-gcc --version
  > 설치 확인

$aarch64-linux-gnu-gcc -Wall [file_name].c -o [executable_file_name] `pkg-config --cflags --libs libnm`

$aarch64-linux-gnu-gcc -Wall wifi_scan.c -o scan_arm64 `pkg-config -I/usr/include/libnm -L/usr/lib/aarch64-linux-gnu -lnm libnm`

Windows _ cmd >pscp \\wsl$\...\[file] root@xxx.xxx.xxx.xxx:/mnt/[executable_file_name]
  > 타켓보드(arm64)로 파일 전송 및 실행 확인
    > $chmod +x [executable_file_name]
    > $./[executable_file_name] 
```
pscp는 https://github.com/EllieKing9/NFS#readme 참고
