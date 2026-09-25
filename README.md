# Tagmark v4.05

v4.04를 기준으로 과거 버전의 빠른 조작 기능을 추가 복원하고, 앞으로의 기능 검증을 위한 기본 테스트 데이터를 포함한 버전입니다.

## 추가된 편의 기능
- Main Page에서 그리드/목록 빠른 전환
- Main Page에서 A→Z / Z→A 빠른 정렬
- 각 Tab Toolbar에서 Grid/List 빠른 전환
- 각 Tab Toolbar에서 정렬 방향 빠른 전환
- 선택한 Bookmark/Record에 기존 Tag를 이름으로 선택해 일괄 추가
- 선택한 Bookmark/Record에 기존 Category를 이름으로 선택해 일괄 추가
- Bookmark 선택 상태에서 새 Folder를 만들면서 즉시 선택 항목을 이동
- Tag Head 삭제 시 소속 Tag를 다른 Head로 이동하거나 Head+Tag를 함께 삭제
- DB 관리에서 별도의 테스트 Page 생성

## 기본 테스트 데이터
새 DB에서는 `테스트 Page`가 생성되며 다음 자료가 들어 있습니다.
- Bookmark 3개: 테스트 북마크 A/B/C
- Tag 4개: SF, 판타지, 즐겨찾기, 나중에 보기
- Tag Head 2개: 장르, 상태
- Category 3개: 테스트 자료 > 영상 / 문서
- Record 2개: Alice, Bob
- Folder 1개: 샘플 Folder

기존 DB를 열 때는 사용자 데이터에 샘플을 자동으로 섞지 않습니다. 필요하면 `DB 관리 → 테스트 Page 생성`으로 독립된 테스트 Page를 추가할 수 있습니다.

## 유지 사항
- v4 Canonical DB 구조 유지
- v4.04의 Bookmark/Record 복제, 등장인물 Record 복사/붙여넣기, Tab 복제, Category 하위 생성 유지
- v4.02 이후 모바일 대응 유지
- 과거 버전의 저장 구조를 되살리지 않고 v4 데이터 모델 위에서 편의 기능만 복원

## 검증
- JavaScript 구문 검사(Node --check): 통과
- Headless Chromium 실제 DOM 클릭 통합 테스트: 통과
  - 기본 테스트 데이터 렌더링
  - Tab Grid/List 전환
  - 정렬 방향 전환
  - 전체 선택
  - Tag/Category 빠른 일괄 추가 모달
  - 선택 Bookmark로 새 Folder 생성 + 이동
  - Record/Tag/Category Tab 전환 및 샘플 데이터 표시
  - Tag Head 삭제 흐름
  - Main Grid/List 전환
  - 테스트 Page 추가
  - Page Settings 열기
- 390×844 모바일 viewport 클릭/레이아웃 테스트: 통과
  - 문서 전체 가로 오버플로 없음
  - Toolbar 자체 가로 스크롤 동작
  - 선택/일괄 작업 UI 접근 가능
  - 모바일 하단 Modal 폭 확인
- 이 실행 환경에서는 브라우저의 로컬 HTTP/file URL 접근이 관리자 정책으로 차단되어, 브라우저 통합 테스트 시 IndexedDB 저장 계층만 인메모리 테스트 스텁으로 대체했습니다. 실제 IndexedDB 코드 자체는 기존 구현을 유지했으며 구문/호출 구조를 검사했습니다.

## 다음 단계
이전 버전 소스를 계속 대조하면서 인라인 Tag/Category 생성, 검색형 Relation 선택, 카드 단축 액션, 과거 Profile/Character 편의 기능 등 아직 누락된 UX를 v4 엔진 위에 추가 복원합니다. 이후 구형 UI의 시각적/조작 체계를 v4 엔진 위에 이식합니다.
