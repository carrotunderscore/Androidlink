# DeckLink Android

Android Studio prototype for using an Android phone as a Bluetooth HID mouse for a Windows PC. It targets Android 9+ and uses `BluetoothHidDevice`; the Samsung Galaxy S21's Android versions meet the minimum API level, subject to the phone firmware exposing the Android HID Device profile.

## Open and run

1. Open this folder in Android Studio.
2. Let Gradle sync. Install Android SDK Platform 37 and Build Tools 36.0.0 if Android Studio asks for them. The project includes the Gradle 9.6 wrapper.
3. Select a Galaxy S21 connected by USB with Developer options and USB debugging enabled, then press Run.
4. On first launch, grant the nearby Bluetooth permissions and approve the visibility request if asked. DeckLink starts Bluetooth mode automatically when opened.
5. On Windows, open **Settings → Bluetooth & devices → Add device → Bluetooth**, then select the phone. DeckLink now displays the phone Bluetooth name in the app. Select that exact name in Windows.
6. Keep DeckLink open in the foreground while using it. The system unregisters a Bluetooth HID app when it is no longer foreground, by Android design.

If Android asks you to confirm a pairing code, confirm it on the phone. After Android reports the phone is paired, DeckLink asks Android to open the HID connection to that paired Windows host. Keep the app open until its status says it is connected. DeckLink starts Bluetooth mode when opened and tries the last connected/paired computer automatically; you can also tap **Återanslut parkopplad dator**. A paired device will not appear as a new device in Windows search; keep it in the paired list. If it still does not connect, choose **Connect** in Windows Bluetooth settings. Removing and pairing again should only be needed if the stored Windows pairing becomes invalid, such as after changing the HID device profile during development.

The main screen contains the touchpad, the connection indicator (tap it for Bluetooth controls), and **Öppna tangentbord**. Bluetooth controls, connect/disconnect, sensitivity, and manual **Scrolla upp**/**Scrolla ner** buttons are on the controls screen. The app applies Android system-bar insets so its controls stay clear of the status and navigation bars. Use the **Muskänslighet** slider to adjust pointer speed. The on-screen keyboard supports tap and hold, modifier shortcuts, Alt+Tab, and Backspace. Its text field sends supported basic Latin letters, numbers, spaces, and common punctuation; accented/non-Latin characters are not supported yet. Touchpad gestures: move with one finger, double-tap for left click, two-finger tap for right click, three-finger tap for middle click, two-finger swipe to scroll, and pinch to zoom using Ctrl+wheel. Zoom depends on the focused Windows app supporting Ctrl+wheel. Wi-Fi pairing and the DeckLink Windows server are not used for Bluetooth input.

## Build prerequisites and limits

- Android Studio with Android SDK Platform 37, Build Tools 36.0.0, and JDK 17 or newer (Android Studio's bundled JBR works).
- Windows needs Bluetooth support and must pair the phone as a Bluetooth input device.
- This is an unsigned prototype; it does not include an APK release pipeline or Play Store packaging.
- Bluetooth HID Device is an Android framework profile available from API 28. Android documents the profile registration and report sending APIs, but device firmware behavior can vary. Verify it on the actual Galaxy S21. If its firmware does not expose HID Device, the app reports that it could not open the profile.

Official references: [BluetoothHidDevice](https://developer.android.com/reference/android/bluetooth/BluetoothHidDevice), [BluetoothHidDeviceAppSdpSettings](https://developer.android.com/reference/android/bluetooth/BluetoothHidDeviceAppSdpSettings), [Android 12 Bluetooth permissions](https://developer.android.com/develop/connectivity/bluetooth/bt-permissions).
