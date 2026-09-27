# Tagmark v4.19

## 인터페이스 단순화
자주 쓰는 생성 / Filter / 선택만 전면에 두고, 구조·보기·설정 계열은 `더보기`로 단계적으로 숨겼습니다.

- Bookmark: Folder / Layout / Field·Input / Tab Settings → 더보기
- Record: Auto Folder / Field·Input / Tab Settings → 더보기
- Tag: Tag Head 생성·관리 / 보기 전환 / Tab Settings → 더보기
- Tag의 정렬 방향 + 전체 색상 표시 방식 → `표시` 메뉴
- Category: 전체 펼침·접기 / Tree·경로 전환 / Tab Settings → 더보기
- 위험 작업과 복합 작업은 기존 Modal 유지

기능과 Canonical DB 구조는 삭제하거나 단순화하지 않았습니다.

## Tag chip
v4.18의 진한 단색 pill을 v1 계열처럼 연하게 변경했습니다.
- 배경: Tag/Head 색상의 약 10% tint
- 글자: 실제 Tag/Head 색상
- 선택 시에만 약 17% tint + 얇은 outline
- 개별 색상 / Head 기본색 / Head 표시 통일 / 일괄 색상 변경 기능은 그대로 유지

## 검증
- JavaScript syntax 검사 통과
- 중복 function 선언 0
- 실제 Chromium 클릭 QA는 이번 패키징 단계에서는 수행하지 않았습니다.
