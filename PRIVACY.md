# Privacy Notice / Datenschutzhinweis

**Nyveil Media Suite 1.0.0**  
**Last updated:** 12 November 2026

This notice explains what happens to data when you use Nyveil Media Suite, visit its GitHub repository or releases, contact the publisher, or use an optional donation channel. It is written for the app as distributed at the time of this notice. If the app changes, this notice will be updated.

---

## 1. Controller / Verantwortlicher

**Jason Bruns**  
Email: **Nyveil@web.de**

No postal address is published. See the note in [LEGAL.md](LEGAL.md) about the German § 5 DDG / Impressum position. For privacy questions and data-protection requests, use the email address above.

---

## 2. Short version

- **No account. No cloud. No telemetry. No analytics. No advertising. No crash reporting. No auto-updater.**
- The publisher does **not** receive your URLs, downloads, files, search terms, device identifiers, or usage statistics from the app.
- The app contacts third-party services only when you ask it to (for example, when you paste a link, load a thumbnail, stream media, or start a file share). Those third parties see ordinary network data such as your IP address under their own policies.
- Files you download or share are written to the folder you choose. They are not uploaded to a Nyveil server, because there is no Nyveil server.
- The only app setting that is saved to disk is the optional File Sharing configuration in `%APPDATA%\NyveilMediaSuite\sharing.json`. It may contain a TURN username and password in plain text if you enter them.

---

## 3. Data processed on your device

Nyveil Media Suite runs locally on Windows. The publisher does not operate a backend for the app.

| Data | Where it is stored | Purpose / retention |
| --- | --- | --- |
| Media URL you paste | Memory only | Used to inspect or download the media. Not saved to a history. |
| Media title and thumbnail | Memory only | Shown as a preview. The thumbnail is fetched from the source. |
| Download / conversion folder | Memory only | Used for the current operation. The app does not persist it. |
| Downloaded or converted files | The folder you select | Remain on your device until you delete them. |
| File Sharing settings (STUN/TURN/relay/host) | `%APPDATA%\NyveilMediaSuite\sharing.json` | Used to configure connections. Remains until you delete the file or the app data. |
| TURN username/password (optional) | The same `sharing.json` file, **in plain text** | Used only for the TURN server you configure. Do not reuse sensitive credentials. |
| Temporary file-sharing part files (`.nyveil-*.part`) | The folder you select | Deleted if a transfer fails or is cancelled. Renamed to the final name only after verification. |
| Share code, peer connection metadata | Memory only | Used for the current share. Not stored after the share ends. |
| Application logs | None intentionally created | The app does not intentionally write an application log file. |
| VLC settings (if you use streaming) | Controlled by your VLC installation | VLC may save its own configuration. That data is handled by VLC, not by Nyveil. |

The app has no account system, no cloud storage, no advertising, no analytics, and no telemetry. It does not implement DRM bypassing, login bypassing, private-content access, paywall circumvention, or other access-control circumvention.

Windows, Explorer, antivirus software, backup tools, and other software on your device may independently process files, recent-file lists, or network traffic under their own settings and policies. The publisher does not control that processing.

---

## 4. Network connections initiated by the app

When you use a feature, the app may connect to the following categories of recipients. The publisher does not control those services and does not receive the content of those connections.

| Feature | Recipient / service | Data that may be visible |
| --- | --- | --- |
| Inspecting or downloading a link | The website or platform behind the URL, through `yt-dlp` and its HTTP stack | Your IP address, request headers, the URL, and technical connection data. |
| Loading a preview thumbnail | The thumbnail host named by the source | Your IP address, a browser-like User-Agent, and the thumbnail URL. |
| Streaming media | The source host; FFmpeg may remux the stream locally, and the embedded player uses the locally installed VLC runtime | Your IP address, request headers, and the media URL. VLC may also process data under its own terms. |
| File sharing — direct mode | The other peer (another Nyveil installation) | Your IP address and port, WebRTC/DTLS connection metadata, the share code, and the file bytes you choose to send. |
| File sharing — relay mode | The signaling relay you configure (for example, the included `tools/signaling_relay.py`) | Connection metadata and WebRTC signaling messages (SDP/ICE), which can include IP addresses. File bytes still travel through WebRTC, not through the relay. |
| File sharing — STUN | By default `stun:stun.l.google.com:19302` (Google) | Your IP address and NAT traversal metadata. You can disable STUN in the settings. |
| File sharing — TURN (optional) | The TURN service whose credentials you configure | IP addresses, ports, and relayed WebRTC packets. The publisher does not provide TURN credentials or a TURN service. |
| Visiting the GitHub repository or releases | GitHub, Inc. | Data described in GitHub's Privacy Statement, such as IP address, device/browser data, and download statistics. |
| Emailing the publisher | Your email provider and **web.de** | Your email address, message content, and any attachments you send. |

**Important:** the source platforms, GitHub, Google STUN, your TURN/relay operator, VLC, and your email provider are independent controllers or processors under their own privacy policies. Their processing is not covered by this notice.

No media, URLs, thumbnails, share codes, or transferred files are uploaded to a Nyveil server. The publisher has no such server.

---

## 5. File sharing: special notes

File sharing sends one file directly between two installations using WebRTC data channels. There is no Nyveil account and no Nyveil-operated relay.

- The **share code** is a bearer credential. Anyone who has it can attempt to connect while the share is active. Treat it like a password.
- The **other peer** receives the file and connection metadata. The receiver is warned that the file is unverified and must choose to download it explicitly. Files are never opened automatically.
- If you use a **signaling relay** or **TURN server**, its operator may see connection metadata, including IP addresses. If you operate the relay yourself, you are responsible for it.
- **STUN** is enabled by default and contacts Google's public STUN service. You can disable it in the connection settings; LAN connections can work without it.
- **TURN credentials** are stored locally in plain text if you enter them. Use a dedicated credential with limited privileges and do not reuse a password from another service.
- Do not share files that you are not allowed to share. The publisher does not moderate, inspect, or store shared files.

---

## 6. Data the publisher may receive

The publisher only receives data that you choose to send or that GitHub makes available in aggregate:

1. **Support and legal correspondence.** If you email **Nyveil@web.de**, the publisher receives your email address, message, and attachments. This is used to answer your request, handle legal notices, and maintain necessary business records.
2. **GitHub repository and releases.** GitHub hosts the repository and release downloads. GitHub may show the publisher aggregate download counts, referrer information, and repository traffic statistics. The publisher does not receive individual downloader identities from GitHub. If you open an issue, your GitHub profile and issue content are public; do not include personal or confidential information.
3. **Donations.** The app is currently free of charge and the publisher does not currently accept donations. If a donation channel is added, the donation provider (for example, GitHub Sponsors, Ko-fi, or PayPal) will process your data under its own privacy policy, and this notice will be updated.

The publisher does **not** receive app telemetry, crash reports, download history, file contents, or usage analytics.

---

## 7. Legal bases (GDPR / DSGVO)

To the extent the publisher processes personal data, the legal bases are:

- **Art. 6(1)(b) GDPR** — performance of a contract or steps prior to entering a contract (for example, responding to a support request about the software).
- **Art. 6(1)(f) GDPR** — legitimate interests in operating and protecting the project, responding to enquiries, handling legal claims, and preventing abuse. The publisher's interest is to provide and maintain a free, non-commercial software project.
- **Art. 6(1)(c) GDPR** — compliance with legal obligations (for example, tax or record-keeping duties, if applicable).
- **Art. 6(1)(a) GDPR** — consent, where a specific processing activity relies on consent. You can withdraw consent at any time with effect for the future.

The app's local processing (URLs, files, settings) is not used by the publisher to identify you. Third-party services named in section 4 rely on their own legal bases.

---

## 8. Recipients and international transfers

Data may be received by:

- **GitHub, Inc.** (repository hosting, releases, issues, traffic statistics), located in the United States. GitHub's Privacy Statement describes the safeguards it uses for international transfers (for example, the EU-US Data Privacy Framework and/or Standard Contractual Clauses).
- **web.de** (email hosting), located in Germany.
- **The source platform / website** you choose to access, which may be located outside the EU/EEA.
- **Your relay, TURN, or STUN operator**, if you configure or use one.
- **A future donation provider**, only if you choose to donate.

The publisher does not sell personal data and does not share it for advertising.

---

## 9. Retention

- **Support and legal emails:** kept until the request is resolved and any statutory retention period has expired, then deleted or anonymised.
- **GitHub data:** retained according to GitHub's policies. Issues and comments remain public until deleted by their authors or the repository owner.
- **App data on your device:** remains until you delete the relevant files or app data. The publisher has no ability to delete it remotely.
- **Donations:** none currently; if added, the provider's retention rules apply, and the publisher keeps only what is required for tax/accounting purposes.

---

## 10. Your rights

Subject to applicable law, you have the right to:

- access your personal data (Art. 15 GDPR);
- rectify inaccurate data (Art. 16 GDPR);
- erase data (Art. 17 GDPR);
- restrict processing (Art. 18 GDPR);
- data portability (Art. 20 GDPR);
- object to processing based on legitimate interests (Art. 21 GDPR);
- withdraw consent at any time (Art. 7(3) GDPR);
- lodge a complaint with a data protection supervisory authority (Art. 77 GDPR). You can contact the authority in your habitual residence, your place of work, or the publisher's place of residence.

To exercise these rights, email **Nyveil@web.de**. Please describe your request and the data concerned. The publisher may need to verify your identity before acting. There is no automated decision-making or profiling in the app.

---

## 11. Security

The app uses WebRTC/DTLS for file-sharing transport and SHA-256 for integrity verification. These measures protect the connection and detect corruption; they do not prove that a sender or file is trustworthy.

Local settings, including any TURN credentials, are stored in a plain-text JSON file under your Windows user profile. Protect your Windows account and do not share the file. The publisher cannot guarantee the security of third-party services, your network, or files sent by other users.

---

## 12. Children

The app is not directed at children under 16. The publisher does not knowingly collect personal data from children. If you believe a child has sent personal data to the publisher, contact **Nyveil@web.de** so it can be deleted.

---

## 13. Changes to this notice

This notice may be updated when the app, distribution, or legal requirements change. The current version is always in the repository and in the app's **Information → Privacy** page. Material changes will be noted in the release notes or repository history.

---

## 14. German short summary / Kurzfassung auf Deutsch

Die App läuft lokal. Es gibt keine Konten, keine Cloud, keine Telemetrie, keine Werbung und keine Analyse. Der Entwickler erhält keine URLs, Downloads, Dateien oder Nutzungsdaten aus der App. Beim Abrufen von Medien, Vorschaubildern, Streams oder beim Dateiaustausch werden jedoch die jeweils beteiligten Dritten (Quell-Website, GitHub, ggf. STUN-/TURN-/Relay-Server, E-Mail-Anbieter) technisch notwendige Verbindungsdaten wie deine IP-Adresse sehen. Die Dateifreigabe-Einstellungen werden lokal unter `%APPDATA%\NyveilMediaSuite\sharing.json` gespeichert; TURN-Zugangsdaten liegen dort im Klartext. Bei Fragen oder zur Ausübung deiner Datenschutzrechte: **Nyveil@web.de**.

Die englische Fassung ist maßgeblich; die deutsche Kurzfassung dient der besseren Verständlichkeit.

---

**Contact:** Jason Bruns — **Nyveil@web.de**
