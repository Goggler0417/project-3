# Tagmark v4.13

## 이번 버전
Main 화면과 Page Shell을 v1/v2 계열의 조밀하고 익숙한 Tagmark UI 쪽으로 통일했습니다.
Bookmark / Tag / Category / Record Tab의 데이터 구조와 기능은 변경하지 않았습니다.

### Main
- Page 검색
- Grid / List 전환 유지
- A→Z / Z→A 정렬 유지
- Page 카드의 아이콘, 설명, Bookmark / Record / Tag / Category 수를 분리 표시
- Page 카드에서 바로 열기 / 복제
- 테스트 Page TEST 표시 유지

### Page Shell
- v2 계열의 짙은 Page Sidebar를 정리
- 현재 Page 강조
- 상단 Context bar
- Page 제목 / 설명을 별도 Header panel로 통일
- Tab bar를 Page Header와 시각적으로 연결
- 기존 Page Settings / Tab 기능 유지

### 모바일
- Sidebar를 고정 폭으로 남겨 화면을 좁히지 않고, 햄버거 메뉴 Drawer로 변경
- Drawer 바깥을 누르면 닫힘
- Main 카드 1열
- Main toolbar 가로 스크롤
- 기존 각 Tab의 모바일 UI 유지

## 구조
- Main 검색어와 Sidebar 열림 상태는 Runtime 전용이며 DB에 저장하지 않습니다.
- 기존 Canonical DB 형식은 변경하지 않았습니다.

## 검사
- VERSION 4.13
- 중복 function 선언 검사
- JavaScript syntax 검사
- ZIP 구조 검사
- 실제 Chromium 브라우저 클릭 검사는 이 패키징 단계에서는 수행하지 않았습니다.
