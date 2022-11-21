---
layout: post
title: 2022-11-21 RPA 중급 - 1
categories: [RPA, UiPath]
---

# RPA개발자 실전과정(개발편)

## RPA 프로젝트 이해
1. 과제 발굴
	- 반복성
	- 수작업 여부
	- 규칙 기반
	- 프로세스 변경주기
	- 전자 입력 방식
	- 표준화된 입력 방식
	- 낮은 예외율

2. 분석/설계
	- 원활한 개발이 가능하도록 사전에 준비하는 작업 및 PC 셋팅 : <br>
	최소사양, 계정 & 권한, 보안, 망 분리 여부, 원격 접속 여부, 디스플레이 최적화, 알림 및 작업 최적화, 전원 및 절전 최적화, 크롬 또는 Edge 브라우저 사용시 Extension 설치 등

	- 제품 설치 및 등록

	- 환경점검 : <br>
	사용 시스템 UI의 클릭 여부 및 작업 시 보안상 이슈 확인<br>
	시스템 UI 선택 여부, 보안, 시스템 변경 요청 고려, 권한, 인터넷 브라우저 점검, IP 제한 여부 등

3. 개발
	- 개발 표준 준수 : <br>
	프로젝트 표준화를 위한 개발 가인드라인<br>
	Naming Rule 준수, 주석 달기, 로그 출력, 각 시스템별 준수사항 등

	- 오류 유형 파악

4. 운영
	- 배포 관리 : <br>
	소스 배포 및 형상관리<br>
	형상관리, 소스 버전 확인 및 유의사항 준수, Orchestrator 관리 소스 버전과 사용 소스 버전 관리, Attended Bot 사용 시 배포방법 준수, UnAttended Bot 사용 시 배포방법 준수 등

	- 안정화 : <br>
	테스트 및 안정화<br>
	에러처리 확인, 이슈사항 확인 및 문제 해결 등

	- 산출물 작성 : <br>
	운영 산출물 작성<br>
	PDD(프로세스 요건 정의서), DSD(개발 요건 정의서), UAT(운영테스트 시나리오) 등

__기본적으로 '4. 운영'에 초점을 맞추고 개발해야 한다.__

## RPA 비즈니스 프로세스 이해
- Linear(선형 프로세스) : 프로세스 단계가 한 번만 실행
- Iterative(반복 프로세스) : 프로세스 단계가 여러 번 실행. __한 항목 처리 시 에러가 발생하면 중단된다.__
- Transactional(트랜잭션 프로세스) : 프로세스 단계가 여러 번 실행. __반복하는 구간이 독립적으로 작동한다. 설계 및 구현이 복잡하다.__

## UiPath 공식 문서
UiPath 홈페이지 > Support & Services > Documentation
<https://docs.uipath.com/>

## 개발 표준 준수
1. 신뢰성 : 로봇은 예상대로 작동해야 하며 예상치 못한 오류를 최소화해야 합니다.
2. 효율성 : 중복 프로세스를 방지하고 가능한 한 실행 시간을 최소화해야 합니다.
3. 유지보수성 : 워크플로우를 이해하고 디버그하기 쉬워야 합니다.
4. 확장성 : 새로운 기능을 쉽게 추가할 수 있어야 합니다.

## 개발 로드맵
1. Datatable을 이용한 2-Depth 이상의 For Each문 사용 시, `Select()` 사용 권장<br>
`Datatable.Select("조건")`

2. Lookup Datatable 액티비티 사용 시 Null 체크<br>
해당 값의 위치를 가져오는 Index가 -1일 경우 Null값의 처리 방안을 구현

3. Datatable 이용 시 Column Index가 아닌 Column Name으로 지정 권장

4. 폭 없는 공백(ZWSP : zero width space) 존재 확인<br>
`str_variable.replace(chr(160), "")`

5. 와일드 카드 처리<br>
`?` 또는 `*`

## 오류 유형
1. `NullReferenceException` : 설정값이 없는 변수를 사용 (초기화 안됨)
2. `IndexOutOfRangeException` : 인덱스가 컬렉션의 제한을 벗어났을 때
3. `ArgumentException` : 매개변수와 전달 인자가 맞지 않을 때
4. `SelectorNotFoundException` : Selector 찾기 실패
5. `ImageOperationException` : 이미지 찾기 실패
6. `TextNotFoundException` : 지정된 시간 내에 텍스트 찾기 실패
7. `ApplicationException` : 응답하지 않는 응용 프로그램과 같은 기술적 문제의 오류
8. `Arithmetic operation resulted in an overflow` : 자리수 초과
9. `Input array is longer than the number of columns of this table.` : Add Data Row 진행 시 Column 수 불일치
10. `Access Denined` : 오케스트레이터의 로봇에 설정된 Windows 암호가 로컬 PC Windows 암호와 불일치

## Config 파일 사용
가변적으로 변하는 정보(ID/PW, 파일 경로, 코드, 담당자명 등)를 관리하기 위한 파일

- `Config.xlsx` 엑셀 파일로 관리
- Config 정보는 `딕셔너리(Dictionary) 타입`으로 관리 (Key-Value)
- Account(계정), Path(경로), 코드(Code), Email(이메일) 등 `시트별로` 정보 관리

## Naming Rule
정해진 규칙에 따라 이름을 명명함으로써 프로젝트 관리를 원활히 수행

- 프로세스(Process)
- 워크플로우(Workflow)
- 변수(Variable)
- 인수(Argument)
- 정보자산(Asset)

## 주석
주석을 사용함으로써 프로젝트 관리를 원활히 수행할 수 있도록 만든다.

- 워크플로우(Workflow)
- 시퀀스(Sequence)
- 액티비티(Activity)

## 로그
오류 위치를 추적<br>
`Log Message` 액티비티를 사용

### 로그 레벨
- Trace : 개발 시 특정 값을 추적
- Info : 운영 모니터링 시 정보를 확인
- Warn : 경고
- Error : 예외처리(Exception) 발생 시 사용
- Fatal : 프로세스 작동 불가 시 사용

### 사용 위치
- 워크플로우(Workflow)의 시작/끝
- Try-Catch문의 Catches

## Invoke Workflow 사용
복잡한 프로세스를 작은 단위로 나누어서 프로젝트 개발 및 운영을 원활히 수행한다.

- Argument(인수) 사용
- 비즈니스 설계에 맞게 기능적으로 제작

## 프로세스 모듈화
각 프로세스 목적에 맞는 기능을 쉽게 사용할 수 있도록 구현한다.

- 라이브러리 사용
- 스니펫 사용

## PDD(Process Definition Document)
회의록의 과제 설명을 AS-IS로 작성 후 RPA 형태의 TO-BE로 작성

## DSD(Development Specifications Document)
- 개발 소스코드 스크린샷
- 소스코드에 대한 간략한 설명 + 사용 변수 설명

## UAT(User of Acceptance)
- AS-IS의 각 단계마다 체크 리스트를 작성
- 현업 담당자가 테스트하고 확인

## 사용자 매뉴얼
1. 실행 방법
2. Config 구성
3. 마스터 파일(템플릿)
4. 업무 프로세스<br>
	RPA 봇을 수행하기 위해 현업이 준비해야 하는 기본 셋팅과 RPA봇의 수행 절차 기술
5. 오류 조치 및 유의사항<br>
	RPA가 비정상적으로 수행된 경우 현업 혹은 운영자의 대처방법 기술

## 정보 관리
가변적인 데이터를 통합, 관리하는 활동

__`Config.xlsx` 엑셀 파일을 사용__

### Config 파일 구조
1. Account : 계정
2. Path : 경로 및 주소
3. Code : 단축코드 및 핵심코드
4. Email : 이메일 주소 및 내용

### Dictionary 선언 및 초기화
`new Dictionary(of String, Object)`

### Config 정의
1. ConfigPath(String)<br>
	Config 파일 경로 할당
2. Config(Dictionary<String, Object>)<br>
	Config 딕셔너리 초기화
3. Config 엑셀 파일 로드
4. `For Each Row in Data Table` 액티비티를 사용해 엑셀 파일 데이터를 Config 딕셔너리에 셋팅<br>
	__`If` 조건문을 사용해 `Not String.IsNullOrWhiteSpace(CurrentRow("Name").ToString.Trim)` 검사하고 만족할 때만 Config 딕셔너리에 할당__<br>
	_* Condition : Name 칼럼(키) 데이터가 Null이거나 공백이 아닐 때_
5. `Config(CurrentRow("Name").ToString.Trim) = CurrentRow("Value")`

## Credential : 자격 증명
계정 관리 = ID/PW 관리

1. Windows 자격 증명 관리
2. 오케스트레이터 내 Asset/Credential 이용

### Windows 자격 증명 관리
1. 제어판 → 사용자 계정 → 자격 증명 관리자 → `Windows 자격 증명` → `일반 자격 증명`에서 계정 생성
2. UiPath Studio에서 Manage Packages → `UiPath.Credentials.Activities 패키지` 설치

### Get Secure Credential 액티비티
1. `Target`에 Config 딕셔너리의 키를 입력<br>
	예시) `Config("System1_Account").ToString.Trim`
2. 속성창의 Output탭에서 `Username(String)`과 `Password(SecureString)` 값을 받을 변수 지정

### Type Secure Text 액티비티
속성창 Input탭의 `SecureText`에 Password(SecureString) 저장한 변수 넣기