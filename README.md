# 나만의 클로드 OS

넥스트스텝(박재성) **"나만의 클로드 OS 만들기"** 4일 워크숍 실습 저장소.

> "OS는 완벽하지 않아도 됩니다. 나만의 관점을 담았다면 그걸로 충분합니다."

## 프로젝트 목적

AI-Native 시대에 *나만의 관점을 담은 클로드 OS*를 점진적으로 구축한다.
완벽함이 아니라 *나의 일하는 방식*을 시스템화하는 것이 목표.

## 워크숍 커리큘럼

| Day | 주제 | 핵심 |
|---|---|---|
| 1 | 에이전틱(Agentic) | OS 목표 정의 및 기본기 |
| 2 | 컨텍스트(Context) | AI에게 양질의 정보를 제공하는 최적화 전략 |
| 3 | 랄프 루프(Ralph Loop) | AI가 스스로 일하게 만드는 루프 설계 |
| 4 | 하네스(Harness) | AI의 한계를 극복하는 구조적 해법 |

## Claude 작업 환경

이 프로젝트의 Claude는 **두 층의 설정**을 합쳐 사용한다.

### 셋업 아키텍처

```
┌─ [별도 저장소] github.com/ericagong/claude ────────────────────┐
│   ├── .claude/CLAUDE.md      ──┐                              │
│   ├── .claude/settings.json  ──┤ symlink                      │
│   └── external/karpathy-skills/  (multica-ai submodule)       │
└────────────────────────────────│──────────────────────────────┘
                                 ↓
            ~/.claude/CLAUDE.md       ← 모든 프로젝트에 자동 로딩
            ~/.claude/settings.json   ← SessionStart hook이 매 세션 시작 시 자동 git pull

┌─ [이 프로젝트] github.com/ericagong/OS ───────────────────────┐
│   └── CLAUDE.md                ← 이 프로젝트에만 적용         │
└───────────────────────────────────────────────────────────────┘
                                 ↓
                  Claude Code가 두 층을 합쳐 컨텍스트로 사용
```

**핵심 메커니즘 3가지:**

1. **symlink**: 글로벌 설정 파일들은 `~/claude/` repo에 실재하고, `~/.claude/`에선 포인터(symlink)로 가리킨다. → 한 파일을 git으로 추적하면서도 Claude Code는 원래 위치에서 읽음
2. **`@import` 문법**: 글로벌 `CLAUDE.md`가 `@~/claude/external/karpathy-skills/CLAUDE.md`로 카파시 원본을 끌어옴. submodule이라 사본 없이 *항상 추적*
3. **SessionStart hook**: `~/claude/.claude/settings.json`에 등록. 매 Claude Code 세션 시작 시 `git pull --ff-only` + `git submodule update --remote`를 10초 이내 자동 실행 → 컴퓨터 간 자동 동기화

### 글로벌 층 → [ericagong/claude](https://github.com/ericagong/claude)

별도 저장소에서 관리. 새 컴퓨터에서도 `git clone` + symlink 두 개면 동일 셋업 완료.

- **카파시 4원칙** ([multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills) submodule을 `@import`)
  - Think Before Coding · Simplicity First · Surgical Changes · Goal-Driven Execution
- **언어 규칙** — 응답·주석·커밋·문서화는 한국어, 식별자는 영어
- **응답 스타일** — 변경 제안 시 AS-IS/TO-BE 비교, 옵션 제시 시 장단점, 추천 시 한계 명시, 새 개념 설명 시 5단계 구조

### 프로젝트 층 → [`./CLAUDE.md`](./CLAUDE.md)

이 OS 프로젝트에만 적용되는 특화 원칙. 세 원칙은 *서로 다른 차원*에서 작동한다.

- **단순함 우선** (*얼마나* 만들까) — 오버엔지니어링 말고 단순하게 구현. 충돌 시 최종 판정자
- **점진적 확장** (*언제* 만들까) — 미리 만들지 말 것, 필요할 때만 점진적으로 확장. 워크숍 단계(에이전틱 → 컨텍스트 → 랄프루프 → 하네스)에 맞춰
- **수단 적극 탐색** (*무엇으로* 풀까) — 적합한 수단이 기존에 있다면 DIY 말고 가장 적합한 것 사용. Skill·Plugin·MCP·서브에이전트·Hook 등 Claude Code ecosystem을 코드 작성의 대안으로 적극 활용

## 참고

- 워크숍: [넥스트스텝 — 나만의 클로드 OS 만들기](https://edu.nextstep.camp/c/anUjcv0e/)
- 라이센스: [LICENSE](./LICENSE)
