La Marzocco Linea Micra external dashboard


# Espresso Dashboard

A small web app for espresso machines that run Bluetooth, such as the La Marzocco Linea Micra, paired with a Bookoo Themis Mini scale. It runs in Chrome on Android and gives you an auto shot timer, live weight, flow, brew ratio, a shot history, a grinder-setting suggestion and a backflush reminder.

Unofficial. Not affiliated with La Marzocco or Bookoo.

## Inspiration

This project was inspired by **[Apollo 2](https://github.com/mlsorensen/Apollo2)** by mlsorensen, an open-source ESP32 firmware for a touchscreen controller that connects to the Linea Micra and to Bookoo scales over Bluetooth. Apollo 2 showed how the machine's Bluetooth service works, which made this web version possible. The Bluetooth identifiers and the token workflow come from that project's documentation. Thanks to its author and contributors.

If you want a dedicated hardware controller rather than a tablet, look at Apollo 2 first.

## What you need

- A La Marzocco Linea Micra (or a compatible machine) with Bluetooth.
- A Bookoo Themis Mini scale (optional, but needed for weight, timer and ratio).
- An Android tablet or phone with **Chrome** and Bluetooth Low Energy.
- The app served over **HTTPS** (for example from Netlify), because Web Bluetooth requires it.
- Your machine's Bluetooth token. Get it with the `lmtoken` tool from the Apollo 2 project. Keep it private.

## Installation

1. Open the app's HTTPS address in Chrome.
2. Tap the browser menu and choose **Install app** (or **Add to Home screen**).
3. Open it from the icon. It works offline once it has loaded.

## Using the app

### 1. Connect the machine
1. Tap **Token**, paste your token and tap **Save**. The token stays only in this browser.
2. Close any other app connected to the machine, because the Micra accepts one Bluetooth connection at a time.
3. Tap **Connect** in the *linea micra* panel and choose the machine.

You can then read the boiler temperatures and targets, adjust them (± 0.5 °C for brew, ± 1 °C for steam), power the machine on or to standby, and toggle steam.

### 2. Connect the scale
1. Turn on the Themis Mini and close any other app connected to it.
2. Tap **Connect** in the *scale* panel and choose the scale.
3. Tap **Tare** with the cup on the scale.

Live weight, battery and the flow graph appear.

### 3. Pull a shot
- Enter the **dose** in grams. The app remembers the last value.
- Optionally set **Alert at (g)**. When the weight reaches that number, the app beeps three times, vibrates if the device allows it, and turns the weight green. It alerts once per shot.
- Start the shot. The timer starts when the weight begins to rise and stops when the flow falls. The ratio (`1 : x`) updates during the shot and is corrected for the last drips after the stop.

Each finished shot goes to **History**, with the coffee name, dose, yield, ratio and time.

### 4. Track your coffees
Tap the coffee button at the top to open **Coffees**.

- Create a coffee with its name, roaster, notes, grinder, grind setting, dose, bag size, grams left and received date.
- Set a **target time** and a **target ratio** (the app starts at 30 s and 1 : 2) and a **grinder step** if you know it.
- **Save and use** selects the coffee and sets its dose.
- Each shot deducts its dose from the coffee's grams left. Edit the number if you need to correct it.

### 5. Grind suggestions
With a target time set, after each shot the app tells you whether the coffee ran slow, fast or on target, and suggests a grind change, for example *"try coarser (+0,2) → 2,6"*. The suggestion starts with a cautious estimate and becomes more accurate as it learns from your own shots with that coffee. **Apply setting** saves the suggested value. It's a guide, not a rule: dose, freshness and distribution also change the result.

### 6. Maintenance
Open **History**, set how many shots you want between backflushes and tap **Backflush done** after cleaning. A banner appears at the top when a backflush is due.

## Limitations

- The timer and the suggestions depend on the scale. Without it you won't get automatic timing or ratios.
- The app can't cut the shot automatically. The Micra doesn't report when the lever is pulled over Bluetooth, so the timer starts from the first weight change.
- It stores data in the browser. Clearing site data or switching browsers erases history and coffees.
- Only one device can hold the machine's Bluetooth connection at a time.
- Web Bluetooth works in Chrome on Android. Other browsers may not support it.

## Privacy

Nothing is sent to a server. Your token, history and coffees stay in the browser on your device.

## Credits and license

Built with help from Claude (Anthropic). The layout takes visual cues from the official La Marzocco app, but no code or assets are reused, and no logos are included.

Apollo 2 is a separate project by mlsorensen. Check its license before reusing its code.
