# WAF IP 근거 확인 필요

서로 다른 public IP 근거가 함께 확인되어 즉시 차단 후보로 표시하지 않습니다. 수동 차단 전 웹 UI에서 최종 차단 대상 IP를 반드시 확인하세요.

- 대표 운영형 시나리오: WAF-G003 고객사 중요 필터 검토
- 운영형 판단 사유: 고객사 커스텀 필터에 해당하는 중요 탐지가 확인되어 IP 차단 검토가 필요합니다.
- 상세 근거: WAF-S007, WAF-S010

## 분석 결과 요약

- 실행 상태: OK
- 조회 날짜: 오늘 / 2026-05-02 ~ 2026-05-02
- 공격자 IP: 수동 확인 필요
- IP 차단 후보: 보류, 수동 확인 필요
- 운영형 정책상 후보: 예
- 운영자 표시 상태: 보류, 수동 확인 필요
- 보류 사유: IP 근거 불일치
- 자동 차단: 아니오
- 세부 시나리오 근거: 있음
- 관측 fallback 기반 추가 검토: 필요
- 운영형 승격: 예
- 일반 반복 IP fallback 검토: 별도 승격 없음
- 최종 수동 확인: 필요
- 관측 fallback 기반 추가 검토 사유: 동일 IP의 단일 요청에서 복수 공격 유형 또는 복수 위험도 신호가 함께 확인되었으나, 동일 IP 이벤트 수가 1건이고 고유 경로가 1개라 운영형 WAF-G005 승격 조건에는 도달하지 않았습니다.
- fallback 차단 후보 승격 보류 사유: scenario 선택 실행에서는 일반 반복 IP fallback을 차단 후보로 승격하지 않음
- evidence scope mismatch: true
- evidence scope mismatch 사유: 선택 row IP와 대표 시나리오 evidence IP가 서로 다릅니다. selectedRowIp=78.153.140.40, representativeScenarioIp=57.141.14.79
- 확인 대상 IP: 수동 확인 필요
- IP 근거 불일치: true
- 권고: 수동 차단 전 웹 UI에서 최종 차단 대상 IP를 반드시 확인하세요.

## 선택 row 기준 요약

- selectedRowIp: 78.153.140.40
- 총 이벤트 수: 3
- 차단 수: 2
- 탐지 수: 1
- 고유 경로 수: 3

## 대표 세부 시나리오 근거 요약

- representativeScenario: WAF-S010 Mixed attack types by same IP
- representativeScenarioIp: 57.141.14.79
- representativeGroupIp: 57.141.14.79
- scenarioEvidenceIps: 57.141.14.79
- evidenceTotalEvents: 1
- evidenceDistinctAttackTypes: 4
- evidenceUniquePaths: 1
- evidenceSamplePaths: /ko/threats/webshell_create_function_vulnerability/
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
- selectedRowIp: 78.153.140.40
- representativeGroupIp: 57.141.14.79
- finalReviewIp: 수동 확인 필요
- scenarioEvidenceIps: 57.141.14.79

- 판단 이유: 대표 운영형 시나리오 WAF-G003 고객사 중요 필터 검토 매칭
- 보류 사유: 선택 row IP와 대표 시나리오 evidence IP가 서로 달라 최종 차단 대상 IP를 자동 확정하지 않음
- 참고 근거: WAF-S010은 low-level evidence로 확인되었으나 WAF-G005 운영형 승격 조건에는 미도달
- 권고 조치: 운영형 시나리오 승격 조건에는 도달하지 않아 차단 후보로 표시하지 않고 관측 기반 수동 검토 evidence로 분리하세요.
- 자동 차단 수행: 아니오
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
- matchedScenarios: [7, 10]
- matchedCount: 2
- representativeScenario: WAF-S010 Mixed attack types by same IP
- representativePriorityScore: 60
- representativeReason: 동일 IP 57.141.14.79에서 복수 공격 유형 또는 복수 위험도 신호가 함께 확인되었습니다.
- evaluatedScenarios: 11
- 운영형 정책상 후보: 예
- 운영자 표시 상태: 보류, 수동 확인 필요
- 자동 차단: 아니오

## 탐지 판단 흐름도

```mermaid
flowchart TD
  nodeA["WAF Row 및 상세 로그\n선택 Row IP: 78.153.140.40"] --> nodeB["세부 시나리오 평가\n매칭: WAF-S007, WAF-S010"]
  nodeB --> nodeC["Allowlist 및 억제\n억제: false\n사유: -"]
  nodeC --> nodeD["운영형 시나리오 평가\n매칭: WAF-G003"]
  nodeD --> nodeE["대표 운영형 그룹\nWAF-G003"]
  nodeE --> nodeF["IP 차단 권고\n운영형 정책상 후보: 예\n운영자 표시 상태: 보류, 수동 확인 필요\n자동 차단: 아니오"]
  nodeF --> nodeG["수동 검토 또는 보고"]
  nodeF --> nodeH["자동 차단 모의 검증 근거"]
```

## 시나리오 근거 관계도

```mermaid
flowchart LR
  nodeR["선택 WAF Row\n78.153.140.40"] --> nodeL["세부 근거"]
  nodeL --> nodeWAFS007["WAF-S007 Customer custom filter\nIP: 57.141.14.79"]
  nodeWAFS007 --> nodeWAFG003["WAF-G003 고객사 중요 필터 검토\n매칭"]
  nodeWAFG003 --> nodeRep["대표 운영형 시나리오\nWAF-G003"]
  nodeL --> nodeWAFS010["WAF-S010 Mixed attack types by same IP\nIP: 57.141.14.79"]
  nodeWAFS010 --> nodeWAFS010Only["세부 근거만 확인"]
  nodeWAFS010 --> nodeWAFG005NotPromoted["WAF-G005 승격 안 됨\n복수 공격 유형은 low-level evidence로 확인되었으나 동일 IP 이벤트 수가 2건 미만이므로 운영형 WAF-G005 조건에는 도달하지 않았습니다."]
  nodeRep["대표 운영형 시나리오\nWAF-G003"] --> nodeRec["IP 차단 검토\n수동 확인 필요"]
```

## IP 근거 분리도

```mermaid
flowchart TD
  nodeSelectedIp["선택 Row IP: 78.153.140.40"]
  nodeRepresentativeIp["대표 시나리오 근거 IP: 57.141.14.79"]
  nodeFinalIp["최종 차단 대상 IP: 수동 확인 필요"]
  nodeWAFS007Ip["WAF-S007 근거 IP: 57.141.14.79"]
  nodeWAFS010Ip["WAF-S010 근거 IP: 57.141.14.79"]
  nodeSelectedIp --> nodeSelectedIpNote["선택 row 근거"]
  nodeSelectedIpNote --> nodeFinalIp
  nodeRepresentativeIp --> nodeRepresentativeIpNote["대표 운영형 근거"]
  nodeRepresentativeIpNote --> nodeFinalIp
  nodeWAFS007Ip --> nodeWAFS007IpNote["WAF-S007 시나리오 근거"]
  nodeWAFS007IpNote --> nodeFinalIp
  nodeWAFS010Ip --> nodeWAFS010IpNote["WAF-S010 시나리오 근거"]
  nodeWAFS010IpNote --> nodeFinalIp
```

> IP 근거 불일치: 수동 차단 전 웹 UI에서 최종 차단 대상 IP를 반드시 확인하세요.

## 운영형 대표 시나리오

- matchedGroupScenarios: [WAF-G003]
- representativeGroupScenario: WAF-G003 고객사 중요 필터 검토
- representativeGroupPriorityScore: 65
- representativeGroupReason: 고객사 커스텀 필터에 해당하는 중요 탐지가 확인되어 IP 차단 검토가 필요합니다.
- representativeLowLevelScenario: WAF-S007

| group | priorityScore | matched | mapped | matchedLowLevel | reason |
|---|---:|---:|---|---|---|
| WAF-G001 반복 스캐닝 기반 IP 차단 검토 | 50 | false | 2, 3, 4, 5 | - | Mapped low-level scenarios did not match. |
| WAF-G002 고위험 단건 공격 검토 | 70 | false | 6 | - | Mapped low-level scenarios did not match. |
| WAF-G003 고객사 중요 필터 검토 | 65 | true | 7 | 7 | 고객사 커스텀 필터에 해당하는 중요 탐지가 확인되어 IP 차단 검토가 필요합니다. |
| WAF-G004 공격 시퀀스 기반 검토 | 85 | false | 9 | - | Mapped low-level scenarios did not match. |
| WAF-G005 복합 공격 유형 검토 | 80 | false | 10 | - | 복수 공격 유형은 low-level evidence로 확인되었으나 동일 IP 이벤트 수가 2건 미만이므로 운영형 WAF-G005 조건에는 도달하지 않았습니다. |
| WAF-G006 분산 유사 공격 검토 | 90 | false | 11 | - | Mapped low-level scenarios did not match. |
| WAF-G007 외부 평판/TI 보강 검토 | 75 | false | 1 | - | Mapped low-level scenarios did not match. |
| WAF-G008 AI 분석 보강 검토 | 60 | false | 8 | - | Mapped low-level scenarios did not match. |

| scenario | priorityScore | matched | attackerIp | reason |
|---|---:|---:|---|---|
| WAF-S001 VT malicious ratio | 90 | false | 78.153.140.40 | VT 분석 결과가 없어 수동차단 후보로 올리지 않습니다. |
| WAF-S002 Scanning Low threshold | 30 | false | - | 스캐닝성 LOW 이벤트가 기준 30건에 도달하지 않았습니다. |
| WAF-S003 Scanning Middle threshold | 40 | false | 185.191.171.10 (다른 IP 기반 미매칭 근거) | 스캐닝성 MIDDLE 이벤트가 기준 20건에 도달하지 않았습니다. |
| WAF-S004 Scanning High threshold | 50 | false | 85.208.96.202 (다른 IP 기반 미매칭 근거) | 스캐닝성 HIGH 이벤트가 기준 10건에 도달하지 않았습니다. |
| WAF-S005 Scanning Critical threshold | 65 | false | 85.208.96.202 (다른 IP 기반 미매칭 근거) | 스캐닝성 CRITICAL 이벤트가 기준 3건에 도달하지 않았습니다. |
| WAF-S006 Non-scanning Critical | 70 | false | - | 비스캐닝 CRITICAL 이벤트가 확인되지 않았습니다. |
| WAF-S007 Customer custom filter | 55 | true | 57.141.14.79 | 고객사 커스텀 필터에 해당하는 중요 탐지가 확인되어 IP 차단 검토가 필요합니다. |
| WAF-S008 AI malicious probability | 75 | false | 185.191.171.10 (다른 IP 기반 미매칭 근거) | AI 분석 결과가 없어 수동차단 후보로 올리지 않습니다. |
| WAF-S009 Threat sequence judgment | 80 | false | 185.191.171.10 (다른 IP 기반 미매칭 근거) | 로그 순서 기반 위협 시퀀스가 확인되지 않았습니다. |
| WAF-S010 Mixed attack types by same IP | 60 | true | 57.141.14.79 | 동일 IP 57.141.14.79에서 복수 공격 유형 또는 복수 위험도 신호가 함께 확인되었습니다. |
| WAF-S011 Distributed similar attack burst | 85 | false | 85.208.96.202 (다른 IP 기반 미매칭 근거) | 분산 유사 공격 기준에 도달하지 않았습니다. |

## 시나리오 상세 근거

### WAF-S007 Customer custom filter
- priorityScore: 55
- attackerIp: 57.141.14.79
- attackerIps: -
- reason: 고객사 커스텀 필터에 해당하는 중요 탐지가 확인되어 IP 차단 검토가 필요합니다.
- recommendation: 웹 화면에서 해당 IP의 요청 경로와 탐지/차단 이력을 확인한 뒤 IP주소 수동차단을 검토하세요.
- customer: WAF-Blog
- matchedRuleId: custom-waf-blog-critical-paths
- matchedPattern: WebShell
- matchedField: path
- matchedEvents: 1
- samplePaths: /ko/threats/webshell_create_function_vulnerability/
- sampleFilters: WebShell

### WAF-S010 Mixed attack types by same IP
- priorityScore: 60
- attackerIp: 57.141.14.79
- attackerIps: -
- reason: 동일 IP 57.141.14.79에서 복수 공격 유형 또는 복수 위험도 신호가 함께 확인되었습니다.
- recommendation: 웹 화면에서 해당 IP의 요청 경로와 탐지/차단 이력을 확인한 뒤 IP주소 수동차단을 검토하세요.
- evidence: {"threshold":2,"totalEvents":1,"distinctAttackTypes":4,"attackTypes":["PROTOCOL VIOLATION","SCANNER","LFI","INJECTION"],"severities":["CRITICAL","HIGH","MIDDLE"],"uniquePaths":1,"samplePaths":["/ko/threats/webshell_create_function_vulnerability/"]}


## 최종 IP 차단 검토 사유

최종 IP 차단 검토 사유: WAF-S007 고객사 커스텀 필터에 해당하는 중요 탐지가 확인되어 IP 차단 검토가 필요합니다. / WAF-S010 동일 IP 57.141.14.79에서 복수 공격 유형 또는 복수 위험도 신호가 함께 확인되었습니다. 자동 IP 차단은 수행하지 않으며 담당자가 웹 화면에서 수동 확인 후 결정합니다.

## 반복 요청 경로

| path |
|---|
| / 0x%5B%5D=androxgh0st |
| /.env |
| / |

## 선택 row 주요 필드

- 출처: WAF 목록에서 선택한 우선순위 이벤트 row

- 공격자 IP: 78.153.140.40
- 대상 도메인: 130.162.156.89
- 요청 Method: POST
- URI/path: /
- 쿼리/요청본문: 0x%5B%5D=androxgh0st
- HTTP 상태값: 406
- 탐지/차단 유형: 차단(OWASP)
- WAF 필터명: Androxgh0st 봇넷
- 위험도/risk: SCANNER>CRITICAL
- 탐지 시각: 2026-05-02 12:48:09.813
- 분석 탭 수집: true
- 로그 탭 수집: true

## 원본 로그 파싱 필드

- method: GET
- uri: /
- host: 130.162.156.89
- remoteIp: 78.153.140.40
- responseStatus: 406

## 담당자 확인 항목

1. 공격자 IP 78.153.140.40의 동일 시간대 반복 요청 전체 확인
2. 반복 경로가 PHP/WordPress 백도어/관리자 경로 스캔인지 확인
3. 차단(OWASP)와 HTTP 406이 정상 차단 정책과 일치하는지 확인
4. 동일 IP의 후속 요청이 계속 발생하는지 확인
5. 웹 UI에서 IP주소 차단 등록 여부 결정