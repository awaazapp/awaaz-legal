# Privacy Policy for Awaaz

**Last updated:** 10 August 2026
**Effective date:** 4 August 2026

---

## Summary (the short version)

Awaaz is a voice-only social network. You get in by signing in with Google, and that is now the only way in. From that sign-in we receive your Google email address, display name and profile photo URL, and we store your email address, your profile photo URL and a username derived from your display name. We also store the voice notes you record and the follow relationships you create. We do not collect your phone number, your location, your contacts, or any advertising identifier. We do not sell your data. We do not share it with third-party advertisers. You can delete your account — and with it, everything we hold about you — from inside the app at any time.

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

Awaaz accounts are created and accessed with **Sign in with Google**. There is no Awaaz password to choose and no separate Awaaz credential to lose.

When you sign in, Google returns a signed identity token for the Google account you picked. From it the app receives:

- **A Google account identifier** — an opaque id that tells us which account signed in.
- **Your email address.**
- **Your Google display name.**
- **Your Google profile photo URL.**

What we then keep:

- **Firebase Authentication** stores the link between your Google account and your Awaaz account, including the account identifier, email address, display name and profile photo URL that Google supplied.
- **Your Awaaz profile** (Cloud Firestore, `users/{your_user_id}`) stores a **username**, your **email address**, and your **profile photo URL**.
- The **username** is derived from your Google display name: the first word, lowercased and reduced to letters, digits and underscores (3–20 characters), with a number or a short random tail added if that handle is already taken. If no usable name can be derived — for example because your display name is not written in the Latin alphabet — a random one is generated instead. Your display name itself is not written to your Awaaz profile.
- Your **email address is never shown to other users**. We do not send marketing email. We use the address to identify your account and to check that a support or deletion request genuinely comes from you.

*Why we need it: to authenticate you, and to give you a route back into your account. Awaaz previously held no email address at all, which meant a lost credential was unrecoverable; delegating sign-in to Google is what fixes that.*

*The sign-in itself takes place on Google's side and is governed by [Google's Privacy Policy](https://policies.google.com/privacy). Awaaz never sees your Google password, and receives only the basic profile and email address described above.*

*Legal basis: performance of a contract (GDPR Art. 6(1)(b)) — we cannot give you an account without this.*

**Accounts created before Google sign-in.** Until August 2026, an Awaaz account was created with a username and an **access code** (a password), and Firebase Authentication was given a synthetic identifier of the form `yourname@awaaz.local` — not a real address, never used to contact anyone, and unable to receive mail. Those accounts have been **disabled**: they can no longer be used to sign in. Firebase Authentication still holds the synthetic identifier and the hashed access code for as long as the account record exists; the access code itself was never readable by us. Recordings made under those accounts are retained — see [Terms §3](terms.md). If you want a pre-migration account and its data deleted, email us; [Account Deletion](delete-account.md) explains how.

### 2.2 Content you create

- **Voice notes** — audio recordings, stored as M4A files in Firebase Storage at the path `voice_notes/{your_user_id}/`. The maximum length is shown in the app and is currently 60 seconds; we may adjust it without changing this policy.
- **Post titles** — short text descriptions you attach to voice notes.
- **Voice replies** — threaded voice recordings on other users' posts.
- **Bio** — an optional text description on your profile.
- **Images you choose to attach** — you may optionally attach one image to a post or a reply, and set a profile photo. These are selected by you from your device using the system image picker and are uploaded to Firebase Storage (`post_images/{your_user_id}/` for post and reply images, and a separate avatar path for profile photos). We only ever receive the specific image you pick; we never browse, scan, or index your photo library, and the app has no camera access.

*Legal basis: performance of a contract (GDPR Art. 6(1)(b)).*

### 2.3 Relationship and activity data

- **Follow graph** — the list of accounts you follow and who follows you.
- **Blocks** — accounts you have blocked. Stored so we can hide their content from you. Not visible to the blocked user.
- **Listens** — when you play a voice note, we record that **you** listened to that post, once. We store this per person rather than as a bare tally so that a post's listen count reflects how many people heard it rather than how many times it was replayed, and so that ranking the feed is not distorted by repeat plays. Listen records are not shown to other users; the post's author sees only the total.
- **Reports** — if you report a user or post, we store the report, the reported target, and a timestamp. Reports are readable only by administrators.

*Legal basis: legitimate interest (GDPR Art. 6(1)(f)) — operating and moderating a functioning social platform.*

### 2.4 Technical and diagnostic data

- **Crash reports** (via Firebase Crashlytics) — if the app crashes, we receive a stack trace, device model, OS version, and app version. These reports do not contain your voice notes, your messages, or your sign-in tokens.
- **Analytics events** (via Firebase Analytics) — we record anonymized, aggregate events such as `signup`, `post_created`, `reply_created`, `listen`, `follow`, `share`, and `app_open`. These help us understand which features are used; they do not identify you personally.
- **Push notification token** (if you enable notifications) — an opaque device-specific token from Firebase Cloud Messaging, used only to deliver notifications you asked for.

*Legal basis: legitimate interest (GDPR Art. 6(1)(f)) — keeping the app stable and usable. You can disable analytics and crash reporting in your device's system settings for Awaaz.*

### 2.5 What we do NOT collect

We want to be explicit about this, because the default for most apps is the opposite. Beyond the basic Google profile and email address described in 2.1, there is:

- No phone number
- No location (neither precise nor approximate)
- No device advertising ID (IDFA / GAID)
- No contacts or address book
- No camera access, and no access to your photo library beyond the single image you explicitly pick (see 2.2)
- No microphone access outside of active recording (the mic is only live while you are holding the record button)
- No data from third-party tracking SDKs
- **Nothing else from your Google account.** Signing in gives Awaaz your basic profile and email address and nothing more — not your Gmail, Drive, Calendar, Contacts, or Photos.

Other users see your username, your bio, your profile photo and what you post. They do not see your email address or your Google display name.

---

## 3. How your data is stored and secured

- All data is stored in **Google Firebase** services (Cloud Firestore for structured data, Firebase Storage for audio files, Firebase Authentication for sign-in records).
- Data in transit is encrypted using TLS 1.2+.
- Data at rest is encrypted using Google Cloud's default server-side encryption (AES-256).
- Access to production data is restricted to the developer account and is governed by **Firestore Security Rules** and **Firebase Storage Security Rules**, which determine what any signed-in client may read or write. Database deletion protection and daily point-in-time recovery are enabled.
- Awaaz does not set, see, or store a password for your account. Sign-in is delegated to Google, which authenticates you and returns a short-lived signed token that Firebase Authentication verifies. Access codes on pre-migration accounts were hashed by Firebase Authentication and were never retrievable by us; those accounts are disabled (see 2.1).

No system is perfectly secure. If we ever become aware of a breach affecting your personal data, we will notify affected users and the relevant supervisory authority **within 72 hours of discovery**, as required by GDPR Art. 33–34 and the DPDP Act.

---

## 4. International data transfers

Awaaz is operated from India and uses Google Firebase, whose infrastructure spans multiple Google Cloud regions. Your data may be stored on, or accessed from, Google Cloud servers located outside your country of residence, including in the United States and the European Union.

Google Cloud is certified under the **EU–U.S. Data Privacy Framework** and offers **Standard Contractual Clauses (SCCs)** for transfers from the EEA, the UK, and Switzerland. These provide the legal safeguards required by GDPR Chapter V.

---

## 5. Who we share data with

We share data only with the infrastructure providers that make the app run:

- **Google Firebase / Google Cloud Platform** — hosting, authentication, storage, analytics, crash reporting, push notifications.
- **Sign in with Google** — when you tap *Continue with Google*, the sign-in happens on Google's side. Google therefore knows that you signed in to Awaaz, and returns your basic profile and email address to the app. That exchange is governed by [Google's Privacy Policy](https://policies.google.com/privacy). Awaaz does not send your recordings, your listens, or your follow graph to the sign-in service.
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

If your account is **disabled** (see [Terms §3](terms.md)), the same data is retained. Disabling stops sign-in; it is not deletion. You can still have the data erased — email us as described in [Account Deletion](delete-account.md), and we will delete it on the same terms as an in-app deletion.

### 6.2 When you delete your account

You can delete your account at any time from **Profile → Delete Account**. Google asks you to confirm the account first — that step exists so that a phone left unlocked cannot be used to erase someone's recordings. Deletion is permanent and is designed to be GDPR-compliant (right to erasure, Art. 17). Specifically:

- **Your profile** (username, email address, profile photo URL, bio, follower counts, badges) is hard-deleted from Firestore.
- **Your follow relationships** (both directions) are hard-deleted.
- **Your Firebase Authentication account** is deleted. That removes the link between your Google account and Awaaz, along with the account identifier, email address, display name and photo URL Google supplied, and the username cannot be used to sign in again. **Deleting your Awaaz account does not delete or change your Google account** — it only ends Awaaz's access to it. You can also revoke that access from your Google account's *Third-party apps & services* settings, though doing so on its own does not delete anything we already hold.
- **Your voice posts that have no replies from other users** are hard-deleted along with their audio files, and any attached images, in Firebase Storage.
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
- **Right to rectification** — correct inaccurate data. You can edit your username, bio, and posts in-app. Your email address and profile photo URL were taken from your Google account at the moment you first signed in and are not refreshed automatically afterwards; if they have gone out of date and you want them corrected, email us.
- **Right to erasure ("right to be forgotten")** — delete your account as described above.
- **Right to data portability** — request a machine-readable export of your data. Email us and we will provide a JSON export of your profile, posts (including audio file links), replies, and follow graph within 30 days.
- **Right to object / restrict processing** — tell us you do not want us to process your data beyond what is required to deliver the service.
- **Right to withdraw consent** — where we rely on consent (e.g. push notifications), you can revoke it at any time from your device settings.
- **Right to lodge a complaint** — with your local data protection authority. For EEA users, this is your national DPA; for Indian users, the Data Protection Board of India.

To exercise any right that you cannot complete inside the app, email **awaazappofficial@gmail.com**. We will respond within **30 days**.

---

## 8. Children and minors

- Awaaz is **not intended for anyone under 18**, anywhere in the world, and we do not knowingly collect data from them. If we learn that we have collected data from someone under 18, we will delete it promptly.
- We ask every person to confirm they are 18 or over before an account is created, and we record that answer. This is a self-declaration, not identity verification, and we do not present it as one.
- Setting the bar at 18 also settles the question that different countries answer differently. India's **DPDP Act, 2023**, for example, treats everyone under 18 as a child and requires *verifiable* parental consent to process their data. Awaaz does not offer a parental-consent flow, and does not need one: nobody under 18 is permitted to use the service.
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

## 12. Grievance Officer (India)

In accordance with **Rule 3(2) of the Information Technology (Intermediary Guidelines and Digital Media Ethics Code) Rules, 2021**, Awaaz publishes the name and contact details of its Grievance Officer. Any user may contact the Grievance Officer about content on Awaaz, a violation of these terms, or the handling of their personal data.

- **Grievance Officer:** Akshay Kapoor
- **Designation:** Grievance Officer, Awaaz
- **Email:** awaazappofficial@gmail.com
- **Address:** Radhey Shyam Park, Sahibabad, Ghaziabad, Uttar Pradesh 201005, India

**How complaints are handled:**

1. We **acknowledge** every complaint within **24 hours** of receipt.
2. We **dispose of** the complaint within **15 days** of receipt, and inform you of the outcome.
3. Complaints concerning content that exposes a person's private area, shows nudity or a sexual act, or is impersonatory in nature are actioned within **24 hours**, as required by Rule 3(2)(b).
4. Reports of **child sexual abuse or exploitation** are handled under our separate [Child Safety Standards](child-safety.md), which commit to acknowledgement within 24 hours and removal without delay.

When you write, please include your username, what you are complaining about (a link or a description of the post, plus the poster's username), and what outcome you are seeking. It helps us meet the timelines above.

---

## 13. Contact

For privacy questions, data subject requests, or breach reports:

- **Email:** awaazappofficial@gmail.com
- **Developer:** Awaaz
- **Response time:** within 30 days for standard requests; within 72 hours for breach reports.

To request deletion of your account without using the app, see [Account Deletion](delete-account.md).

---

*This policy is hosted publicly so that its version history is auditable. The canonical URL is linked from the Awaaz app ("Settings → Privacy Policy") and from the Google Play Store listing.*
