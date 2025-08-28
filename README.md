# Sakuware
Sakuware โปรแกรมสำหรับ ซ่อม แฟลชไดรฟ์ ที่ติดไวรัส พัฒนาโดย NodeJs 

You are an AI coding assistant. Please generate a complete Electron + Node.js project that can be packaged into Windows (.exe), macOS (.dmg/.pkg), and Linux (.AppImage/.deb) desktop applications.

App Name: Saku USB Repair  
App Logo: Place a modern flat logo in `assets/logo.png`. Use it as the app icon and in the UI header.  

Description: A bilingual (English + Thai) modern desktop app to scan and repair virus-infected USB flash drives. The app must detect connected USB drives, allow scanning, show infected files, and offer actions (quarantine, delete, repair autorun/hidden attributes). It must also show drive status clearly.

---

### Version & Auto Update
1. Store the current app version in `package.json`.  
2. On startup, fetch `https://raw.githubusercontent.com/<your-username>/<your-repo>/main/api.txt`.  
   - `api.txt` contains a single line: the latest version (e.g. `1.0.3`).  
3. Compare local app version with the version in `api.txt`.  
   - If different, notify the user and trigger auto-update.  
   - Use `electron-updater` for handling update downloads and installation.  
4. Auto-update must support Windows, macOS, and Linux.  
   - For Windows: build `.exe` installer.  
   - For macOS: build `.dmg` or `.pkg`.  
   - For Linux: build `.AppImage` or `.deb`.  

---

### Functional Requirements
1. **Drive Detection**  
   - Use `drivelist` to list connected drives.  
   - Use `usb-detection` to detect attach/detach events.  
   - Show drive letter, size, name, free space.  

2. **Virus Scan**  
   - Integrate with ClamAV via Node wrapper (`clamscan` or `clamdjs`).  
   - Provide a **mock scanner mode** for development.  
   - Show infected/suspicious files in a results table.  

3. **Repair Actions**  
   - Quarantine: move file to `quarantine/`.  
   - Delete: remove infected file (with confirmation).  
   - Repair: remove autorun.inf, restore hidden attributes.  

4. **Drive Status Indicators**  
   - Safe / Infected / Scanning / Quarantined / Repaired / Error.  
   - Show as colored labels and icons.  
   - Log results to `repair-log.txt` on the USB and in the app logs.  

5. **Languages**  
   - English + Thai via JSON (`locales/en.json`, `locales/th.json`).  
   - Toggle button to switch language.  

6. **UI/UX**  
   - Modern responsive design (Tailwind).  
   - Header: Logo + “Saku USB Repair”.  
   - Progress bar for scanning.  
   - Toast notifications for scan complete, errors, updates.  

7. **Security**  
   - Confirm before deleting files.  
   - Show warning: “Please backup your files before repair.”  
   - Log all actions with timestamp.  

---

### Deliverables
- `package.json` with dependencies: `electron`, `electron-builder`, `electron-updater`, `drivelist`, `usb-detection`, `clamscan`, `tailwindcss`, `i18n`.  
- `main.js` (Electron main process with auto-update code).  
- `preload.js` for secure IPC.  
- `renderer/` with Tailwind UI.  
- `assets/logo.png` placeholder.  
- `locales/en.json` and `locales/th.json`.  
- Example version check + update logic (using `electron-updater` and fetching from GitHub `api.txt`).  
- `README.md` bilingual (Thai/English): instructions for dev, mock mode, packaging for Windows/Mac/Linux, and how to set up `api.txt` in GitHub for updates.  

---

### Safety Constraints
- Do not upload or exfiltrate user files.  
- Always log and confirm destructive actions.  

Please generate a working prototype with all the above features, including auto-update via GitHub `api.txt`.

