# probe-skills

AI와 함께 짧은 시간 안에 요구사항을 정리하고, 조각 단위로 구현하고, 사용자 눈으로 검토한 뒤 결정을 설명할 수 있게 만드는 Codex 스킬 여섯 개입니다. 어떤 주제의 과제에도 쓰도록 만들었고, 특정 과제의 답이나 조건은 들어 있지 않습니다.

모든 스킬은 같은 원칙을 따릅니다. 스킬은 분석과 정리를 맡고, 판단은 사람이 합니다. 그래서 스킬마다 반드시 멈추는 곳이 있고, 그 자리에서 사람이 고르거나 확인한 뒤에야 다음으로 넘어갑니다. 커밋은 사람이 눈으로 확인하고 '통과'라고 말한 뒤에만 합니다. 스킬이 저절로 끼어들지 않도록 모두 `agents/openai.yaml`에서 자동 호출을 끄고, `$스킬이름`으로 부를 때만 움직이게 했습니다.

## 언제 무엇을 부르나

`DATA.md`는 별도 Skill로 만들지 않습니다. 데이터 조사 이후 Codex에 직접 작성을 요청하고, 내용과 사용 계획을 본인이 확인·확정한 다음 `$probe-slice`를 호출합니다.

| 순서 | 때 | 부르는 말 | 만드는 것 | 멈추고 사람이 하는 일 |
| --- | --- | --- | --- | --- |
| 1 | 과제를 읽은 직후 | `$probe-interview` | INTERVIEW.md 틀 (질문 메모 칸 포함) | 인터뷰하며 채우고, 물은 줄은 지움 |
| 2 | 인터뷰와 데이터 사용 계획 확정 뒤 | `$probe-slice` | REQUIREMENTS.md, 인터뷰 대조표(빠짐·격하·추가·미답), 의존 관계 표, 시간 예산 표 | 빠짐과 격하를 고치고, 조각 순서와 미룸을 확정 |
| 3 | 킥오프 전 | `$probe-setup` | AGENTS.md, ENV.md, DECISIONS.md·HANDOFF.md 틀 | '이번 과제' 칸 확인 |
| 4 | 조각마다 | Codex에 직접 구현 지시 | 계획 5줄 → 구현과 확인 → 클릭 3개 → 통과 시 커밋 | 직접 눌러 보고 판정 |
| 5 | 동결 직후, 새 대화 | `$probe-blackbox` | REVIEW.md 시나리오(동시 수정 포함), R 대조표, 데모 동선 | 시나리오를 눌러 결과를 알려 주고 고칠 것 1~2개 고름 |
| 6 | 같은 검토 대화 | `$probe-security` | REVIEW.md 보안 점검 표 | 지금 고칠 것을 고름 |
| 7 | 제출 전 | `$probe-exam` | ARCHITECTURE.md, 예상 질문 8개와 답 재료 | 사실과 다른 줄을 고치고 서술형 준비 |

## 설치

작업 폴더(과제 저장소) 안에서 아래를 실행하면 스킬이 `.agents/skills`에 들어갑니다. Codex는 작업 폴더부터 저장소 맨 위까지의 `.agents/skills`를 읽고, 스킬이 바뀌면 대개 스스로 알아챕니다.

```
git clone https://github.com/jjw4649/probe-skills /tmp/probe-skills
mkdir -p .agents/skills
cp -R /tmp/probe-skills/.agents/skills/. .agents/skills/
```

Codex 입력줄에 `/skills`를 입력해 여섯 개가 보이는지 확인합니다. 보이지 않으면 Codex를 껐다가 다시 켭니다. 첫 커밋 때 `.agents` 폴더를 함께 커밋해 두면, 제출한 저장소만 보고도 어떤 작업 체계로 일했는지 알 수 있습니다.

## 파일 구성

```
.agents/skills/
  probe-interview/  SKILL.md, assets/INTERVIEW 틀, agents/openai.yaml
  probe-slice/      SKILL.md, assets/REQUIREMENTS 틀, agents/openai.yaml
  probe-setup/      SKILL.md, assets/(AGENTS·ENV·DECISIONS·HANDOFF 틀), agents/openai.yaml
  probe-blackbox/   SKILL.md, agents/openai.yaml
  probe-security/   SKILL.md, agents/openai.yaml
  probe-exam/       SKILL.md, agents/openai.yaml
```

## 만든 파일들의 관계

INTERVIEW.md는 들은 말 그대로, DATA.md는 데이터 조사와 사람이 확정한 사용 계획, REQUIREMENTS.md는 핵심 흐름과 성공 기준과 조각 순서, AGENTS.md는 AI가 일하는 규칙, ENV.md는 실행 환경과 할 수 없는 것, DECISIONS.md는 결정과 누가 정했는지와 약점과 오류, HANDOFF.md는 지금 상태 한 장, REVIEW.md는 검토 결과와 R 대조, ARCHITECTURE.md는 구조 설명입니다. 스킬은 이 파일들만 읽고 쓰기 때문에, 대화를 새로 열어도 같은 방식으로 이어집니다.
