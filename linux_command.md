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

## 실행 결과를 파일로 저장 : Redirection(재지향)
- 일반적으로 명령어를 실행하면 화면에 출력해주는 것에 그치는데, redirection 개념을 사용해 실행 결과를 파일에 저장할 수 있다.
- 예시 1: `train.py` 실행 결과를 `test.txt` 파일에 저장하기 (단, 에러 메시지는 저장되지 않음.)
```bash
python train.py > test.txt
```
- 예시 2: `test.py` 실행 결과를 **에러 메시지**를 포함하여 `test2.txt` 파일에 저장하기.
```bash
python test.py > test2.txt
```

## GPU 관리
1. 1초마다 GPU 상태 모니터링
```bash
watch -n 1 nvidia-smi
```
2. 그래픽카드 이름 확인
```bash
nvidia-smi --query | fgrep 'Product Name'
```

3. 사용자별 GPU 사용현황 확인
```bash
pip install gpustat # 설치
gpustat -i
```

## 인터넷에서 파일 다운로드
1. 기본 사용법
```bash
wget [download_url]
```
2. 다른 이름으로 다운로드
```bash
wget -O target.zip [download_url]
```
3. 다운로드 속도 지정
```bash
wget --limit-rate=200k [download_url]
```
4. 이어받기
```bash
wget -c [download_url]
```
5. 백그라운드에서 다운로드
```bash
wget -b [download_url]
```
6. 다운로드 가능 여부 확인
```bash
wget --spider [download_url]
```
7. 재시도 횟수 지정
```bash
wget --tries=50 [download_url]
```
8. 특정 파일 타입만 다운로드
```bash
wget -r -A.pdf [download_url] # pdf만 다운로드
```
9. 제외하려는 파일 타입 지정
```bash
wget --reject=pdf [download_url]
```
10. 로그 기록
```bash
wget -o download.log [download_url]
```

## 파일 및 폴더 개수 확인
1. 현재 위치에서의 폴더 개수 확인
```bash
ls -l | grep ^d | wc -l
```
2. 현재 위치에서의 파일 개수 확인
```bash
ls -l | grep ^- | wc -l
```
3. 현재 위치 하위 디렉토리의 파일 개수 확인
```bash
find . -type f | wc -l
```