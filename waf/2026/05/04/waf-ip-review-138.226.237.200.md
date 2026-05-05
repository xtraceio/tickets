# WAF IP 승인 검토 Ticket

## 1. 기본 정보

| 항목 | 값 |
|---|---|
| 상태 | blocked-after-review |
| 승인 상태 | approved |
| 후보 유형 | auto-block approval candidate |
| IP | 138.226.237.200 |
| 발생 일자 | 2026-05-04 |
| sourceRunId | 2026-05-05T00:03:27.002Z |
| 실제 차단 실행 | false |
| 운영자 승인 필요 | true |
| 실행 상태 | completed-by-manual-review |
| 이전 자동 실행 실패 사유 | Live auto-block executor is not configured. |

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
| 승인 시각 | - |
| 승인 사유 | Approved after operator review and AI recommendation |

## 자동 차단 실행 결과

| 항목 | 값 |
|---|---|
| 실행 방식 | manual-block-prefill + operator confirmation |
| 실제 자동 차단 실행 | false |
| 수동 차단 완료 | true |
| 이전 자동 실행 실패 사유 | Live auto-block executor is not configured. |
| rollback-plan | artifacts/waf/rollback-plan.json |

승인 완료 후보가 있더라도 자동 실행하지 않습니다.
다음 조치는 `manual-block-prefill`로 운영자가 직접 수동 차단하거나 live auto-block executor 구현/설정을 확인하는 것입니다.

## 검증 결과

| 항목 | 값 |
|---|---|
| verify-review 상태 | blocked-after-review |
| 검증 상태 | verified |
| 차단 확인 | true |


## 최종 상태

수동 차단 후 차단 목록에서 확인되었습니다.  
추가 차단 조치는 필요하지 않습니다.

## 5. 승인 전 확인 사항

- [ ] IP가 내부/협력사/정상 크롤러/점검망이 아닌지 확인
- [ ] 원본 WAF 로그와 ticket 근거 확인
- [ ] matchedRuleId가 critical-rce-webshell-lfi인지 확인
- [ ] wouldBlock=true인지 확인
- [ ] 이미 차단된 IP가 아닌지 확인
- [ ] MAX_PER_RUN=1 수동 실행 원칙 확인

## 6. 운영자 승인 명령

```powershell
npm run plura:waf:ticket-approve -- --ip=138.226.237.200 --reason="Approved after operator review and AI recommendation"
```

## 7. 운영자 반려 명령

```powershell
npm run plura:waf:ticket-reject -- --ip=138.226.237.200 --reason="Rejected after operator review"
```

## 8. 수동 차단 보조 명령

```powershell
npm run plura:waf:manual-block-prefill -- --ip=138.226.237.200
```

주의: 수동 차단 보조 명령은 IP 입력까지만 수행하며, 최종 확인 버튼은 운영자가 직접 클릭해야 합니다.

수동 차단 화면: [https://d-xdr.plura.io/ipblock/manual/waf](https://d-xdr.plura.io/ipblock/manual/waf)

## 9. 승인 후 1건 실행 원칙

승인 후 실행은 반드시 수동 세션에서 `PLURA_WAF_AUTO_BLOCK_MAX_PER_RUN=1`로만 수행합니다.
Scheduler를 approved-auto-block으로 변경하지 않습니다.

```powershell
$env:PLURA_WAF_MONITOR_MODE="approved-auto-block"
$env:PLURA_WAF_AI_REVIEW_ENABLED="true"
$env:PLURA_WAF_MONITOR_NOTIFY_ENABLED="true"
$env:GMAIL_ENABLED="true"
$env:GMAIL_DRY_RUN="true"
$env:PLURA_WAF_AUTO_BLOCK="true"
$env:PLURA_WAF_AUTO_BLOCK_DRY_RUN="false"
$env:PLURA_WAF_AUTO_BLOCK_REQUIRE_APPROVAL="true"
$env:PLURA_WAF_AUTO_BLOCK_MAX_PER_RUN="1"
$env:PLURA_WAF_MONITOR_NOTIFY_LIVE_SEND_CONFIRM="false"

npm run plura:waf:monitor-once
```

## 10. 안전 원칙

* 이 ticket은 이미 수동 차단 완료 상태입니다.
* 추가 자동 차단 실행은 필요하지 않습니다.
* Scheduler는 monitor-only 상태를 유지합니다.
* AutoBlock task는 preflight 통과 및 운영자 명시 판단 없이는 실행하지 않습니다.

## 자동 차단 평가

| 항목 | 값 |
|---|---|
| 평가 상태 | auto-block-candidate |
| dry-run | true |
| 정책 파일 | config/waf-auto-block-policy.json |
| 매칭 정책 | critical-rce-webshell-lfi |
| 실제 차단 실행 | false |
| 판단 사유 | High-confidence exploit attempt suitable for auto-block candidate review. |

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
