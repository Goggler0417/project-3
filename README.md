# Tagmark v4.14

## 이번 버전
공통 Modal/Form UI와 Field/Input 편집 화면을 정리했습니다. Canonical DB 형식은 변경하지 않았습니다.

### 공통 Modal/Form
- 모든 기본 Modal에 공통 Header / 닫기 버튼 / 스크롤 Body / 고정 Footer 적용
- 데스크톱 wide / narrow 크기 지원
- 모바일에서는 bottom sheet 형태 유지
- Input / Select / Textarea의 간격, focus, 도움말 스타일 통일
- Sub Modal도 같은 시각 체계로 통일

### Field / Input
- Field / Input 화면을 wide 관리 화면으로 재구성
- Field 수 / 현재 Schema Input 수 / Placement 수 표시
- Field 순서 변경, 이름 변경, Bookmark 카드 Field 배치 유지
- Placement를 접이식 항목으로 정리
- Placement 순서 변경 / Placement 제거 추가
- 기존 Input을 원하는 Field에 추가 배치 가능
- 빈 Field 생성 가능
- 새 Input + Field 생성에서 Text / Long text / Number / Boolean / URL / Date / DateTime / Duration / Tag·Record·Bookmark·Category Relation 지원
- Relation 다중값 선택 가능
- Bookmark 카드 표시 형식 / 라벨 / 입력 방식 / 접두·접미 유지
- Independent / Priority 및 Display Rule 유지
- Page Input Library에서 Input 종류와 배치 수 확인 및 현재 Schema에 배치 가능
- Field 삭제와 Placement 제거는 실제 Input 값 자체를 삭제하지 않음

### 기존 기능
- v4.13 Main / Page Shell 유지
- Bookmark / Tag / Category / Record UI 및 기능 유지
- v1 / v2 Bookmark 프리셋 유지

## 검증
- JavaScript syntax 검사 통과
- 중복 function 선언 0건
- Chromium 실제 DOM 클릭 smoke test 통과
  - Bookmark Tab → Field / Input 열기
  - 공통 Modal Header / Body / Footer / 닫기 버튼
  - 빈 Field 생성
  - 기존 Input 배치 Sub Modal
  - Placement 생성
  - Field / Input 저장
  - Tab Settings wide Modal
  - 새 Input + Field Sub Modal의 Duration / Relation 타입 확인
- 390×844 모바일 viewport에서 document 전체 가로 overflow 없음
- 모바일 Modal이 bottom sheet 형태로 전환되는 것 확인

## 테스트 제한
이 실행 환경은 `file:` 및 localhost/data URL을 Chromium에서 정책상 차단합니다.
따라서 테스트 HTML을 about:blank 문서에 주입하고 실제 DOM 버튼을 클릭하는 방식으로 UI/Controller를 검사했습니다.
저장 계층은 테스트 시 인메모리 persist로 대체했으며, 실제 IndexedDB 브라우저 재시작 영속성은 이번 검사 범위에 포함되지 않습니다.
배포용 `index.html`의 IndexedDB 구현 자체는 변경하지 않았습니다.
