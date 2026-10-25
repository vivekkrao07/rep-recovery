# Rep Recovery — iPhone-ready PWA

A mobile-first personal workout recovery dashboard designed to be hosted as a static website and added to the iPhone Home Screen.

## Features in this first version
- Ten muscle groups with estimated time-based recovery windows.
- Manual workout logging with date/time and muscle groups.
- Manual sleep, resting heart rate, and HRV check-ins.
- A cautious readiness estimate based on entered metrics and personal recent values.
- Recent activity list, delete controls, and JSON backup export.
- Installable/offline-capable PWA shell.
- No account and no external analytics. App data is stored in the browser's local storage on the device.

## Important limitations
- A website running in iPhone Safari cannot directly read Apple Health / HealthKit data. Noise REP measurements visible in Apple Health must be entered manually in this version, or imported through a separate supported workflow.
- Data stays in that browser on that device. Clearing Safari website data can remove it. Use **Export backup** periodically.
- The readiness score is a rough personal trend indicator, not a medical measure or a diagnosis.
- Recovery windows are editable in `index.html` under `MUSCLES`.

## Host on GitHub Pages
1. Create a new GitHub repository, e.g. `rep-recovery`.
2. Upload the contents of this folder (not the ZIP itself) to the repository root.
3. Open **Settings → Pages**.
4. Under Build and deployment, select **Deploy from a branch**, choose `main` and `/ (root)`, then Save.
5. Wait for GitHub Pages to publish the site. Your address will look like `https://YOUR-USERNAME.github.io/rep-recovery/`.

## Add to iPhone Home Screen
1. Open the published HTTPS address in **Safari** on your iPhone.
2. Tap **Share**.
3. Choose **Add to Home Screen**.
4. Name it `Rep Recovery`, then tap **Add**.

## Next step: Noise REP / Apple Health integration
For genuine automatic syncing, we need to decide on a supported data route. A normal PWA cannot access HealthKit directly. Options include manually entering values, exporting/importing files where supported, or using a secure backend endpoint fed by a Shortcut. Do not expose private tokens or health data in a public repository.


## Cloudflare API sync
This version includes **Upload device data** and **Load cloud data** buttons connected to:
`https://rep-recovery-api.vivekraosm2005.workers.dev`

- Upload sends the workouts and health check-ins currently saved in this browser to the Worker.
- Load fetches the latest 100 API records and merges recognized workout/health records into this browser.
- Sync is manual; it does not automatically read Apple Health or Hevy.
- The Worker is currently configured without authentication for testing. Anyone who knows the endpoint can read/write records while that remains the case. Do not upload real/private health data until you choose to secure it.
- Apple Health still requires a supported iPhone Shortcut workflow; the website cannot directly access HealthKit from Safari.
