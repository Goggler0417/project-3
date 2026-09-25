# Tagmark v4.03

v4.02의 모바일 UI와 기존 기능을 유지하면서 남아 있던 v4 핵심 기능을 확장한 버전입니다.

## 이번 버전
- Bookmark/Record Filter: AND/OR 선택 지원
- Tag Filter: 중립 → 포함 → 제외 순환
- Category Filter: Category 선택 + 하위 포함/정확히 조건
- Display Rule: 모두/equals/contains/Remaining
- Input 분배: Independent / Priority
- 미지정 정보: Entity 편집 화면에서 직접 수정 가능
- 기존 Bulk Input 편집 및 Folder 이동 유지
- DB Check: 안전하게 판단 가능한 일부 dangling/order 문제 자동 수리
- 대량 결과 렌더링 보호: 한 화면 최대 300 logical results 렌더링
- v4.02 모바일 대응 유지
- Tab/Field 순서 변경 및 등장인물/Record 복합 추가 기능 유지

## 이후 단계
v4 핵심 기능 안정화 이후에는 v1/v2/v3의 실제 파일을 다시 대조하여, v4에 아직 없는 편의 기능과 사용 흐름을 선별 복원합니다. UI도 구형 Tagmark의 익숙한 배치/스타일을 기준으로 이식하되 v4 데이터 구조는 유지합니다.

## 검사
- JavaScript `node --check` 구문 검사 통과.
- 실제 브라우저/모바일 기기에서의 클릭·터치 통합 테스트는 이 환경에서 수행하지 않았습니다.
