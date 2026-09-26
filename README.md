# Tagmark v4.12

## 이번 버전
Record Tab의 UI를 일반 Record 구조를 유지하면서 v1의 Profile / Character 화면을 재현할 수 있도록 복원했습니다.

### Record Tab
- Profile / Grid / List 보기 전환
- v1 Profile 스타일 카드: 이름, 종류/역할, 성별, Series, Tag, 설명, 추가 정보
- Profile 보기에서 Auto Folder와 결합해 v1의 Series별 접이식 Profile Folder 재현
- Record별 Bookmark 역참조 개수 표시
- Record 선택 / Bulk bar
- 검색, Sort, Filter, Auto Folder, Field/Input, Tab Settings 통합
- Profile 카드에서 수정 / 복제 / 삭제
- Tag Head 색상을 사용하는 Tag chip

### ID 기반 Profile 표시 연결
Tab Settings에서 실제 Input ID를 다음 역할에 연결합니다.
- 이름
- 종류/역할
- 성별
- Series / 그룹
- Tag relation
- 설명

Input 이름을 바꿔도 연결은 유지됩니다. Record 자체는 Character 전용 데이터가 아니며,
Profile 보기는 일반 Record 데이터 위에 얹히는 표시 방식입니다.

### v1 Profile 프리셋
Record Tab Settings의 `v1 Profile 프리셋 적용`을 사용하면:
- 필요한 Profile용 Input이 없을 때만 생성
- Profile 보기 활성화
- Series Input을 Auto Folder 기준으로 연결

### 테스트 Page
기능 테스트 Page의 Record Tab은 Alice / Bob 샘플 Record를
v1 Profile 보기 + Series Auto Folder 형태로 바로 확인할 수 있습니다.

## 검증
- JavaScript syntax 검사 통과
- 중복 function 선언 0건
- Headless Chromium 실제 DOM 클릭 통합 검사 통과
  - Record Tab 진입
  - Profile 카드 렌더링
  - Series Auto Folder
  - Record 편집 Modal
  - 선택 / Bulk bar
  - Profile / Grid / List 전환
  - Tab Settings Profile Input 연결
  - v1 Profile 프리셋
  - Folder 접기/펼치기
- 390×844 모바일 viewport에서 document 전체 가로 overflow 없음
- Runtime exception 0건
- v4.11 형식 Record Tab의 v4.12 설정 마이그레이션 별도 검사 통과
- 사용자가 명시적으로 비워 둔 Profile 연결값(null)은 마이그레이션이 다시 채우지 않도록 확인

## 테스트 제한
실행 환경 정책 때문에 실제 IndexedDB를 사용한 브라우저 재시작 영속성 테스트는 수행하지 못했습니다.
DOM 클릭 통합 검사에서는 저장 계층만 인메모리 방식으로 대체했습니다.
배포 index.html의 IndexedDB 구현 자체는 유지됩니다.
