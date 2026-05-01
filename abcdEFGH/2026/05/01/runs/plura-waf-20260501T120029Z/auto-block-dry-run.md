# PLURA-XDR WAF auto-block dry-run

- enabled: true
- mode: dry-run
- dryRun: true
- policyVersion: 1.0
- reviewIp: 85.208.96.194
- candidateCount: 1
- dryRunCandidate: true
- wouldAutoBlockIfSafetyReady: true
- wouldBlock: false
- wouldBlockReason: Candidate exists, but auto apply remains disabled. This plan is for dry-run review only.
- autoApplyReady: false
- autoBlockExecuted: false
- representativeGroupScenario: WAF-G003 고객사 중요 필터 검토
- matchedGroupScenarios: [WAF-G003]
- matchedScenarios: [7, 10]
- candidateGroups: [WAF-G003]
- reason: Dry-run candidate confirmed for WAF-G003, but auto apply remains blocked: TTL policy is required but PLURA_WAF_AUTO_BLOCK_TTL_SECONDS is not configured; rollback policy is required but rollback execution is not enabled

## Safety Checks

- autoMode: dry-run
- applyEnabled: false
- dryRun: true
- maxIpsPerRun: 1
- ttlDays: 0
- allowlistChecked: true
- suppressionChecked: true
- privateIpExcluded: true
- clickedManualBlock: false
- clickedConfirm: false
- clickedSaveOrConfirm: false
- autoBlockExecuted: false

## Candidates

| IP | Representative Group | Events | Suppressed | Would Block | Reason | TTL | Action |
| --- | --- | ---: | --- | --- | --- | ---: | --- |
| 85.208.96.194 | WAF-G003 | 1 | false | false | Auto-block candidate is present, but apply remains disabled by current policy. Dry-run evidence only. | 0 | dry-run-only |

## Blocked By Safety

- TTL policy is required but PLURA_WAF_AUTO_BLOCK_TTL_SECONDS is not configured
- rollback policy is required but rollback execution is not enabled

## Notes

- Dry-run only: no PLURA IP block UI/API save, register, or confirm action was attempted.
- Threat-intel only (WAF-G007) and AI only (WAF-G008) group matches do not become standalone auto-block dry-run candidates.
- Audit log target: C:\git\quark\quark\artifacts\waf\auto-block-audit.jsonl