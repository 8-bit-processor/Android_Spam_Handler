# Anti-Scam Guardian (Android Spam & Scam Documenting kit)

**Anti-Scam Guardian** is a 100% free, open-source, privacy-first native Android watchdog designed to intercept fraudulent calls, analyze phishing text messages, preserve digital evidence, and format standardized complaints for submission to regulatory authorities (FTC, FCC, and FBI IC3).

---

## 🛡️ Key Architectural Principles

* **0% Passive Battery Consumption**: Uses Android’s official, event-driven `CallScreeningService`. There are no background polling loops, no persistent notifications, and no battery wake locks. The app process is woken by the Android Telecom subsystem only when an incoming call arrives, evaluates the number in under 10 milliseconds, and returns to sleep.
* **Non-Destructive & No System Conflicts**: Works cooperatively with your default dialer and messaging app. Calls are filtered at the OS Telecom layer; incoming text messages are analyzed read-only without modifying or hiding your SMS inbox.
* **Safe-List Contacts Protection**: Automatically checks incoming callers against your local address book (`ContactsContract`). Calls from saved friends, family, doctors, or colleagues are guaranteed never to be screened or blocked.
* **100% On-Device Privacy**: All incident logs, evidence notes, and screenshots are stored exclusively in your local device SQLite database. No analytics, no third-party trackers, and no remote servers.
* **Official Law Enforcement Exports**: One-tap export to standardized complaint formats (Plaintext, CSV spreadsheets, and JSON) ready for direct submission to the Federal Trade Commission (FTC), Federal Communications Commission (FCC), and FBI Internet Crime Complaint Center (IC3).
* **System Share Sheet Integration**: Select text or screenshots in any app (WhatsApp, Google Messages, Browser) and tap **Share ➔ Anti-Scam Guardian** to instantly document the incident.

---

## 🏗️ Core Features

1. **Intelligent Call Screening**:
   * Pre-seeded with known international fraud rings (Jamaican lottery fraud `+1876*`, Wangiri callback fraud `+232*`, Caribbean one-ring scams `+1809*`, `+1284*`, `+1473*`, and US `+1900*`).
   * Configurable action: **Reject (Drop)**, **Silence Ringer**, or **Flag & Log Only**.
   * Preserves records in the standard phone call log with a "Screened / Blocked" tag.
   * Optional toggle to block hidden / private caller IDs.

2. **SMS Phishing & Scam Analyzer**:
   * Inspects incoming SMS for high-risk top-level domains (`.xyz`, `.top`, `.ru`), URL shorteners (`bit.ly`, `tinyurl`), and raw IP hostnames.
   * Heuristic category detection for Bank Impersonation, Package Delivery scams (USPS/FedEx/UPS), Government Extortion (IRS/Social Security), Prize/Lottery scams, and Tech Support fraud.
   * Interactive on-demand scanner to paste and analyze suspicious messages or URLs anytime.

3. **Screenshot & Evidence Preservation**:
   * Attach screenshot evidence of fraudulent text messages, fake caller IDs, or phishing emails.
   * Stored securely in internal app storage with thumbnail preview and full-screen inspection.
   * Attached directly when sharing evidence reports with authorities.

4. **Multi-Format Reporting & Regulatory Portals**:
   * Direct deep links to:
     * **FTC Report Fraud**: [reportfraud.ftc.gov](https://reportfraud.ftc.gov/)
     * **FCC Consumer Complaints**: [consumercomplaints.fcc.gov](https://consumercomplaints.fcc.gov/)
     * **FBI IC3**: [ic3.gov](https://www.ic3.gov/)
     * **National Do Not Call Registry**: [donotcall.gov](https://www.donotcall.gov/)
   * Export formats:
     * **Complaint Text Report**: Pre-formatted for pasting into official portal forms.
     * **CSV Spreadsheet**: Structured tabular record of all incidents.
     * **JSON Document**: Complete raw data export for technical investigation.

---

## ⚙️ How It Works: The Telecom Call Pipeline

When an incoming cellular call arrives, Android Telecom routes it through a strict sequential pipeline:

```
Incoming Call ──▶ 1. Emergency Call (911/112)? ──▶ Rings immediately (Always bypassed)
                        │
                        ▼ (No)
                  2. Built-in Phone Blocklist? ──▶ Drops call (System handled)
                        │
                        ▼ (Not in system blocklist)
                  3. Contact in Address Book? ──▶ Rings normally (Safe-List Guard)
                        │
                        ▼ (Not in contacts)
                  4. Anti-Scam Guardian ───────▶ Matches Rule? ──▶ Rejects/Silences ringer
                        │                                          & logs evidence
                        ▼ (Allowed)
                  5. Default Phone App Rings Normally
```

---

## 🚀 Building & Testing

### Prerequisites
* JDK 17 or JDK 21
* Android SDK (API 36 / Build Tools 35+)

### Build Commands
```bash
# Run unit tests (Phishing heuristics, Report exporters, Rule matchers)
./gradlew test

# Build debug APK
./gradlew assembleDebug

# Output location
app/build/outputs/apk/debug/app-debug.apk
```

---

## 📜 Open Source License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

### ⚠️ Disclaimer
Anti-Scam Guardian is an independent open-source utility designed for consumer protection, education, and fraud documentation. It is not affiliated with, maintained by, or endorsed by the Federal Trade Commission (FTC), Federal Communications Commission (FCC), Federal Bureau of Investigation (FBI), or any law enforcement agency. All software is provided "AS IS" without warranties of any kind under the MIT License.
