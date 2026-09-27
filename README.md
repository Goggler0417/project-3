# Tagmark v4.18

## 이번 버전
v1/v2 시각 컴포넌트 견본판에서 확정한 규칙을 본체에 적용했습니다.

### 확정된 시각 규칙
- 데이터 카드: v2
  - 1px border
  - radius 12px
  - padding 14px
  - 매우 약한 shadow
- Tag chip: v2 pill
  - 4px 8px
  - 12px
  - Tag 색상을 pill 배경으로 사용
  - pill 글자색은 배경 밝기에 따라 자동으로 검정/흰색 선택
- 버튼: v2
  - radius 9px
  - 기본 높이 38px
- Tabs: v2
- Bookmark Folder: v1
  - header/body 분리
  - radius 12px
- Category / Profile / Settings Box: 기존 확정안 유지
- Modal Shell: v2
  - 공통 radius 15px
  - 공통 Header / Body / Footer 규칙
  - 내용에 따라 narrow / normal / wide 폭만 다름
- Page Card / Empty State: 기존 확정안 유지

### 공통 Form 규격
Input / Select / Textarea를 전역 공통 규격으로 통일했습니다.
- border 1px
- radius 8px
- 일반 Input/Select 높이 38px
- padding 9px 10px
- 같은 focus ring
- color input만 기능상 별도 높이/내부 padding 사용
- textarea는 같은 외형 규격을 쓰되 내용 입력을 위해 높이만 더 큼

즉 Modal마다 Input 규격을 별도로 정의하지 않습니다.

## Tag 색상 시스템

### 기본 동작
- Tag Head에는 기본 색상이 있습니다.
- 각 Tag는 선택적으로 고유 색상을 가질 수 있습니다.
- 고유 색상이 없으면 Head 색상을 사용합니다.

### 표시 전용 Head 통일
Tag Tab toolbar에서 Page 전체 표시 방식을 선택할 수 있습니다.

- `색상: 개별 + Head 기본`
  - Tag 고유 색상이 있으면 그것을 표시
  - 없으면 Head 색상 사용
- `색상: Head로 표시 통일`
  - 모든 Tag pill을 현재 Head 색상으로 표시
  - 각 Tag에 저장된 고유 색상 정보는 변경하거나 삭제하지 않음

이 표시 방식은 Bookmark 카드 Tag chip, Record Profile Tag chip, Tag 관리 화면 등에 동일하게 적용됩니다.

### 선택 Tag 색상 일괄 변경
Tag 선택 → `색상 변경`에서 세 가지 작업을 지원합니다.

1. `Head 기본값 따라가기`
   - Tag의 고유 색상 값을 제거
   - 이후 Head 색상을 따라감
2. `현재 Head 색으로 값 저장`
   - 선택된 각 Tag의 현재 Head 색상을 해당 Tag의 고유 색상 값으로 복사
   - 서로 다른 Head의 Tag를 동시에 선택해도 각각 자기 Head 색상을 저장
   - 이후 Head 색이 바뀌어도 저장된 Tag 색은 유지
3. `지정 색상 적용`
   - 선택된 Tag 전체에 사용자가 고른 동일 색상 적용

## 검증
- JavaScript syntax 검사 통과
- 중복 function 선언 0건
- Chromium 실제 DOM 통합 검사
  - v2 버튼: radius 9px / min-height 38px
  - v2 Tab radius 확인
  - Bookmark 데이터 카드: radius 12px / padding 14px
  - v1 Folder: radius 12px / header padding 11px 12px
  - 공통 Input: radius 8px / min-height 38px
  - Tag 개별 색상 표시 확인
  - Head 표시 통일 시 실제 Tag 색상 값이 보존되는 것 확인
  - 선택 Tag `현재 Head 색으로 값 저장` 확인
  - 선택 Tag 사용자 지정 색상 일괄 적용 확인
  - `Head 기본값 따라가기`로 고유 색상 제거 확인
  - Bookmark 카드에 colored Tag pill 표시 확인
  - Record Profile에 colored Tag pill 표시 확인
  - v2 Modal radius 15px 확인
  - validate(db) 구조 오류 0
  - dangling relation 0
  - runtime exception 0
- 모바일 390×844
  - Bookmark / Record / Tag / Category 모두 document horizontal overflow 0

## 테스트 제한
브라우저 실행 정책 때문에 실제 배포 파일의 IndexedDB 저장 → 브라우저 프로세스 종료 → 재실행 영속성 검사는 이번 DOM 테스트에서 수행하지 않았습니다.
DOM 통합 테스트에서는 저장 함수만 인메모리 방식으로 대체했고, 배포용 `index.html`의 IndexedDB 코드는 변경하지 않았습니다.
