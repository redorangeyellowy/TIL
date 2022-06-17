# 리눅스 명령어 정리
자주 쓰지는 않지만 알아두면 유용한 명령어들을 정리하였다.

## 파일 찾기, 파일 속 문자열 찾기
1. 파일명 찾는 방법
```bash
find '찾을 위치' -name '파일명'
```
- 예시 1: 최상위 디렉토리부터 하위로 ‘coco’로 시작하는 파일 찾기.
```bash
find / -name 'coco*'
```
- 예시 2: `usr` 디렉토리부터 하위로 ‘pose’로 시작하는 파일 찾기.
```bash
find /usr/ -name 'pose*'
```
2. 파일 내부 문자열 찾는 방법
```bash
grep -r '찾을 문자열' '대상 파일들'
```
- 예시 1: 현재 폴더에 있는 `train.log`파일 내부에 ‘coco’라는 문자열 찾기.
```bash
grep -r 'coco' ./train.log
```
- 예시 2: `var` 디렉토리부터 하위 모든 파일 내부에서 ‘coco’라는 문자열 찾기.
```bash
grep -r 'coco' /var/* [--include '*.pth']
```
> `include` 옵션으로 특정 확장자만 지정하여 검색할 수도 있다.

## 다른 서버와 파일 복사
1. 다른 서버로부터 복사
```bash
scp [option] [다른 서버 계정]@[다른 서버 주소]:[다른 서버의 파일 또는 디렉토리][지금 서버의 디렉토리]
```
- 예시1 : 서버의 `/home/test1` 폴더를 로컬의 `.`에 복사하기.
```bash
scp -r abc1234@111.222.33.44:/home/test1 .
```
2. 다른 서버에 복사
```bash
scp [option] [지금 서버의 파일 또는 디렉토리] [다른 서버 계정]@[다른 서버 주소]:[다른 서버의 디렉토리]
```
- 예시 2: 로컬의 `test2.yaml` 파일을 서버의 `/home/test3`에 복사하기.
```bash
scp ./test2.yaml abc1234@111.222.33.44:/home/test3 
```

## 디렉토리 용량 확인
- 현재 디렉토리 기준으로 하위 디렉토리들의 크기를 KB 단위로 출력.
- 옵션
    - `-h`: 디렉토리 또는 파일 크기를 KB, MB, GB 단위로 출력.
    - `-s`: 디렉토리 전체 사용량만 출력.
    - `--max-depth=N`: 최대 N번째 하위 디렉토리까지 출력.
- 예시 1: 현재 디렉토리만의 전체 사용량만을 출력하기.
```bash
du -sh .
```
> 현재 디렉토리를 나타내는 `.`은 생략 가능하다.
- 예시 2: `/database2/database`를 기준으로 하위 2번째 디렉토리까지 출력하기.
```bash
du -h --max-depth=2 /database2/database
```

## 스크린
1. 설치
```bash
sudo apt-get install screen
```
2. 사용법
- `test`라는 스크린 만들기
```bash
screen -S test
```
- 스크린 목록 보기
```bash
screen -ls
```
- 스크린 접속하기
```bash
screen -r [session name]
```
- 스크린 종료하기
```
ctrl + a + d
```
- 스크린 삭제하기
```bash
screen -X -S [session name] kill
```
