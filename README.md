# 8 Ways to Clear System Data on Your Mac

If you've ever opened your Mac's storage breakdown and found **System Data** quietly consuming 40, 60, or even 80 GB of your drive, you're not imagining things — and you're far from alone. This bloated category is one of the most common reasons Mac users run out of space, yet macOS gives you almost no built-in tools to manage it directly.

System Data can easily consume anywhere from **20 to 80 GB** on a typical Mac, and it tends to grow silently over months of normal use. Old caches, forgotten backups, log files, and leftover installers pile up behind the scenes without any warning. The result: a "Your disk is almost full" alert that seems to come out of nowhere.

This guide breaks down exactly what System Data contains and walks you through 8 practical methods to clear system data on Mac — all using built-in macOS tools and Terminal commands.

---

## Table of Contents

- [Quick Fix Summary](#quick-fix-summary)
- [What Is System Data on Mac?](#what-is-system-data-on-mac)
- [Why Is System Data So Large?](#why-is-system-data-so-large)
- [How to Clear System Data on Mac](#how-to-clear-system-data-on-mac)
  - [1. Delete Time Machine Local Snapshots](#1-delete-time-machine-local-snapshots)
  - [2. Remove Old iOS and iPhone Backups](#2-remove-old-ios-and-iphone-backups)
  - [3. Clear System Cache Files](#3-clear-system-cache-files)
  - [4. Delete DMG Installers and Disk Images](#4-delete-dmg-installers-and-disk-images)
  - [5. Remove Old macOS Installers](#5-remove-old-macos-installers)
  - [6. Clear Mail Attachments](#6-clear-mail-attachments)
  - [7. Delete Log Files](#7-delete-log-files)
  - [8. Update macOS](#8-update-macos)
- [FAQ](#faq)
- [Conclusion](#conclusion)

---

## Quick Fix Summary

| Fix | Brief Description |
| --- | --- |
| 1. Delete Time Machine snapshots | Remove local APFS snapshots via Terminal (5–20 GB) |
| 2. Remove old iOS/iPhone backups | Delete outdated device backups from Finder or Library (10–20 GB) |
| 3. Clear system cache files | Purge user and system-level cache folders (2–5 GB) |
| 4. Delete .DMG installers | Remove disk images from Downloads folder (1–5 GB) |
| 5. Remove old macOS installers | Delete leftover "Install macOS" apps from Applications (12+ GB each) |
| 6. Clear Mail attachments | Delete cached email attachment downloads (1–3 GB) |
| 7. Delete log files | Clean out system and user log directories (0.5–2 GB) |
| 8. Update macOS | Install the latest update to optimize storage and reclaim space |

---

## What Is System Data on Mac?

**System Data** is a catch-all storage category in macOS that contains files the operating system and your applications generate during normal use — but that don't fit neatly into categories like Apps, Photos, or Documents. It's essentially everything macOS considers "system overhead" that isn't the operating system itself (which gets its own **macOS** category in the storage bar).

If you've been using Macs for a while, you might remember this category under a different name. Before **macOS Monterey (12)**, it was simply labeled **"Other"** in the storage breakdown — an equally vague label. Starting with **macOS Ventura (13)**, Apple renamed it to **"System Data"** and also split some of its contents into a separate **"macOS"** category. The underlying files are largely the same; only the labeling changed.

Here's what typically lives inside System Data:

- **System and application caches** — temporary files that apps and macOS create for faster loading
- **Time Machine local snapshots** — APFS snapshots stored on your internal drive between backups
- **Old iOS/iPadOS backups** — device backups from when you sync an iPhone or iPad via Finder or iTunes
- **Log files** — system, application, and diagnostic logs that accumulate over time
- **Disk images (.dmg files)** — installer packages you downloaded but never deleted
- **macOS installers** — full installer apps left in your Applications folder after an upgrade
- **FileVault encryption files** — overhead from full-disk encryption
- **System temporary files** — swap files, sleep images, and other transient data
- **Mail attachment downloads** — cached attachments from the Mail app
- **Spotlight index data** — the search index macOS maintains for quick file lookups

**To check how much System Data you have:**

**On macOS Ventura (13), Sonoma (14), and Sequoia (15):**

1. Click the **Apple menu ()** in the top-left corner.
2. Select **About This Mac**.
3. Click **More Info** — this opens System Settings.
4. Scroll down and click **Storage Settings** (or go to **System Settings > General > Storage**).

**On macOS Monterey (12) and earlier:**

1. Click the **Apple menu ()**.
2. Select **About This Mac**.
3. Click the **Storage** tab.
4. Hover over the color-coded bar to see the **Other** (or **System**) category.

> **Tip:** The storage bar can take a minute to fully calculate after you open it. If the numbers look off, wait for the spinning indicator to finish before drawing conclusions.

The frustrating part is that macOS doesn't let you click on System Data to see what's inside or delete anything from this view. That's why you need the manual methods below.

---

## Why Is System Data So Large?

System Data tends to balloon over time for several compounding reasons. Understanding the root causes helps you target the right files and prevent the category from growing back immediately.

Common reasons your Mac's System Data is too large:

- **Time Machine is enabled but your backup drive isn't always connected** — macOS stores local snapshots on your internal SSD to protect recent changes; these can consume 5–20 GB or more depending on how long it's been since your last full backup.
- **You've backed up iPhones or iPads to your Mac** — a single device backup can be 10–20 GB, and old backups from devices you no longer own may still be sitting on your drive.
- **Caches haven't been cleared in months or years** — browsers, Xcode, Slack, Spotify, Adobe apps, and dozens of other applications accumulate gigabytes of cached data that macOS counts as System Data.
- **You download .dmg installers and never delete them** — every app you install from outside the App Store typically comes as a disk image that stays in your Downloads folder after you drag the app to Applications.
- **Old macOS installers are left in your Applications folder** — a single macOS installer ("Install macOS Sonoma," "Install macOS Ventura," etc.) takes up 12–13 GB.
- **Log files have been accumulating** — system diagnostic logs, crash reports, and app logs pile up in **/var/log**, **~/Library/Logs**, and **/Library/Logs**.
- **Mail downloads cached attachments** — the Mail app quietly caches attachments you've previewed, and these copies persist even after you delete the emails.
- **FileVault encryption is enabled** — FileVault creates encryption overhead files that show up under System Data.
- **Your macOS version is outdated** — Apple frequently includes storage optimizations in macOS updates that can reclaim space automatically.

In most cases, it's not a single culprit but a combination of several. The methods below address each of these causes individually, so you can work through them in order and reclaim the maximum amount of space.

---

## How to Clear System Data on Mac

Work through these methods in order — they're organized from the largest potential space savings to the smallest. Together, they can typically reclaim **30–60 GB** depending on how long it's been since you last cleaned up.

### 1. Delete Time Machine Local Snapshots

**Potential space reclaimed: 5–20 GB**

Time Machine doesn't just back up to an external drive. When your backup disk isn't connected, macOS automatically creates **local APFS snapshots** on your internal SSD. These snapshots preserve the state of your files at various points in time so you can recover recent changes even without your backup drive. The problem is that these snapshots can grow to consume 20 GB or more, and macOS is slow to delete them on its own — especially if you rarely connect your backup drive.

Local snapshots are one of the single biggest contributors to an inflated System Data category. If you have Time Machine enabled but don't back up regularly to an external disk, this is likely your largest source of hidden storage consumption.

**To list local snapshots:**

1. Open **Terminal** (search for it in Spotlight or find it in **Applications > Utilities**).
2. Run the following command:

<img width="1810" height="1163" alt="image" src="https://github.com/user-attachments/assets/d623f381-d8e3-41c9-b4ee-cf7db59405ff" />

```bash
tmutil listlocalsnapshots /
```

This will return a list of snapshots with timestamps, like:

```
com.apple.TimeMachine.2025-04-01-093042.local
com.apple.TimeMachine.2025-04-03-143512.local
```

**To delete a specific snapshot:**

```bash
sudo tmutil deletelocalsnapshots 2025-04-01-093042
```

Replace the date string with the actual timestamp from the list. You'll be prompted for your admin password.

**To delete all local snapshots at once:**

```bash
for snapshot in $(tmutil listlocalsnapshots / | awk -F'.' '{print $4}'); do sudo tmutil deletelocalsnapshots "$snapshot"; done
```

> **Important:** Deleting local snapshots is safe — it only removes the local copies, not your actual Time Machine backups on the external drive. However, you won't be able to restore files from these time points afterward unless you have a full external backup.

**To prevent snapshots from accumulating again**, you can disable local snapshots entirely:

```bash
sudo tmutil disablelocal
```

Note that this command works on older macOS versions. On newer APFS-based systems (Catalina and later), macOS manages snapshots more aggressively and will recreate them automatically. The most reliable long-term fix is to connect your Time Machine backup drive regularly so macOS purges the local snapshots on its own.

---

### 2. Remove Old iOS and iPhone Backups

**Potential space reclaimed: 10–20 GB per backup**

Every time you back up an iPhone or iPad to your Mac through Finder (or iTunes on older macOS versions), a full device backup is stored locally. These backups can range from **5 to 50 GB** depending on the device and how much data it contains. If you've owned multiple iPhones over the years, you may have several old backups sitting on your drive — from devices you've already sold, traded in, or replaced.

macOS counts these backups as System Data, and it never deletes them automatically.

**To check and remove backups on macOS Ventura and later:**

1. Connect your iPhone or iPad (or just proceed without connecting).
2. Open **System Settings > General > Storage**.
3. Click **iOS Files** (if the category appears) to see device backups.

<img width="1538" height="1188" alt="image" src="https://github.com/user-attachments/assets/d327f9bf-8890-471a-98cb-bbd588c7c5d7" />

**To remove backups manually via Finder (macOS Catalina and later):**

1. Open **Finder**.
2. Connect your iPhone or click any device in the sidebar.
3. Click **Manage Backups** in the General tab.
4. Select outdated backups and click **Delete Backup**.

**To remove backups directly from the file system:**

The backups are stored at:

**~/Library/Application Support/MobileSync/Backup/**

1. Open **Finder**.
2. Press **Shift + Command + G** and paste the path above.
3. You'll see folders with long alphanumeric names — each one is a device backup.
4. To identify which device a backup belongs to, look at the **Info.plist** file inside each folder — it contains the device name and last backup date.
5. Delete the folders for devices you no longer need.
6. **Empty the Trash** afterward to actually free the space.

> **Tip:** Before deleting any backup, make sure the device is backed up to **iCloud** or that you no longer need the data. Once you delete a local backup, it's gone permanently. You can check your iCloud backup status on your iPhone under **Settings > [Your Name] > iCloud > iCloud Backup**.

---

### 3. Clear System Cache Files

**Potential space reclaimed: 2–5 GB**

Caches are temporary files that apps and macOS create to speed up repeated operations — loading web pages, rendering thumbnails, indexing content, and more. Over time, these caches accumulate, become stale, and occupy significant space. macOS stores them in multiple locations, and they're a reliable contributor to System Data bloat.

There are three main cache directories on your Mac. The user-level cache is the safest to clean. The system-level caches require more care — delete only the contents of folders you recognize, not the top-level folders themselves.

**To clear user caches:**

1. Open **Finder**.
2. Press **Shift + Command + G** and type:

**~/Library/Caches**

3. Select all the folders inside (named after apps, like `com.apple.Safari`, `com.spotify.client`, `com.google.Chrome`).
4. Move them to the Trash.

**To clear system-level caches:**

1. Open **Finder**.
2. Press **Shift + Command + G** and type:

**/Library/Caches**

3. Delete the **contents** of individual app cache folders — do not delete the top-level folder names themselves.
4. You'll need to enter your admin password to modify some of these folders.

**To check the size of your caches before deleting:**

```bash
du -sh ~/Library/Caches
du -sh /Library/Caches
```

> **Important:** Clearing caches is safe, but expect a few things afterward: apps may take slightly longer to launch the first time (they'll rebuild their caches), and you may be logged out of some websites in Safari or Chrome. Critical system caches will be regenerated automatically by macOS.

> **Tip:** If you use **Xcode**, check **~/Library/Developer/Xcode/DerivedData** — this folder alone can consume 5–20 GB on development machines. You can delete its contents safely; Xcode will rebuild what it needs.

---

### 4. Delete DMG Installers and Disk Images

**Potential space reclaimed: 1–5 GB**

Whenever you install an app from outside the Mac App Store, you typically download a **.dmg** (disk image) file, open it, drag the app to Applications, and then — if you're like most people — forget the .dmg file exists. These disk images stay in your **Downloads** folder indefinitely and are counted as System Data in your storage breakdown.

A single .dmg file might be anywhere from 50 MB to 2 GB depending on the app. If you've installed dozens of apps over the life of your Mac, these add up quickly.

**To find and delete disk images:**

1. Open **Finder**.
2. Navigate to your **Downloads** folder (or press **Shift + Command + G** and type **~/Downloads**).
3. Click the **Search** icon or press **Command + F**.
4. Change the search scope to **"Downloads"** rather than "This Mac."
5. Click the **Kind** dropdown and select **Disk Image** (or type `.dmg` in the search bar).
6. Sort by **Size** to find the largest files first.
7. Select all the .dmg files you no longer need and move them to the Trash.

**Using Terminal to find all .dmg files on your Mac:**

```bash
find ~ -name "*.dmg" -size +100M 2>/dev/null
```

This finds all .dmg files larger than 100 MB in your home directory.

**To delete them directly:**

```bash
find ~/Downloads -name "*.dmg" -delete
```

> **Tip:** Also check for **.pkg** (package installer) files in your Downloads folder. These are another type of installer that lingers after installation and can take up significant space. You can search for them the same way: `find ~/Downloads -name "*.pkg" -size +50M`.

---

### 5. Remove Old macOS Installers

**Potential space reclaimed: 12+ GB per installer**

When you download a macOS update, the full installer app is saved to your **Applications** folder. After the update completes, macOS doesn't always clean up after itself — especially if you downloaded the installer manually from the App Store or using the `softwareupdate` command. Each macOS installer weighs in at **12 to 13 GB**, and if you've upgraded through multiple macOS versions, you could have two or three of these sitting in your Applications folder.

These installers are counted as System Data, and they serve no purpose once you've already upgraded.

**To check for old macOS installers:**

1. Open **Finder** and navigate to **Applications** (press **Shift + Command + G** and type **/Applications**).
2. Look for apps named:
   - **Install macOS Sequoia**
   - **Install macOS Sonoma**
   - **Install macOS Ventura**
   - **Install macOS Monterey**
   - (or any older version)
3. Right-click the installer and select **Move to Trash**.
4. Empty the Trash.

**Using Terminal:**

```bash
ls -lh /Applications/Install\ macOS*.app 2>/dev/null
```

If any results appear, delete them:

```bash
sudo rm -rf "/Applications/Install macOS Sonoma.app"
```

Replace the name with whichever installer you find.

> **Important:** If you intentionally keep a macOS installer for creating bootable USB drives or reinstalling on other Macs, move it to an external drive instead of keeping it on your startup disk. You can always re-download it from the App Store when needed.

---

### 6. Clear Mail Attachments

**Potential space reclaimed: 1–3 GB**

If you use Apple's built-in **Mail** app, it caches every attachment you've ever previewed or opened — even from emails you've already deleted. These cached downloads pile up at a hidden path and are counted as part of System Data. If you receive a lot of emails with PDFs, images, or document attachments, this folder can grow to several gigabytes over time.

**To find and clear Mail attachment downloads:**

1. Open **Finder**.
2. Press **Shift + Command + G** and type:

**~/Library/Containers/com.apple.mail/Data/Library/Mail Downloads**

3. Select all the files and folders inside.
4. Move them to the Trash.
5. Empty the Trash.

**To check the size first:**

```bash
du -sh ~/Library/Containers/com.apple.mail/Data/Library/Mail\ Downloads
```

Deleting these files does **not** delete the attachments from your actual emails. The original attachments remain on the mail server (if you use IMAP or Exchange) and will re-download if you open them again in Mail. You're only removing the local cached copies.

> **Tip:** If you want to prevent this folder from growing large again, go to **Mail > Settings > Accounts**, select your account, and set **Download Attachments** to **None** or **Recent** instead of **All**. This way, Mail will only download attachments when you explicitly click on them.

---

### 7. Delete Log Files

**Potential space reclaimed: 0.5–2 GB**

macOS and its applications generate log files constantly — system event logs, crash reports, diagnostic data, and app-specific logs. Under normal conditions, these files are small. But if an app is crashing frequently, or if your system has been running for a long time without a clean install, log files can accumulate into several gigabytes. They're scattered across three main locations on your Mac.

**Log file locations:**

- **/var/log** — system-level logs (Wi-Fi, kernel, installation, etc.)
- **~/Library/Logs** — user-level application logs
- **/Library/Logs** — system-wide application logs and diagnostic reports

**To check the total size of each:**

```bash
sudo du -sh /var/log
du -sh ~/Library/Logs
sudo du -sh /Library/Logs
```

**To clear user-level logs:**

1. Open **Finder**.
2. Press **Shift + Command + G** and type **~/Library/Logs**.
3. Select all files and folders inside.
4. Move them to the Trash.

**To clear system-level logs (requires admin privileges):**

```bash
sudo rm -rf /var/log/*.log
sudo rm -rf /var/log/*.gz
sudo rm -rf /Library/Logs/DiagnosticReports/*
```

> **Important:** Don't delete the **/var/log** directory itself — only its contents. macOS will recreate log files as needed. Also, if you're currently troubleshooting a system issue, keep the logs until you've resolved the problem — they contain diagnostic information that can be critical for debugging.

> **Tip:** You can use the **Console** app (found in **Applications > Utilities**) to browse log files before deleting them. This is useful if you want to check whether any app is generating an unusual amount of log data.

---

### 8. Update macOS

**Potential space reclaimed: varies (often 2–10 GB through optimization)**

This might sound counterintuitive — downloading an update to free space? — but macOS updates frequently include **storage optimizations** that reclaim space you can't recover any other way. Apple periodically refines how APFS manages snapshots, how caches are pruned, and how System Data is calculated. Some updates also consolidate or remove superseded system files from previous versions.

Beyond direct storage optimization, updating also ensures that known bugs related to storage reporting are fixed. There have been multiple cases in macOS Monterey and Ventura where System Data was reported incorrectly due to bugs that Apple later patched. If your System Data number looks unreasonably high (say, 100+ GB), an outdated macOS version could be misreporting it.

**To check for and install macOS updates:**

**On macOS Ventura and later:**

1. Open **System Settings**.
2. Go to **General > Software Update**.
3. If an update is available, click **Update Now** or **Upgrade Now**.

**On macOS Monterey and earlier:**

1. Open **System Preferences**.
2. Click **Software Update**.
3. Install any available updates.

**Using Terminal:**

```bash
softwareupdate --list
```

This shows all available updates. To install them:

```bash
sudo softwareupdate --install --all
```

> **Tip:** Before updating, make sure you have at least **15–20 GB of free space** for the update process. If you're already critically low on space, work through methods 1–7 above first to free up enough room. Also ensure you have a current backup — either Time Machine or a manual copy of your important files.

After updating and restarting, check your storage breakdown again. You may find that System Data has shrunk noticeably without any additional action on your part.

*Also read: [How to Free Up Space on Mac]()*

*Also read: [How to Speed Up Your MacBook]()*

---

## FAQ

### Should I Delete System Data on Mac?

Yes — but selectively. Not everything in System Data is junk. Some of it (like active caches and the Spotlight index) serves a purpose and will be regenerated automatically. But a significant portion — old backups, stale caches, forgotten installers, accumulated logs — is genuinely wasted space that you can safely remove. The methods in this guide target only the files that are safe to delete. As a general rule, if your System Data exceeds **15–20 GB**, there's almost certainly recoverable space inside it.

### Is It Safe to Remove Cache Files?

Yes, with one caveat. Deleting cache files from **~/Library/Caches** and **/Library/Caches** is safe in the sense that it won't corrupt your system or cause data loss. Apps and macOS will rebuild any caches they need. However, you may notice slightly slower app launches for the first session after clearing caches, and you'll be logged out of some websites. Avoid deleting caches from folders you don't recognize inside **/System/Library/Caches** — those are core macOS system caches and are better left alone.

### Why Does System Data Keep Growing Back?

System Data grows back because the files that comprise it are continuously generated during normal Mac use. Every time you browse the web, caches are written. Every time Time Machine runs, local snapshots are created. Every time an app logs an event, log files expand. This is normal behavior — the issue isn't that these files exist, but that they're never cleaned up automatically. The most effective long-term strategy is to clean your caches and logs every few months, connect your Time Machine drive regularly so local snapshots are purged, and delete .dmg installers immediately after installing apps.

### Can I Move System Data to an External Drive?

Not directly. System Data isn't a single folder you can relocate — it's an aggregate of files scattered across dozens of directories. You can't tell macOS to store its caches or logs on an external drive. However, you **can** move some of the largest contributors to an external drive: specifically, iOS device backups. In Finder, you can change the backup location for your iPhone to an external drive using a symbolic link (symlink). Beyond that, the best approach is simply to reduce System Data through the cleanup methods in this guide rather than trying to relocate it.

---

## Conclusion

System Data is one of the most opaque and frustrating storage categories on macOS. Apple gives it a vague name, hides its contents, and provides no built-in tool to manage it. But now that you know what's actually inside it — Time Machine snapshots, old device backups, stale caches, forgotten installers, and accumulated logs — you can target each component individually and reclaim significant storage.

For most Mac users, working through the eight methods above in order will recover anywhere from **20 to 60 GB** of space, depending on how long it's been since you last cleaned up. The biggest wins typically come from deleting Time Machine local snapshots and removing old iOS backups, but the cumulative effect of clearing caches, logs, disk images, and old installers adds up quickly.

Going forward, build a simple maintenance habit: clear your Downloads folder of .dmg files after every install, connect your Time Machine drive at least weekly so local snapshots are purged, and do a full System Data cleanup every three to six months. Your Mac will run faster, update more reliably, and stop surprising you with "disk full" warnings.
