# GITHUB-TIL 

(IDE : vscode)
## 원하는 로컬 디렉토리에 git 활성화.

```
user@DESKTOP-ABOICSH MINGW64 /c/TIL
$ git init
Initialized empty Git repository in C:/TIL/.git/
```

## 원격저장소 HTTPS 주소로 연결.

```
user@DESKTOP-ABOICSH MINGW64 /c/TIL (master)
$ git remote add origin "https://github.com/yu-je0ng/TIL.git"
```

## 로컬 저장소 파일 업로드.

```
user@DESKTOP-ABOICSH MINGW64 /c/TIL (master)
$ git add --all
```
```
user@DESKTOP-ABOICSH MINGW64 /c/TIL (master)
$ git commit -m "connect github"
[master (root-commit) 2c3eadd] connect github
 1 file changed, 17 insertions(+)
 create mode 100644 github.md
 ```

## [에러1] 
 ```
 user@DESKTOP-ABOICSH MINGW64 /c/TIL (master)
$ git push origin master
To https://github.com/yu-je0ng/TIL.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'https://github.com/yu-je0ng/TIL.git'      
hint: Updates were rejected because the remote contains work that you do      
hint: not have locally. This is usually caused by another repository pushing  
hint: to the same ref. You may want to first integrate the remote changes     
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details. 
```

**원인** : 원격 저장소에 있던 디렉토리를 사용하게 됨으로써 git pull을 먼저해야 했음.
    ( README.md 파일을 먼저 로컬에 저장해야됨.)

**해결** : 아래 명령어를 통해서 원격 저장소의 파일을 불러와 로컬 저장소의 파일을 동일하게 함.
```
git pull origin master
```

### [연관에러]
pull 명령 실행시 아래의 문구로 인해 진행되지 않으면
```
fatal: refusing to merge unrelated histories
```
다음 명령으로 실행해야 됨.
```
git pull origin master --allow-unrelated-histories
```

[관련 자료](https://gdtbgl93.tistory.com/63)
`--allow-unrelated-histories`
: 이 명령 옵션은 이미 존재하는 두 프로젝트의 기록(history)을 저장하는 드문 상황에 사용된다고 한다. 즉, git에서는 서로 관련 기록이 없는 이질적인 두 프로젝트를 병합할 때 기본적으로 거부하는데, 이것을 허용해 주는 것이다.

## [다시] 로컬 저장소 파일 업로드.

