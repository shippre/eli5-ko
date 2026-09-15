# eli5-ko · 한국어로 쉽게 설명하기

**개념·코드·오류·기술 문서를 독자의 배경지식에 맞춰 쉬운 한국어로 설명하는 Codex 스킬입니다.**

초등학생부터 대학생, 엔지니어, 관리자까지 독자와 목적에 따라 어휘·비유·깊이를 조절합니다. 원리와 사실, 코드 식별자와 오류 원문을 보존하면서 이해를 돕습니다.

## 사용 예시

```text
$eli5-ko 과적합을 대학생 수준으로 설명해 줘.
학습 성능과 검증 성능이 왜 달라지는지도 작은 예시로 보여 줘.
```

```text
$eli5-ko 이 오류를 비전공자도 이해하게 설명해 줘: KeyError: 'age'
확인된 사실과 추가로 살펴봐야 할 부분을 구분해 줘.
```

```text
$eli5-ko 이 설계 문서를 팀장에게 설명할 수 있게 정리해 줘.
업무 영향, 선택 이유, 비용과 위험을 중심으로 설명해 줘.
```

## 설명 방식

1. 핵심 뜻이나 결론을 먼저 설명합니다.
2. 필요하면 친숙한 비유나 작은 예시를 듭니다.
3. 예시를 실제 작동 원리와 연결합니다.
4. 독자가 알아야 할 의미와 적용 범위를 정리합니다.

기본 말투는 자연스러운 한국어 존댓말입니다. 대상이 지정되지 않은 “쉽게 설명” 요청은 입문자 수준으로 시작합니다. 전문적인 깊이를 요청하면 그 수준에 맞춰 설명하며, 나이·직업·가족관계만으로 배경지식을 단정하지 않습니다.

코드를 읽은 결과와 실제 실행 결과를 구분합니다. 오류 메시지만으로 원인을 확정하지 않고, 비유가 실제 현상과 다른 부분은 필요한 만큼 설명합니다. 설명 요청 자체로 파일 수정이나 모델 학습을 시작하지 않습니다.

## 설치 — Windows PowerShell

원하는 폴더에서 저장소를 받습니다.

```powershell
git clone https://github.com/shippre/eli5-ko.git
Set-Location -LiteralPath .\eli5-ko
```

저장소 루트에서 아래 명령을 실행하면 개인 스킬 폴더에 설치합니다. 기존 `eli5-ko`가 있으면 멈추므로, 기존 사용자는 변경 내용을 먼저 비교해 주세요.

```powershell
$eli5SkillBase = if ($env:CODEX_HOME) {
    Join-Path $env:CODEX_HOME 'skills'
} else {
    Join-Path $env:USERPROFILE '.codex\skills'
}
$eli5Source = Join-Path (Get-Location).Path 'skills\eli5-ko'
$eli5Target = Join-Path $eli5SkillBase 'eli5-ko'
if (-not (Test-Path -LiteralPath (Join-Path $eli5Source 'SKILL.md'))) {
    throw '저장소 루트에서 실행해 주세요.'
}
if (Test-Path -LiteralPath $eli5Target) {
    throw '기존 eli5-ko가 있습니다. 변경 내용을 비교한 뒤 갱신해 주세요.'
}
New-Item -ItemType Directory -Path $eli5SkillBase -Force | Out-Null
Copy-Item -LiteralPath $eli5Source -Destination $eli5Target -Recurse
```

설치 후 새 작업에서 `$eli5-ko`를 호출합니다. 목록에 나타나지 않으면 사용 중인 클라이언트의 스킬 목록을 새로 고치거나 앱을 다시 엽니다. Markdown 지침이므로 별도 서버나 Python 실행 의존성은 없습니다.

## 파일 구성

```text
LICENSE
skills/eli5-ko/
  SKILL.md
  LICENSE
  agents/openai.yaml
```

설치·갱신할 때 라이선스를 포함한 `skills/eli5-ko` 전체를 사용합니다. 저장소 루트의 `LICENSE`와 스킬 폴더의 `LICENSE`는 같은 문서입니다.

## 출처와 라이선스

설치된 스킬의 출처 표시에 따라 [DreambigOu/ELI5](https://github.com/DreambigOu/ELI5)의 대상별 설명 방식을 참고한 Codex용 재구성입니다. 한국어 출력, 존댓말, 사실 정확성, 코드 확인과 실행의 구분을 포함합니다.

기존 [MIT 라이선스](LICENSE)의 저작권·허가 문구를 그대로 보존했습니다. 스킬 내부의 [출처 표시](skills/eli5-ko/SKILL.md)도 유지했습니다.

## 배포 검증

2026-09-16 기준 설치된 스킬에서 배포본을 만들었습니다. `skill-creator`의 구조 검사와 UTF-8·YAML·상대 링크 검사를 통과했습니다. 스킬 파일 3개의 SHA-256 해시가 설치된 원본과 일치했고, 저장소 루트의 라이선스 사본도 원본과 일치했습니다. 검사는 패키지의 구조와 복사 상태를 확인하며 독자의 이해도 개선을 측정한 성능 시험은 아닙니다.
