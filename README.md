# cmux-browser-first

CMUX 내장 브라우저를 Claude Code의 기본 브라우저 도구로 설정하는 플러그인 마켓플레이스.

## 플러그인

### cmux-browser-first

브라우저 작업 시 `cmux_browser_*` 도구를 항상 우선 사용하도록 강제합니다.
`mcp__claude-in-chrome__*`은 CMUX 불가 시에만 fallback.

#### 슬래시 커맨드

| 커맨드 | 설명 |
|--------|------|
| `/browse <url>` | CMUX 브라우저로 URL 열기 + 스냅샷 |
| `/browse-check` | 현재 페이지 품질 검증 |
| `/browse-compare <url1> <url2>` | 두 페이지 비교 |

## 설치

```bash
# Claude Code 설정에서 마켓플레이스 추가 후
claude plugins install cmux-browser-first
```

## 요구사항

- CMUX 터미널 앱
- CMUX MCP 서버 (`claude mcp add cmux`)
