# Tagmark v4.24

이번 수정은 탭 설정 단순화, Record/Bookmark 보기 방식 정리, 선택 툴바 축소, 표시 구성 drag & drop 교체에 초점을 맞췄습니다.

## 변경사항

- 표시 구성 drag & drop을 HTML5 `draggable` 기반에서 Pointer Events 기반으로 교체
  - 영역 순서 이동
  - 같은 영역 안 표시 위치 이동
  - 다른 영역으로 표시 위치 이동
  - 빈 영역으로 이동
  - drag 중 실제 삽입 위치 표시
  - 모달 가장자리에서 자동 스크롤
- Record 보기 방식 정리
  - 기존 Record 카드 보기를 `그리드`로 통일
  - 별도 일반 격자 보기는 제거
  - `그리드 / 목록` 두 상태만 순환 버튼으로 전환
- Bookmark 보기 방식
  - 탭 메인에 `보기 · 그리드 / 목록` 순환 버튼 배치
- 선택 툴바 축소
  - Bookmark / Record / Tag / Category 선택 툴바 공통 축소
  - 버튼 높이·패딩·글자 크기를 기존 일반 버튼보다 작게 조정
- 탭 설정 단순화
  - Bookmark/Record 카드의 정보 연결 설정 제거
  - 카드에 무엇을 어떻게 보여줄지는 `표시 구성`에서 관리하도록 정리
  - Bookmark 탭 설정에는 폴더 제목 아래 요약 정보만 유지
  - Tag 탭 설정에는 표시할 태그 그룹 설정 유지
- 기존 DB 호환성 유지
  - 이전 `recordPresentation`, convenience 매핑 값은 내부 호환 목적으로 유지할 수 있으나 탭 설정에서 노출하지 않음

## 정적 QA

- VERSION: 4.24
- JavaScript syntax: 통과
- 중복 named function: 없음
- native `prompt() / alert() / confirm()`: 없음
- HTML5 `draggable=`: 없음
- 표시 구성 drag handle은 Pointer Events 사용
- Bookmark/Record 탭 설정에서 Record 표시 정보 매핑 UI 제거 확인

브라우저 자동화 환경에서는 로컬 파일/localhost 실행이 관리자 정책에 의해 차단되어 실제 포인터 제스처 기반 runtime QA는 수행하지 못했습니다. 실제 브라우저에서 마우스/트랙패드/iPad 터치로 최종 확인이 권장됩니다.
