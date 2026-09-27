# Tagmark v4.16

## 목적
v4.15 이후 첫 안정화 버전입니다. 새 기능 확장보다 데이터 보호, 실행 안정성, 검색 입력 UX, Page/Tab 관리 안전성에 집중했습니다.

## 주요 변경

### 1. 비파괴 DB 부팅 복구
- 시작 시 DB 구조 오류가 감지되면 기존 DB를 즉시 새 DB로 덮어쓰지 않습니다.
- 오류 원본을 IndexedDB의 `recovery-last` 복구 스냅샷으로 먼저 보관합니다.
- 안전하게 자동 수리 가능한 오류는 복구 후 정상 실행합니다.
- Format 손상 등 자동 수리가 불가능하면 **복구 모드**로 진입합니다.
- 복구 모드에서는 일반 데이터 변경/Undo/Redo를 잠가 원본 덮어쓰기를 방지합니다.
- DB 관리에서 복구 원본 다운로드, 자동 수리 재시도, 새 DB로 시작을 선택할 수 있습니다.
- 새 DB로 시작해도 기존 손상 원본 복구 스냅샷은 남깁니다.

### 2. Validator / DB Check 강화
다음 구조 문제를 추가 검사/수리합니다.
- pageOrder / tabOrder의 끊어진 참조
- Page / Tab / Schema / Field ID 불일치 일부
- Bookmark의 없는 Folder 참조
- Category의 없는 부모 / cycle
- Schema의 없는 Field / Placement / Input 참조
- allocator counter가 기존 ID보다 뒤처진 경우 안전하게 상향
- DB Check에서 끊어진 Relation 수와 Input 정의가 없는 보존 값 수를 별도 진단

### 3. Runtime 상태 안정화
- 삭제/Undo/Redo/Import 후 현재 Page/Tab이 사라졌을 때 stale runtime pointer를 정리합니다.
- 현재 Tab에 존재하지 않는 선택 ID를 자동 정리합니다.
- 저장 실패 상태를 상단에서 확인하고 DB 관리로 바로 진입할 수 있습니다.

### 4. 검색 입력 UX 수정
기존에는 검색창 `oninput`마다 전체 Tab body가 다시 만들어져 입력 focus가 끊길 수 있었습니다.

v4.16에서는 다음 검색창 모두 입력 후 focus/cursor를 복원합니다.
- Main Page 검색
- Bookmark 검색
- Record 검색
- Tag 검색
- Category 검색

### 5. 키보드 조작
- `Esc`: Sub Modal → Modal → 모바일 Sidebar 순서로 닫기
- `Ctrl/Cmd + Z`: Undo
- `Ctrl/Cmd + Shift + Z` 또는 `Ctrl/Cmd + Y`: Redo
- `/`: 현재 화면의 검색창으로 focus
- 입력창 내부에서는 브라우저 기본 텍스트 Undo를 방해하지 않습니다.

### 6. Page / Tab 관리 안전성
- **Page 삭제** 추가
- Page 삭제는 in-app 확인창을 거쳐 실행
- 삭제 직후 Undo로 복구 가능
- Tab 삭제도 확인창 추가
- Tab 생성/삭제/순서 변경 후 Page Settings가 닫히지 않도록 개선
- Page Settings의 아직 저장하지 않은 이름/설명 draft를 Tab 관리 중 유지

### 7. Field 편집 흐름
- Field 순서 변경 / Field 제거 후 Field/Input 편집창을 바로 다시 표시해 반복 편집 흐름을 끊지 않도록 변경
- Input 값 자체는 기존 원칙대로 Field 제거만으로 삭제되지 않음

## 검증 결과

### 정적 검사
- JavaScript syntax 검사 통과
- 중복 function 선언 0건
- inline event handler의 미정의 함수 참조 0건
- browser `prompt / alert / confirm` 사용 0건

### Chromium DOM 통합 검사
인메모리 저장 stub을 사용해 실제 DOM 버튼/입력 조작을 검사했습니다.
- Bookmark / Record / Tag / Category 검색 다중 문자 연속 입력 후 focus 유지
- Main 검색 focus 유지
- `/` 검색 shortcut
- `Esc` Modal 닫기
- Page Settings에서 Tab 생성 후 Modal 유지
- Tab 삭제 확인 → 삭제 → Page Settings 유지
- Page 삭제 확인창
- Undo → Redo 상태 복원
- 390×844 viewport에서 document 전체 가로 overflow 없음
- runtime exception 0건

### 주요 Tab smoke test
- Bookmark 생성 Modal 열기
- Folder Modal
- Bookmark Filter Modal
- Record 생성: 2 → 3개
- Tag 생성: 6 → 7개
- Category 생성: 3 → 4개
- DB Check: 구조 오류 0건
- runtime exception 0건

### 복구 로직 단위 통합 검사
IndexedDB API를 인메모리 stub으로 대체해 `load()` 복구 흐름 자체를 검사했습니다.
- pageOrder 손상 DB: 사용자 정의 `KEEP_ME` Page를 유지하면서 자동 수리 성공
- 오류 원본 recovery snapshot 생성 확인
- Format 손상 DB: 복구 모드 진입 확인
- 복구 모드에서 기존 손상 DB를 새 fresh DB로 자동 덮어쓰지 않는 것 확인

## 테스트 제한
현재 실행 환경의 Chromium 정책이 `localhost`, `file:`, 임의 테스트 origin navigation을 차단하여 **실제 IndexedDB를 사용한 브라우저 reload 영속성 테스트는 수행하지 못했습니다.**

따라서 v4.16의 IndexedDB recovery/load 흐름은 동일 API 계약의 인메모리 stub으로 검증했고, 실제 DOM 통합 검사는 Chromium에서 수행했습니다.
