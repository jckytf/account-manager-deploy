# Deployment Notes

## Build Info

**Date:** 2026-05-13  
**Build Size:** 284 KB (80.7 KB gzipped)  
**Status:** ✓ Production build ready

## What's Deployed

### New Feature: Benefits Tracker
- **Files Added:**
  - `src/services/benefitService.js` — Pure functions for benefit lifecycle (create, validate, auto-reset)
  - `src/hooks/useBenefitsData.js` — State management with localStorage key `financialBenefits`
  - `src/components/BenefitsModal.jsx` — Modal UI with grouped checklist, account picker, add/edit form

- **Files Modified:**
  - `src/components/account-manager/ui/AppHeader.jsx` — Added Benefits button (Gift icon)
  - `src/components/account-manager/FinancialAccountsApp.jsx` — Wired modal state and hook
  - `src/hooks/useDataPersistence.js` — Updated export/import to include `benefits` array
  - `src/components/account-manager/FilterControls.jsx` — Fixed import path (was `../config/`, now `../../config/`)

### Features
- ✓ Benefits grouped by timeframe (Monthly, Quarterly, Annually, One-time)
- ✓ Auto-reset logic: benefits reset when period rolls over (checked on modal open)
- ✓ Completion history with account snapshot (last 12 entries stored per benefit)
- ✓ Account picker with search and selected-to-top float
- ✓ Person name display in both picker dropdown and benefit list (separate pills)
- ✓ Import/export JSON support (`benefits` array serialized with accounts, notes, calendarDates)

### Sample Data
- **File:** `Docs/sampleJSON/financial_accounts_export - 2026-05-13T202400.679.json`
- **Contains:** 60 pre-configured benefits across active credit cards (Amex Plat, Gold, Hyatt, Marriott, IHG, CSR/CSP, United, BOA Premium, US Bank Altitude, Chase Freedom, Discover, Citi Costco, Ink Business, etc.)
- **Import via:** UI Import button to seed data for testing

## Testing Checklist

- [ ] Benefits button opens/closes modal with ESC and backdrop click
- [ ] Add a benefit: select accounts, name, description, timeframe, amount
- [ ] Monthly benefit: check it off, advance to next month, open modal → auto-resets, history logs prior period
- [ ] Account filter works in modal
- [ ] Search in account picker filters and floats selected to top
- [ ] Export JSON includes `benefits` array
- [ ] Import JSON with benefits loads correctly
- [ ] Lint check passes: `npm run lint`

## Known Issues

- Existing lint errors (pre-existing PropTypes and React import warnings across codebase — not in scope for this feature)

## Rollback

If needed: revert commits for new service, hook, modal, and the modifications to header/main app/persistence files. Delete `src/services/benefitService.js`, `src/hooks/useBenefitsData.js`, `src/components/BenefitsModal.jsx`.
