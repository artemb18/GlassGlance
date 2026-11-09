# ClassGlance

**Your class schedule at a glance.** A small, fast Android timetable app with resizable home-screen widgets that always show the lesson you are in and the one that comes next, with a live countdown.

- 🕘 **Now & next** – current lesson, time range, countdown, then the next lesson
- 🧩 **Widgets from 1×1 to 3×3** – every size in between (1×2, 2×1, 3×2 …), resizable where your launcher allows it
- 🌍 **8 languages** – English, Русский, Français, Deutsch, 简体中文, 한국어, Türkçe, العربية (with right-to-left layout)
- 🌙 **Light and dark theme** – follows the system
- 📦 **Move your schedule anywhere** – export/import as a `.json` file or as text (Telegram, clipboard)
- 🔒 **Fully offline** – no internet permission, no accounts, no ads, no analytics

## Install

1. Download the latest `ClassGlance-x.y.apk` from the [Releases](../../releases) page.
2. Open it on your phone and allow installing from this source when asked.
3. Open ClassGlance, add your lessons, then add a widget to the home screen.

Requires **Android 7.0 (API 24)** or newer.

**Updating:** install the new APK over the old one – your schedule and widgets are kept. This works as long as the new version is signed with the same key and has a higher version code (releases from this repository always are).

## Using the app

| What | How |
| --- | --- |
| Add a lesson | **Add lesson** → name, day, start and end time |
| Edit / delete | Tap a lesson |
| Add a widget | **Add widget to home screen** (choose a size), or long-press the home screen → Widgets → ClassGlance |
| Change language | ⚙ Settings → Language (English is used on first launch) |
| Move to another phone | ⚙ Settings → Save to file / Load from file / Send as text / Paste from clipboard |

A `.json` file received in Telegram or a file manager can also be opened directly with ClassGlance.

### Widget sizes

| Size | Shows |
| --- | --- |
| 1×1 | lesson name and countdown (yellow = in progress, dark = next lesson) |
| 1×2, 1×3 | now and next lesson; 1×3 adds two more lessons |
| 2×1, 3×1 | now on the left, next on the right |
| 2×2 | now with time range and countdown, plus the next lesson |
| 2×3, 3×3 | large current lesson, next lesson and three more |
| 3×2 | two columns: now / next and two more |

Widgets are updated exactly when a lesson starts or ends.

> **Xiaomi / HyperOS / MIUI:** to keep widgets exact, open *Settings → Apps → ClassGlance* and set battery usage to **No restrictions** and enable **Autostart**.

## Schedule file format

UTF-8 JSON, identical in every app language, easy to edit by hand:

```json
{"app":"classglance","version":1,"lessons":[
{"day":"Mon","start":"09:00","end":"10:00","name":"Mathematics"},
{"day":"Mon","start":"10:10","end":"11:00","name":"Physics"}
]}
```

On import `day` can also be a number (`1` = Monday … `7` = Sunday) or a full English name. Times may be written `9:00` or `9.00`. Lessons with a wrong day or time, an empty name, or that overlap another lesson are skipped, and the app tells you how many.

## Build from source

The project uses only the Android SDK (Java 8, no third-party libraries).

- **Android Studio / Gradle:** open the folder in Android Studio (JDK 17). The Gradle files are included for convenience; the release APKs themselves are built with `build.sh`.
- **Without Gradle:** `build.sh` (aapt2 + javac + dx + apksigner). The tools it needs are listed at the top of the script.

Source layout (`app/src/main/java/com/lessonwidget/app/`):

| File | Purpose |
| --- | --- |
| `MainActivity` | schedule screen and lesson editor |
| `SettingsActivity` | language and import/export |
| `LessonWidget`, `Widget1x1` … `Widget3x3` | widgets for every size and the alarm that refreshes them |
| `Schedule` | "now / next" logic and texts |
| `Transfer` | import and export |
| `Lang` | in-app language selection |
| `Store`, `Lesson` | storage and model |

The application id stays `com.lessonwidget.app` so that new versions install over older ones.

## Translations

All texts live in `app/src/main/res/values*/strings.xml` (`values/` is English). To fix a translation or add a language, edit or add a `values-xx/strings.xml` file, add the language to `Lang.java`, and open a pull request. Plural forms use Android `<plurals>`, so every language needs the plural categories of its own grammar.

## Privacy

ClassGlance stores your schedule only on your device. The only permissions are *receive boot completed* and *exact alarms* (to refresh the widget exactly on time).
