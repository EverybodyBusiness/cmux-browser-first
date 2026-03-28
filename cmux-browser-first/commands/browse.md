---
description: "CMUX 브라우저로 URL 열기 + 스냅샷 확인"
argument-hint: "<url>"
---

CMUX 내장 브라우저를 사용하여 $ARGUMENTS URL을 탐색합니다.

## 실행 순서

1. `cmux_identify`로 현재 컨텍스트(window/workspace/surface) 확인
2. `cmux_browser_open`으로 브라우저 열기 + URL 이동
   - URL이 제공되지 않으면 사용자에게 물어보기
3. `cmux_browser_snapshot`으로 페이지 접근성 트리 + 제목 + URL 확인
4. 페이지 로드 결과 보고:
   - 페이지 제목
   - 현재 URL
   - 주요 콘텐츠 구조 요약
5. 에러가 있으면 `cmux_browser_network(action: "errors")` + `cmux_console_log`로 확인

**중요**: `mcp__claude-in-chrome__navigate`가 아닌 반드시 `cmux_browser_open`을 사용할 것.
