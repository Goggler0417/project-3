# Tagmark v4.26

Record 입력기를 `Relation · Record` 기반의 범용 입력기로 확장한 버전입니다.

## 주요 변경

- Record 유형을 Record Schema 기준으로 구분합니다.
- 각 Record는 자신이 속한 `schemaId`를 보존합니다.
- `Relation · Record` 정보 항목에서 불러올 Record 유형을 지정할 수 있습니다.
- Record 검색 결과는 지정된 Record 유형만 표시합니다.
- 기존 Record 검색/단일·복수 선택/제거 기능을 유지합니다.
- 검색어와 같은 새 Record를 현재 Bookmark 입력 중 바로 등록할 수 있습니다.
- 새 Record 등록 폼은 해당 Record Schema의 정보 항목을 불러옵니다.
- 표시 구성 > 고급 > `Record 입력 설정`에서 다음을 조정할 수 있습니다.
  - 불러올 Record 유형
  - 단일/복수 선택
  - 새 Record 즉시 등록 허용 여부
  - 새 Record 등록 폼에 보여줄 정보
  - 검색 결과/선택 카드에 보여줄 보조 정보
  - Record 정보 → Bookmark 정보 자동 채우기 대상
- 선택한 Record는 이름만 있는 chip 대신 유형과 보조 정보가 포함된 작은 Record 블록으로 표시됩니다.
- Bookmark에서 Record를 선택하면 설정된 정보를 빈 Bookmark 입력칸에 자동으로 복사합니다.
- 같은 Input을 Bookmark와 Record Schema가 공유하면 별도 매핑 없이 같은 Input으로 자동 채웁니다.
- 기존 사용자가 직접 입력한 값은 자동으로 덮어쓰지 않습니다.
- 자동으로 채운 값의 출처를 Bookmark 내부 metadata로 보존합니다.
- `정보 다시 불러오기`로 해당 Record의 최신 정보를 수동 재적용할 수 있습니다.
- Record 연결을 해제해도 이미 Bookmark에 복사된 다른 정보는 자동 삭제하지 않습니다.
- 기존 v4 Record는 로드 시 기존 기본 Record Schema에 안전하게 귀속됩니다.
- Bookmark의 기존 Character/Cast 전용 빠른 추가 버튼은 Record 입력기에서 대체됩니다.

## QA

- JavaScript `node --check` 통과
- 중복 named function 0
- native `prompt / alert / confirm` 0
- HTML5 `draggable=true` 0
- Record Schema별 검색 필터 및 legacy Record type migration 로직 테스트 통과

브라우저 실행 기반 QA는 현재 실행 환경의 로컬 페이지 접근 제한 때문에 수행하지 못했습니다. Mac/iPad의 실제 브라우저에서 Record 검색, 새 Record 등록, 자동 채우기 흐름을 한 번 최종 확인하는 것이 좋습니다.
