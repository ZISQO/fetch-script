### createinstaller-scripts

#### fetch.py

이 스크립트는 Apple의 소프트웨어 업데이트 카탈로그를 이용해 사용 가능한 macOS 설치 프로그램이 포함된 디스크 이미지를 다운로드 받을 수 있도록 합니다

 `./fetch.py --help`를 이용해 사용가능한 옵션을 확인할 수 있습니다 

Fetch.py는 Apple의 소프트웨어 업데이트 서버(swdn)에서 패키지를 다운로드 한 다음, 새로운 빈 디스크에 이미지를 설치해 전체 이미지는 dmg 파일로 생성되며 이 파일 안에 "macOS 설치" app 파일을 생성합니다 

만약, 자신의 리얼맥 SMBIOS에서 지원하지 않는 OS를 설치하려고 할 경우 오류가 발생할 수 있습니다만, 이를 회피하기 위해선 오픈코어 부트로더를 EFI 폴더에 넣은 다음 새로운 OS에서 지원하는 SMBIOS로 Spoof를 설정해 불필요한 설치용 패치를 하지 않아도 됩니다 (현재 오픈코어 부트로 0.6.0의 경우 SMBIOS Spoof는 Generic 값의 3가지 값만 수정하면 손쉽게 타워형 MacPro5,1에서도 빅서를 설치할 수 있습니다) 

 `/usr/bin/installer` 과정에서 문제가 발생할 경우  `/var/log/install.log`경로의 로그 파일을 이용해 문제 분석을 하면 됩니다


#### createbootvolfromautonbi.py

(이 도구는 10.14 이전부터 테스트/업데이트되지 않았습니다 현재 버전의 macOS에서는 예상대로 작동하지 않을 수 있으며 업데이트 또한 예정되어 있지 않습니다)

autonbi의 출력에서 ​​부팅 가능한 디스크 볼륨을 만드는 도구이며 imagr 및 'SIP-ignoring'커널을 포함하는 부팅 가능한 디스크를 만드는 데 특히 유용합니다 특히 imagr은 SIP 상태에 영향을주는 스크립트를 실행하고 UAKEL 옵션을 설정하며 startosinstall구성 요소를 실행할 수 있습니다.

이를 통해 Imagr에서 사용하거나 필요로하는 Netboot 환경처럼 작동하는 부팅 가능한 외부 디스크를 생성 할 수 있습니다.

이 명령은 Imagr의 출력을 `make nbi`로 부팅 가능한 USB 디스크로 변환합니다
`sudo ./createbootvolfromautonbi.py --nbi ~/Desktop/10.13.6_Imagr.nbi --volume /Volumes/ExternalDisk`


#### make_firmwareupdater_pkg.sh

이 스크립트는 초기 High Sierra 설치 프로그램에서 펌웨어 업데이터를 추출하고 이미징을 통해 High Sierra를 설치하기 전에 Mac 펌웨어를 업그레이드하여 사용할 수있는 독립 실행형 설치 프로그램 패키지를 만드는 데 사용되었습니다만 High Sierra 설치 프로그램 변경으로 인해 이 스크립트가 손상되었습니다 Apple은 이미징을 통해 High Sierra를 설치하는 것이 권장되지 않으며 다른 대안도 제공되므로 이 도구를 수정하거나 업그레이드 할 계획은 없습니다

