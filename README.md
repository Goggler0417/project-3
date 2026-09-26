# Tagmark v4.10

## 이번 버전
v4.09를 기준으로 **Tag Tab의 시각적 UI와 관리 흐름을 v1/v2 계열에 가깝게 복원**한 버전입니다. 다른 데이터 모델이나 Bookmark/Record/Category 구조를 새로 바꾸는 작업은 하지 않았습니다.

### Tag Tab UI
- 전체폭 접이식 **Tag Head 섹션 + Tag chip** 기본 보기
- 별도 **리스트 보기** 제공
- Tag 이름과 Tag Head 이름을 함께 검색
- `전체 / 사용 중 / 미사용` 표시 필터
- `이름순 / 사용량순 / 최근 생성순` 정렬 및 방향 전환
- Tag 사용량을 현재 Page의 Bookmark/Record 참조에서 계산하여 표시
- 미사용 Tag는 흐리게 표시
- 미사용 필터에서는 각 Tag 옆 `×`로 바로 삭제 가능

### 통합 Tag 입력
- v1 계열처럼 하나의 입력창에서 Tag 생성
- 여러 Tag Head를 동시에 선택하여 같은 이름의 Tag를 각 Head에 한 번에 등록 가능
- 선택한 Head 상태는 해당 Tag Tab 설정에 저장되며 등록 후에도 유지
- Tag 이름 입력값은 Head 선택 변경 때문에 사라지지 않도록 Runtime draft로 유지
- 각 Tag Head의 `＋` 버튼은 통합 입력창을 해당 Head에 맞춰 바로 준비

### Tag 관리
- Tag chip 클릭은 관리 선택으로 동작
- 단일 선택 시 수정 가능
- 선택 Tag 일괄 Head 이동
- 선택 Tag 일괄 색상 변경
- `Head 색 사용`으로 개별 Tag 색상 override 제거 가능
- Tag Head 이름/색상 수정
- Tag Head 순서 ↑/↓ 변경
- Tag Head 삭제는 기존 v4 방식 유지:
  - 소속 Tag를 다른 Head로 이동 후 Head 삭제
  - 또는 Head + 소속 Tag 함께 삭제
- 삭제된 Head가 통합 입력창 선택 상태에 남지 않도록 정리

### 표시 색상
- Tag Head에 색상을 저장
- Tag는 기본적으로 소속 Head 색상을 사용
- 필요할 경우 Tag별 개별 색상 override 가능
- 테스트 Page의 Head에도 구분 가능한 샘플 색상 포함

### 기타 수정
- 브라우저 inline event handler에서 `body()` 이름이 HTML `body`와 충돌할 수 있는 문제를 확인하여 내부 화면 갱신 함수를 `renderBody()`로 정리했습니다.
- 기존 테스트 Page는 계속 Bookmark / Record / Tag / Category / Folder 샘플 데이터를 포함합니다.

## 이번에 보류한 항목
v1의 `중립 → 포함 → 제외 → 중립` Tag filter UI는 이번 Tag Tab 복원에는 노출하지 않았습니다. v4에서는 Filter가 Tab별 설정이므로, 향후 **Bookmark Tab에서 여는 Tag Filter modal**의 의미와 대상 Relation Input을 확정한 뒤 넣는 편이 버그 위험이 낮습니다.

## 확인한 테스트
- JavaScript syntax check 통과
- 중복 함수 선언 0건
- Headless Chromium DOM 클릭 테스트 통과:
  - Bookmark 검색
  - Tag Tab 진입
  - 기본 Tag/Head 렌더링
  - 통합 입력 Head 선택 유지
  - 입력 중 Head 선택 변경 시 draft 유지
  - 다중 Head Tag 생성
  - 미사용 Tag 즉시 삭제
  - Tag 선택/Bulk bar
  - 색상 일괄 변경
  - Head 일괄 이동
  - 시각화/리스트 전환
  - Tag Head 이름 검색
  - Record/Category Tab 이동 smoke test
- 모바일 390×844 기준 document horizontal overflow 없음

### 테스트 제한
현재 실행 환경은 로컬 파일 URL 접근이 브라우저 정책으로 차단되어 있으므로, Chromium 통합 테스트에서는 IndexedDB 계층만 인메모리 테스트 저장으로 대체했습니다. 실제 UI/DOM event와 Controller 동작은 Chromium에서 실행했지만, 실제 IndexedDB에 저장한 뒤 브라우저를 완전히 재시작하는 영속성 테스트까지 수행한 것은 아닙니다.
