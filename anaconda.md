# Anaconda (아나콘다) 명령어 정리
자주 쓰지는 않지만 알아두면 유용한 명령어들을 정리하였다.

## Export, import, clone
기존에 사용하고 있던 아나콘다 가상환경을 다른 머신에서 사용하고 싶을 때, 혹은 별도의 동일한 가상환경을 만들고 싶을 때 유용한 명령어들이다.
1. Export
- `test`라는 가상환경을 yaml 파일 형태로 export 하기.
```bash
conda env export -n test > test.yaml
```
- 현재 위치한 디렉토리에 `test.yaml` 파일이 생성된다.
- 이를 새로 설치할 머신에 옮겨주면 된다.
2. Import
- export된  `test` 가상환경을 다른 머신에서 import하여 동일한 가상환경 설치하기.
```bash
conda env create -f test.yaml
```
- 새롭게 생성된 가상환경의 이름은 yaml 파일명으로 정해지므로, 다른 이름의 가상환경을 설치하고 싶다면 위 파일명을 다르게 바꾸어주면 된다.
3. Clone
- 같은 머신 상에서 가상환경을 똑같이 만들고자 한다면, export & import 하는 것보다 복제(clone)하는 것이 더 편한 방법이다.
```bash
conda create -n test2 --clone test
```
- `test`라는 기존의 가상환경을 복제하여 `test2`라는 새로운 가상환경을 생성한다.