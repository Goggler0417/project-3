# Tagmark v4.23

v4.22의 컴팩트 Field 편집기를 바탕으로, 사용자에게 보이는 개념과 명칭을 다시 정리한 버전입니다.

## 핵심 변경

- 표시 유형의 `Profile` 명칭을 `Record`로 통일
- Field 편집의 `정보 유형 + 입력 방식 + 표시 유형` 3축을 `정보 형식 + 표시 방식` 중심으로 단순화
- 정보 형식은 6개 개념군으로 묶음
  - Text: 한 줄 / 여러 줄 / URL
  - Number: 숫자 / 시간 길이
  - Date & Time: 날짜 / 날짜+시간
  - Boolean: 예/아니오
  - Choice: 드롭다운 / 라디오 / 체크박스(복수 선택) / 순환 버튼
  - Relation: Tag / Record / Category — 모두 같은 검색/선택 UI를 사용하고 대상만 다름
- 표시 방식은 Title / Item / Tag / Memo / Record 체계 유지
- 기존 `Hidden` 표시가 있는 데이터는 호환을 위해 `표시 안 함 (기존 설정)`으로만 노출

## 작명 정리

내부 데이터 키와 ID 구조는 그대로 유지하면서 사용자 UI만 더 직관적으로 바꿨습니다.

- Field → 영역 / 표시 영역
- Input → 정보 항목
- Placement → 표시 위치
- Field / Input → 표시 구성
- Input Library → 전체 정보 항목
- Tag Head → 태그 그룹
- Auto Folder → 값별 자동 그룹
- Tab Settings → 탭 설정
- Sort / Filter → 정렬 / 필터
- Profile 보기/표시 → Record 카드

## 고급 표시 설정

기존의 추상적인 이름을 기능이 바로 드러나도록 변경했습니다.

- `Field 배치` → `영역 안 항목 배치`
  - `세로로 한 항목씩`
  - `한 줄에 나란히`
- `라벨` → `항목 이름 표시`
  - `표시하지 않음`
  - `값 위에 표시`
  - `값 앞에 표시`
- `규칙` → `언제 표시할지`
  - `항상 표시`
  - `값이 지정한 값과 같을 때만`
  - `값에 지정한 내용이 들어 있을 때만`
  - Tag 정보에서는 `선택한 태그 그룹의 태그만 표시`
- `규칙 값` → 조건에 따라 `같아야 하는 값` / `포함해야 하는 내용`
- `접두` → `값 앞에 붙일 글자`
- `접미` → `값 뒤에 붙일 글자`

## 호환성

- DB format과 IndexedDB 이름은 v4.22와 동일
- 기존 Relation / Field / Placement / Input 내부 구조 유지
- 같은 정보 항목을 여러 표시 위치에서 참조하는 구조 유지
- 기존 distribution 데이터는 UI에서는 숨기지만 레거시 렌더링 호환을 위해 내부적으로 유지
- Choice 선택지 삭제에 대한 파괴적 새 동작은 추가하지 않음

## QA

- JavaScript syntax 검사 통과
- 중복 named function 0
- native prompt / alert / confirm 0
- Field/Placement drag & drop 함수 유지 확인
- 표시 구성에서 별도 입력 방식 dropdown 제거 확인
- `Tag Head =`, `값 =`, `접두`, `접미`, `라벨`, `규칙` 등의 추상적 UI 문구 제거
- 데스크톱 및 390px 모바일 폭에서 표시 구성 modal 가로 overflow 0 확인
- 브라우저 스텁 환경에서 초기 렌더 + 표시 구성 modal runtime error 0 확인
