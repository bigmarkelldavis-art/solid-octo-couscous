# FM-1 Chop (PWA)

Chop audio into 16 pads and upload them to a Felucca user sample slot on the M-VAVE FM-1,
from a phone or computer. It is a web app that installs to your home screen and works offline.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app |
| `manifest.webmanifest` | Name, colors and icons for installing |
| `sw.js` | Caches the app so it opens offline |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` | App icons |

All files must stay in the same folder.

## What you need

- Android phone or tablet with Chrome (Edge also works), or a Windows / Mac / Linux computer with Chrome or Edge.
- The FM-1 running Felucca firmware.
- A USB cable. On a phone, use a USB-C OTG adapter or a cable that lets the phone act as the USB host.
- iPhone and iPad are not supported: Safari has no Web MIDI.

## 1. Put it online (GitHub Pages, free)

Installing as an app and Web MIDI both need an https address.

1. Sign in at github.com and create a new **public** repository, for example `fm1-chop`.
2. Click **Add file > Upload files**, drag in every file from this folder (not the folder itself), and click **Commit changes**.
3. Open the repository's **Settings > Pages**.
4. Under **Build and deployment**, set **Source** to **Deploy from a branch**, choose branch `main` and folder `/ (root)`, then **Save**.
5. Wait a minute or two. The page shows your address, which looks like `https://YOUR-USERNAME.github.io/fm1-chop/`.

Any other static host with https (Netlify, Cloudflare Pages) works the same way.

## 2. Install it on your phone

1. Open the address in Chrome on your Android phone.
2. Tap the **Install app** button at the top of the page. If it does not appear, open Chrome's menu (three dots) and choose **Install app** or **Add to Home screen**.
3. Open **FM-1 Chop** from your home screen. It runs full screen.

## 3. Send pads to the FM-1

1. Plug the FM-1 into the phone (OTG adapter) with Felucca running.
2. In the app, tap **Connect**. Allow the MIDI permission when Chrome asks, including the option to use system exclusive messages. If you pick the wrong port, choose Felucca in the port list that appears.
3. Tap **Read slots** to check the link. You should see USR1 to USR3 listed.
4. Tap **Load audio** and pick a file.
5. Place markers: tap the waveform to set the cursor, then **Add marker**. Drag a marker to move it. Or use **Equal slices** or **Auto chop**.
6. Tap pads to hear each chop. Keep the capacity bar under its limit (about 7.4 seconds in total).
7. Choose a slot and a name, then tap **Upload to slot** and confirm.
8. On the FM-1, select a SAMPLE track and set its SET to the slot you used (USR1, USR2 or USR3). Pad 1 plays the note shown on pad 1; the rest follow in order.

Uploading stops the transport and takes a few seconds. If it fails halfway, run Upload again.

## Updating the app

1. Change `index.html` and upload it to the repository again.
2. Open `sw.js` and change `fm1-chop-v1` to `fm1-chop-v2` (then v3, and so on), and upload that too. Without this, installed copies keep showing the old version.
3. Open the app twice to load the new version.

## Optional: make an APK

Once the app is hosted, you can wrap it as an Android APK. It stays a Chrome-based app, so Web MIDI keeps working.

1. Go to pwabuilder.com and enter your page's address.
2. Let it check the manifest, then choose the Android package.
3. Download the package and follow its steps to sign and install the APK.

The site's screens change over time, so follow what it shows. Do not use a plain WebView wrapper (Cordova, or Capacitor without a MIDI plugin): Android's WebView does not support Web MIDI, so uploads would not work.

## Troubleshooting

- **Connect says no MIDI output:** check the cable and OTG adapter, and make sure the FM-1 is running Felucca. Close other apps that may be using the port.
- **No MIDI permission prompt, or Web MIDI missing:** use Chrome or Edge, and open the app from the https address (not from a file in your downloads).
- **Pads play but notes do not match the keys:** change the octave on the FM-1, or change **First pad** and **Pad keys** in the app, then upload again.
- **Slot looks empty after an error:** upload again. The device empties the slot when an upload starts.

## Credits and license

The slot format and upload protocol come from Felucca by Leo Kuroshita (Hügelton Instruments),
which is GPL-3.0. The encoder in `index.html` follows `tools/sampleio.py` from that project, so keep this app
under GPL-3.0 as well if you share it.
