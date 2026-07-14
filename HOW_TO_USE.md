# How to use Cashflow Monitor

Cashflow Monitor is a local, offline cashflow and bill-projection tracker, available as a
browser extension for **Chrome** and **Safari**. By default nothing you enter ever leaves
your device, unless you turn on the optional Google Drive sync feature yourself — see
`PRIVACY.md` for details.

## Installing

**Chrome** — install from the [Chrome Web Store](https://chromewebstore.google.com/detail/cashflow-monitor/pdjdpmadgjgkdoladhmgkbalagpghjof).
Open it from the toolbar icon or the Chrome side panel picker. Once open, the sidebar's
**Open in full tab** / **Open in side panel** link switches between the two at any time.

**Safari (macOS)** — download the latest `.dmg` from [GitHub Releases](https://github.com/abdoukm/cashflow-monitor/releases/latest),
open it, and drag "Cashflow Monitor" into your Applications folder. Launch it once (you
can quit it right after — this just registers the extension with Safari), then:
1. Safari → Settings → Extensions → enable **Cashflow Monitor Extension**.
2. Click its toolbar icon to open the app.

The app itself works the same on both — the sidebar on the left is always visible and
lets you jump between the pages described below.

## 1. Set up your accounts

Go to **Accounts** and add one entry per bank account, credit card, or cash account you
want to track.

- **Account type** — Checking, Savings, Credit Card, Loan, or Mortgage. For the three debt
  types (Credit Card, Loan, Mortgage), the balance tracks what you **owe** instead of what
  you have — charges/interest increase it, payments decrease it — and the fields relabel
  accordingly ("Starting balance owed", "Balance alert threshold" instead of "Low-balance
  warning threshold").
- **Starting balance** and **As of date** — the balance you actually had on that date.
  This is the anchor everything else projects forward from.
- **Low-balance warning threshold** (optional; a balance-**above**-this alert for debt
  accounts — naturally read as the credit limit for a Credit Card) — leave blank to only
  warn on actual overdrafts (or, for debt accounts, not warn at all).
- **Currency** — defaults to your Settings currency, but each account can be set to a
  different one (USD, CAD, EUR, GBP, AUD, CHF, JPY, EGP). A Transfer between two accounts
  in different currencies gets its own Exchange rate field (see below).
- **Color** — used for the account's icon badge throughout the app (Dashboard cards,
  account tags in the Ledger, etc).

**Credit Card accounts** additionally have: **APR for purchases** and **APR for cash
advances** (optional, %), a **Minimum payment** rule (a fixed dollar amount or a percent
of balance), and a **Statement closing date** (the day your billing cycle closes). These
feed the Dashboard's projected-balance estimate and the "Minimum payment" / "Full
statement balance" Transfer amount modes below.

**Loan and Mortgage accounts** additionally have: **Term** (years, informational),
**Annual Percentage Rate**, **Payment** (the regular installment amount), and **Extra
principal payment** (informational). These feed the Dashboard's projected-balance and
estimated-payoff-date, and the "Account's payment amount" Transfer amount mode.

All three debt types also have a **Payment frequency** (Monthly or Bi-weekly) and a
**Due date** — set these to unlock the "smart" due-date-relative Transfer options below
and the "Debt payment due soon" notification.

You can edit or delete an account later; deletion is blocked while any income, bill, or
transfer still references it (so you don't silently orphan scheduled entries).

## 2. Add your recurring money movements

- **Income sources** — paychecks, deposits, anything that adds money to an account.
- **Bills** — rent, subscriptions, loan payments, anything that takes money out.
- **Transfers** — moving money between two of your own accounts, or to/from an external
  account (leave "From" or "To" blank for an external inflow/outflow).

Each of these supports four recurrence types:

- **One time** — a single scheduled date.
- **Weekly** — every N weeks from the start date.
- **Monthly** — every N months, optionally pinned to a specific day of month (clamped to
  the end of shorter months).
- **X times per year** — a custom list of month/day anchor dates (e.g. quarterly taxes).

All three list pages (Income sources, Bills, Transfers) work the same way: add, edit, or
delete an entry, and the table shows its next-run recurrence description.

**Smart debt-payment transfers** — when a Transfer's "To" account is a Credit Card, Loan,
or Mortgage, two fields switch from fixed values to dynamic ones you can opt into:

- **Amount** can follow the account instead of a number you maintain by hand: "Minimum
  payment" or "Full statement balance" for a Credit Card, or "Account's payment amount"
  for a Loan/Mortgage. The real amount is recalculated fresh for each occurrence from the
  account's own fields (e.g. its minimum-payment rule), so it stays correct as your
  balance changes — no need to re-edit the transfer every month.
- **Date** can be set to "On the due date" or "N days before the due date" instead of a
  manual recurrence — derived from the account's own Due date and Payment frequency.

Both require the target account to have a Due date/relevant fields set (see Accounts
above). A Loan/Mortgage transfer also shows a live **Estimated payoff** date (or "Won't
pay off at this payment amount" if the payment doesn't cover accruing interest) right in
the form as you adjust amount/dates.

**Cross-currency transfers** — if the "From" and "To" accounts use different currencies,
an **Exchange rate** field appears (1 source-currency unit = ? destination-currency
units) along with a toggle to type the amount in either currency. Leave the rate blank
and it defaults to 1:1, which is very likely wrong — fill in a real rate for an accurate
conversion.

## 3. Dashboard

The Dashboard is your daily overview, with a **Balance as of** date picker at the top —
change it to see projected balances for any past or future date (as far back as the
earliest account's starting-balance date).

**Account balances** — each account tile shows two figures:
- **Available** — the balance including every scheduled transaction up to that date,
  cleared or not. This is what drives low-balance/overdraft warnings.
- **Cleared** — the balance including only transactions you've explicitly checked off as
  cleared in the Ledger (see below). Useful for tracking what's actually posted to your
  real bank balance versus what's merely scheduled.

Click anywhere on an account tile to jump straight to the **Ledger**, pre-filtered to
that account, with the date range set from the Dashboard's selected date out to three
months later.

**Transfer reminders** — upcoming one-time transfers that need you to actually go move
the money (this app doesn't move money for you). Click **Done** once you've made the
transfer in your bank/card app — this only dismisses it from the reminder list; the
transfer itself and its Ledger entries are untouched. **Edit** lets you adjust its date
or amount without dismissing it.

For a Credit Card, Loan, or Mortgage account, the tile also shows a **Next Close
Projected Balance** — an interest-aware estimate of what you'll owe at the next statement
close (Credit Card) or due date (Loan/Mortgage), factoring in APR and any scheduled
payments between now and then. Loan/Mortgage tiles additionally show an **Est. payoff**
date (or "Won't pay off" if the current payment doesn't cover accruing interest). Both are
purely informational estimates — nothing is ever written to the Ledger for them.

**Overdraft warnings** — every upcoming point where an account's Available balance dips
below $0 (overdraft) or below its warning threshold (low balance), across your whole
projection horizon — or, for a debt account, rises above its threshold ("Over limit" for
Credit Card, "Above threshold" for Loan/Mortgage). Click **Cover** on an overdraft to get
suggestions for which other account(s) can fund a transfer to bring it back down —
accepting a suggestion creates the covering transfer for you.

## 4. Ledger

The Ledger is the full, itemized list of every scheduled transaction, with a **From**/
**To** date range at the top (defaults to today → your projection horizon; From can go
as far back as the earliest account's starting-balance date).

- **Clear checkbox** — check off a transaction once it's actually posted/reconciled
  against your real bank statement. Cleared rows sort to the top of the table (then by
  date); unreconciled rows follow, sorted by date.
- **Balance column** — for an unreconciled row, shows the projected **Available**
  balance plus a smaller **Cleared** balance underneath. Once a row is checked off as
  cleared, the two necessarily agree, so it collapses to a single number.
- **Edit** — change just one occurrence's date or amount (e.g. rent went up one month
  only) without touching earlier or later occurrences of the same recurring item.
  **Reset to scheduled** undoes that, while leaving the Clear checkbox state untouched.
- **Cover** — same overdraft-coverage helper as the Dashboard, available on any
  currently-or-future overdrawn row.
- Filters along the header (date, description, type, account, amount, balance) narrow
  the table further; up to three filters can be active at once.

## 5. Settings

- **Projection horizon (months ahead)** — how far into the future the Ledger and
  Dashboard project by default.
- **Currency** — the default display currency (USD, CAD, EUR, GBP, AUD, CHF, JPY, EGP)
  for any account that doesn't set its own currency (see Accounts above).

### Backup (Export / Import)

Settings has an **Export data** / **Import data** pair:

- **Export data** downloads a JSON file with everything — accounts, income sources,
  bills, transfers, cleared/override status, and settings. Keep it somewhere safe as a
  backup, or use it to move your data to a new computer or browser profile.
- **Import data** picks a previously exported JSON file and restores it. Importing
  **replaces all current data** — you'll get a confirmation prompt showing exactly what
  it's about to overwrite before anything changes.

### Google Drive sync (optional)

By default nothing syncs anywhere — this is a single-browser-profile tool. If you'd
rather have your data follow you across devices or Chrome profiles automatically,
Settings has an **Enable Google Drive sync** checkbox (off by default; see `PRIVACY.md`
for exactly what this shares and when).

- **Enabling it** signs you in with your Google account and connects to a single file
  ("cashflow-monitor-data.json") in your Drive. If both this device and that file
  already have data, you'll get a prompt to choose **Use Drive's data** or **Upload this
  device's data** — whichever you don't pick gets overwritten, so read the counts in the
  prompt before choosing. If only one side has data, it's adopted automatically with no
  prompt.
- Once connected, every add/edit/delete is saved locally instantly (as always) and also
  pushed to the Drive file a moment later. Opening the app on any device with sync
  enabled pulls the latest copy from Drive automatically.
- **Sync now** forces an immediate sync instead of waiting for the next change.
- **Reconnect** appears if your Google sign-in has expired or been revoked — click it to
  sign in again. (Google's "Testing" publishing mode for unverified apps can require
  re-signing in roughly every 7 days; that's expected, not a bug.)
- **Disconnect** turns sync off. Nothing is deleted on either side — your local data
  stays as it is, and the Drive file is left untouched.

### Notifications (optional)

Settings has an **Enable notifications** checkbox (off by default). Once on, choose which
kinds you want as native browser notifications, each with its own toggle:

- **Bill due soon**
- **Low balance / overdraft / over-limit warning**
- **Debt payment due soon** (Credit Card / Loan / Mortgage)

**Days before due to notify** controls the shared lookahead for the bill/debt-payment
checks. **Send a test notification** fires one immediately so you can confirm your
browser/OS is letting them through. Everything runs on a background alarm entirely
on-device — see `PRIVACY.md` for details.

## Tips

- By default nothing syncs anywhere. If you switch computers or reinstall the extension
  (Chrome or Safari), your data doesn't come with you unless you've exported and
  re-imported it, or turned on Google Drive sync beforehand.
- Archiving vs. deleting: an account can't be deleted while referenced elsewhere, so
  clear out or reassign its incomes/bills/transfers first if you want it gone entirely.
- On Accounts, Bills, Income sources, and Transfers, clicking anywhere on a row opens it
  for editing (same as clicking its Edit button); clicking a different row switches to
  that one instead, and closing/switching away from unsaved changes asks first. Drag the
  bar between the table and the edit panel to resize how much space each gets.
