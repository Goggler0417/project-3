# Tagmark v4.15

## 이번 버전
v1 / v2 / v3.05와 현재 v4.14를 다시 대조해, 기존 세대에서 유용했던 편의 기능 중
v4의 현재 정보 구조와 충돌하지 않는 항목을 복원했습니다.

## 복원 / 개선

### Bookmark 검색
- v1식 쉼표 다중 검색 복원
  - `SF, Example Saga`처럼 입력하면 각 검색어를 AND로 처리
- 검색 Scope별 검색 후보 datalist 추가
  - 제목
  - Tag
  - Record / Character
  - Category 경로
- `초기화` 버튼 추가
  - 검색어
  - Search Scope
  - 빠른 Category
  - 현재 Tab Filter
  를 한 번에 초기화
  - Sort / Layout은 유지

### Bookmark Tag Filter
- 기존에 보류했던 v1식 순환 Tag Filter를 Bookmark Filter 안에 구현
- 상태:
  - 중립
  - 포함
  - 제외
  - 다시 중립
- 포함 Tag는 모두 존재해야 함
- 제외 Tag가 하나라도 존재하면 제외
- Tag Relation Input이 여러 개라면 Filter에서 대상 Input을 직접 선택
- 일반 AND / OR Input Filter와 함께 사용 가능
- Filter 버튼에 활성 조건 수 표시

### Tag Tab
- v3 계열의 `표시할 Tag Head` 개념 복원
- Tab Settings에서 현재 Tag Tab에 표시할 Head를 복수 선택 가능
- 아무 Head도 선택하지 않으면 전체 표시
- Tag 생성 Head 선택 영역도 현재 Tab의 Head 표시 설정을 따름
- Head별 전용 Tag Tab을 만들 수 있음
- 미사용 보기에서 `표시된 미사용 삭제` 일괄 정리 추가
  - 현재 검색 + Head 표시 조건에 보이는 미사용 Tag만 삭제

## 2차 감사에서 확인했지만 의도적으로 복원하지 않은 것
- v1 Cloud 로그인 / Supabase 동기화
  - v4에서는 Storage Adapter 계층으로 분리하는 방향 유지
- v1의 legacy Text / HTML Bookmark Import
  - 현재 설계대로 v4 Format 1 Import만 유지
- v2 Folder 전용 Tab
  - v4에서는 Folder를 Bookmark의 수동 분류 관계로 유지
- v1 Folder 자체의 Artist / Series 메타데이터
  - v4 Folder는 메타데이터 없는 순수 분류 객체라는 기존 결정 유지
  - 필요한 정보는 Folder Header Input 표시로 대체
- v3 Profile 전용 entity model
  - v4 Record + Profile/Character 표시 프리셋으로 대체
- browser prompt / alert / confirm UI
  - v4 공통 in-app Modal 원칙 유지

## 이미 v4에 복원되어 있어 추가 변경하지 않은 주요 기능
- Bookmark Folder 생성 / 이동 / Unfile / 삭제
- Character / Cast 빠른 추가
- Character / Record 관계 복사·붙여넣기
- Tag Head / 색상 / 다중 Head Tag 등록
- Category Tree / reparent / child add
- Record Profile 보기 / Series Auto Folder
- Field / Input / Placement
- Relation 검색 Picker + inline 생성
- Bulk Tag / Category / Input 편집
- Page / Tab 복제 및 순서 변경
- Backup / Restore / Export / v4 Import
- DB Check / 테스트 Page

## 검증
- JavaScript syntax 검사 통과
- 중복 function 선언 0건
- Chromium 실제 DOM 통합 테스트 통과
  - Bookmark 초기 화면
  - 검색 후보 datalist
  - 쉼표 AND 검색: 테스트 데이터에서 2개 결과 확인
  - `초기화` 후 3개 결과 복귀
  - Filter 버튼으로 Bookmark Filter Modal 진입
  - SF Tag 순환:
    - 포함 → 2개
    - 제외 → 1개
    - 중립 → 3개
  - Tag Tab Settings에서 Head 1개만 표시하도록 저장
  - 표시 Tag 및 Tag 생성 Head가 해당 Head로 제한되는 것 확인
  - 임시 미사용 Tag 생성 → 미사용 필터 → `표시된 미사용 삭제` → 실제 삭제 확인
  - 390×844 모바일 viewport에서 document 전체 가로 overflow 없음
  - 테스트 중 runtime / unhandled rejection 0건

## 테스트 제한
실제 IndexedDB 브라우저 재시작 영속성은 이번 통합 테스트 범위에 포함하지 않았습니다.
DOM 통합 테스트에서는 저장 함수만 인메모리 방식으로 대체했으며,
배포용 `index.html`의 IndexedDB 구현은 변경하지 않았습니다.
