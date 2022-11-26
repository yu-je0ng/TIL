# 모던 리눅스 관리

- 리눅스는 모든 작업이 일반 텍스트 파일로 이루어짐.

  - 파일 시스템 : 물리적 디스크의 식별할 수 있는 고유 위치에 저장된 데이터와 논리적 개념 단위인 파일을 연결하는 일종의 데이터 테이블이나 인덱스

    - 데이터를 신뢰성 있게 읽으려면 찾으려는 리소스를 일관되게 가리킬 수 있는 일종의 인덱스가 필요함.

    - 파일시스템은 이 인덱스를 이용해 파티션이라는 단일 디스크 분할 영역안에서 구성된 디렉터리와 파일들을 제공함.

    - 리눅스에서 상용되는 파일 시스템 : ext4

      - FAT32, NTFS 등 다른 플렛폼의 파일 시스템 사용 가능.

    - 디렉터리를 구성하는 방법 : 유닉스 파일 시스템 계층구조 표준(FHS, Filesystem Hierarchy standard)

      - | /           | 파일 시스템 최상위 디렉터리                                  |
        | ----------- | ------------------------------------------------------------ |
        | /bin, /sbin | 리눅스 핵심 명령어의 실행 파일<br /> /bin : 사용자 명령인 ls, cat, cp 등의 실행 파일 <br />/sbin : 부팅 과정에서 필요한 명령이나 관리자용 명령어인 fsck, shutdown 등의 실행 파일 |
        | /boot       | 리눅스가 부팅될때 필요한 파일 부트 로더 설정 파일, 커널 이미지 등 |
        | /dev        | 디바이스 드라이버들과 관련된 파일들을 저장하는 디바이스 디렉터리 모든 하드웨어는 이 디렉터리에 있는 파일을 통해 접근 가능 |
        | /etc        | 리눅스 시스템에서 가장 중요한 디렉터리 시스템 중요 환경 설정 파일, 서버 프로그램 설정 파일, 시스템 초기화 스크립트 등 |
        | /home       | 사용자 계정 홈 디렉터리                                      |
        | /lib        | /bin, /sbin에 있는 프로그램들이 의존하는 라이브러리 파일들   |
        | /media      | USB 메모리나 CD/DVD-ROM같은 탈부착이 가능한 저장 장치가 자동으로 마운트될 때 마운트 지점을 제공 |
        | /proc       | 커널이 사용하는 가상의 파일 시스템 메모리, CPU같은 시스템 자원 관련 정보, 실행 중인 프로세스 관련 정보, 커널 관련 정보 등 |
        | /root       | 루트 계정 디렉터리                                           |
        | /usr        | 리눅스 핵심 명령 외 대부분의 사용자 명령, 게임, X 윈도우 시스템, 온라인 매뉴얼 등 /usr/bin : 압축, 네트워크 관련 실행 파일 등 /usr/sbin : 이메일, 네트워크 관련 관리자용 명령 실행 파일 등 /usr/include : C, C++ 헤더 파일들 /usr/lib : /usr/bin, /usr/sbin에 있는 프로그램들이 의존하는 라이브러리 파일들 |
        | /var        | 시스템 운영 중에 필요한 가변 자료들 주로 시스템 운영 로그, 스풀 디렉터리, 임시 파일 등 메일 서버, 웹 서버, ftp 서버 운영 시에는 해당 하위 디렉터리에 사용자 메일박스, 웹 콘텐츠, 공유 파일을 기록하기 위해 사용 |

### 1.2.2 리눅스 탐색 도구

- **ls(리스트)**

```
ls -l

# 파일들이 차지하는 전체 디스크공간(MB단위) 출력
ls -lh
ls -h(== --human-readable)
# 현재 디렉터리에 포함된 하위 디렉터리와 파일 모두 나열
ls -R
```

- **pwd(현재 작업 디렉터리)**

-  **cd(디렉터리 변경)**

- **cat(파일 내용 출력)**
  - cat : '연결한다'라는 뜻의 concatenate에서 유래됨.

- **less(파일 내용 표시)**
  - 파일 내용을 조금씩 보여주어 텍스트 내용을 읽기 쉽게 해줌.


- **Note : bash는 유닉스에서 가장 인기 있는 셀**
  - 셀(shell) : 명령줄 인터페이스(CLI, Command-line Interface)나 그래픽 사용자 인터페이스(GUI, Graphical User Interface)로 제공되며, 사용자의 명령을 해석해 실행하는 일을 함.
    - 컴퓨터와 대화하는 창구의 역할.



### 1.2.3 리눅스 파일 관리 도구

- **touch(파일 생성)**

  - 파일 편집기
    - 워드 프로세서는 파일에 문서 형식을 위해 보이지 않는 마커(marker)들을 집어넣어 시스템 수준의 파일을 손상시킴.
    - 주로 사용하는 편집기 세가지 종류
      - GUI 환경 
        - **getdit**(우분투에서는 텍스트 편집기(text editor)이라고 함.)같은 **일반 텍스트 편집기** 
      - terminal session 
        - **nano**나 **Pico**처럼 직관적인 인터페이스를 제공하는 **명령줄 편집기**(command-line editor)
      - **vim**(원형인 vi 편집기)

- **stat(파일의 inode와 같은 자세한 정보 출력)**

  - 리눅스 파일 시스템의 모든 개체는 '**inode**'라는 고유한 메타데이터의 집합으로 표현됨.
    - 파일시스템의 인덱스는 드라이브의 inode에 연관된 메타데이터로부터 만들어짐.
    - inode : 파일 시스템 안에 있는 파일의 디스크 위치와 속성을 알기 위해 유닉스 시스템이 사용하는 개체
  - stat 명령
    - 파일명, 속성, 타임스템프뿐만 아니라 inode ID 번호도 보여줌.

- **rm(rmdir) -r(--ignore-fail-on-non-emty)**

  - **-r**  : 하위에 폴더나 디렉토리가 있어도 해당 디렉터리 지움.
    - rm이나 rmdir 사용시 복구 불가능함.

- **cp file1 newdir**

  - "file1 파일을 newdir 디렉터리에 복사함."
  - 파일이나 디렉터리 사본을 생성.

- **mv file? /some/other/dir/**

  - ""파일명이 file이거나 file 뒤에 문자가 하나 거 있는 파일 모두를 대상 디렉토리로 이동함."
  - 파일을 한 장소에서 다른 장소로 옮김.
  - 하위 디렉터리도 모두 함께 이동함.
  - mvnewfile 파일이 없을 때 
    - `mv myfile mynewfilw ` : 파일명을 myfile에서 mynewfile로 바꿈.



- **파일 글로빙(globbing)**

  - 명령이 처리할 파일명에 와일드카드 문자를 적용하는 것을 말함.

  ```
  # 현재 디렉토리에 있는 내용을 모두 다른 위치로 옮기고 싶을 때.
  mv * /some/other/directory/
  
  # 파일명에 어떤 문자열이 있는 파일만 옮기고 싶을 때
  mv file* /some/other/directory/
  
  # file1에서 file15인 파일들이 있을때 file1에서 file9까지만 옮기고 싶을 때
  mv file? /some/other/directory/
  ```

  - 물음표는 임의의 문자 하나에 대응되므로 `file?`명령어는 file 뒤에 문자가 하나만 있는 파일들에만 명령이 적용되고 file10에서 file15는 현재 디렉터리에 그대로 둠.



### 1.2.5 의사 파일 시스템

- 일반적인 파일은 시스템을 재부팅하고 나서도 계속해서 안정적으로 접근할 수 있는 데이터의 집합임.

- **sys나 proc등의 디렉터리에 있는 리눅스 의사 파일(pseudo file 또는 virtual file)의 내용은 시스템의 특정 상태를 보여주고자 OS에서 동적으로 생성함.**

  - 예시) sda로 지정한 디스크에 저장된 파일들이 사용하는 공간을 확인.

    ```
    cat /sys/block/sda/size
    ```

- 의사 파일 시스템

  - 리눅스는 의사 파일 시스템을 사용해 프로세스와 사용자에게 하드웨어 환경 데이터를 보여줌.
  
  - 시스템이 부팅될 때나 부팅 후에 자동으로 생성되는 동적 데이터를 담은 파일들이 들어 있는 디렉터리.

- **Note : 저장장치**

  - 시스템에서 지정한 첫번째 저장장치가 /dev/sda/면 두번째 장치는 /dev/sdb, 세번째는 /dev/sdc/라고 추축가능함.
    - 원래 sda는 SCSI Device A를 나타냄.(Storage Device A)
  - 시스템에 따라 /dev/hda/(하드 디스크 드라이브), /dev/sr0/(DVD 드라이브), /dev/cdrom/(CD-ROM 드라이브), /dev/fd0/(플로피 디스크 드라이브)등의 장치명을 지정할 수 있음.

- 리눅스는 연결된 저장 장치들을 블록장치(block device)로 분류하므로 /sys/block/ 디렉터리로 이동해 확인 가능.

  - sda 디렉터리 : 시스템을 부팅하는데 사용하는 첫 번째 드라이브

    ```
    cd sda
    ls
    # sda1, sda2, sda5 같은 이름이 출력됨.
    # 해당 파일들은 리눅스가 드라이브의 데이터를 더욱 효율적으로 관리하고자 만든 디스크 파티션을 나타냄.
    ```

    

## 1.3 도움말

### 1.3.1 맨 페이지

- 리눅스 프로그램을 설치할 때 대부분 맨 페이지 파일도 설치됨.

- 알고 있는 명령어의 쓰임새를 알고 싶을 때

  - man 뒤에 알고 싶은 명령을 입력하면 해당 명령의 맨 페이지를 보여줌.

  ```
  man man
  
  # sudo 명령어 사용에 관련된 메뉴얼 문서를 보여줌.
  man sudo
  ```

### 1.3.2 Info

- 명령 이름을 모를 때

  ```
  info
  ```

  - 설치

    ```
    sudo apt install info
    ```

### 1.3.3 인터넷

#### 시스템 로그에서 오류 정보 가져오기

- `journalctl` : 우분투 14.04 이후에 나온 대부분의 리눅스 배포판에서 사용 가능.

  - 모든 시스템 로그에 접근.
  - 굉장히 많은 로그 데이터 출력됨.

- `grep` : 찾고자 하는 정보를 걸러내는 방법.

  ```
  journalctl | grep filename.php
  ```

  - `파이프 문자(|)`는 어떤 명령(예제에서는 journalctl)의 출력을 다른 명령(grep)의 입력으로 연결함. (shift + \\)

    ```
    # filename.php에 대한 저널 항목 중 'error'단어가 포함된 줄만 출력.
    journalctl | grep filename.php | grep error
    
    # filename.php에 대한 저널 항목 중 'error'단어가 없는 줄만 출력.
    journalctl | grep filename.php | grep -v error
    ```


### 2.4.1 요약

- 버추얼박스 같은 하이퍼바이저들은 가상 OS가 하드웨어 리소스에 안전하게 접근할 수 있는 환경을 제공하지만, 경량 컨테이너들은 호스트의 소프트웨어 커널을 공유함.
- APT나 RPM(Yum)같은 리눅스 패키지 관리자는 원격 저장소의 상태를 미러링한 인덱스를 주기적으로 업데이트함으로써 온라인 저장소에서 소프트웨어를 가져와 설치하고 관리함.

### 2.4.2 핵심용어

- **가상화(virtualization)** : 여러 프로세스 간에 연산, 저장공간, 네트워킹 리소스를 논리적으로 공유함으로써 마치 물리적으로 컴퓨터 환경처럼 각 프로세스를 실행할 수 있게 함.
- **하이퍼바이저(hypervisor)** : 시스템 리소스를 게스트 계층에 제공하고자 호스트 컴퓨터에서 실행되는 소프트웨어로, 완전한 컴퓨터 구조를 갖춘 게스트 VM을 실행하고 관리함.
- **컨테이너(Container)** : 완전한 컴퓨터 구조 대신 호스트 컴퓨터의 핵심 OS 커널 위에서 실행되는 VM으로, 단기적 요구에 맞춰 간단히 실해하고 종료할 수 있음.

#### 관리자 셸 실행

```
sudo su
```



## 3.1 암호화의 중요성

- 과거 네트워크를 통해 원격으로 로그인할 수 있는 텔넷(telnet)이 존재했음.
  - 텔넷 프로토콜 : 빠르고 신뢰성있으며 규모가 작고 단순한 네트워크에서 용이했음.
    - 텔넷 세션이 데이터 패킷을 암호화하지 않고 전송하는 것이 문제가 되었음.

- SSH는 1990년대에 유닉스 계열 OS에서 원격 로그인할 때 전송되는 데이터를 안전하게 암호화하려고 만들어짐.
  - 이 프로토콜을 구현한 OpenSSH

#### OpenSSH설치

```
# 설치
apt install openssh-server


# 실행 확인
systemctl status ssh
# 시스템 부팅시 자동 실행(활성화-enable/ 비활성화-disable)
systemctl enable ssh
```

- openssh-client 
  - 로컬 PC(클라이언트) openssh-client패키지로 원격 서버에 로그인.
- openssh-server
  - 원격 서버 openssh-server패키지로 로그인 세션 처리

#### OpenSSH 환경 설정 파일

```
/etc/ssh/
```

- 원격 클라이언트(remote client)가 컴퓨터에 로그인하는 방법을 제어하는 설정
  - /etc/ssh/sshd_config
- 해당 컴퓨터의 사용자가 원격 호스트(remote host)에 클라이언트로서 로그인하는 방법을 제어하는 설정
  - /etc/ssh/ssh_config 
- 해당 파일들에 정의된 설정들은 컴퓨터에서 사용자가 로그인하는 방법을 SSH로 제어하는 것외에도 원격에서 로컬 프로그램들에 대한 GUI 접근을 허용할 것인지를 제어하는데 사용됨.



#### 패키지 정보 확인

```
# 설치된 패키지 확인.
dpkg -s <패키지명>

# 아직 설치되지 않은 패키지 정보 확인.
apt search <패키지명>
```

- 우분투/데비안 : 어떤 패키지들이 설치되어 있는지 dpkg 패키지 관리자로 확인할 수 있음.
  - 명령줄 도구인 dpkg는 APT 시스템에 속한 소프트웨어 패키지들을 관리하고 상태를 확인함.

#### IP 주소 확인

```
# 컴퓨터에 있는 네트워크 인터페이스를 모두 나열함.
ip addr
...
inet 10.0.3.114
```

#### 서버에 접속

```
ssh <로그인계정>@<서버IP주소>
ssh ubuntu@10.0.0.114

# 서버 통신 가능 여부 확인.
ping 서버IP
ping 10.0.3.114
```

- ping 요청 실패시.

  ```
  ping 10.0.3.145
  PING ...
  From ... ... ... Host Unreachable #ping 요청에 대한 실패 응답 기록
  ```

  

## 3.4 패스워드 없이 ssh 접근하기.

- 특별한 키 쌍을 생성한 다음 로그인하려는 원격 호스트에 공개 키를 복사화는 방법

- 클라이언트 컴퓨터에서 `ssh-keygen`프로그램으로 공개 키와 개인 키 쌍을 생성함.

  - RSA 암호 알고리즘에 기반을 둔 키 쌍 생성됨.

    ```
    ubuntu@ubuntu:~$ ssh-keygen
    ubuntu@ubuntu:~$ ls -l .ssh
    total 16
    -rw-rw-r-- 1 ubuntu ubuntu  567 Nov 13 14:55 authorized_keys
    -rw------- 1 ubuntu ubuntu 2602 Nov 13 14:55 id_rsa
    -rw-r--r-- 1 ubuntu ubuntu  567 Nov 13 14:55 id_rsa.pub
    -rw-r--r-- 1 ubuntu ubuntu  222 Nov 13 15:44 known_hosts
    ```

  - 공개 키는 생성하고 나면 호스트의 .sshauthorized_keys 파일로 복사 가능함.

    - 공개 키가 있어야 클라이언트에서 개인 키로 서명한 암호 메시지가 진짜인지 호스트에서 실행되는 openssh가 검증할 수 있기 때문.
    - 메시지가 검증되면 ssh 세션이 시작됨.

- 원격 호스트에서 ssh셀 세션을 열지 않고 명령 수행하는 방법

  ```
  # 10.0.3.142서버에 .ssh 디렉토리 생성.
  ubuntu@ubuntu:~$ ssh ubuntu@10.0.3.142 mkdir -p .ssh
  ubuntu@10.0.3.142's passhword:
  
  # 공개키 10.0.3.142서버에 전송.
  ubuntu@ubuntu:~$ cat .ssh/id_rsa.pub \
  | ssh ubuntu@10.0.3.142 \
  "cat >> .ssh/authorized_keys"
  ubuntu@10.0.3.142's passhword:
  ```

  - cat으로 id_rsa.pub 파일에 있는 텍스트를 모두 읽어 이를 메모리에 저장한다. 그리고 원격 호스트에 SSH로 로그인해서 해당 텍스트를 파이프*로 전달한다. 마지막으로 원격 호스트에서 텍스트를 다시 읽고 이를 authorized_keys라는 파일에 추가한다.

    - 이때 해당 파일이 없으면 추가도구(>>)는 이 파일을 생성하고, 파일이 있으면 파일에 텍스트를 추가한다.
    - 파이프*(|)를 이용해 명령 간 데이터를 전달가능함.

  - 해당 작업이 완료되면 기존 ssh 명령을 실행할 때 패스워드를 입력하지 않아도 됨.

    

#### 다중 암호화 키 이용하기

- AWS EC2 서비스

  ```
  ssh -i .ssh/mykey.pem ubuntu@10.0.3.142
  ```

  - .pem : aws ec2 인스턴스처럼 다양한 vm에 접근할 때 사용되는 형식.
    - 키가 저장되었음을 의미함.

  

## 3.5 scp로 안전하게 파일 복사하기.

- cp 사용시 네트워크 로그 데이터 검색시 파일 내용이 노출됨.

- s(secure) + cp : 보안을 지원하는 SCP 프로그램 사용.

  - SCP 프로그램은 파일 전송을 위해 SSH 프로토콜을 상용해 어떤 파일이라도 동일한 키와 패스워드, 패스프레이즈(passphrase)로 복사할 수 있음.

    ```
    # 공개키를 authorized_keys라는 다른 이름으로 바꿔 원격 호스트에 복사
    scp .ssh/id_rsa.pub ubuntu@10.0.3.142:/home/ubuntu/.ssh/authorized_keys
    ```

    - 패스워드는 일반적인 문자열이나, 패스프레이즈에는 공백과 구두점도 포함됨.

- 키를 원격 호스트에 안전하게 복사하는 공식적인 방법

  - ssh-copy-id

    ```
    ssh-copy-id -i .ssh/id_rsa.pub ubuntu@10.0.3.142
    # 공개키를 원격 호스트의 적절한 곳에 자동으로 복사함.
    ```



#### ssh 터널링(tunneling)

- 원격 HTTP 서비스를 안전하고 비밀리에 사용할 수 있도록 포트포워딩(port forwarding)할 수 있음.



## 3.7 리눅스 프로세스 관리하기

- **소프트웨어** : 사람을 대신해 컴퓨터 하드웨어를 제어하는 명령을 담은 프로그램 코드
- **프로세스** : 실행 중인 소프트웨어 프로그램의 인스턴스
- **OS** : 컴퓨터 하드웨어 리소스를 효율적으로 사용하고자 인스턴스들(즉, 프로세스들)을 정리하고 관리하는 도구.
- **systemctl** : 시스템 서비스의 가용성과 응답성은 systemd의 systemctl 프로세스 관리자가 관리함.
- **ps** : 실행 중인 프로세스들에 대한 정보를 보여줌.
- **pstree -p** : 부모와 자식 셸/프로세스를 시각화해서 보여줌.
  - systemd(1) : 최상위 프로세스
  - 부모 셸(parent shell)은 자식 셸을 실행하고 이 셸로 프로그램을 실행할 수 있는 셸 환경.
  - 최상위 셸은 리눅스가 부팅될 때 실행되는 셸.
  - **셸(shell)** : bash처럼 사용자가 명령을 실행할 수 있게 하는 명령줄 인터프리터를 제공하는 터미널 환경.
    - 셸 자체도 하나의 프로세스임.

```
# 10초 동안 백그라운드(&)에서 아무것도 하지 않고 있다가(sleep) 종료하는 명령어
ubuntu@ubuntu:~$ for i in {1..10}; do sleep 1; done &
[1] 2901

ubuntu@ubuntu:~$ ps
    PID TTY          TIME CMD
   2793 pts/0    00:00:00 bash
   2901 pts/0    00:00:00 bash
   2903 pts/0    00:00:00 sleep
   2904 pts/0    00:00:00 ps
...

ubuntu@ubuntu:~$ ps
    PID TTY          TIME CMD
   2793 pts/0    00:00:00 bash
   2913 pts/0    00:00:00 ps
[1]+  Done                    for i in {1..10};
do
    sleep 1;
done
...

ubuntu@ubuntu:~$ ps
    PID TTY          TIME CMD
   2793 pts/0    00:00:00 bash
   2914 pts/0    00:00:00 ps
```

```
ubuntu@ubuntu:~$ ps -ef | grep init
root           1       0  0 21:06 ?        00:00:14 /sbin/init auto noprompt
ubuntu      2917    2793  0 21:46 pts/0    00:00:00 grep --color=auto init
```

- grep으로 데이터 스트림을 걸러낼 수 있음.

```
ubuntu@ubuntu:~$ pstree -p
systemd(1)─┬─ModemManager(906)─┬─{ModemManager}(933)
           │                   └─{ModemManager}(945)
           ├─NetworkManager(822)─┬─{NetworkManager}(937)
           │                     └─{NetworkManager}(940)
           ├─VGAuthService(788)
           ├─accounts-daemon(810)─┬─{accounts-daemon}(820)
           │                      └─{accounts-daemon}(834)
           ├─acpid(811)
           ├─avahi-daemon(815)───avahi-daemon(896)
           ├─bluetoothd(816)
           ├─colord(2172)─┬─{colord}(2173)
           │              └─{colord}(2176)
           ├─cron(818)
           ├─cups-browsed(914)─┬─{cups-browsed}(958)
           │                   └─{cups-browsed}(959)
           ├─cupsd(819)
           ├─dbus-daemon(821)
...
```



### 3.7.2 systemd

- 오랫동안 모든 유닉스 기반 OS에서는 부팅 과정에서 처음 실행하는 프로세스로  init을 사용해왔으나, 이를 systemd가 대체함.
  - 대체(drop-in replacement)는 실제로 수행하는 작업은 다르나, init이 해왔던 일을 systemd가 대신한다는 의미.
  - /sbin/init 파일은 현재 systemd 프로그램에 대한 심볼릭 링크로서 존재함.
- 시스템 관리 작업을 하는데 systemd를 사용하지 않고 systemctl을 사용함.
  - systemd의 주요 임무는 개별 프로세스를 생성하고, 유지하고, 종료하는 방법을 제어하는 것.
  - systemctl 명령은 이런 작업에 주로 사용되는 도구이나, systemd 개발자는 전통적인 프로세스 관리 기능을 확대해 다양한 시스템 서비스에도 적용하고 있음.
    - systemd 체제에 로그관리자(journald), 네트워크 관리자(nerworkd), 장치관리자(udevd)등의 도구들이 포함되어 있음.
    - 관리자 이름 : -d로 끝나는데 백그라운드에서 실행되는 시스템 프로세스인 데몬(daemon)을 나타냄.







## 9.2 네트워크 접근 제어하기

### 9.2.1 방화벽 설정하기

#### 주요 용어


- **하이퍼텍스트 전송 프로토콜(HTTP, Hypertext Transfer Protocal)**

  - 네트워크에서 웹 클라이언트와 웹 서버간의 리소스 교환을 중재한다. 예를 들어, 브라우저가 하이퍼텍스트 마크업 언어(HTML, Hypertext Markup Language)로 작성된 웹 페이지를 요청하면 웹 서버가 해당 페이지 내용을 전송한다.

- **메타데이터(Matadata)**

  - 세션 상태에 대한 정보가 들어있다. 데이터를 전송할 때마다 생성되고 이 정보는 나중에 관리자가 문제를 해결하는데 사용된다.

- **전송 계층 보안(TLS, Transport Layer Security)**

  - HTTPS는 TLS 프로토콜로 암호화된 데이터를 안전하게 전송한다.

- **패킷(packet)**

  - 큰 데이터 파일이나 아카이브에서 전송하기 전에 떼어낸 조그만 데이터 단위다.
  - 전송받은 쪽에서는 패킷으로 원래 파일을 다시 조립할 수 있다.


- **전송 제어 프로토콜(TCP, Transmission Control Protocol)**
  - 네트워크에서 데이터 전송에 TCP를 사용하면 수신된 패킷에 오류가 있는지 확인하고 필요하면 패킷을 재전송한다.
- **사용자 데이터그램 프로토콜(UDP, User Datagram Protocol)**
  - TCP보다 약간 더 빠르지만, 오류를 검사하고 정정하지 않으므로 오류가 발생해도 어느정도 견딜 수 있는 서비스에 사용된다.

- **프로토콜(Protocol)**
  - 컴퓨터들 간의 원활한 통신을 위해 지키기로 약속한 규약. 
  - 프로토콜에는 신호 처리법, 오류처리, 암호, 인증, 주소 등을 포함한다.

- **라우터**
  - 여러 가지 네트워크를 묶어서 교통정리를 해주는 장비를 라우터라 부른다.
- **게이트웨이**
  - 하나의 네트워크를 벗어나 다른 네트워크에 접속하는 장비를 게이트웨이라고 부른다. 
  - 무선 네트워크를 유선 네트워크에 연결시켜 주는 유무선 인터넷 공유기도 넓게 보면 게이트웨이이며 또한 라우터이다.
- **MQTT**
  - 초경량 통신 프로토콜. 사물인터넷에 최적화 되어 있다.
- **방화벽**
  - 네트워크 규칙의 집합
  - 데이터 패킷이 네트워크 공간으로 들어오거나 나갈때 패킷의 내용(출발지, 목적지, 프로토콜)을 방화벽 규칙에 따라 검사해 이 패킷을 통과시킬지 결정함.
  - 리눅스 컴퓨터는 `iptables`라는 프로그램으로 커널 수준에서 방화벽 규칙을 적용할 수 있음.
    - 많은 리눅스 배포판에서는 이보다 쉽고 편리한 도구를 제공함.
    - CentOS의 `firewalld`와 우분투의 `UFW(Uncomplicated Firewall)`



#### firewalld

- firewalld 는 systemd의 일부임.

  - 데비안/우분투에서 선택적으로 설치되나 레드헷이나 CentOS에는 기본으로 설치됨.

- **우분투에서 설치하는 명령어**

  ```
  apt updata
  apt install firewalld
  
  # firewalld 설정 관리(--state : 방화벽의 현재 상태 확인)
  firewall-cmd --state
  ```

- **웹 서버를 열기 위한 HTTP와 HTTPS 포트 열기**

  - `--add-port` 네트워크 프로토콜과 포트번호 직접 입력

    ```
    firewall-cmd --permanet --add-port=80/tcp
    firewall-cmd --permanet --add-port=443/tcp
    
    # 변경된 규칙 적용
    firewall-cmd --reload
    ```

    - `--permanet` : 서버가 부팅될 때마다 firewalld가 이 규칙을 로드함.

  - `--add-service` 서비스 지정

    ```
    firewall-cmd --permanet --add-service=http
    firewall-cmd --permanet --add-service=https
    
    # 현재 방화벽 설정 확인
    firewall-cmd --list-services
    ```

- **기존에 열려 있던 SSH 세션 제거**

  ```
  firewall-cmd --permanet --remove-service=ssh
  firewall-cmd --reload
  ```

  - ssh 세션에서 방화벽 규칙 변경시 주의해야 됨.
    - 사용해야 하는 세션 자체도 막아버리려 아예 서버에 접근할 수 없게 될 수 있음.

- **지정한 IP만 접근 허용**

  ```
  # IP주소가 192.168.1.5이고 22번 포트로 들어오는 TCP 트래픽만을 허용하는 규칙을 추가.
  firewall-cmd --add-rich-rule='rule family="ipv4" \
  source address="192.168.1.5" port protocol="tcp" port="22" accept'
  ```

  - 22번 포트 : SSH가 기본으로 사용하는 포트
  - `--add-rich-rule` : 부유언어 집합으로 규칙을 정하겠다고 firewall-cmd에 알려주는 인자.
    - 부유언어(rich language) : 복잡한 방화벽 규칙을 간단히 생성하려고 설계된 고급 언어
      -  공식문서 : http://mng.bz/872B

  

#### UFW

- 우분투 설치

  ```
  apt install ufw
  ```

- ufw는 기본적으로 모든 포트를 막고 시작하므로 ufw를 활성화하면 ssh 세션을 새로 열지 못할 수 있음.

  - ufw에 ssh를 허용하는 규칙 추가

    ```
    ufw allow ssh #ssh 비활성화 : ufw deny ssh
    ufw enable # 방화벽을 시작한다 (ufw 비활성화 : ufw disable)
    ```

  - IPV6 지원 활성화시 오류 가능성 높음.

    ```
    # /etc/default/ufw
    ...
    IPV6=no 
    ```

    - IPV6의 값을 yes에서 no로 바꾸면 IPv6가 비활성화되고 UFW 오류가 생기지 않음.

- **웹 서버에 대한 HTTP와 HTTPS 접근 허용**

  ```
  ufw allow 80
  ufw allow 443
  ```

  ```
  ufw status
  Status: active
  To				Action	From
  --				------	----
  80				ALLOW	Anywhere
  22				ALLOW	Anywhere
  443				ALLOW	Anywhere
  ```

- **특정 IP에서만 접근 허용**

  ```
  # 규칙 변경전 ufw 비활성화
  ufw disable
  # ufw status 명령으로  나열되는 두번째 방화벽 규칙 제거
  ufw delete 2
  # 지정된 IP주소에서 오는 SSH 트래픽만 허용
  ufw allow from 10.0.3.1 to any port 22
  
  ufw enable
  ufw statua
  Status: active
  To				Action	From
  --				------	----
  80				ALLOW	Anywhere
  443				ALLOW	Anywhere
  22				ALLOW	10.0.3.1 # 지정된 IP주소에서 들어오는 SSH 트래픽만 허용하는 새규칙
  ```

- **TCP 프로토콜 사용**

  ```
  ufw allow 53987/tcp
  # 52900과 53000 사이의 포트 모두 열기.
  ufw allow 52900:53000/tcp
  ```

#### 네트워크 포트

- 네트워크 포트는 총 65,535개가 있으며 다음과 같이 세 가지 범주로 나뉨.
  - **잘 알려진 포트(well-known port) : 1 ~ 1023**
    - SSH(22)나 HTTP(80)처럼 잘 알려진 서비스를 위해 예약된 포트
    - 직접 개발할 애플리케이션에 이 포트를 사용하면 충돌 문제가 발생할 수 있음.
  - **등록된 포트(registered port) : 1024 ~ 49151**
    - 표준으로 채택된 것은 아니지만, 기업이나 기관에서 자신들의 애플리케이션에 사용하고자 할당을 요청한 포트들이 포함됨.
    - 예를 들어, RADIUS 인증 프로토콜에는 1812번, MySQL에는 3306번이 지정되어 있음.
  - **동적 포트(dynamic port) : 47152 ~ 65535**
    - 등록되지 않은 포트로 동적 할당 가능함.
    - 이 범위의 포트들은 사설 네트워크에서 임의로 사용할 수 있으며, 잘 알려진 애플리케이션이나 서비스와 충돌하지 않는다고 확신할 수 있음.



## 11.1 시스템 로그 이용하기

- 로그 항목(log entry) : 시스템 이벤트에 대한 텍스트 형태의 기록.
- 로깅(logging) : 로그 항목을 남기는 행위.
- 수십 년간 리눅스 로깅은 syslogd 데몬이 관리해왔음.
  - syslogd는 시스템 프로세스와 애플리케이션들이 /dev/log 가상 장치로 보낸 로그 메시지를 수집한 뒤 메시지를 /var/log/ 디렉터리에 있는 적절한 평문 로그 파일에 저장함.
  - 각 메시지에는 메타데이터 필드를 담은 헤더(타임스탬프, 메시지 출력, 우선순위)가 있어 syslogd는 각 메시지를 어디에 저장할지 알 수 있었음.
- 최근 journald가 이를 대신하고 있음.
  - 평문 텍스트가 아닌 이진 파일에 로그를 저장함.
  - syslogd 로그를 포함해 journald 로그는 journalctl 명령줄 도구로 사용함.
  - syslogd 사라지지 않았으며 여전히 대부분의 전통적인 로그는 /var/log에 남고 있음.

### 11.1.1 journald로 로깅하기

#### journalctl

- 현재 시스템에 저장된 오래된 로그부터 모두 출력됨.
- `journalctl -n 20` : 최근 항목 20개만 출력됨.
- `journalctl -p emerg` : 긴급(emergency)으로 분류된 로그만 출력됨.
  - 이 외에도 `debug`, `info`, `notice`, `warning`, `err`, `crit`, `alert` 메시지를 필터링할 수 있음.
- `journalctl -f`
  - `-f` 플래스를 추가하면 최근 항목 10개와 그 후에 생성된 항목들을 보여줌. 즉, 이벤트를 실시간으로 감시할 수있음.

- `journalctl --since 15:50:00 --until 15:52:00`
  - 원하는 시간대의 로그 필터링 가능함.



### 11.1.2 syslogd로 로깅하기

- syslogd 시스템에서 이벤트가 생성한 로그는 모두 /var/log/syslog 파일에 추가됨.

  - 로그의 특성에 따라 같은 디렉터리의 다른 파일에도 저장할 수 있음.

  - syslogd로 로그 메시지를 분산시키는 방법은 /etc/rsyslog.d/ 디렉터리의 50-default.conf 파일에서 결정됨.

    ```
    # /etc/rsyslog.d/50-default.conf
    # cron 관련 로그 메시지들은 cron.log 파일에 저장됨.
    cron.*	/var/log/cron.log
    ```

    

#### 많이 사용되는 syslogd 파일들

| 파일명   | 용도                                       |
| -------- | ------------------------------------------ |
| auth.log | 시스템 인증과 보안 이벤트                  |
| boot.log | 부팅 관련 이벤트 기록                      |
| dmesg    | 장치 드라이버 관련 커널링 버퍼 이벤트      |
| dpkg.log | 소프트웨어 패키지 관리 이벤트              |
| kern.log | 리눅스 커널 이벤트                         |
| syslog   | 모든 로그 모음                             |
| wtmp     | 사용자 세션 추적(who와 last 명령으로 접근) |

- 각 애플리케이은 자신만의 고유한 로그 파일에 이벤트를 저장하기도 함.
  - 예시) /var/log/mysql , /var/log/apache2



## 11.2 로그 파일 관리하기

### 11.2.1 journald 방식

- 저장 공간 제한

  - /etc/systemd/journald.conf 파일
    - SystemMaxUse 와 RuntimeMaxUse 를 시스템 환경에 따라 선택하여 조정.

- journald는 기본으로 로그를 /run/log/journal 파일에 쌓고 보관

  - 휘발성 파일로 시스템이 부팅될 때마가 자동으로 삭제됨.

  - /var/log/journal 디렉토리에 영구 저장 명령 가능함.

    ```
    mkdir /var/log/journal
    systemd-tmpfiles --create --prefix /var/log/journal
    ```

    

## 13.1 CPU 부하 문제

- 시스템(system) : 서비스를 제공하는 데 사용하는 하드웨어와 소프트웨어 환경을 말하며, 애플리케이션, 데이터베이스, 웹 서버 또는 간단한 독립형 워크스테이션 등이 이에 포함됨.
  - 시스템의 4대 요소
    - 중앙처리 장치(CPU)
    - 메모리(RAM과 가상 메모리)
    - 저장장치
    - 네트워크(의 부하 관리)

### 13.1.1 CPU 부하 측정하기

- CPU 상태는 CPU부하와 CPU 이용률로 파악함.
  - CPU부하 (CPU load) 
    - 최대 처리 용량 대비 CPU가 수행하는 작업량(현재 활성화되고 큐에 들어가 있는 프로세스 수)의 비를 백분율로 나타낸 것.
    - 평균 부하는 일정 시간의 시스템 활동을 나타내므로 시스템 상태를 좀 거 정확히 보여주는 좋은 지표임.
  - CPU 이용률(CPU utilization)
    - 최대 처리 용량 대비 CPU가 유휴 상태(idle)가 아닌 시간의 비를 백분율로 나타낸 것.
- 싱글 코어 CPU에서 CPU 부하 점수 1점은 CPU가 100% 사용됨을 나타냄.
  - 쿼드 코어 CPU에서는 부하 점수 4가 최대 용량을 나타냄.
  - 일단 CPU 이용률이 75%를 넘어가면 사용자가 속도 저하를 느끼기 시작함.
    - 이때 CPU 부하 점수는 싱글코어에서 0.75, 쿼드 코어에서는 3임.

#### uptime

- 현재시간, 최근 시스템 부팅 후 경과시간, 현재 로그인한 사용자 수, 가장 중요한 지난 1분간, 5분간, 15분간의 평균 부하를 보여줌.

  ```
  ubuntu@ubuntu:~$ uptime
   20:25:41 up 2 min,  1 user,  load average: 3.83, 1.83, 0.71
  ```

  - 싱글 코어 CPU의 평균 부하 1.27은 CPU가 평균적으로 최대 용량을 사용하고 있는 프로세스의 27%가 CPU를 사용하려고 대기하고 있음을 의미함.
    - 이와 반대로 CPU가 하나인 시스템에서 평균부하 0.27은 평균적으로 CPU가 해당 시간의 73%동안 사용되지 않았음을 의미함.
  - 쿼드 코어 CPU의 평균부하가 2.1이면 최대 용량의 50% 약간 넘게 사용됨을 나타냄.
    - 해당 시간의 52%동안 놀고 있었다는 의미.

#### 코어 수 확인

```
# CPU 코어 전체 개수를 확인
ubuntu@ubuntu:~$ grep -c processor /proc/cpuinfo
2

ubuntu@ubuntu:~$ cat /proc/cpuinfo | grep processor
processor	: 0
processor	: 1

# CPU에 대한 전체 정보 확인
cat /proc/cpuinfo
```



### 13.1.2 CPU 부하관리하기

