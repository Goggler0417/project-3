# Tagmark v4.11

## 이번 버전
Category Tab의 시각적 UI와 관리 흐름을 v1의 계층형 카테고리 감각 + v4의 Page/Tab 구조에 맞게 복원했습니다.

### Category Tab
- 전체폭 계층형 Tree UI
- Category / 전체 경로 검색
- 전체 / 사용 중 / 미사용 필터
- 이름순 / 사용량순 정렬 + 방향 전환
- Category 직접 사용량 / 하위 포함 사용량 / 자식 수 표시
- 펼치기 / 접기 및 전체 펼치기 / 전체 접기
- 각 Category에서 하위 Category 빠른 추가
- Category 이름 및 부모 수정
- Tree / 경로 목록 보기 전환
- 관리 선택 모드
- 현재 결과 전체 선택 / 선택 해제
- 선택 Category 부모 일괄 변경
- 상위/하위 동시 선택 시 최상위 선택 Category만 이동하여 내부 계층 보존
- 삭제 시 두 방식 지원
  - 현재 Category만 삭제하고 하위 Category 승격
  - 하위 트리까지 함께 삭제
- Bulk 삭제에서도 동일한 안전 규칙 적용
- 삭제된 Category 참조는 Bookmark / Record 값에서 정리

## 기존 기능
v4.10까지의 Bookmark Tab, Tag Tab, Record, Folder, Schema/Input, Backup/Restore/Import/Export 등 기존 기능을 유지합니다.

## 테스트
- JavaScript syntax 검사 통과
- 중복 function 선언 0건 확인
- Headless Chromium DOM 클릭 통합 검사:
  - Category Tab 진입
  - Root Category 생성
  - 하위 Category 생성
  - Category 수정
  - 현재 Category만 삭제 후 하위 승격
  - 선택 모드 / Bulk bar
  - 부모 일괄 변경 Modal
  - Tree → 경로 목록 전환
  - 사용 상태 필터
  - 검색
- 390×844 모바일 viewport에서 문서 전체 가로 overflow 없음
- 위 테스트 중 runtime exception 0건

## 테스트 제한
실행 환경 정책으로 로컬 파일/localhost에서 실제 IndexedDB를 포함한 브라우저 재시작 영속성 테스트는 수행할 수 없었습니다.
DOM 클릭 통합 검사에서는 저장 계층만 인메모리 방식으로 대체했습니다.
실제 배포 index.html의 IndexedDB 구현 자체는 변경하지 않았습니다.
