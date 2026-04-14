<p align="center">
  <img src="harness_banner.png" alt="Hermes Meta Harness Banner" width="600">
</p>

# Hermes Meta Harness

Hermes Agent용 메타 하네스 스킬입니다.

이 저장소는 원래의 "harness" 개념을 Hermes에 맞게 다시 구성합니다. 도메인 분석, 멀티에이전트 위임 패턴 설계, 재사용 가능한 스킬 생성, 그리고 Hermes 도구 체계에 맞는 오케스트레이션 문서 작성을 목표로 합니다.

## 무엇을 하나요?

Hermes Meta Harness는 상위 레벨의 설계 스킬입니다. 트리거되면 다음을 수행하도록 설계됩니다.

- 도메인 또는 프로젝트를 분석한다
- 파이프라인, 팬아웃/팬인, 생성-검증, 감독자, 하이브리드 중 적절한 구조를 선택한다
- 전문 역할을 Hermes 서브에이전트 프롬프트와 워크플로우로 정리한다
- 반복 가능한 절차를 Hermes 스킬로 생성한다
- 이후 세션에서도 재사용 가능한 오케스트레이션 문서를 만든다
- 실제로 운영 가능한지 검증 체크리스트까지 제공한다

## 왜 별도 포팅이 필요한가?

원본 harness는 Claude Code의 에이전트 팀과 `.claude/*` 구조를 전제로 합니다.
하지만 Hermes는 실행 모델이 다릅니다.

- `TeamCreate`/`SendMessage` 대신 `delegate_task`
- 공유 실행 계획은 `todo`
- 지속 정보는 `memory`
- 스킬 경로는 `~/.hermes/skills/`
- 필요 시 `cronjob`, `browser`, `terminal`, `file` 조합 사용

따라서 단순 복사보다, Hermes 방식으로 재설계한 메타 하네스가 필요합니다.

## 저장소 구조

```
hermes-meta-harness/
├── README.md
├── README_KO.md
├── LICENSE
├── skills/
│   └── hermes-meta-harness/
│       ├── SKILL.md
│       └── references/
│           ├── delegation-patterns.md
│           ├── orchestrator-template.md
│           ├── skill-authoring-guide.md
│           ├── testing-guide.md
│           └── migration-notes.md
└── 원본 프로젝트에서 가져온 배너/이미지 자산
```

## 설치 방법

### Hermes에 수동 설치

```bash
mkdir -p ~/.hermes/skills
cp -r skills/hermes-meta-harness ~/.hermes/skills/hermes-meta-harness
```

설치 후 새 Hermes 세션을 시작하면 스킬 탐지가 쉬워집니다.

## 예상 트리거 문장

예시:
- "이 프로젝트용 하네스 설계해줘"
- "Hermes용 메타 하네스 만들어줘"
- "이 레포를 위한 재사용 가능한 에이전트 워크플로우 구성해줘"
- "전문 스킬과 오케스트레이션 문서를 생성해줘"
- "기존 하네스를 감사하고 진화시켜줘"

## 산출물 철학

이 하네스는 일회성 대화 답변이 아니라, 반복 실행 가능한 운영 자산을 만드는 데 초점을 둡니다.

대표 산출물:
- `SKILL.md`와 references를 갖춘 Hermes 스킬 폴더
- 역할, 입력, 출력, 실패 복구 경로를 담은 오케스트레이션 문서
- 재실행 가능한 workspace 규칙
- 검증 체크리스트와 스모크 테스트

## 지원 패턴

- 파이프라인
- 팬아웃 / 팬인
- 전문가 풀
- 생성 / 검증
- 감독자 패턴
- 하이브리드 오케스트레이션

자세한 내용은 `skills/hermes-meta-harness/references/delegation-patterns.md`를 보세요.

## 원본 harness와의 관계

이 저장소는 원본 `revfactory/harness` 저장소의 개념과 구조를 Hermes Agent용으로 포팅한 결과물입니다.
즉, 원본 repo의 메타 하네스 철학, 워크플로우, 역할 분리 아이디어를 Hermes 도구와 규약에 맞게 명시적으로 옮긴 버전입니다.

이 저장소는 Claude Code 플러그인이 아닙니다.
대신 원본의 유용한 발상을 유지하면서, 실제 실행 계층은 `delegate_task`, `todo`, `memory`, Hermes 스킬 디렉토리, 파일 기반 산출물 오케스트레이션 같은 Hermes 방식으로 번역했습니다.

## 라이선스

Apache 2.0
