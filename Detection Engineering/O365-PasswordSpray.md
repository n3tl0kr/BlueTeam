## Potential Password Spray Detected

### Description
This detection rule monitors login activities in Office 365 and identifies patterns indicative of password spraying attacks. It flags instances where multiple failed login attempts are made from the same internet service provider (ISP) within a short time frame, targeting various user accounts with a limited set of passwords.

### Platform
Microsoft 365 Defender

### Detection Logic
```
//M365 Password Spray Detection - Advanced Hunting
let timeWindow = 4m;
let threshold = 300;
IdentityLogonEvents
| where FailureReason != ""
| summarize (Timestamp, ReportID)=arg_max(Timestamp, ReportId), count() by ISP, FailureReason, bin(Timestamp, timeWindow)
| where count_ > threshold
| project ISP, FailureReason, Timestamp = Timestamp1, ReportID
```
