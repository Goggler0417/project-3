# Tagmark v4.22

Field 편집을 3축 드롭다운 중심으로 다시 단순화한 버전입니다.

- Tag Head 앞 장식 점 markup 제거
- Field/Placement 순서 변경 버튼 제거
- Field와 Placement 순서는 drag & drop으로 변경
- Placement 기본 행은 Input / 정보 유형 / 입력 방식 / 표시 유형으로 한 줄 구성
- 정보 유형은 Value(Text/Long Text/Number/Boolean/URL/Date/DateTime/Duration/Choice), Tag, Profile/Record, Category 지원
- 입력 방식과 표시 유형은 정보 유형에 맞는 후보만 노출
- 같은 Input 분배 설정 UI 제거 (기존 레거시 데이터는 호환을 위해 내부적으로 보존)
- Label / Rule / Prefix / Suffix는 고급 설정 안에만 유지
- 저장 값이 있는 Input은 정보 유형 변경 잠금

DB format과 IndexedDB 이름은 유지됩니다.
