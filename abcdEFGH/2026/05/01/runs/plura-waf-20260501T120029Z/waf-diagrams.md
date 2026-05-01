# WAF Scenario Diagrams

이 문서는 WAF 분석 흐름, WAF-S/WAF-G 역할 분리, manual guide, auto dry-run 흐름을 도식화한 문서입니다.

## 1. WAF 전체 분석 파이프라인

```mermaid
flowchart TD
  row["WAF Rows and Detail Logs"] --> low["Low-level Scenario Engine"]
  low --> s["WAF-S001 to WAF-S011"]
  s --> sup["Allowlist and Suppression"]
  sup --> grp["Group Scenario Engine"]
  grp --> g["WAF-G001 to WAF-G008"]
  g --> rep["Representative Group Scenario"]
  rep --> rec["IP Block Recommendation"]
  rec --> report["Report Artifacts"]
  rec --> guide["Manual Guide Overlay"]
  rec --> dry["Auto Dry-run Plan"]
  dry --> safe["Safety Checks"]
  safe --> audit["Audit and Tickets Evidence"]
```

## 2. WAF-Sxxx and WAF-Gxxx 역할 분리

```mermaid
flowchart LR
  ev["WAF Event Evidence"] --> s["WAF-S Low-level Rules"]
  s --> s1["S001 TI and VT"]
  s --> s2["S002 to S005 Repeated Scanning"]
  s --> s3["S006 Critical Single Attack"]
  s --> s4["S007 Customer Custom Filter"]
  s --> s5["S009 Attack Sequence"]
  s --> s6["S010 Mixed Attack Types"]
  s --> s7["S011 Distributed Similar Attack"]
  s --> g["WAF-G Group Scenarios"]
  g --> op["Operator Report and Guidance"]
```

## 3. Manual Report, Guide, Auto Dry-run 모드 구조

```mermaid
stateDiagram-v2
  [*] --> Preview
  Preview --> ManualReport
  Preview --> ManualGuide
  Preview --> AutoDisabled
  AutoDisabled --> AutoDryRun
  ManualReport --> ReportArtifacts
  ManualGuide --> OverlayShown
  OverlayShown --> AnalystDecision
  AutoDryRun --> SafetyChecks
  SafetyChecks --> DryRunPlan
```

## 4. 수동차단 Guide Mode 흐름

```mermaid
sequenceDiagram
  participant Analyst as Analyst
  participant UI as PLURA WAF UI
  participant Agent as Quark Agent
  Agent->>UI: Open WAF detail view
  UI-->>Agent: Analysis and log tabs
  Agent->>Agent: Evaluate WAF-S and WAF-G scenarios
  Agent-->>Analyst: Show IP block guidance overlay
  Analyst->>UI: Review paths, logs, and IP
  Analyst->>UI: Click manual block button
  UI-->>Analyst: Show manual block dialog
  Note over Agent,UI: Agent never clicks Confirm, Save, or Register
```

## 5. Auto Dry-run Safety Flow

```mermaid
flowchart TD
  grp["Matched Group Scenario"] --> cand["Auto Dry-run Candidate"]
  cand --> sup{"Suppressed or Allowlisted?"}
  sup -->|Yes| ex["Exclude from Auto Candidate"]
  sup -->|No| safe["Safety Checks"]
  safe --> apply{"Auto Apply Enabled?"}
  apply -->|No| wb["wouldBlock false"]
  apply -->|Yes| hold["Blocked by Current Phase Policy"]
  wb --> json["Write auto-block-dry-run.json"]
  wb --> md["Write auto-block-dry-run.md"]
  wb --> audit["Append Audit Log"]
  json --> tickets["Tickets Evidence"]
  md --> tickets
```
