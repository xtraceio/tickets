# WAF 분석 결과 요약

서로 다른 public IP 근거가 함께 확인되어 즉시 차단 후보로 표시하지 않습니다. 수동 차단 전 웹 UI에서 최종 차단 대상 IP를 반드시 확인하세요.

- 대표 운영형 시나리오: -
- 운영형 판단 사유: -
- 상세 근거: WAF-S010

## 분석 결과 요약

- 실행 상태: OK
- 조회 날짜: 오늘 / 2026-05-02 ~ 2026-05-02
- 공격자 IP: 수동 확인 필요
- IP 차단 후보: 보류, 수동 확인 필요
- 시나리오 정책상 후보: 아니오
- 세부 시나리오 근거: 있음
- 관측 fallback 기반 추가 검토: 필요
- 운영형 승격: 아니오
- 일반 반복 IP fallback 검토: 별도 승격 없음
- 최종 수동 확인: 필요
- 관측 fallback 기반 추가 검토 사유: 동일 IP의 단일 요청에서 복수 공격 유형 또는 복수 위험도 신호가 함께 확인되었습니다. 다만 동일 IP 이벤트 수가 1건이고 고유 경로가 1개이므로 운영형 WAF-G005 승격 조건에는 도달하지 않았습니다. 복수 공격 유형은 low-level evidence로 확인되었으나 동일 IP 이벤트 수가 2건 미만이므로 운영형 WAF-G005 조건에는 도달하지 않았습니다.
- fallback 차단 후보 승격 보류 사유: scenario 선택 실행에서는 일반 반복 IP fallback을 차단 후보로 승격하지 않음
- evidence scope mismatch: false
- 확인 대상 IP: 수동 확인 필요
- IP 근거 불일치: false
- 권고: 수동 차단 전 웹 UI에서 최종 차단 대상 IP를 반드시 확인하세요.

## 선택 row 기준 요약

- selectedRowIp: 20.64.97.136
- 총 이벤트 수: 1
- 차단 수: 1
- 탐지 수: 0
- 고유 경로 수: 1

## 대표 시나리오 근거 요약

- representativeScenario: WAF-S010 Mixed attack types by same IP
- representativeScenarioIp: 20.64.97.136
- representativeGroupIp: 20.64.97.136
- scenarioEvidenceIps: 20.64.97.136
- evidenceTotalEvents: 1
- evidenceDistinctAttackTypes: 2
- evidenceUniquePaths: 1
- evidenceSamplePaths: /druid/index.html
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
- IP 근거 불일치: false
- 권고: 수동 차단 전 웹 UI에서 최종 차단 대상 IP를 반드시 확인하세요.
- selectedRowIp: 20.64.97.136
- representativeGroupIp: 20.64.97.136
- finalReviewIp: 수동 확인 필요
- scenarioEvidenceIps: 20.64.97.136

- 판단 이유: 동일 IP의 단일 요청에서 복수 공격 유형 또는 복수 위험도 신호가 함께 확인되었습니다. 다만 동일 IP 이벤트 수가 1건이고 고유 경로가 1개이므로 운영형 WAF-G005 승격 조건에는 도달하지 않았습니다. 복수 공격 유형은 low-level evidence로 확인되었으나 동일 IP 이벤트 수가 2건 미만이므로 운영형 WAF-G005 조건에는 도달하지 않았습니다.
- 권고 조치: 운영형 시나리오 승격 조건에는 도달하지 않아 차단 후보로 표시하지 않고 관측 기반 수동 검토 evidence로 분리하세요.
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
- representativeReason: 동일 IP 20.64.97.136에서 복수 공격 유형 또는 복수 위험도 신호가 함께 확인되었습니다.
- evaluatedScenarios: 11
- 시나리오 정책상 후보: 아니오
- 운영자 표시 상태: 보류, 수동 확인 필요
- 자동 차단: 아니오

## 탐지 판단 흐름도

```mermaid
flowchart TD
  nodeA["WAF Row 및 상세 로그\n선택 Row IP: 20.64.97.136"] --> nodeB["세부 시나리오 평가\n매칭: WAF-S010"]
  nodeB --> nodeC["Allowlist 및 억제\n억제: false\n사유: -"]
  nodeC --> nodeD["운영형 시나리오 평가\n매칭: -"]
  nodeD --> nodeE["대표 운영형 그룹\n-"]
  nodeE --> nodeF["IP 차단 권고\n시나리오 정책상 후보: 아니오\n운영자 표시 상태: 보류, 수동 확인 필요\n자동 차단: 아니오"]
  nodeF --> nodeG["수동 검토 또는 보고"]
  nodeF --> nodeH["자동 차단 모의 검증 근거"]
```

## 시나리오 근거 관계도

```mermaid
flowchart LR
  nodeR["선택 WAF Row\n20.64.97.136"] --> nodeL["세부 근거"]
  nodeL --> nodeWAFS010["WAF-S010 Mixed attack types by same IP\nIP: 20.64.97.136"]
  nodeWAFS010 --> nodeWAFS010Only["세부 근거만 확인"]
  nodeWAFS010 --> nodeWAFG005NotPromoted["WAF-G005 승격 안 됨\n복수 공격 유형은 low-level evidence로 확인되었으나 동일 IP 이벤트 수가 2건 미만이므로 운영형 WAF-G005 조건에는 도달하지 않았습니다."]
  nodeRep["대표 운영형 시나리오\n-"] --> nodeRec["IP 차단 검토\n20.64.97.136"]
```

## IP 근거 분리도

```mermaid
flowchart TD
  nodeSelectedIp["선택 Row IP: 20.64.97.136"]
  nodeRepresentativeIp["대표 시나리오 근거 IP: 20.64.97.136"]
  nodeFinalIp["최종 차단 대상 IP: 20.64.97.136"]
  nodeWAFS010Ip["WAF-S010 근거 IP: 20.64.97.136"]
  nodeSelectedIp --> nodeSelectedIpNote["선택 row 근거"]
  nodeSelectedIpNote --> nodeFinalIp
  nodeRepresentativeIp --> nodeRepresentativeIpNote["대표 운영형 근거"]
  nodeRepresentativeIpNote --> nodeFinalIp
  nodeWAFS010Ip --> nodeWAFS010IpNote["WAF-S010 시나리오 근거"]
  nodeWAFS010IpNote --> nodeFinalIp
```

## 운영형 대표 시나리오

- matchedGroupScenarios: []
- representativeGroupScenario: -
- representativeGroupPriorityScore: -
- representativeGroupReason: -
- representativeLowLevelScenario: -

| group | priorityScore | matched | mapped | matchedLowLevel | reason |
|---|---:|---:|---|---|---|
| WAF-G001 반복 스캐닝 기반 IP 차단 검토 | 50 | false | 2, 3, 4, 5 | - | Mapped low-level scenarios did not match. |
| WAF-G002 고위험 단건 공격 검토 | 70 | false | 6 | - | Mapped low-level scenarios did not match. |
| WAF-G003 고객사 중요 필터 검토 | 65 | false | 7 | - | Mapped low-level scenarios did not match. |
| WAF-G004 공격 시퀀스 기반 검토 | 85 | false | 9 | - | Mapped low-level scenarios did not match. |
| WAF-G005 복합 공격 유형 검토 | 80 | false | 10 | - | 복수 공격 유형은 low-level evidence로 확인되었으나 동일 IP 이벤트 수가 2건 미만이므로 운영형 WAF-G005 조건에는 도달하지 않았습니다. |
| WAF-G006 분산 유사 공격 검토 | 90 | false | 11 | - | Mapped low-level scenarios did not match. |
| WAF-G007 외부 평판/TI 보강 검토 | 75 | false | 1 | - | Mapped low-level scenarios did not match. |
| WAF-G008 AI 분석 보강 검토 | 60 | false | 8 | - | Mapped low-level scenarios did not match. |

| scenario | priorityScore | matched | attackerIp | reason |
|---|---:|---:|---|---|
| WAF-S001 VT malicious ratio | 90 | false | 20.64.97.136 | VT 분석 결과가 없어 수동차단 후보로 올리지 않습니다. |
| WAF-S002 Scanning Low threshold | 30 | false | - | 스캐닝성 LOW 이벤트가 기준 30건에 도달하지 않았습니다. |
| WAF-S003 Scanning Middle threshold | 40 | false | - | 스캐닝성 MIDDLE 이벤트가 기준 20건에 도달하지 않았습니다. |
| WAF-S004 Scanning High threshold | 50 | false | 20.64.97.136 | 스캐닝성 HIGH 이벤트가 기준 10건에 도달하지 않았습니다. |
| WAF-S005 Scanning Critical threshold | 65 | false | 20.64.97.136 | 스캐닝성 CRITICAL 이벤트가 기준 3건에 도달하지 않았습니다. |
| WAF-S006 Non-scanning Critical | 70 | false | - | 비스캐닝 CRITICAL 이벤트가 확인되지 않았습니다. |
| WAF-S007 Customer custom filter | 55 | false | - | 매칭되는 고객사 커스텀 필터 탐지가 없어 수동차단 후보로 올리지 않습니다. |
| WAF-S008 AI malicious probability | 75 | false | 20.64.97.136 | AI 분석 결과가 없어 수동차단 후보로 올리지 않습니다. |
| WAF-S009 Threat sequence judgment | 80 | false | 20.64.97.136 | 로그 순서 기반 위협 시퀀스가 확인되지 않았습니다. |
| WAF-S010 Mixed attack types by same IP | 60 | true | 20.64.97.136 | 동일 IP 20.64.97.136에서 복수 공격 유형 또는 복수 위험도 신호가 함께 확인되었습니다. |
| WAF-S011 Distributed similar attack burst | 85 | false | - | 분산 유사 공격 기준에 도달하지 않았습니다. |

## 시나리오 상세 근거

### WAF-S010 Mixed attack types by same IP
- priorityScore: 60
- attackerIp: 20.64.97.136
- attackerIps: -
- reason: 동일 IP 20.64.97.136에서 복수 공격 유형 또는 복수 위험도 신호가 함께 확인되었습니다.
- recommendation: 웹 화면에서 해당 IP의 요청 경로와 탐지/차단 이력을 확인한 뒤 IP주소 수동차단을 검토하세요.
- evidence: {"threshold":2,"totalEvents":1,"distinctAttackTypes":2,"attackTypes":["BROKEN ACCESS CONTROL","SCANNER"],"severities":["CRITICAL","HIGH"],"uniquePaths":1,"samplePaths":["/druid/index.html"]}


## 최종 IP 차단 검토 사유

최종 IP 차단 검토 사유: WAF-S010 동일 IP 20.64.97.136에서 복수 공격 유형 또는 복수 위험도 신호가 함께 확인되었습니다. 자동 IP 차단은 수행하지 않으며 담당자가 웹 화면에서 수동 확인 후 결정합니다.

## 반복 요청 경로

| path |
|---|
| /druid/index.html |

## 우선순위 차단 이벤트

- 공격자 IP: 20.64.97.136
- 대상 도메인: 130.162.156.89
- 요청 Method: GET
- URI/path: /druid/index.html
- 쿼리/요청본문: -
- HTTP 상태값: 406
- 탐지/차단 유형: 차단(OWASP)
- WAF 필터명: 웹 콘솔 관리 접근취약점 스캐너 UA
- 위험도/risk: BROKEN ACCESS CONTROL>CRITICALSCANNER>HIGH
- 탐지 시각: 2026-05-02 11:23:25.358
- 분석 탭 수집: true
- 로그 탭 수집: true

## 원본 로그 주요 필드

- method: GET
- uri: /druid/index.html
- host: 130.162.156.89
- remoteIp: 20.64.97.136
- responseStatus: 406

## 담당자 확인 항목

1. 공격자 IP 20.64.97.136의 동일 시간대 반복 요청 전체 확인
2. 반복 경로가 PHP/WordPress 백도어/관리자 경로 스캔인지 확인
3. 차단(OWASP)와 HTTP 406이 정상 차단 정책과 일치하는지 확인
4. 동일 IP의 후속 요청이 계속 발생하는지 확인
5. 웹 UI에서 IP주소 차단 등록 여부 결정