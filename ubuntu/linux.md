# File and Directory commanads(1)

|commands|description|
|---|---|
|`chgrp` [options] group file|Change the ownership of files or dir|
|`chmod` [options] file|Change the permission|
|`chown` [options] owner file|Change the user and group ownership of a given file ,dir or link|
|`cp` [options] file1 file2|make copies|
|`mv` [options] file1 file2|Move files and dirs from one location to another, and optionally rename them|
|`rm` [options] file|Delete file|
|`ln` [options] source target|Create a link to a file or dir|

```bash
# 활용
nginx -t
sudo chmod 777 -R filename
```

---

# File and Directory commanads(2)
|commands|description|
|---|---|
|cp|복사|
|mv|옮기거나 이름바꾸기|
|rm|지우기|
|ln|링크파일 생성(symbolic link, hard link)|

```bash
# 활용

$ cp file1 file2
# file1과 똑같은 내용의 파일을 file2라는 이름으로 생성

$ cp DirA/file1 DirB
# DirA파일 안의 file1을 DirB로 복사한다.(복붙)

$ cp -r DirA DirB
# DirA를 통째로 복사해서(안에있는 파일 포함) DirB라는 이름으로 하나 더 생성

$ mv file1 file2
# file1이름을 file2로 변경

$ mv file1 dir1/
# file1을 뒤(디렉토리 명)으로 옮김

```

## Symbolic Link, Hard Link의 차이
- *Symbolic Link* : 단순히 원본파일을 가리키도록 링크만 시켜둔 것으로 MS의 윈도우시스템에서 흔히 사용하는 '바로가기' 같은 것이며, 원본파일을 가리키고만 있으므로 원본파일의 크기와는 무관한다. 그리고 심볼릭링크에서는 원본파일이 삭제되어 존재하지 않을 경우에 링크파일은 깜박거리면서 링크파일의 원본파일이 없다는 것을 알려준다.


- *Hard Link* : 원본파일과 다른 이름으로 존재하는 동일한 파일이며 원본파일과 동일한 내용의 다른 파일이라고 할 수 있다. 그리고 하드링크에서는 원본파일과 링크파일 두개가 서로 다른 파일이기 때문에 둘 중 하나를 삭제하더라도 나머지 하나는 그대로 남아 있다. 또한 하드링크에서는 원본파일의 내용이 변경될 경우에는 링크파일의 내용 또한 자동으로 변경된다. 
해당 파일의 포인터라고 생각하면 됨!
```bash
# 하드링크 사용법 : ln 원본파일 대상파일(대상디렉토리)
$ ln hard_source hard_link 

# 심볼릭 링크 사용법 : ln -s 원본파일 대상파일(대상디렉토리)
$ ln -s shared-file link-name
```



# Permissions

```bash
$ ls -l
# 권한 확인
> -rw-r--r-- 1 82106 197609 2529 4월   2 19:35 linux.md
```
- 첫번 째 나오는 인자부터 user, group, others 의 permission

## octal value 
|read|write|execute|
|---|---|---|
|r|w|x|
|4|2|1|

|User|Group|Others|
|---|---|---|
|rwx|r-x|r-x|
|421|4-1|4-1|
|7|5|5|

```bash
# 활용
-> chmod 755 filename
```

```bash
format : chmod options mode file/dir

-> chmod -R options 755 filename
# -R옵션을 주면 포함, 하위 요소들에게 모두 권한을 준다.
```



## ps 명령어

`meaning of ps output`
- PID : Process ID
- TIME : The amount of CPU time used so far(MM:SS)
- CMD : The name of commands

`ps options`
- -e : options instructs ps to include all running process
- -f : options causes ps to generate a full listing
- -l : options generetes a long listing

```bash
$ ps -ef 
# 걍 저는 거의 이거씀
```

## kill 명령어

- 그냥 kill하면 프로그램이 시그널을 알아 듣지 못함!
- 따라서 시그널 옵션 -9(sure kill)을 같이 보내줘야한다!
```bash
$ kill -9 [PID]
```



---

## Using Filters with Pipes
```bash
$ command1 | command2
```


## uniq command
```bash
$ cat > uni.txt
1 2 3 4
3 4 6 7 
1 1 1 1 
1 1 1 1 
...

$ uniq uni.txt uni_new.txt

$ cat uni_new.txt

# 요놈은 3,4 번째 줄에 중복을 없애주는데 말그래도 unique하게 1줄만남게함


ex)

$ ls /bin/ sort | uniq | less
>> 알아서 정리되서 뜸
```


## head/tail command
```bash
$ head -n 3 test.txt
-> 처음 세줄만 보여줌
# -n 옵션은 n 줄이라는 뜻

$ tail -n 3 test.txt
-> 뒤부터 3줄
```

## cut commnad
`cut options file_list`

### options
- -c character_list : 리스트에 정의된 것 추출

- -f field_list : 이것도 같은데 file_list

- -d delimeter : 

```bash
$ cut -c 1-4 test.txt
# 요놈 해보니까 2열까지만 추출됨
```

## sort command
### options
- -k : sort based on a `key field`
- -n : perform sorting based on the `numeric evaluation` of a string
- -r : sort in `reverse` order


## wc -l
- -l 옵션을 사용하면 line별로 세준다.
- text기준.. 등 많음


## grep command
```bash
# "of"가 포함된 내용 찾기
$ grep "of" temp.txt
```
```bash
# 응용) of 가 들어있는 라인 갯수 찾기
$ grep "of" movie_list_a.txt | wc -l
```

## tip
```bash
echo 넣고싶은 문자 >> filename
# 문자 넣어줌
```
```bash
sort movie_list_a.txt >> movie_list_a_sorted.txt
# 오름차순 정렬하고 새로운 이름으로 생성
```
```bash
wc -l filename
# line별 갯수 세줌
```