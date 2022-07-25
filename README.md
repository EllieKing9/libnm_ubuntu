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
  
$gcc -Wall [file_name].c -o [excute_file_name] `pkg-config --cflags --libs libnm`   

$gcc -Wall [file_name].c -o [excute_file_name] `pkg-config --cflags --libs glib-2.0 dbus-glib-1 libnm-util libnm`

```

* for arm64
