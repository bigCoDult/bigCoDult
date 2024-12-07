# 파일과 디렉토리

## 파일 시스템
- **파일 시스템**: 운영체제 내에서 파일과 디렉터리를 다루어 주는 프로그램

## 파일과 디렉터리
- **파일**: 의미 있고 관련 있는 정보를 모은 논리적 단위
- **디렉터리**: 파일과 폴더를 조직화하여 관리하는 논리적 단위

### 파일의 구성
1. **파일을 실행하기 위한 정보**
2. **부가 정보 (속성, 메타 데이터)**

### 파일의 속성
파일의 속성은 운영체제에 따라 다를 수 있습니다.

- **유형**: 파일의 종류 (확장자)
- **크기**: 파일의 현재 크기와 허용 가능한 최대 크기
- **보호**: 파일 접근 권한 (읽기, 실행)
- **생성 날짜**: 파일이 생성된 날짜
- **마지막 접근 날짜**: 마지막으로 파일에 접근한 날짜
- **마지막 수정 날짜**: 마지막으로 파일이 수정된 날짜
- **생성자**: 파일을 생성한 사용자
- **소유자**: 파일을 소유한 사용자
- **위치**: 파일의 보조기억장치 상 위치

### 파일 연산을 위한 시스템 호출
1. 파일 생성
2. 파일 삭제
3. 파일 열기
4. 파일 닫기
5. 파일 읽기
6. 파일 쓰기

## 디렉터리
- **디렉터리**: 윈도우에서는 "폴더"라고도 함

### 디렉터리 구조
1. **1단계 디렉터리**: 옛날 방식
2. **트리 구조 디렉터리**: 여러 계층으로 파일 및 폴더를 관리 (현재 방식)
   - **최상위 디렉터리**: 루트 디렉터리 `/`
   - **서브 디렉터리**: 하위 계층 디렉터리

### 경로
- **절대 경로**: 루트 디렉터리에서 시작해 파일까지 이르는 경로 (`/home/guest/a.sh`)
- **상대 경로**: 현재 디렉터리를 기준으로 파일까지 이르는 경로 (`guest/d.jpg`)

### 디렉터리 연산을 위한 시스템 호출
1. 디렉터리 생성
2. 디렉터리 삭제
3. 디렉터리 열기
4. 디렉터리 닫기
5. 디렉터리 읽기

### 디렉터리의 구성
- 디렉터리는 "포함된 정보가 특별한 파일"
  - 파일의 내부: 파일과 관련된 정보
  - 디렉터리의 내부: 포함된 대상과 관련된 정보
- **디렉터리 엔트리**
  - 디렉터리에 포함된 대상의 이름
  - 대상이 보조기억장치에 저장된 위치 정보
  - 파일과 관련된 부가 정보 (운영체제에 따라 다름)
  - `.`, `..`, 하위 디렉터리, 파일 등이 포함됨

---

# 파일 시스템

## 정의
- **파일 시스템**: 파일과 디렉터리를 보조기억장치에 할당하고 접근하는 방법

## 파일 시스템의 종류
- FAT 파일 시스템
- 유닉스 파일 시스템

### 파티셔닝과 포매팅
- **파티셔닝**: 저장 장치를 논리적인 영역으로 구획하는 작업
- **포매팅**: 파일 시스템을 설정하여 데이터를 쓸 준비를 하는 작업

### 파일 할당 방법
운영체제는 파일/디렉터리를 블록 단위로 읽고 씀.

#### 연속 할당
- 연속적인 블록에 파일을 저장
- 단점: 외부 단편화, 접근 속도 문제

#### 불연속 할당
1. **연결 할당**: 각 블록이 다음 블록 주소를 저장하여 연결 리스트 형태로 관리
   - 단점: 느린 임의 접근 속도, 블록 손상 시 데이터 손실

2. **색인 할당**: 파일의 모든 블록 주소를 하나의 "색인 블록"에 모아 관리
   - 임의 접근 용이

---

# FAT 파일 시스템

### FAT의 특징
- 연결 할당 기반이나 단점을 보완
- 각 블록의 다음 블록 주소를 한데 모아 **FAT (File Allocation Table)**로 관리
- FAT12, FAT16, FAT32: 블록을 표현하는 비트 수

### FAT 영역 구성
1. 예약 영역
2. FAT 영역
3. 루트 디렉터리 영역
4. 데이터 영역

### FAT에서 디렉터리 엔트리 구성
- 파일 이름
- 확장자
- 속성
- 예약 영역
- 생성 시간
- 마지막 접근 시간
- 마지막 수정 시간
- 시작 블록
- 파일 크기

### FAT에서 파일 읽는 과정
- FAT 영역: 디스크의 파일 데이터와 관련된 정보가 담김

---

# 유닉스 파일 시스템

### 유닉스 파일 시스템의 특징
- 색인 할당 기반 파일 시스템
- **색인 블록 (i-node)**: 파일 속성 정보와 블록 주소를 저장
  - i-node에 파일 이름 제외한 모든 정보를 저장

### 유닉스 영역 구성
1. 예약 영역
2. i-node 영역
3. 데이터 영역

### 유닉스 저장 구조
1. **직접 블록**: 데이터가 저장된 블록
2. **단일 간접 블록**: 데이터 블록 주소를 저장한 블록
3. **이중 간접 블록**: 단일 간접 블록의 주소를 저장한 블록
4. **삼중 간접 블록**: 이중 간접 블록의 주소를 저장한 블록

### 유닉스 디렉터리 엔트리
- i-node 번호
- 파일 이름

### 유닉스 파일 읽기 과정
- 유닉스 파일 시스템은 항상 루트 디렉터리 위치를 기억 (i-node 2)
- 루트 디렉터리에서 시작해 각 i-node를 따라가며 파일을 찾음































### Tech & Tool
![C Badge](https://img.shields.io/badge/C-A8B9CC?style=flat-square&logo=c&logoColor=white)
![Git Badge](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![Ubuntu Badge](https://img.shields.io/badge/Ubuntu-E95420?style=flat-square&logo=ubuntu&logoColor=white)
![WSL2 Badge](https://img.shields.io/badge/WSL2-4D4D4D?style=flat-square&logo=windows&logoColor=white)
![HTML5 Badge](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![React Badge](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=React&logoColor=white)
![CSS3 Badge](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)
![Tailwind CSS Badge](https://img.shields.io/badge/TailwindCSS-06B6D4?style=flat-square&logo=TailwindCSS&logoColor=white)
![JavaScript Badge](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=JavaScript&logoColor=black)
![PocketBase Badge](https://img.shields.io/badge/PocketBase-B8DBE4?style=flat-square&logo=PocketBase&logoColor=white)
![Vite Badge](https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white)
![Zustand Badge](https://img.shields.io/badge/🐻Zustand-000?style=flat-square&logoColor=white)
<!--
### 42 Stats
<p align="left" style="margin: 0; padding: 0;">
  <img src="https://badge42.coday.fr/api/v2/clsx4chzw823401p4dwbfo4wt/stats?cursusId=9&coalitionId=piscine" style="width: 50%;" >
  <br>
  <img src="https://badge42.coday.fr/api/v2/clsx4chzw823401p4dwbfo4wt/stats?cursusId=21&coalitionId=457" style="width: 50%;" >
</p>
-->

### Stats
<p align="left" style="margin: 0; padding: 0; display: flex; justify-content: space-around;">
  <img src="https://github-readme-stats.vercel.app/api?username=bigCoDult&show_icons=true&count_private=true&theme=transparent&hide_border=false&border_radius=5" style="width: 50%;"/>
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=bigCoDult&show_icons=true&count_private=true&layout=compact&theme=transparent&hide_border=false&border_radius=5" style="width: 38%;" />
</p>

<p align="left" style="margin: 0; padding: 0;">
  <img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2FbigCoDult%2Fhit-counter&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false" />
</p>
