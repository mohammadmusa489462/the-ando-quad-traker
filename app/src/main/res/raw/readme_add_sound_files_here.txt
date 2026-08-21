=== Athan (full audio at each prayer time) ===
Add your own audio file(s) here (app/src/main/res/raw/) - looked up by
name at runtime, so nothing breaks if missing (falls back to a plain
notification automatically).

  - One file for every prayer:      athan.mp3
  - A different file per prayer:    athan_fajr.mp3, athan_dhuhr.mp3,
                                     athan_asr.mp3, athan_maghrib.mp3,
                                     athan_isha.mp3
    (useful since Fajr's athan traditionally has an extra phrase)
    Per-prayer files are checked first; athan.mp3 is the fallback for
    any prayer that doesn't have its own file.

A GENUINELY FREE, PUBLIC-DOMAIN-LICENSED SOURCE:
    https://archive.org/details/adhan.recordings.from.doha.qatar
    (marked "Public Domain Mark 1.0"). Has separate Fajr/Dhuhr/Asr/
    Maghrib/Isha recordings already, matching the naming above.

A WORD OF CAUTION: most other adhan audio online (including plenty on
Internet Archive itself) is uploaded by users without clear rights to
redistribute it, and recitations by named, famous reciters are personal
copyrighted performances even though the Quran/adhan text itself isn't
anyone's property. Stick to sources explicitly marked public-domain or
openly licensed.

=== Notification sounds - a distinct pair per prayer ===
Each prayer has TWO different notification sounds, for its two
different situations:

  1. "On track" sound - used both for the heads-up before this prayer
     starts AND the alert at its exact start time, but ONLY when the
     prayer before it was already marked done:
        notification_fajr.mp3      notification_dhuhr.mp3
        notification_asr.mp3       notification_maghrib.mp3
        notification_isha.mp3

  2. "About to be missed" sound - used when THIS prayer itself hasn't
     been marked done and its qada window is about to close (this
     covers both the moment the next prayer is about to begin, and the
     separate qada-reminder alert if you've turned that on):
        notification_fajr_missed.mp3      notification_dhuhr_missed.mp3
        notification_asr_missed.mp3       notification_maghrib_missed.mp3
        notification_isha_missed.mp3

Example: between Dhuhr and Asr, as Asr approaches -
  - if Dhuhr is marked done  -> plays notification_asr.mp3
  - if Dhuhr is NOT done yet -> plays notification_dhuhr_missed.mp3
  (i.e. the sound always names the prayer the alert is actually about)

All go in this same folder (app/src/main/res/raw/). Fallback order:
  - "on track" sounds:      its own file -> notification_sound.mp3 -> system default
  - "missed" sounds:        its own file -> notification_reminder.mp3 -> notification_sound.mp3 -> system default
Add as many or as few as you like - any combination works, and nothing
breaks if none of them exist.

  Shared fallback (used for any of the above that's missing):
                            notification_sound.mp3
  Shared fallback for any "missed" sound specifically:
                            notification_reminder.mp3

--- Filename rule for everything in this folder ---
Android resource files must be lowercase, letters/numbers/underscores
only - "Athan.MP3" or "athan-1.mp3" are NOT valid, "athan_1.mp3" is.

--- If you're changing sounds on an app you've already installed ---
Android locks a notification channel's sound once it's first created
on the device. If you add/change a sound file and reinstall but don't
hear the new sound, that's why - not a bug. Fully uninstalling the app
before reinstalling clears the old channels so the new sounds take
effect immediately.
