# Asset linking strategy

Keep reusable UI assets relative to the application:
- `client/assets/logo.png`
- `client/assets/name.png`

For organisation-controlled templates, seals, letterheads and generated document artwork, store the URL/path in the organisation's Firebase profile/configuration, then render that value in templates. This allows each client to change its own artwork without modifying the shared core.

Recommended profile fields:
- logoUrl
- wordmarkUrl
- faviconUrl
- letterheadUrl
- sealUrl
- invoiceTemplateUrl
- receiptTemplateUrl

Only introduce these fields where the existing client data model permits it; do not overwrite existing Firestore fields without migration.
