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
	- `include` 옵션으로 특정 확장자만 지정하여 검색할 수도 있다.
