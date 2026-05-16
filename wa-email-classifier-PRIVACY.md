# WA Classifier add-on — Privacy Policy

**Audience:** internal whitearrow.com users only. The add-on is published
as an "Internal" Workspace Marketplace app — it is not available to
anyone outside the whitearrow.com domain.

**Effective date:** 2026-05-16.

## What data the add-on touches

When you open an email in Gmail and the WA Classifier sidebar renders,
the add-on does two things:

1. **Reads metadata about the currently open message.** Specifically:
   - `messageId` and `threadId` — Gmail's internal identifiers
   - `inbox` — your own email address (`Session.getActiveUser().getEmail()`)

2. **Sends those identifiers + your Google ID token** over HTTPS to the
   WA Classifier bridge (a Google Cloud Function in the White Arrow GCP
   project). The bridge verifies that the token is valid and was issued
   to a `whitearrow.com` account, then forwards the lookup to White
   Arrow's internal classifier service.

The add-on does **not** read the body of any email. It does **not**
upload attachments. It does **not** make outbound calls to any host
outside the White Arrow GCP project.

## What data is stored

The classifier service stores per-message classification rows in White
Arrow's internal database for the following purposes:

- **Decisions table** — the classifier's verdict for each processed
  message (action, category, confidence, source). Used to render the
  add-on sidebar and to detect drift over time.
- **Corrections table** — when you click a "Correct" button in the
  sidebar, the chosen action + scope is written to this table so the
  classifier learns from your correction.
- **Audit log** — every write is associated with the actor's email
  address for accountability.

Storage is on White Arrow infrastructure. No data is shared with third
parties or used for training external models.

## Retention

Records are retained for the operational lifetime of the wa-email-
classifier service. There is no fixed expiry; records may be deleted
during routine database maintenance or upon employee separation.

## Access

Records are visible to:

- The employee whose inbox they reference
- White Arrow administrators with operational access to the classifier
  service

No external party has access.

## Contact

Questions: Chris Ceausu, cceausu@whitearrow.com.
