# WAF IP 수동 검토 Ticket

## 기본 정보

| 항목 | 값 |
|---|---|
| 상태 | auto-block-candidate |
| 발생일 | 2026-05-04 |
| 대상 IP | 78.153.140.148 |
| 탐지 위치 | PLURA-XDR > 웹방화벽 |
| 검토 기준 | IP차단 > 수동 > 웹방화벽 / IP주소 |
| 처리 방식 | 운영자 수동 검토 |
| 자동 차단 여부 | false |

## 탐지 요약

| 항목 | 값 |
|---|---|
| 위험도 | SCANNER>CRITICAL |
| 탐지 필터 | Androxgh0st 봇넷, 환경 파일 접근제한 파일 접근 |
| 탐지 횟수 | 2 |
| 메소드 | POST |
| 경로 | / |
| 호스트/도메인 | 130.162.156.89 |
| 탐지 시각 | 2026-05-04 18:56:06.631 |

## 탐지 근거

- WAF 후보 row 수집 중 신규 미차단 IP로 확인
- 기존 수동 차단 목록에 없음
- manual review queue에 등록됨
- 자동 차단은 수행하지 않음

## 처리 이력

### 1. 탐지

- 상태: review-required
- 생성 시각: 2026-05-04T10:12:59.827Z
- 근거 파일:
  - `artifacts/waf/ip-review-queue.json`
  - `artifacts/waf/ip-review-queue.md`

### 2. 수동 검토

- 운영자 확인 필요
- PLURA-XDR 화면에서 수동 차단 여부를 결정
- 차단 시 `npm run plura:waf:verify-review`로 검증 필요

### 3. 검증 결과

- 아직 verify-review 결과 없음

## 자동 차단 평가

| 항목 | 값 |
|---|---|
| 평가 상태 | auto-block-candidate |
| dry-run | true |
| 정책 파일 | config/waf-auto-block-policy.json |
| 매칭 정책 | critical-rce-webshell-lfi |
| 실제 차단 실행 | false |
| 판단 사유 | High-confidence exploit attempt suitable for auto-block candidate review. |

## 자동 차단 승인

| 항목 | 값 |
|---|---|
| 승인 상태 | pending |
| 승인자 | - |
| 승인 시각 | - |
| 승인 사유 | - |
## 자동 차단 실행

- 이번 단계에서는 실제 차단을 수행하지 않음
- 자동 차단 실행 전 운영자 승인 또는 별도 실행 모드 필요

## 최종 판정

수동 검토 대기.

## AI 차단 판단

| 항목 | 값 |
|---|---|
| AI 판단 상태 | approve-recommended |
| 차단 권고 | true |
| 오탐 가능성 | 낮음 |
| 위험도 | 치명 |
| 신뢰도 | high |
| 판단 방식 | rule-based-gpt-ready |
| 판단 시각 | 2026-05-04T22:15:13.043Z |

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


## 운영자 승인 검토 요약

| 항목 | 값 |
|---|---|
| 승인 검토 상태 | 승인 검토 필요 |
| 후보 유형 | auto-block approval candidate |
| IP | 78.153.140.148 |
| AI 판단 | approve-recommended |
| 위험도 | critical |
| 오탐 가능성 | low |
| 신뢰도 | high |
| matchedRuleId | critical-rce-webshell-lfi |
| wouldBlock | true |
| 실제 차단 실행 | false |
| 운영자 승인 필요 | true |

## 탐지 근거 요약

- auto-block policy matched
- wouldBlock=true
- matchedRuleId=critical-rce-webshell-lfi
- high-risk WAF detection
- attack-pattern evidence present
- new or unblocked candidate pending operator approval

## AI 권고

운영자 승인 후 자동 차단을 권고합니다.

## 승인 전 확인 사항

- [ ] IP가 내부/협력사/정상 크롤러/점검망이 아닌지 확인
- [ ] 원본 WAF 로그와 ticket 근거 확인
- [ ] matchedRuleId가 critical-rce-webshell-lfi인지 확인
- [ ] wouldBlock=true인지 확인
- [ ] 이미 차단된 IP가 아닌지 확인
- [ ] MAX_PER_RUN=1 수동 실행 원칙 확인

## 운영자 승인 명령

```powershell
npm run plura:waf:ticket-approve -- --ip=78.153.140.148 --reason="Approved after operator review and AI recommendation"
```

## 운영자 반려 명령

```powershell
npm run plura:waf:ticket-reject -- --ip=78.153.140.148 --reason="Rejected after operator review"
```

## 수동 차단 보조 명령

```powershell
npm run plura:waf:manual-block-prefill -- --ip=78.153.140.148
```

주의: 수동 차단 보조 명령은 IP 입력까지만 수행하며, 최종 확인 버튼은 운영자가 직접 클릭해야 합니다.

## 승인 후 1건 실행 원칙

승인 후 실행은 반드시 수동 세션에서 `PLURA_WAF_AUTO_BLOCK_MAX_PER_RUN=1`로만 수행합니다.
Scheduler를 approved-auto-block으로 변경하지 않습니다.

AI approve-recommended는 운영자 승인 상태가 아닙니다.
운영자 승인은 반드시 ticket-approve CLI로만 수행합니다.
