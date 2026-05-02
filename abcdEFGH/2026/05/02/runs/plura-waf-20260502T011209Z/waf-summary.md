# WAF IP 근거 확인 필요

서로 다른 public IP 근거가 함께 확인되어 즉시 차단 후보로 표시하지 않습니다. 수동 차단 전 웹 UI에서 최종 차단 대상 IP를 반드시 확인하세요.

- 대표 운영형 시나리오: WAF-G005 복합 공격 유형 검토
- 운영형 판단 사유: 동일 IP 85.208.96.209에서 복수 공격 유형 또는 복수 위험도와 다수 경로가 함께 확인되었습니다.
- 상세 근거: WAF-S010

## 분석 결과 요약

- 실행 상태: OK
- 조회 날짜: 오늘 / 2026-05-02 ~ 2026-05-02
- 공격자 IP: 수동 확인 필요
- IP 차단 후보: 보류, 수동 확인 필요
- 시나리오 기반 차단 후보: 예, 수동 검토 후보
- 관측 기반 수동 검토: 불필요
- 일반 반복 IP fallback 적용: 아니오
- fallback 차단 후보 승격 보류 사유: scenario 선택 실행에서는 일반 반복 IP fallback을 차단 후보로 승격하지 않음
- evidence scope mismatch: true
- evidence scope mismatch 사유: 선택 row IP와 다른 scenario no-match evidence IP가 분리되어 표시됨: 85.208.96.209
- 확인 대상 IP: 수동 확인 필요
- IP 근거 불일치: true
- 권고: 수동 차단 전 웹 UI에서 최종 차단 대상 IP를 반드시 확인하세요.
- 총 이벤트 수: 1
- 차단 수: 1
- 탐지 수: 0
- 고유 경로 수: 1
- 사용자 수동 확인 대기: true
- 브라우저 유지: false
- 자동 IP 차단 수행: false
- 확인 대상 IP: 수동 확인 필요
- IP 차단 후보: 보류, 수동 확인 필요
- 발송 판단: 반복성 낮음 또는 발송 조건 미충족
- 종료 방법: 설정된 대기 시간 후 자동 종료

## IP 차단 검토 안내

- IP 차단 후보: 보류, 수동 확인 필요
- 확인 대상 IP: 수동 확인 필요
- IP 근거 불일치: true
- 권고: 수동 차단 전 웹 UI에서 최종 차단 대상 IP를 반드시 확인하세요.
- selectedRowIp: 77.83.39.197
- representativeGroupIp: 85.208.96.209
- finalReviewIp: 85.208.96.209
- scenarioEvidenceIps: 85.208.96.209

- 판단 이유: 대표 운영형 시나리오 WAF-G005 복합 공격 유형 검토 매칭: 동일 IP 85.208.96.209에서 복수 공격 유형 또는 복수 위험도와 다수 경로가 함께 확인되었습니다.
- 권고 조치: 웹 화면에서 해당 IP의 요청 경로와 탐지/차단 이력을 확인한 뒤 IP주소 차단을 검토하세요.
- 자동 차단 수행: false
- 수동차단 안내 활성화: true
- 브라우저 안내 overlay 표시: true
- 수동차단 버튼 위치 확인: false
- 수동차단 버튼 selector: -
- 수동차단 버튼 클릭: false
- 저장/확인 클릭: false
- 수동 IP 차단 매뉴얼: https://docs.plura.io/ko/v6/fn/comm/ipblock/manual

## Allowlist / Suppression

- suppressed: false
- action: -
- matchedRuleId: -
- matchedValue: -
- matchedField: -
- matchedIp: -
- reason: -
- result: allowlist suppression 미적용

## 매칭된 시나리오

- 선택: 1-11 => [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
- matchedScenarios: [10]
- matchedCount: 1
- representativeScenario: WAF-S010 Mixed attack types by same IP
- representativePriorityScore: 60
- representativeReason: 동일 IP 85.208.96.209에서 복수 공격 유형 또는 복수 위험도와 다수 경로가 함께 확인되었습니다.
- evaluatedScenarios: 11
- finalIpBlockCandidate: true
- autoBlock: false

## 탐지 판단 흐름도

```mermaid
flowchart TD
  nodeA["WAF Row and Detail Log\nSelected row IP: 77.83.39.197"] --> nodeB["Low-level Scenario Evaluation\nMatched: WAF-S010"]
  nodeB --> nodeC["Allowlist and Suppression\nSuppressed: false\nReason: -"]
  nodeC --> nodeD["Group Scenario Evaluation\nMatched: WAF-G005"]
  nodeD --> nodeE["Representative Group\nWAF-G005"]
  nodeE --> nodeF["IP Block Recommendation\nCandidate: true\nFinal candidate: true\nAuto block: false"]
  nodeF --> nodeG["Manual Review or Report"]
  nodeF --> nodeH["Auto Dry-run Evidence"]
```

```mermaid
flowchart LR
  nodeR["Selected WAF Row\n77.83.39.197"] --> nodeL["Low-level Evidence"]
  nodeL --> nodeWAFS010["WAF-S010 Mixed attack types by same IP\nIP: 85.208.96.209"]
  nodeWAFS010 --> nodeWAFG005["WAF-G005 복합 공격 유형 검토\nMatched"]
  nodeWAFG005 --> nodeRep["Representative Group Scenario\nWAF-G005"]
  nodeRep["Representative Group Scenario\nWAF-G005"] --> nodeRec["IP Block Review\nManual confirmation required"]
```

## IP 근거 분리도

```mermaid
flowchart TD
  nodeSelectedIp["Selected Row IP: 77.83.39.197"]
  nodeRepresentativeIp["Representative Group IP: 85.208.96.209"]
  nodeFinalIp["Final Review IP: Manual confirmation required"]
  nodeWAFS010Ip["WAF-S010 Evidence IP: 85.208.96.209"]
  nodeSelectedIp --> nodeSelectedIpNote["Selected row evidence"]
  nodeSelectedIpNote --> nodeFinalIp
  nodeRepresentativeIp --> nodeRepresentativeIpNote["Representative group evidence"]
  nodeRepresentativeIpNote --> nodeFinalIp
  nodeWAFS010Ip --> nodeWAFS010IpNote["WAF-S010 evidence"]
  nodeWAFS010IpNote --> nodeFinalIp
```

> 참고: 우선순위 row IP와 일부 scenario evidence IP가 다릅니다. 수동 차단 전 웹 화면에서 최종 차단 대상 IP를 반드시 확인하세요.

## 운영형 대표 시나리오

- matchedGroupScenarios: [WAF-G005]
- representativeGroupScenario: WAF-G005 복합 공격 유형 검토
- representativeGroupPriorityScore: 80
- representativeGroupReason: 동일 IP 85.208.96.209에서 복수 공격 유형 또는 복수 위험도와 다수 경로가 함께 확인되었습니다.
- representativeLowLevelScenario: WAF-S010

| group | priorityScore | matched | mapped | matchedLowLevel | reason |
|---|---:|---:|---|---|---|
| WAF-G001 반복 스캐닝 기반 IP 차단 검토 | 50 | false | 2, 3, 4, 5 | - | Mapped low-level scenarios did not match. |
| WAF-G002 고위험 단건 공격 검토 | 70 | false | 6 | - | Mapped low-level scenarios did not match. |
| WAF-G003 고객사 중요 필터 검토 | 65 | false | 7 | - | Mapped low-level scenarios did not match. |
| WAF-G004 공격 시퀀스 기반 검토 | 85 | false | 9 | - | Mapped low-level scenarios did not match. |
| WAF-G005 복합 공격 유형 검토 | 80 | true | 10 | 10 | 동일 IP 85.208.96.209에서 복수 공격 유형 또는 복수 위험도와 다수 경로가 함께 확인되었습니다. |
| WAF-G006 분산 유사 공격 검토 | 90 | false | 11 | - | Mapped low-level scenarios did not match. |
| WAF-G007 외부 평판/TI 보강 검토 | 75 | false | 1 | - | Mapped low-level scenarios did not match. |
| WAF-G008 AI 분석 보강 검토 | 60 | false | 8 | - | Mapped low-level scenarios did not match. |

| scenario | priorityScore | matched | attackerIp | reason |
|---|---:|---:|---|---|
| WAF-S001 VT malicious ratio | 90 | false | 77.83.39.197 | VT 분석 결과가 없어 수동차단 후보로 올리지 않습니다. |
| WAF-S002 Scanning Low threshold | 30 | false | - | 스캐닝성 LOW 이벤트가 기준 30건에 도달하지 않았습니다. |
| WAF-S003 Scanning Middle threshold | 40 | false | 85.208.96.209 (다른 IP 기반 미매칭 근거) | 스캐닝성 MIDDLE 이벤트가 기준 20건에 도달하지 않았습니다. |
| WAF-S004 Scanning High threshold | 50 | false | 85.208.96.209 (다른 IP 기반 미매칭 근거) | 스캐닝성 HIGH 이벤트가 기준 10건에 도달하지 않았습니다. |
| WAF-S005 Scanning Critical threshold | 65 | false | 85.208.96.209 (다른 IP 기반 미매칭 근거) | 스캐닝성 CRITICAL 이벤트가 기준 3건에 도달하지 않았습니다. |
| WAF-S006 Non-scanning Critical | 70 | false | - | 비스캐닝 CRITICAL 이벤트가 확인되지 않았습니다. |
| WAF-S007 Customer custom filter | 55 | false | - | 매칭되는 고객사 커스텀 필터 탐지가 없어 수동차단 후보로 올리지 않습니다. |
| WAF-S008 AI malicious probability | 75 | false | 85.208.96.209 (다른 IP 기반 미매칭 근거) | AI 분석 결과가 없어 수동차단 후보로 올리지 않습니다. |
| WAF-S009 Threat sequence judgment | 80 | false | 85.208.96.209 (다른 IP 기반 미매칭 근거) | 로그 순서 기반 위협 시퀀스가 확인되지 않았습니다. |
| WAF-S010 Mixed attack types by same IP | 60 | true | 85.208.96.209 | 동일 IP 85.208.96.209에서 복수 공격 유형 또는 복수 위험도와 다수 경로가 함께 확인되었습니다. |
| WAF-S011 Distributed similar attack burst | 85 | false | 85.208.96.209 (다른 IP 기반 미매칭 근거) | 분산 유사 공격 기준에 도달하지 않았습니다. |

## 시나리오 상세 근거

### WAF-S010 Mixed attack types by same IP
- priorityScore: 60
- attackerIp: 85.208.96.209
- attackerIps: -
- reason: 동일 IP 85.208.96.209에서 복수 공격 유형 또는 복수 위험도와 다수 경로가 함께 확인되었습니다.
- recommendation: 웹 화면에서 해당 IP의 요청 경로와 탐지/차단 이력을 확인한 뒤 IP주소 수동차단을 검토하세요.
- evidence: {"threshold":2,"totalEvents":2,"distinctAttackTypes":2,"attackTypes":["SCANNER","LFI"],"severities":["CRITICAL","HIGH","MIDDLE"],"uniquePaths":2,"samplePaths":["/ko/threats/ftp_security_vulnerabilities_and_defense_measures/","/ja/column/plura-xdr-ai-infosec-moat/"]}


## 최종 IP 차단 검토 사유

최종 IP 차단 검토 사유: WAF-S010 동일 IP 85.208.96.209에서 복수 공격 유형 또는 복수 위험도와 다수 경로가 함께 확인되었습니다. 자동 IP 차단은 수행하지 않으며 담당자가 웹 화면에서 수동 확인 후 결정합니다.

## 반복 요청 경로

| path |
|---|
| /.env |

## 우선순위 차단 이벤트

- 공격자 IP: 77.83.39.197
- 대상 도메인: 130.162.156.89
- 요청 Method: GET
- URI/path: /.env
- 쿼리/요청본문: -
- HTTP 상태값: 406
- 탐지/차단 유형: 차단(OWASP)
- WAF 필터명: 환경 파일 접근제한 파일 접근
- 위험도/risk: SCANNER>CRITICALLFI>HIGH
- 탐지 시각: 2026-05-02 10:04:36.945
- 분석 탭 수집: true
- 로그 탭 수집: true

## 원본 로그 주요 필드

- method: GET
- uri: /.env
- host: 130.162.156.89
- remoteIp: 77.83.39.197
- responseStatus: 406

## 담당자 확인 항목

1. 공격자 IP 77.83.39.197의 동일 시간대 반복 요청 전체 확인
2. 반복 경로가 PHP/WordPress 백도어/관리자 경로 스캔인지 확인
3. 차단(OWASP)와 HTTP 406이 정상 차단 정책과 일치하는지 확인
4. 동일 IP의 후속 요청이 계속 발생하는지 확인
5. 웹 UI에서 IP주소 차단 등록 여부 결정