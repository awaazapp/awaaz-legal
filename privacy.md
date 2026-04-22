# Privacy Policy for Awaaz

**Last updated:** 22 April 2026
**Effective date:** 22 April 2026

---

## Summary (the short version)

Awaaz is a voice-only social network. To make it work, we store the username you pick, the voice notes you record, and the follow relationships you create. We do not collect your email, your phone number, your location, your contacts, or any advertising identifier. We do not sell your data. We do not share it with third-party advertisers. You can delete your account — and with it, everything we hold about you — from inside the app at any time.

If you only read one section, read this one. The rest of this document explains the same thing in the detail that privacy law requires.

---

## 1. Who we are (Data Controller)

Awaaz is operated by an independent developer ("we", "us", "Awaaz"). For the purposes of the EU General Data Protection Regulation (GDPR) and India's Digital Personal Data Protection Act, 2023 (DPDP Act), we are the **Data Controller** (or "Data Fiduciary" under the DPDP Act) for the data described in this policy.

**Contact:** awaazappofficial@gmail.com
**Developer:** Awaaz
**Jurisdiction:** India

---

## 2. What data we collect and why

We collect only what the app needs to function. Each item below lists the data, the purpose, and the legal basis under GDPR.

### 2.1 Account information

- **Username** — a unique handle you choose during signup (3–20 characters, alphanumeric and underscore). Used to identify you within the app.
- **Password** — stored only as a cryptographic hash by Firebase Authentication. We never see, log, or transmit your plaintext password.

For internal routing, Firebase Authentication requires an email-like identifier. We synthesize one from your username (e.g. `yourname@awaaz.local`). It is not a real email address, is never used to contact you, and cannot receive mail.

*Legal basis: performance of a contract (GDPR Art. 6(1)(b)) — we cannot give you an account without this.*

### 2.2 Content you create

- **Voice notes** — audio recordings up to 60 seconds, stored as M4A files in Firebase Storage at the path `voice_notes/{your_user_id}/`.
- **Post titles** — short text descriptions you attach to voice notes.
- **Voice replies** — threaded voice recordings on other users' posts.
- **Bio** — an optional text description on your profile.

*Legal basis: performance of a contract (GDPR Art. 6(1)(b)).*

### 2.3 Relationship and activity data

- **Follow graph** — the list of accounts you follow and who follows you.
- **Blocks** — accounts you have blocked. Stored so we can hide their content from you. Not visible to the blocked user.
- **Listen counts** — aggregate play counts per post. **We do not record *who* listened to a given post**, only that the count increased.
- **Reports** — if you report a user or post, we store the report, the reported target, and a timestamp. Reports are readable only by administrators.

*Legal basis: legitimate interest (GDPR Art. 6(1)(f)) — operating and moderating a functioning social platform.*

### 2.4 Technical and diagnostic data

- **Crash reports** (via Firebase Crashlytics) — if the app crashes, we receive a stack trace, device model, OS version, and app version. These reports do not contain your voice notes, messages, or password.
- **Analytics events** (via Firebase Analytics) — we record anonymized, aggregate events such as `signup`, `post_created`, `reply_created`, `listen`, `follow`, `share`, and `app_open`. These help us understand which features are used; they do not identify you personally.
- **Push notification token** (if you enable notifications) — an opaque device-specific token from Firebase Cloud Messaging, used only to deliver notifications you asked for.

*Legal basis: legitimate interest (GDPR Art. 6(1)(f)) — keeping the app stable and usable. You can disable analytics and crash reporting in your device's system settings for Awaaz.*

### 2.5 What we do NOT collect

We want to be explicit about this, because the default for most apps is the opposite:

- No email address
- No phone number
- No real name
- No location (neither precise nor approximate)
- No device advertising ID (IDFA / GAID)
- No contacts or address book
- No photos, camera access, or gallery access
- No microphone access outside of active recording (the mic is only live while you are holding the record button)
- No data from third-party tracking SDKs

---

## 3. How your data is stored and secured

- All data is stored in **Google Firebase** services (Cloud Firestore for structured data, Firebase Storage for audio files, Firebase Authentication for credentials).
- Data in transit is encrypted using TLS 1.2+.
- Data at rest is encrypted using Google Cloud's default server-side encryption (AES-256).
- Access to production data is restricted to the developer account and is governed by **Firestore Security Rules** and **Firebase App Check** (Play Integrity), which prevent unauthorized clients from reading or writing data directly.
- Passwords are hashed by Firebase Authentication; we have no mechanism to retrieve them.

No system is perfectly secure. If we ever become aware of a breach affecting your personal data, we will notify affected users and the relevant supervisory authority **within 72 hours of discovery**, as required by GDPR Art. 33–34 and the DPDP Act.

---

## 4. International data transfers

Awaaz is operated from India and uses Google Firebase, whose infrastructure spans multiple Google Cloud regions. Your data may be stored on, or accessed from, Google Cloud servers located outside your country of residence, including in the United States and the European Union.

Google Cloud is certified under the **EU–U.S. Data Privacy Framework** and offers **Standard Contractual Clauses (SCCs)** for transfers from the EEA, the UK, and Switzerland. These provide the legal safeguards required by GDPR Chapter V.

---

## 5. Who we share data with

We share data only with the infrastructure providers that make the app run:

- **Google Firebase / Google Cloud Platform** — hosting, authentication, storage, analytics, crash reporting, push notifications.
- **Google Play Services** — only if you install the app from the Play Store. Governed by Google's privacy policy.

We do **not**:

- Sell your data to anyone, ever.
- Share your data with advertisers or data brokers.
- Use your voice recordings to train machine learning models.
- Allow third parties to embed tracking inside the app.

We may disclose data if compelled by a valid legal order from a court of competent jurisdiction. If we receive such an order and are not legally prohibited from doing so, we will attempt to notify the affected user before complying.

---

## 6. Data retention and deletion

### 6.1 While your account is active

Your account data, voice notes, and activity records are retained as long as your account exists.

### 6.2 When you delete your account

You can delete your account at any time from **Profile → Delete Account**. Deletion is permanent and is designed to be GDPR-compliant (right to erasure, Art. 17). Specifically:

- **Your profile** (username, bio, follower counts, badges) is hard-deleted from Firestore.
- **Your follow relationships** (both directions) are hard-deleted.
- **Your Firebase Authentication account** is deleted, so the username cannot be used to log in again.
- **Your voice posts that have no replies from other users** are hard-deleted along with their audio files in Firebase Storage.
- **Your voice posts that have replies from other users** are **tombstoned** — the audio file is deleted from Storage and the post's own text and author reference are stripped, but the post record remains so that other users' replies on the thread are not orphaned. A tombstoned post displays as "[deleted]" and contains none of your personal data. This is the minimum footprint required to preserve other users' content that they chose to make.
- **Your replies on other users' posts** follow the same rule — audio and author reference removed, structural placeholder may remain if needed to preserve thread integrity.

Audio files deleted from Firebase Storage may persist in encrypted Google Cloud backups for up to **30 days** before being permanently overwritten. After this period, the data is unrecoverable.

### 6.3 Retained beyond account deletion

- **Reports you filed or that were filed against you** — retained in anonymized form for up to 12 months after account deletion for abuse-pattern analysis and legal defense. Personal identifiers are stripped.
- **Aggregate, non-identifying analytics** — event counts that cannot be tied back to you are retained indefinitely.

---

## 7. Your rights

Depending on where you live, you have some or all of the following rights. Awaaz honors them for **all users, globally**, regardless of local law:

- **Right of access** — see all data we hold about you. Most of it is visible inside the app; for anything else, email us.
- **Right to rectification** — correct inaccurate data. You can edit your username, bio, and posts in-app.
- **Right to erasure ("right to be forgotten")** — delete your account as described above.
- **Right to data portability** — request a machine-readable export of your data. Email us and we will provide a JSON export of your profile, posts (including audio file links), replies, and follow graph within 30 days.
- **Right to object / restrict processing** — tell us you do not want us to process your data beyond what is required to deliver the service.
- **Right to withdraw consent** — where we rely on consent (e.g. push notifications), you can revoke it at any time from your device settings.
- **Right to lodge a complaint** — with your local data protection authority. For EEA users, this is your national DPA; for Indian users, the Data Protection Board of India.

To exercise any right that you cannot complete inside the app, email **awaazappofficial@gmail.com**. We will respond within **30 days**.

---

## 8. Children and minors

- Awaaz is **not intended for users under 13** anywhere in the world, and we do not knowingly collect data from them. If we learn that we have collected data from a child under 13, we will delete it promptly.
- In India, the **DPDP Act, 2023** treats anyone under 18 as a minor and requires verifiable parental consent for processing their data. Awaaz does not currently have a parental consent flow, and is therefore **not intended for users under 18 in India**.
- If you are a parent or guardian and believe your child has created an Awaaz account, email us at awaazappofficial@gmail.com and we will delete the account.

---

## 9. Moderation, safety, and community guidelines

- You can **report** any post or user for violating community guidelines. Reports are stored in a separate collection readable only by administrators.
- You can **block** any user. Blocked users cannot see your posts or replies in their feed, and their content is hidden from yours. Blocks are not disclosed to the blocked user.
- Reports are reviewed by administrators and may result in content removal or account suspension.
- We cooperate with law enforcement only in response to valid legal process.

---

## 10. Cookies and trackers

Awaaz is a mobile application and does not use web cookies. Our mobile SDKs (Firebase) use local device storage to cache authentication tokens and pending uploads. This storage is cleared when you uninstall the app.

Awaaz **does not** use any third-party advertising SDK, attribution SDK, or cross-app tracking technology.

---

## 11. Changes to this policy

We may update this policy over time. When we do:

- The "Last updated" date at the top will change.
- **Material changes** (anything affecting what we collect, how we use it, or who we share it with) will be announced via an in-app notice at least 14 days before taking effect, giving you time to review and, if you disagree, delete your account.
- The full history of changes is available in the git history of the public repository where this policy is hosted.

---

## 12. Contact

For privacy questions, data subject requests, or breach reports:

- **Email:** awaazappofficial@gmail.com
- **Developer:** Awaaz
- **Response time:** within 30 days for standard requests; within 72 hours for breach reports.

---

*This policy is hosted publicly so that its version history is auditable. The canonical URL is linked from the Awaaz app ("Settings → Privacy Policy") and from the Google Play Store listing.*
