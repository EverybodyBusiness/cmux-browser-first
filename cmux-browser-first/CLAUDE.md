# CMUX Browser First — 브라우저 우선순위 규칙

브라우저 작업이 필요할 때 **반드시 CMUX 브라우저 도구를 먼저** 사용한다.
`mcp__claude-in-chrome__*` 도구는 CMUX 브라우저가 불가능한 경우에만 fallback으로 사용한다.

## 우선순위

1. **CMUX 브라우저** (`cmux_browser_*`) — 항상 첫 번째 선택
2. **Chrome in Chrome** (`mcp__claude-in-chrome__*`) — CMUX 불가 시에만 fallback

## CMUX 브라우저 도구 워크플로우

기본 순서: `cmux_browser_open` → `cmux_browser_snapshot` → `cmux_browser_query` → `cmux_browser_interact`

## 도구 매핑 (CMUX 우선)

| 작업 | CMUX (우선) | Chrome (fallback) |
|------|------------|------------------|
| URL 열기 | `cmux_browser_open` | `mcp__claude-in-chrome__navigate` |
| 페이지 읽기 | `cmux_browser_snapshot` | `mcp__claude-in-chrome__read_page` |
| 텍스트 추출 | `cmux_browser_query(action: "text")` | `mcp__claude-in-chrome__get_page_text` |
| JS 실행 | `cmux_browser_evaluate(action: "eval")` | `mcp__claude-in-chrome__javascript_tool` |
| 클릭/입력 | `cmux_browser_interact` | `mcp__claude-in-chrome__computer` / `mcp__claude-in-chrome__form_input` |
| 에러 확인 | `cmux_browser_network(action: "errors")` + `cmux_console_log` | `mcp__claude-in-chrome__read_console_messages` |
| 네트워크 | `cmux_browser_network(action: "requests")` | `mcp__claude-in-chrome__read_network_requests` |
| 스크린샷 | `cmux_browser_snapshot` | `mcp__claude-in-chrome__read_page` |
| 탭 관리 | `cmux_surface_manage` + `cmux_browser_open` | `mcp__claude-in-chrome__tabs_create_mcp` |

## CMUX fallback 조건

다음 경우에만 Chrome in Chrome으로 전환:
- CMUX MCP 서버가 연결되지 않은 경우
- CMUX 브라우저 도구 호출이 실패하고 재시도해도 안 되는 경우
- 사용자가 명시적으로 Chrome 사용을 요청한 경우
- CMUX에 없는 고유 기능이 필요한 경우 (예: GIF 녹화 `gif_creator`)

## 주의사항

- "URL 열어봐", "사이트 확인해봐" 등의 요청 시 → 항상 `cmux_browser_open` 사용
- 페이지 분석/스크래핑 요청 시 → `cmux_browser_snapshot` + `cmux_browser_query` 사용
- DOM 조작/폼 입력 시 → `cmux_browser_interact` 사용
- 절대 Chrome 도구를 먼저 시도하지 않는다
