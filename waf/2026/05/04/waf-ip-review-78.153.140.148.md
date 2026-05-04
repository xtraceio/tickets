# WAF IP 승인 검토 Ticket

## 1. 기본 정보

| 항목 | 값 |
|---|---|
| 상태 | auto-block-candidate |
| 승인 상태 | pending |
| 후보 유형 | auto-block approval candidate |
| IP | 78.153.140.148 |
| 발생 일자 | 2026-05-04 |
| sourceRunId | 20260505-075506 |
| 실제 차단 실행 | false |
| 운영자 승인 필요 | true |

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
| 승인 상태 | pending |
| 승인자 | - |
| 승인 시각 | - |
| 승인 사유 | - |

## 5. 승인 전 확인 사항

- [ ] IP가 내부/협력사/정상 크롤러/점검망이 아닌지 확인
- [ ] 원본 WAF 로그와 ticket 근거 확인
- [ ] matchedRuleId가 critical-rce-webshell-lfi인지 확인
- [ ] wouldBlock=true인지 확인
- [ ] 이미 차단된 IP가 아닌지 확인
- [ ] MAX_PER_RUN=1 수동 실행 원칙 확인

## 6. 운영자 승인 명령

```powershell
npm run plura:waf:ticket-approve -- --ip=78.153.140.148 --reason="Approved after operator review and AI recommendation"
```

## 7. 운영자 반려 명령

```powershell
npm run plura:waf:ticket-reject -- --ip=78.153.140.148 --reason="Rejected after operator review"
```

## 8. 수동 차단 보조 명령

```powershell
npm run plura:waf:manual-block-prefill -- --ip=78.153.140.148
```

주의: 수동 차단 보조 명령은 IP 입력까지만 수행하며, 최종 확인 버튼은 운영자가 직접 클릭해야 합니다.

수동 차단 화면: https://d-xdr.plura.io/ipblock/manual/waf

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

* 이 ticket은 승인 검토용입니다.
* 이 ticket 파일 생성은 ticket approve/reject를 수행하지 않습니다.
* 이 ticket 파일 생성은 IP 차단을 수행하지 않습니다.
* 실제 차단은 운영자 승인 후 별도 수동 실행에서만 수행합니다.
* Scheduler는 monitor-only 상태를 유지합니다.
