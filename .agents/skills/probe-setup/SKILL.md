---
name: probe-setup
description: 요구사항을 확정한 뒤 작업 규칙 파일을 만든다. AGENTS.md(고정 세 칸 + 그날 채우는 두 칸), ENV.md(실행 환경 점검), DECISIONS.md와 HANDOFF.md 틀을 만들고 멈춘다. "$probe-setup"으로 부를 때만 쓴다.
---

# 작업 공간 준비

## 언제
REQUIREMENTS.md에서 조각 순서를 확정한 뒤, 킥오프 전에 한 번 부른다. 코드는 쓰지 않는다.

## 읽을 것
과제 README, INTERVIEW.md('## 물을 것' 칸은 사람의 질문 메모이므로 읽지 않는다), DATA.md, REQUIREMENTS.md, 이 스킬의 assets 폴더에 있는 틀 네 개.

## 순서
1. `assets/AGENTS-template.md`를 그대로 복사해 AGENTS.md를 만든다. 앞의 세 칸(일하는 방식, 확인과 기록, 품질 기준)은 한 글자도 바꾸지 않는다.
2. '데이터 규칙' 칸: DATA.md '사용 계획'이 있으면 그 파일과 열 이름을 한 줄 더한다. 없으면 틀의 기본 네 줄만 둔다.
3. '이번 과제' 칸: INTERVIEW.md의 금지·절차·1순위와 REQUIREMENTS.md의 한계선만 (금지)/(절차)/(목표) 꼬리표로 한 줄씩 옮긴다. 팀장이 말하지 않은 숫자는 쓰지 않고, 비어 있으면 "(목표) 미정, 내가 채움"으로 둔다.
4. ENV.md: 읽기만 하는 명령(언어 버전, 패키지 관리자, git 상태, 폴더 목록)을 승인 요청하고, 결과로 `assets/ENV-template.md`를 채운다. 서버를 켜거나 패키지를 설치하지 않는다.
5. DECISIONS.md가 없으면 `assets/DECISIONS-template.md`를 그대로 복사한다(머리줄과 작업 체계 한 줄).
6. HANDOFF.md가 없으면 `assets/HANDOFF-template.md`로 빈 틀만 만든다. 내용은 채우지 않는다.

## 멈추는 곳
다 만들면 아래 다섯 줄만 보고하고 멈춘다. 커밋은 사람이 '통과'라고 한 뒤에만 한다.
- 만든 파일 목록
- AGENTS.md '이번 과제' 칸 전체
- ENV.md에서 '할 수 없는 것'과 대체 방법
- 비어 있어 사람이 채워야 할 칸
- 사람이 할 일 한 줄

## 하지 말 것
- 고정 세 칸을 고치거나 줄을 더하기 ("자세히 설명해 줘", "필요하면 질문해 줘" 같은 줄 금지)
- INTERVIEW.md와 REQUIREMENTS.md에 없는 조건을 추측해서 '이번 과제'에 쓰기
- 코드 작성, 서버 켜기, 설치
