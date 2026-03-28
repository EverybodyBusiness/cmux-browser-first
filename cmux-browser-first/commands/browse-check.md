---
description: "현재 브라우저 페이지 품질 검증 (에러, 접근성, 레이아웃)"
---

현재 열린 CMUX 브라우저 페이지의 품질을 종합 검증합니다.

## 검증 항목

### 1. 기본 정보 수집
- `cmux_browser_snapshot`으로 페이지 구조 확인 (제목, URL, 접근성 트리)

### 2. 에러 검사
- `cmux_browser_network(action: "errors")`로 네트워크 에러 확인 (4xx, 5xx)
- `cmux_console_log`로 JavaScript 콘솔 에러 확인

### 3. 접근성 검사
- 스냅샷의 접근성 트리에서 주요 요소 확인:
  - heading 구조 (h1~h6 계층)
  - 이미지 alt 텍스트 유무
  - 폼 요소 label 연결
  - 링크 텍스트 의미

### 4. 레이아웃/콘텐츠 확인
- `cmux_browser_query(action: "text")`로 주요 텍스트 콘텐츠 추출
- `cmux_browser_evaluate(action: "eval")`로 viewport 크기, 스크롤 가능 영역 확인

### 5. 결과 보고
검증 결과를 표로 정리:

| 항목 | 상태 | 상세 |
|------|------|------|
| 페이지 로드 | PASS/FAIL | ... |
| 네트워크 에러 | PASS/FAIL | ... |
| JS 에러 | PASS/FAIL | ... |
| 접근성 | PASS/WARN/FAIL | ... |
| 콘텐츠 | PASS/FAIL | ... |
