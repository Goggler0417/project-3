# Tagmark v4.00

v4의 첫 구현 기준선입니다. 기존 v2/v3에 패치를 덧붙이지 않고 새로운 Canonical DB 구조와 Page-local ID 체계를 사용하는 단일 HTML 앱으로 작성했습니다.

## 구현된 핵심
- Main → Page → Tab 계층
- Bookmark / Record / Tag / Category Tab
- Page-local Base36 ID allocator, Page만 DB-global ID
- Bookmark 수동 Folder (`folderId`), Folder 삭제 시 Bookmark는 Unfiled
- Record Input 기반 Auto Folder(group by)
- Page-level Input, Schema → Field → Placement 구조
- Field 삭제 시 실제 Input/value 보존
- Bookmark/Record relation Input 기반 값 저장
- Page 복제: 새 Page ID만 발급하고 내부 local ID는 그대로 유지
- 선택 / 현재 검색 결과 전체 선택 / Bulk delete
- Runtime Undo/Redo
- IndexedDB autosave + revision
- v4 Format 1 Export/Import
- Import 직전 Emergency Export 다운로드
- 기본 DB Check / Category cycle 검사
- 앱 내부 modal 사용

## 아직 v4.00에서 제한적인 부분
- Filter AST의 고급 UI 및 Tag/Category 전용 AND/OR 필터
- Placement Display Rule의 Independent/Priority 편집 UI
- Unassigned Information 전용 UI
- 고급 Bulk Edit(Tag/Category/relation add/remove/replace)
- Tag Head 관리 UI
- Category 트리 전용 UI와 reparent/subtree delete UX
- 내부 persistent backup store/Restore UI (현재 Backup은 JSON 다운로드)
- 고급 Validator 자동 수리 및 영향도 보고
- Virtual rendering

이 항목들은 v4 데이터 모델을 깨지 않고 후속 구현할 수 있도록 분리했습니다.

## 검증
- HTML에서 JavaScript를 추출하여 Node.js `--check` 구문 검사를 수행.
- 주요 데이터 구조/ID/참조 코드를 정적 점검.
- 실제 브라우저에서 버튼을 직접 클릭하는 상호작용 테스트는 이 환경에서 수행하지 않았습니다. 따라서 브라우저 런타임/UI 회귀는 추가 확인이 필요합니다.
