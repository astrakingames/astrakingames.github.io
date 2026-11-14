# Pepper Puff: Burger Chase — GitHub Pages legal update package (draft)

Prepared 12 November 2026 for `astrakingames/astrakingames.github.io`.

This ZIP contains only files to ADD/REPLACE in the repository root. It does not contain the pre-existing `/assets` and `/style.css` files, which must remain unchanged. Do not use the ZIP as a replacement for the entire repository.

## Files
- `index.html` — links to new legal pages
- `support/index.html` — deletion support and links
- `privacy/pepper-puff-burger-chase/index.html` — revised draft privacy notice
- `terms/pepper-puff-burger-chase/index.html` — new draft terms
- `delete-account/pepper-puff-burger-chase/index.html` — new email-based deletion pathway draft

## Before merging, production approval, or submitting to Google Play
1. Inspect the final signed game and complete SDK/network inventory. Confirm Google/Apple sign-in, Ads, Billing, and analytics configuration on each platform. Adjust privacy and Data safety answers consistently.
2. Deploy backend and test in-game Delete Account functionality, deletion of linked data/entitlements, staff processing of email requests, and whether purchase records must be retained.
3. Confirm the precise retained data categories, actual retention periods, the support response timeline, processor names, contact identity and legal entity details.
4. Confirm Families policies, parental safeguards, advertising and consent settings. Confirm HTTPS for all user-data transfers.
5. Have owner and appropriate counsel approve both policies, remove draft notices and robots noindex directives, set their real effective dates.
6. Merge on a dedicated branch/PR; do not overwrite unrelated files. Confirm the published Privacy, Terms, Support, and Deletion URLs resolve and have working navigation and email requests.
7. Enter the actual public deletion URL in Play Console Data safety only **after** the website and deletion process are operating. Add links in-game and in relevant store listing fields.

**Proposed deletion URL:** `https://astrakingames.github.io/delete-account/pepper-puff-burger-chase/` (NOT LIVE until merged and GitHub Pages publishes).

The generated pages intentionally show a draft warning and carry `noindex` until a review confirms actual app and backend behavior. They do not constitute legal advice or establish production compliance.

## Implementation review

- **Signed Android evidence.** The checksum matched the locally audited non-debuggable 0.24.9 (34) Internal testing AAB. It supports guest play and local saves with public accounts, purchases and ads disabled. Billing 9.1.0 is packaged with blank SKU and verifier configuration. The payload audit found no AdMob, UMP or Firebase Analytics. The 12 November store status report records a reported Internal testing rollout and six configured cosmetic products. Live Console status, Play-installed QA, the exact production AAB, and its full SDK and traffic audit need confirmation.
- **Purchase requirement.** Current Godot code checks for an Android account session and purchase binding before launching real billing and rechecks after the parental gate. Current PostgreSQL integration tests reject guest purchase verification and exercise authenticated binding with mocked providers. Older optional purchase-association notes describe an earlier flow. Verify an authenticated Play license purchase, denial for guests, restoration and refund on the intended build. Confirm which providers ship and exercise Apple auth and revocation if offered.
- **In-game deletion.** QA source implements the Account Settings control and authenticated DELETE endpoint. Local Google QA mode hides the deletion controls. Existing PostgreSQL integration coverage exercises the separate code-based form and its shared deletion transaction with mocked providers. Run the actual in-game flow on the intended build and check session invalidation, device data, store restoration and database results.
- **Public email deletion.** The website can compose a request without opening the game. The QA backend's separate form needs an in-app-issued code. Confirm the mailbox operator, identity verification without the app, staff access to execute deletion, completion notice and response timeline. Use a synthetic account to test delivery through fulfillment and processor-side deletion.
- **Retention.** QA removes provider identities, sessions, handoff codes, cloud saves and account entitlements. It clears the account reference on retained purchase rows containing proof hashes, product IDs, state and timestamps. It retains the deleted player ID and timestamps and a linked completion record. Local progress and store transaction history are separate. The reviewed implementation establishes neither the legal basis nor actual purge intervals for retained records. Confirm the schedule for the purchase ledger, deletion records, logs, backups and support messages, including procedures after backup restoration.
- **Release review.** Confirm the production backend and recipients, HTTPS traffic, Play Data safety, Ads and target audience declarations, Families safeguards, consent and mediation settings, legal entity, contact identity and owner and counsel approval. Set real effective dates only after approval. Verify links on the deployed site and in the app before entering them in Play Console. See [Google Play account deletion requirements](https://support.google.com/googleplay/android-developer/answer/13327111).
- **Website QA.** Chromium checks of the reviewed page layouts passed at 320, 390, 700, 768 and 1280 px. Navigation, internal links, assets and the game fragment resolved locally. External Google documentation links resolved. The email action check exercised the link and decoded recipient, subject and body. Mail delivery and account deletion fulfillment remain open.

Source references in the game project include `scripts/store/purchase_manager.gd`, `scripts/account/account_view.gd`, `backend-dotnet/src/PepperPuff.Api/Accounts.cs`, `backend-dotnet/src/PepperPuff.Api/Data/Database.cs` and `backend-dotnet/tests/PepperPuff.Api.Tests/Integration.cs`.

## Synthetic deletion verification

Status: blocked. This review has no confirmed synthetic release account, verified access to the actual support mailbox, or authorized operation for deleting that account through the intended backend. No request was sent and no account was deleted. The signed Internal testing build 0.24.9 (34) has public accounts and purchases disabled. Testing purchase authentication and in-game deletion requires the intended Android build with those features enabled and an authorized test environment.

The studio needs to identify the responsible mailbox operator and backend operator. For the synthetic test, record a request ID, timestamps for sending, receipt and completion, how ownership was verified without opening the game, who executed the authorized deletion, and sanitized before/after checks for the identity, sessions, saves, and entitlements. Confirm the requester receives the completion notice. For missing mail, failed verification or backend errors, keep the request pending, record the failure and notify the requester of the next step. Send a completion notice only after checking the backend outcome. These are proposed handling steps until the operators validate them.

| Records | Current evidence | Outstanding verification |
| --- | --- | --- |
| Deleted player record and linked completion entry | Retained by QA deletion | Legal basis, period and purge mechanism |
| Purchase verification rows and proof hashes | QA retains rows and clears the user reference | Legal basis, period and purge mechanism |
| Hosting and access logs | Production configuration unverified | Data recorded, legal basis, period and purge mechanism |
| Backups | Production handling unverified | Retention, expiry, access and reapplication of deletions after restore |
| Support email and deletion correspondence | Actual mailbox retention unverified | Responsible operator, legal basis, period and deletion procedure |
