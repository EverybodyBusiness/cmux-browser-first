---
description: "두 페이지를 나란히 열고 구조/스타일 비교"
argument-hint: "<url1> <url2>"
---

두 URL의 페이지를 CMUX 브라우저로 나란히 열고 구조와 콘텐츠를 비교합니다.

$ARGUMENTS에서 두 URL을 파싱합니다 (공백으로 구분).

## 실행 순서

### 1. 환경 준비
- `cmux_identify`로 현재 컨텍스트 확인
- `cmux_surface_manage(action: "split", direction: "horizontal")`로 화면 분할

### 2. 페이지 A 열기 (왼쪽 패널)
- `cmux_browser_open`으로 첫 번째 URL 열기
- `cmux_browser_snapshot`으로 구조 캡처
- `cmux_browser_query(action: "text")`로 텍스트 추출

### 3. 페이지 B 열기 (오른쪽 패널)
- 새 서피스로 포커스 이동
- `cmux_browser_open`으로 두 번째 URL 열기
- `cmux_browser_snapshot`으로 구조 캡처
- `cmux_browser_query(action: "text")`로 텍스트 추출

### 4. 비교 분석
두 페이지를 다음 항목으로 비교:

| 비교 항목 | 페이지 A | 페이지 B |
|-----------|----------|----------|
| 제목 | ... | ... |
| URL | ... | ... |
| heading 구조 | ... | ... |
| 주요 콘텐츠 | ... | ... |
| 링크 수 | ... | ... |
| 이미지 수 | ... | ... |
| 에러 유무 | ... | ... |

### 5. 차이점 요약
- 구조적 차이 (DOM 트리, heading 계층)
- 콘텐츠 차이 (텍스트, 이미지, 링크)
- 기술적 차이 (에러, 성능)
