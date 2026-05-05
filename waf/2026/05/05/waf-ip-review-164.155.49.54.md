# WAF IP 승인 검토 Ticket

## 1. 기본 정보

| 항목 | 값 |
|---|---|
| 상태 | auto-block-candidate |
| 승인 상태 | pending |
| 후보 유형 | auto-block approval candidate |
| IP | 164.155.49.54 |
| 발생 일자 | 2026-05-05 |
| 실제 차단 실행 | false |
| 운영자 승인 필요 | true |
| 실행 상태 | not-attempted |

## 2. 탐지 요약

| 항목 | 값 |
|---|---|
| 위험도 | critical |
| matchedRuleId | critical-rce-webshell-lfi |
| wouldBlock | true |
| alreadyBlocked | false |
| 경로 | /containers/json |
| 탐지 필터 | 취약점 스캐너 UA |
| 탐지 횟수 | 20 |

## 3. 자동 차단 평가

| 항목 | 값 |
|---|---|
| 평가 상태 | auto-block-candidate |
| dry-run | true |
| 정책 파일 | config/waf-auto-block-policy.json |
| 매칭 정책 | critical-rce-webshell-lfi |
| 실제 차단 실행 | false |
| 판단 사유 | High-confidence exploit attempt suitable for auto-block candidate review. |

## 4. 자동 차단 승인

| 항목 | 값 |
|---|---|
| 승인 상태 | pending |
| 승인자 | - |
| 승인 시각 | - |
| 승인 사유 | - |

## 5. AI 차단 판단

| 항목 | 값 |
|---|---|
| AI 판단 상태 | approve-recommended |
| 차단 권고 | true |
| 오탐 가능성 | 낮음 |
| 위험도 | 높음 |
| 신뢰도 | high |
| 판단 방식 | rule-based-gpt-ready |

## 6. AI 판단 근거

- auto-block policy matched
- wouldBlock=true
- matchedRuleId=critical-rce-webshell-lfi
- high-risk WAF detection
- attack-pattern evidence present
- new or unblocked candidate pending operator approval

## 7. AI 권고

운영자 승인 후 자동 차단을 권고합니다.

## 8. 승인 전 확인 사항

- [ ] IP가 내부/협력사/정상 크롤러/점검망이 아닌지 확인
- [ ] 원본 WAF 로그와 ticket 근거 확인
- [ ] matchedRuleId가 critical-rce-webshell-lfi인지 확인
- [ ] wouldBlock=true인지 확인
- [ ] alreadyBlocked=false인지 확인
- [ ] MAX_PER_RUN=1 수동 실행 원칙 확인

## 9. 운영자 승인 명령

```powershell
npm run plura:waf:ticket-approve -- --ip=164.155.49.54 --reason="Approved after operator review for AutoBlock rehearsal"
```

## 10. 운영자 반려 명령

```powershell
npm run plura:waf:ticket-reject -- --ip=164.155.49.54 --reason="Rejected after operator review"
```

## 11. 수동 차단 보조 명령

```powershell
npm run plura:waf:manual-block-prefill -- --ip=164.155.49.54
```

주의: 수동 차단 보조 명령은 IP 입력까지만 수행하며, 최종 확인 버튼은 운영자가 직접 클릭해야 합니다.

수동 차단 화면: [https://d-xdr.plura.io/ipblock/manual/waf](https://d-xdr.plura.io/ipblock/manual/waf)

## 12. 승인 후 AutoBlock preflight

승인 후에는 반드시 아래 명령으로 preflight를 다시 확인합니다.

```powershell
npm run plura:waf:auto-block-preflight
```

`safeToStart=true`가 나오기 전에는 `PLURA-WAF-AutoBlock-Once`를 실행하지 않습니다.

## 13. 안전 원칙

* 이 ticket은 승인 검토용입니다.
* 이 ticket 파일 생성은 ticket approve/reject를 수행하지 않습니다.
* 이 ticket 파일 생성은 IP 차단을 수행하지 않습니다.
* 실제 차단은 운영자 승인 및 preflight 통과 후 별도 수동 실행에서만 수행합니다.
* Scheduler는 monitor-only 상태를 유지합니다.
