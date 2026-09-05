# biziqoo — reusable core + health-clinic client

This package uses the supplied health-clinic ZIP as the source of truth for module names, existing Firebase collection/document names, templates and business logic.

## Architecture

`core/` is the reusable biziqoo UI foundation:
- fixed Inter font
- core design tokens
- header
- 250px desktop sidebar
- mobile bottom navigation
- responsive layout
- shared components
- source Firebase config/rules kept separately

`client/` contains the health-clinic implementation from the supplied source, including all module HTML files and assets.

## Exact source preservation

The original client files are preserved rather than silently renaming their Firebase collections or business fields. See `client/module-inventory.json` for the extracted Firestore collection names and document-number observations.

## Organisation identity

Client logo/name/organisation setup should ultimately be loaded from the client's `settings/company_profile` data after authentication. The core components should not contain a hardcoded clinic identity.

## Important source observations

- `patients` uses `patientId`; one creation flow generates `P` plus five random digits.
- `appointments` uses Firestore appointment document IDs and passes the ID as `appointmentId` when preparing invoices.
- `temp-invoice.html` supports `billNo` / `invoiceNo` and has an `INV-` timestamp fallback.
- `estimates` exists as a Firestore collection, but no universal estimate-number field was found in the supplied source.
- `transactions` is the common collection for transaction/payment/receipt/cash/bank flows; no universal transaction/receipt number field was found.
- Company profile is read from `settings/company_profile` in `company.html`; another appointment invoice flow reads `settings/company`.

## Firebase

The exact supplied Firebase configuration is retained in:
`core/js/services/firebase-config.source.js`

The supplied Firestore rules are retained in:
`core/firestore.rules`

Do not expose or reuse one client's Firebase project configuration for another client. Each deployed client should have its own approved Firebase project/configuration and rules.

## Assets

Client assets remain under:
`client/assets/`

Shared biziqoo core assets should be placed under:
`core/assets/`

For templates, seals, letterheads and similar documents, prefer central URLs/configuration or Firebase Storage references rather than duplicating hardcoded assets into every module.
