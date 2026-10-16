# المهند للصرافة والتحويلات — Android starter

A Kotlin + Jetpack Compose + Room starter project for an Arabic, RTL, offline-first Android application.

## Included in this first implementation
- Arabic RTL dashboard with royal navy/gold visual identity.
- Local Room/SQLite schema for currencies, customers, append-only ledger entries, transfers, and exchange rates.
- Initial currencies seeded on first launch: YER, SAR, USD. More currencies can be inserted through the DAO.
- Monetary arithmetic helper that avoids floating point and checks insufficient balances.
- Unit tests for the money arithmetic helper.
- No Internet permission declared; app is designed for local-only operation.

## Build
1. Install Android Studio with JDK 17 and Android SDK platform 35.
2. Open this directory as a project.
3. Allow Gradle sync to download dependencies.
4. Run the `app` configuration on an Android device/emulator (Android 8.0 / API 26 or newer).
5. For an APK: **Build > Build Bundle(s) / APK(s) > Build APK(s)**.

## Important limitations
This is the foundation, not a production-ready money-transfer system. The dashboard is a UI shell and feature cards are not yet connected to forms. Before real use, implement transactional posting rules, reversal workflows, proper balance/accounting model, PIN/password authentication, encrypted backup/export, restore tests, audit review, and comprehensive acceptance tests. Room database files are stored in app-private storage, but this alone is not a complete security or backup strategy.

## Data design notes
- Store monetary values as integer minor units (`Long`), never `Float` or `Double`.
- `ExchangeRateEntity` stores a rate scaled by 1,000,000; use a consistent scale and documented rounding policy.
- Ledger entries are intended to be append-only. Corrections should be new reversal entries, not edits/deletions.
- A production posting workflow must update related records atomically in a Room `withTransaction` block and enforce idempotency/unique references.
