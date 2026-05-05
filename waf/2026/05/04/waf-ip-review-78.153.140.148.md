# WAF IP 승인 검토 Ticket

## 1. 기본 정보

| 항목 | 값 |
|---|---|
| 상태 | blocked-after-review |
| 승인 상태 | approved |
| 후보 유형 | auto-block approval candidate |
| IP | 78.153.140.148 |
| 발생 일자 | 2026-05-04 |
| sourceRunId | 2026-05-05T00:03:27.002Z |
| 실제 차단 실행 | false |
| 운영자 승인 필요 | true |
| 실행 상태 | not-attempted |

## 2. 탐지 요약

| 항목 | 값 |
|---|---|
| 위험도 | critical |
| AI 판단 | approve-recommended |
| 오탐 가능성 | low |
| 신뢰도 | high |
| matchedRuleId | critical-rce-webshell-lfi |
| wouldBlock | true |
| AI provider | rule-based |
| GPT enabled | false |
| GPT dry-run | true |

## 3. 탐지 근거

- auto-block policy matched
- wouldBlock=true
- matchedRuleId=critical-rce-webshell-lfi
- high-risk WAF detection
- attack-pattern evidence present
- new or unblocked candidate pending operator approval

## 4. AI 권고

운영자 승인 후 자동 차단을 권고합니다.

AI approve-recommended는 운영자 승인 상태가 아닙니다.  
운영자 승인은 반드시 ticket-approve CLI로만 수행합니다.

## 자동 차단 승인

| 항목 | 값 |
|---|---|
| 승인 상태 | approved |
| 승인자 | operator |
| 승인 시각 | 2026-05-04T23:58:17.448Z |
| 승인 사유 | Approved after operator review and AI recommendation |

## 자동 차단 실행

- 이번 단계에서는 실제 차단을 수행하지 않음
- 자동 차단 실행 전 운영자 승인 또는 별도 실행 모드 필요

## AI 차단 판단

| 항목 | 값 |
|---|---|
| AI 판단 상태 | approve-recommended |
| 차단 권고 | true |
| 오탐 가능성 | 낮음 |
| 위험도 | 치명 |
| 신뢰도 | high |
| 판단 방식 | rule-based-gpt-ready |
| 판단 시각 | 2026-05-05T00:10:10.458Z |

## AI 판단 근거

- auto-block policy matched
- wouldBlock=true
- matchedRuleId=critical-rce-webshell-lfi
- high-risk WAF detection
- attack-pattern evidence present
- new or unblocked candidate pending operator approval

## AI 권고

운영자 승인 후 자동 차단을 권고합니다.

## AI Provider

| Item | Value |
|---|---|
| AI provider | rule-based |
| GPT enabled | false |
| GPT dry-run | true |
| 판단 모델 | gpt-5.5-thinking |
| GPT status | SKIPPED |

AI approve-recommended is not operator approval. Operator approval must use the ticket-approve CLI.
