# 금주의 키워드 — 주니어 개발자를 위한 안내서

매주 키워드 하나를 골라, **왜 그것이 존재하게 됐는지**부터 **우리 스택 어디에 숨어 있는지**까지 한 편으로 끝내는 학습 문서 모음입니다.

각 편은 **독립적**입니다. 다른 편을 읽지 않아도 완결되고, 필요한 개념은 그 자리에서 정의합니다.

## 목록

| # | 키워드 | 날짜 |
|---|---|---|
| 07 | [멱등성 — 같은 요청이 두 번 와도, 세상은 한 번만 바뀐다](idempotency-guide.html) | 2026-08-11 |
| 06 | [패킷 — HTTP 요청은 문자열 전송이 아니다](packet-guide.html) | 2026-08-03 |
| 05 | [WAL — Write-Ahead Logging](wal-guide.html) | 2026-07-28 |
| 04 | [안정 해싱 (Consistent Hashing Ring)](consistent-hashing-guide.html) | 2026-07-20 |
| 03 | [스케줄러 (CPU)](scheduler-cpu-guide.html) | 2026-07-16 |
| 02 | [CGI — 웹서버와 WAS는 왜 갈라졌나](cgi-was-guide.html) | 2026-07-16 |
| 01 | [CQRS & 결정론적 알고리즘](cqrs-deterministic-guide.html) | 2026-07-01 |

## 작성 원칙

- **정확성** — 연도·수치·인물은 공식 문서와 원 논문으로 검증하고, 각 편 하단에 실제 확인에 쓴 출처만 남긴다. 검증 안 된 수치는 쓰지 않는다.
- **주니어 눈높이** — 전문 용어는 첫 등장 자리에서 한 문장으로 정의한다.
- **독립성** — "지난 편" 참조 금지. 한 편만 읽어도 완결된다.
- **실무 연결** — 추상 이론에서 끝내지 않고 Python·Django·nginx·PostgreSQL로 번역한다.

## 구조

정적 HTML 파일이 전부입니다. 빌드 단계 없음, 프레임워크 없음.

```
index.html                 목록 랜딩
<topic>-guide.html         각 편 (자체 완결형: CSS·JS 인라인)
```

외부 의존은 Google Fonts CDN 하나뿐이라 폴더째 복사해도 그대로 동작합니다.

## 로컬에서 보기

`file://`은 브라우저 자동화 도구가 막으므로 로컬 서버를 씁니다.

```bash
python3 -m http.server 8899 --bind 127.0.0.1
# http://127.0.0.1:8899
```

## 새 편 추가하기

1. `<topic>-guide.html` 작성 — 디자인 시스템은 기존 편의 `<style>` 블록을 그대로 복사한다 (시리즈 일관성, 다크/라이트 자동 대응 포함).
2. `index.html` 맨 위에 카드 추가 — 번호 +1, hero의 `📚 N편` pill도 함께 올린다.
3. 이 README의 목록 표에 한 줄 추가.
4. **모바일 확인** — 375px과 320px에서 `documentElement.scrollWidth > clientWidth`이면 실패(페이지 전체 가로 스크롤).

### 모바일에서 자주 깨지는 지점

- **표 안의 긴 식별자는 반드시 `<code>`로 감쌀 것.** `innodb_flush_log_at_trx_commit` 같은 20자+ 토큰이 맨 텍스트로 있으면 표가 뷰포트를 밀어내 페이지 전체에 가로 스크롤이 생긴다. 줄바꿈 허용(`overflow-wrap: anywhere`)은 `code`에만 걸려 있다.
- **줄바꿈 허용을 셀(`td`) 전체로 넓히지 말 것.** 표는 안 넘치지만 `PostgreSQL`이 `Post/greS/QL`로 글자 단위로 쪼개진다.
- **표는 3열까지.** 375px에서 4열은 각 열이 80px 미만이 된다.
- `pre`와 `.diagram`은 `overflow-x: auto`로 자체 스크롤한다. 본문을 밀지 않으므로 정상이다.
