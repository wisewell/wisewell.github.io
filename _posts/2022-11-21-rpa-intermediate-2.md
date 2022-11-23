---
layout: post
title: 2022-11-22 RPA 중급 - 2
categories: [RPA, UiPath]
---

# RPA개발자 실전과정(개발편)

## 모듈 관리
RPA 공통 프로세스를 수시로 활용

1. 라이브러리(Library)
	- 유용한 기능을 모아둔 패키지 파일
	- 개발된 프로세스를 NuGet에 업로드한 후 패지키를 다운로드하는 방식
	- 누구나 접근 가능 (Manage Packages에서 검색 후 다운로드)

2. 스니펫(Snippet)
	- 유용한 기능을 모아둔 소스
	- 개발한 프로세스를 특정 폴더에 저장해서 원본 그대로 사용하는 방식
	- 최초 스니펫을 만든 컴퓨터만 사용

## 라이브러리(Library) 사용법
라이브러리로 만들기

- 오케스트레이터 X : 특정 폴더 설정 후 사용
- 오케스트레이터 O : 오케스트레이터 서버에 업로드해서 사용

## 스니펫(Snippet) 사용법
프로세스로 만들기

## 디렉토리 문법
파일 및 폴더를 생성, 삭제, 복사, 이동 등 관리

- Create Folder 액티비티 : 폴더 경로
- Create File 액티비티 : 폴더 경로, 파일 이름 + 확장자명
- Move File 액티비티 : 파일 경로, 파일 이름 + 확장자명, 덮어씌우기 여부
- Copy File 액티비티 : 파일 경로, 파일 이름 + 확장자명, 덮어씌우기 여부
- Delete 액티비티 : 폴더/파일 경로

### Path Exists 액티비티
지정된 경로에 폴더/파일이 있는지 확인

### For Each File in Folder / For Each Folder in Folder 액티비티
특정 폴더내 파일/폴더 순회 반복문

\* 스니펫 활용의 경우<br>
1. Select folder 액티비티 사용 또는 `selectFolder = File Path`
2. `files = Directory.GetFiles(selectFolder)`
3. 반복문 사용

## 셀렉터 활용
UI 속성값을 저장한 표준 XML 코드<br>
__변수(String) 처리가 가능 → \{\{VariableName\}\}__

## 기타 액티비티

### Merge Data Table
데이터테이블 병합

- `Destination` : 병합될 데이터테이블(기준)
- `MissingSchemaAction` : 데이터를 어떻게 병합할지 설정하는 옵션
	- Add : 모든 데이터 병합
	- Ignore : DT1과 동일한 칼럼 데이터만 병합
	- Error : DT2의 칼럼이 DT1의 칼럼과(스키마가) 완전히 동일하지 않으면 에러 발생
	- AddWithKey : Add 옵션과 동일
- `Source` : 병합할 데이터테이블(추가)

### Lookup Data Table
엑셀 VLOOKUP 함수와 동일 (특정 칼럼을 기준으로 값 찾기)

- Input > DataTable : 데이터를 찾을 데이터테이블 (DT2)
- Input > LookupValue : 기준값 (DT1)
- Lookup Column > ColumnName : 기준값의 칼럼명 (DT2)
- Target Column > ColumnName : (기준값과 동일행에 있는) 찾을 값의 칼럼명 (DT2)
- Output > CellValue : (기준값과 동일행에 있는) 찾는 값 → 변수에 저장 (DT2)
- Output > RowIndex : 찾는 값의 Row Index (DT2)

## Path.Combine(String, String)
\\\(역슬래시)를 붙여준다.