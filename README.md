# Spark Homes Repair Estimator

Mobile-first repair cost estimator for Spark Homes acquisition walkthroughs.

The app is a static Progressive Web App (PWA). It can be installed on Android and iPhone from a hosted HTTPS URL, then opened from the home screen like an app.

## What It Does

- Create and save multiple property estimates.
- Add or remove rooms and sections during a walkthrough.
- Select repair line items from the built-in Spark price list.
- Prepopulate unit cost and measurement from default pricing.
- Override unit cost or measurement per project.
- Add custom repair items.
- Attach photos to repair items.
- Use Deal Guard to calculate max allowable offer.
- Export a ZIP with Excel estimate data and photos.
- Save project data locally on the device.

## Files Required For Deployment

Deploy these files together:

```text
index.html
manifest.json
sw.js
Logo.png
favicon.png
icon-180.png
icon-192.png
icon-512.png
icon-maskable-512.png
```

No build step is required.

## Run Locally

From the project folder:

```powershell
cd E:\sparkgroup
python -m http.server 4173 --bind 0.0.0.0
```

Open on the computer:

```text
http://127.0.0.1:4173/index.html
```

Open on a phone connected to the same Wi-Fi:

```text
http://YOUR-PC-IP:4173/index.html
```

Example:

```text
http://192.168.0.76:4173/index.html
```

Local HTTP is good for layout and workflow testing. Full install/offline testing should be done from HTTPS.

## Install On Android

Use Chrome on Android.

1. Open the deployed HTTPS URL.
2. Tap the Chrome menu.
3. Tap `Install app` or `Add to Home screen`.
4. Name it `Spark Estimate`.
5. Open it from the Android home screen icon.

The app should open without the browser address bar after install.

## Install On iPhone

Use Safari on iPhone.

1. Open the deployed HTTPS URL in Safari.
2. Tap the Share button.
3. Tap `Add to Home Screen`.
4. Name it `Spark Estimate`.
5. Tap `Add`.
6. Open it from the iPhone home screen icon.

Use Safari for iPhone install testing. Chrome on iPhone does not install PWAs the same way.

## Offline Use

Offline mode requires the app to be installed from HTTPS.

Test offline behavior:

1. Open the HTTPS URL while online.
2. Install the app to the home screen.
3. Open the app once while online.
4. Create or open a project.
5. Turn on airplane mode.
6. Reopen the app from the home screen.

Expected offline behavior:

- App shell opens.
- Saved projects load.
- Repair selections remain available.
- Unit costs and measurements remain available.
- Deal Guard works from local data.
- Export works from local data.

Photos and project data are stored locally in the browser. Clearing site data or removing the app can remove saved projects.

## Basic Workflow

1. Tap `P` to create or switch projects.
2. Add rooms or sections as needed.
3. Open a repair group.
4. Select repair items.
5. Enter quantity.
6. Confirm or override unit cost.
7. Confirm or change measurement.
8. Add notes or photos if needed.
9. Review the running total.
10. Open `Deal Guard`.
11. Enter ARV, offer, target profit, holding cost, and risk buffer.
12. Export the ZIP when the walkthrough is complete.

## Deal Guard

Deal Guard helps the acquisition agent decide whether the offer still works after repairs.

It uses:

- ARV
- Repair total
- Risk buffer
- Holding and closing cost
- Target profit
- Offer price

It returns:

- Max allowable offer
- Deal status
- Critical scope warnings

## Export

Tap `Export ZIP`.

The ZIP contains:

- Excel estimate workbook
- Deal Guard sheet
- Attached photos

The Excel file includes room, group, item, unit, unit cost, quantity, line total, notes, and serial fields.

## Troubleshooting

If Android still shows an older version:

- Close the app.
- Remove the home-screen icon.
- Clear site data for the domain.
- Reinstall from the HTTPS URL.

If iPhone blocks local HTTP:

- Test from the deployed HTTPS URL.
- Or turn off HTTPS-only mode temporarily for local testing.

If the app does not load on a phone from the local server:

- Confirm phone and PC are on the same Wi-Fi.
- Bind the server to `0.0.0.0`.
- Use the PC Wi-Fi IP address.
- Allow Python through Windows Firewall on private networks.

## Tech Notes

- Static HTML, CSS, and JavaScript.
- No framework.
- No server required after deployment.
- PWA manifest included.
- Service worker included.
- Local project data uses `localStorage`.
- Pricing is embedded in the app from the provided price list.
