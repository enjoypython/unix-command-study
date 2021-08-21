# Unix Command 학습정리
> Ubuntu 로 명령어 공부하면서 정리한 노트

<br>

# 목차
- [Command](#1)
    - [Managing Packages](#2)
    - [Navigating the file system](#3)
    - [Manipulating files and directories](#4)
    - [Managing env variables](#5)
    - [Managing processes](#6)
    - [Managing user and groups](#7)
    - [Usermod Detail](#8)
    - [Managing File Permissions](#9)


- [레퍼런스 링크](#99)

<br>

<a name="1"></a>

# Command

<a name="2"></a>

### Managing Packages
```docker
apt update
apt list
apt install [패키지 이름]
apt remove [패키지 이름]
```

<br>
<a name="3"></a>

### Navigating the file system
```bash
pwd             # print the current working directory
ls              # list the files and directories
ls -l           # print ls commend in long list
cd /            # go to the root directory
cd [상대경로]    # go to 상대경로
cd ..           # go to one level up
cd -            # go to the home directory


# find명령어
find -type d # (directory type 만 찾기)
find -type f # (file type 만 찾기)

# (파일타입중에서 f로 시작하는 이름 모두찾기) (대소문자 구분)
find -type f -name "f*" 

# (파일타입중에서 f로 시작하는 이름 모두찾기) (대소문자 구분안함)
find -type f -iname "f*" 

# (root directory에서 *.py 패턴에 일치하는 파일을 모두 가져오기)
find / -type f -name "*.py" 
```


#### ls -l 할경우 해당경로 내 파일,폴더를 권환내용과 함께 출력된다.
> d로 시작하는것은 directory

> \- 로 시작하는것은 file을 의미한다.

<br>

```

<a name="4"></a>

### Manipulating files and directories
```bash
mkdir [directory name]            # create directory
mv [old_filename] [new_filename]  # rename file or directory
touch [filename]                  # create file
rm [filename]                     # remove filename
rm -r [directory]                 # recursively remove a directory
```

<a name="5"></a>

### Managing env variables
```bash
printenv            # print all env path
printenv [PATH]     # print selected env path
echo $[PATH]        # print selected env path
export name=bob     # set variable path
```

<a name="6"></a>

### Managing processes
```bash
ps                  # list runnning processes
kill [process ID]   # kill the process with selected ID value
```


<a name="7"></a>

### Managing user and groups
```bash
useradd [name]   # create a user with out a home directory
useradd -m [name]   # create a user with a home directory

# to add a user interactive with default value from "/etc/adduser.conf"
adduser [name]      # useradd와 비슷하지만 더 많은 기능 보유
usermod             # modify user
userdel             # delete user

groupadd [group name]   # create a group
groups [username]       # get username's group list
groupmod                # modify group
groupdel                # delete group
```

```bash
groupadd developers # cat /etc/group 에서 group목록 확인가능

usermod -G developers john # developers 그룹에 john을 추가한다

# john의 password를 확인하고싶을때 두 가지 방법
-  cat /etc/passwd | grep john
- grep john /etc/passwd
```


<a name="8"></a>

### Usermod Detail
```bash
# ref: https://dololak.tistory.com/270

usermod -c <"이름"> <계정> # 계정의 이름을 변경합니다.
usermod -d <"경로"> <계정>	# 계정의 홈 디렉터리를 변경합니다.
usermod -s <"셸"> <계정> # 계정의 로그인 기본 셸을 변경합니다.
usermod -e <날짜> <계정> # 계정이 해당 날짜에 만료되도록 합니다.
ex) usermod -e 2018-05-01 myuser

usermod -g <그룹> <계정> # 사용자의 기본 소속 그룹을 변경합니다.
usermod -G <그룹> <계정> # 계정의 소속 그룹을 변경합니다.
# 만약 여러 그룹을 지정할 때에는 ,(콤마) 로 구분하여 지정합니다.

usermod -a -G <그룹> <계정>	# 계정의 소속 그룹을 추가(add) 합니다.
```
<br>
<a name="9"></a>

# 접근권환의 의미
- rwx (read, write, execute)
- rw- (read, write, )
- r-x (read, , execute)

<br>

- chmod u : user who owns the file
- chmod g : groups that owns the file
- chmod o : others

<br>

### Managing File Permissions
```bash
# ref : codewithmosh.com
chmod u+x [file name]     # give the owning user execute permission
chmod g+x [file name]     # give the owning group execute permission
chmod o+x [file name]     # give everyone else execute permission
chmod ug+x [file name]    # to give the owning user and group
                          # execute permission

chmod ug-x [file name]    # to remove the execute permission from
                          # the owning user and group

# deploy.sh 파일에 u 사용자에게 execute 권한을 부여한다
chmod u+x deploy.sh

```


<a name="10"></a>

### Reading Text files
```bash
# concatenate
cat
more

# apt install less
less
head -n 5 # 첫 5줄 출력
tail -n 5 # 마지막 5줄 출력
```


<a name="11"></a>

### Cat 커맨드 심화
```bash
# file1.txt 파일내용을 읽은 후 file2.txt 다름이름으로 저장한다
cat file1.txt > file2.txt

# 한번에 두 파일을 읽어서 모든 합친내용을 출력
cat file1.txt file2.txt

# file1.txt와 file2.txt을 합쳐서 읽은 후 combined.txt로 다른이름으로 저장
cat file1.txt file2.txt > combined.txt 

# echo로 입력한 문자를 file1.txt로 저장
echo {문자} > file1.txt 
```


<a name="12"></a>

### Grep 명령어
```bash
global regular expression


grep -i # (대소문자 구분안하는 명령어)

# 대소문자 구분없이 'root' 이라는 단더를 /etc/passwd 경로에서 탐색
grep -i  root /etc/passwd


# 대소문자 구분없는 "hello": 단어를 file1.txt, file2.txt 파일 탐색
grep -i hello file1.txt file2.txt

# 대소문자 구분없는 "hello" 단어를 'file'이름을 가진 모든파일 내에서 검색
grep -i hello file*


# 이렇게 하면 . 이 directory라서 오류 발생
grep -i hello . 


# 현재다이렉토리 (.) 내에서 재귀식으로 대소문자 구분없는 'hello' 파일 읽기
grep -i -r hello . 


# 동일한 기능, 동일한 결과물 출력됨
grep -i -r hello .   
grep -ir hello .
```

<br>

# Command Chain

<a name="13"></a>
```bash
# ; 로 여러 명령어를 한줄로 처리가능하다.
mkdir test; cd test; echo done

# 커맨드 실행오류가 발생한 경우 그 뒤에 있는 커맨드는 실행하지 않는다.
mkdir test && cd tst && echo done

# 좌측 커맨드 실행오류가 난 경우 우측 커맨드 실행
mkdir test || echo "mkdir test failed"
```


```bash
# ls /bin의 결과물을 less 커맨드 결과물로 출력하는 방식
ls /bin | less 
```

```bash
# 커맨드를 여러줄로 끊어서 작성
mkdir test; \
cd test; \
echo done
```

<br>

<a name="99"></a>
# 입문레퍼런스 링크
- [mbodo/Linux - Commands cheatsheet.md](https://gist.github.com/mbodo/4705709a098fa985b53e185a98bbcea7)
- [khazeamo/linux-cheatsheet.md](https://gist.github.com/khazeamo/f762f532bfbc17d5bf396e9d4c2a9586#file-hierarchy-standard-fhs)
- [sudheerj/Linux-cheat-sheet](https://github.com/sudheerj/Linux-cheat-sheet/blob/master/README.md)
- [riipandi/linux-cmd-cheatsheet.md](https://gist.github.com/riipandi/3097780)
- [crhuber/linux-cheatsheet](https://github.com/crhuber/linux-cheatsheet)
- [Linux 리눅스 usermod 명령어 - 계정 정보 변경](https://dololak.tistory.com/270)
- [The Linux Command Handbook](https://www.freecodecamp.org/news/the-linux-commands-handbook/)