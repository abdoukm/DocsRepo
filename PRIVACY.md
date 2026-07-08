# Privacy Policy — Cashflow Monitor

**Last updated:** 2026-07-08

Cashflow Monitor stores your data locally on your device by default. It also has an
optional, off-by-default Google Drive sync feature you must explicitly turn on in
Settings — until you do, the extension makes no network requests at all.

## What data the extension handles

Everything you enter — accounts, starting balances, income sources, bills, transfers,
recurrence rules, cleared/reconciled status, and app settings — is financial planning
data you type in yourself. None of it is auto-imported from any bank, card issuer, or
other service.

## Where your data is stored

All data is stored using the browser's built-in `chrome.storage.local` API, scoped to
your Chrome profile on your own device. Cashflow Monitor has no server or backend of its
own, and no login/account system beyond the optional Google sign-in used for Google
Drive sync (see below), which you control entirely.

## What the extension does NOT do

- By default, it does not transmit your data anywhere — no network requests are made
  unless you turn on Google Drive sync yourself (see below).
- It does not use analytics, telemetry, or crash reporting.
- It does not share data with any third party. Google Drive sync, when you enable it,
  talks only to Google's Drive API on your behalf, using your own Google account — the
  developer of this extension never sees your data.
- It does not use cookies or any cross-site tracking.

## Data retention and deletion

Your data persists in `chrome.storage.local` until you remove it yourself, either by
deleting individual items in the app or by uninstalling the extension (which clears its
local storage) or clearing the extension's site data from Chrome's settings.

## Syncing across devices

By default, Cashflow Monitor does not sync your data across devices or browser
profiles — data entered in one Chrome profile stays in that profile only. Settings has
an Export/Import feature so you can move your data to a new profile or device yourself,
or keep a backup — the exported file is a plain JSON file that stays wherever you save
it; it is not uploaded anywhere by the extension.

## Google Drive sync (optional, off by default)

Settings has an **Enable Google Drive sync** option. It is off by default and only does
anything once you explicitly turn it on and sign in with your Google account.

- **Scope requested:** `drive.file` — the narrowest Google Drive permission available.
  It only allows the extension to see and edit the one file it creates for itself
  ("cashflow-monitor-data.json" in your My Drive); it cannot see, list, or modify any
  other file in your Drive.
- **What data leaves your device, and when:** the same data as the manual Export feature
  — accounts, income sources, bills, transfers, cleared/override status, and settings —
  as JSON. It's sent to that one Drive file shortly after any add/edit/delete while sync
  is enabled, and read back from that file each time you open the app.
- **Why:** so the same data can follow you across devices or Chrome profiles without
  manually exporting and importing a backup file each time.
- **Turning it off:** disabling the toggle immediately stops all network activity. Your
  local data and the Drive file are both left exactly as they were — nothing is deleted.
- Cashflow Monitor's own developer has no access to this data; it goes directly from
  your browser to your Google Drive over Google's API.

## Changes to this policy

If this extension ever adds a feature that changes how data is handled, this policy will
be updated first and the change will be opt-in — as was done for Google Drive sync
above.

## Contact

This is a personal, independently developed extension. If you have questions about this
policy, reach out through the same channel you obtained the extension from.
