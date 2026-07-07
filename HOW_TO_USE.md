# Cashflow Monitor — How to Use

Cashflow Monitor is a local, offline Chrome extension that projects your account
balances forward in time based on your income, bills, and transfers, so you can see
upcoming low-balance and overdraft situations before they happen — and fix them.

All data stays on your device (see [PRIVACY.md](./PRIVACY.md)). Nothing is ever sent
anywhere.

## Getting started

1. Click the Cashflow Monitor icon in the Chrome toolbar to open the full dashboard in
   its own tab. You can also open it as a **side panel** (via Chrome's side panel picker)
   to keep it docked alongside another tab — both views share the same data live.
2. Start in the **Accounts** tab and add each account you want to track.
3. Add your **Income sources** and **Bills**, and any recurring **Transfers** between
   accounts.
4. Open **Dashboard** or **Ledger** to see the projection.

## Accounts

Each account needs:
- **Name**
- **Starting balance** and the **date** that balance is accurate as of
- An optional **low-balance warning threshold** — leave blank if you only want to be
  warned about actual overdrafts (below $0)
- A **color**, used as a small identity dot next to the account name throughout the app

Deleting an account is blocked if any income, bill, or transfer still references it —
you'll see exactly which items to update or remove first.

## Income sources & Bills

Both use the same form shape: a name, an amount, which account it hits, an effective
start date (and optional end date), and a **recurrence**:

- **One time** — a single occurrence on a specific date.
- **Weekly** — every N weeks, anchored to the effective start date's weekday.
- **Monthly** — every N months, on a chosen day of month. If a month is too short for
  that day (e.g. day 31 in February), the occurrence clamps to the last day of that
  month instead of skipping or rolling into the next month.
- **X times per year** — a list of specific month/day anchors (e.g. quarterly payments
  on Jan 15 / Apr 15 / Jul 15 / Oct 15), rather than evenly-spaced intervals — this
  matches how real recurring bills (insurance, property tax) actually fall on specific
  calendar dates.

Amounts are always entered as a positive number; income adds to the account, bills
subtract from it.

## Transfers

Transfers move money between two of your accounts on the same recurrence model as
income/bills. Leave **From account** blank to represent money arriving from outside the
app (an external deposit), or leave **To account** blank for money leaving the tracked
accounts entirely (an external payment) — at least one side is required.

## The Ledger

The Ledger is the full chronological list of every projected income, bill, and transfer
occurrence within your projection horizon (see Settings), with a running balance per
account.

- **Filter by column** — Date, Description, Type, Account, Amount, and Balance after
  each have their own filter control in the header row (up to 3 active at once). Amount
  and Balance filters accept operators like `>100` or `<=200`, or plain text.
  The header row stays frozen while you scroll.
- **Edit a single occurrence** — click **Edit** on any row to change just that
  occurrence's date or amount (e.g. "rent was $50 more this month," or "paycheck landed
  two days late"). This does **not** change the recurring rule — every other past and
  future occurrence in that series is unaffected. Edited rows show a small blue dot;
  use **Reset to scheduled** in the edit dialog to undo it.
- **Cover an overdraft** — any row where the running balance goes negative shows a red
  **Cover** button (see below).

## Dashboard

- **Balance as of** — pick any date to see each account's projected balance at that
  point in time.
- **Account cards** — one per account, flagged with a low-balance or overdraft badge
  when relevant to the selected date.
- **Upcoming one-time transfers** — a to-do list of every one-time transfer scheduled
  today or later (including ones you create via "Cover an overdraft," below). **Edit**
  opens it for changes; **Done** removes it once you've carried it out in real life.
- **Upcoming warnings** — every projected low-balance or overdraft point across the
  whole horizon, each with its own **Cover** button for overdrafts.

## Covering an overdraft

When an account is projected to go negative, click **Cover** (on a Ledger row, a
Dashboard account card, or a warnings-panel row). Cashflow Monitor checks every other
account's projected balance on that same date and suggests:

- **A single account** that can cover the full shortfall on its own, if one exists, or
- **A combination** of accounts (largest balance first) that together cover it, with
  a note if even all accounts combined can't fully cover the gap.

Clicking **Use this account** or **Apply this combination** creates real one-time
transfer(s) dated that day — they immediately show up in the Ledger, Transfers list,
and the Dashboard's to-do list, and the overdraft recalculates from there.

## Settings

- **Projection horizon** — how many months ahead (rolling from today) the Ledger and
  Dashboard project. Increase it to see further out; decrease it for a shorter, faster
  view.
- **Currency** — display currency for all amounts.

## Data & backup

Everything is stored locally via `chrome.storage.local`. There is currently no built-in
export/import — if you need to move data between machines, you'd need to do so via
Chrome's own profile sync or manual re-entry.
