# CadiVault

**A free, open-source, offline tracker for subscriptions, bills and recurring costs.**
Made by Cadi Media in Ghana. It has no account, no server and no tracking. Your data stays on your device.

CadiVault is a single `index.html` file. You can open it in any browser, or package it as an Android app with [Capacitor](https://capacitorjs.com).

## Features

- **Every billing cycle.** Weekly, bi-weekly, monthly, quarterly, yearly or every N days. Month-end dates are handled correctly: a plan due on Jan 31 renews on Feb 28, then Mar 31.
- **Several currencies.** GHS, USD, EUR, GBP and NGN, with exchange rates you set yourself, since the app is offline.
- **Monthly or annual totals.** Switch the KPI cards, category chart and plan list between the two.
- **Four charts.**
  - **Categories:** spend by category.
  - **Next 12 months:** the cash due in each coming month.
  - **Paid:** what was actually paid in each of the last 12 months.
  - **Plans:** your plans ranked by cost.
- **Business or personal.** Tag each plan, flag it as tax-deductible, and filter everything by Business or Personal.
- **Monthly budget.** Months that go over the budget are flagged in the charts.
- **Payment history.** "Mark Paid" logs each payment with that day's exchange rate, so changing rates later does not rewrite past costs.
- **Reminders.** Phone notifications before each renewal (Android app), or an `.ics` file to import into any calendar app.
- **Calendar view** of renewals, with a total for each day and each month.
- **Exports.** A subscriptions CSV and a payment-history CSV (both open in Excel or Sheets), plus a JSON backup and restore. In the Android app, exports are saved to `Documents/CadiVault`.
- **Safety nets.** Undo for Mark Paid and Delete, dark and light themes, and the Android back button closes open sheets.

## Use it in a browser

Download `index.html` and open it. Everything is saved in that browser's local storage, so export a backup from time to time.

## Build the Android app (Capacitor 8)

You need Node.js 22 or newer and the Android SDK.

```bash
npm init -y
npm install @capacitor/core @capacitor/cli @capacitor/android
npm install @capacitor/app @capacitor/filesystem @capacitor/share @capacitor/local-notifications
npx cap init "CadiVault" "com.yourname.cadivault" --web-dir www
mkdir -p www && cp index.html www/
npx cap add android
npx cap sync android
npx cap open android        # then build the APK in Android Studio
```

What each plugin does in CadiVault:

| Plugin | Used for |
|---|---|
| `@capacitor/app` | The hardware Back button closes open sheets |
| `@capacitor/filesystem` | Saving exports to `Documents/CadiVault` |
| `@capacitor/share` | The Share button after an export |
| `@capacitor/local-notifications` | Renewal reminders |

The app still runs if any of these are missing. The feature that needs it shows a message explaining why it is unavailable.

> **Keep your app ID once people have installed it.** Android stores the app's data under that ID. A build with a different ID installs as a separate app and starts empty.

After you change `index.html`, copy it into `www/` again and run `npx cap sync android` before rebuilding.

## Your data

- Data is stored in the WebView's local storage on the device. Nothing is sent anywhere.
- The JSON backup is plain, **unencrypted** text, so keep it somewhere private.
- Calendar exports leave out account details and notes, because calendars often sync to the cloud.

## Contributing

Issues and pull requests are welcome. The app is one self-contained HTML file with no build step and no external dependencies.

## License

[MIT](LICENSE) © 2026 Cadi Media
