# v0.2.5 Pilot Validation

Use this checklist for the three-person pilot. All testers must download the
same archive from the `trial-v0.2.5` GitHub Release and verify SHA-256 before
testing.

## Test Environment

```text
Tester:
Windows version:
Archive SHA-256:
Adapter:
Driver:
Vendor tool and version:
Target device/board:
BSDL:
Single-device or multi-device chain:
```

## Existing-Feature Checklist

| Check | Result | Evidence |
| --- | --- | --- |
| Native application starts | Pass / Fail | Screenshot or log |
| Seven-day trial is shown | Pass / Fail | Remaining time |
| Adapter is detected | Pass / Fail | Adapter type |
| Connection succeeds | Pass / Fail | Interface Log |
| Physical IDCODE matches BSDL | Pass / Fail | IDCODE |
| Wrong BSDL is rejected | Pass / Fail | Error text |
| Start Scan produces samples | Pass / Fail | Scan/s |
| Waveform shows real transitions | Pass / Fail | Sanitized screenshot |
| Time/Div and horizontal navigation work | Pass / Fail | Observation |
| Scan history keeps each scan | Pass / Fail | Scan timestamps |
| `.cjwave` save completes | Pass / Fail | File size/time |
| `.cjwave` reload preserves transitions/timestamps | Pass / Fail | Comparison |
| Export functions follow trial limits | Pass / Fail | Export type |
| Stop/disconnect exits cleanly | Pass / Fail | Interface Log |

## Runtime Measurements

```text
Selected pin count:
Scan/s:
Effective/s:
Render FPS:
Dropped samples:
Longest continuous run:
Recording size:
Save duration:
Load duration:
Engineering intervention required:
```

Do not upload confidential BSDL, board profiles, waveforms, device identifiers,
serial numbers, or customer logs to a public Issue.
