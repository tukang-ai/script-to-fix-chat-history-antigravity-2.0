# Antigravity 2.0 Chat History Restorer

[Indonesian]
Script Python ini dirancang untuk memulihkan riwayat chat (conversation history) yang hilang di **Antigravity IDE 2.0**. Script ini bekerja dengan memindai file `.pb` (protocol buffer) percakapan lokal Anda dan membangun kembali indeks pencarian di database `state.vscdb`.

[English]
This Python script is designed to recover lost chat/conversation history in **Antigravity IDE 2.0**. It works by scanning your local `.pb` (protocol buffer) conversation files and rebuilding the index in the `state.vscdb` database.

---

## ⚠️ PRASYARAT UTAMA / CRITICAL PREREQUISITE

### [ID] MATIKAN ANTIGRAVITY IDE SEPENUHNYA
**PENTING:** Anda **harus mematikan/menutup Antigravity IDE secara penuh** sebelum menjalankan script ini. 
Jika IDE sedang berjalan ketika script dijalankan:
1. IDE memegang kunci (lock) pada database `state.vscdb`.
2. Saat IDE ditutup nanti, data dari memori IDE (yang kosong/hilang) akan langsung menimpa (overwrite) database yang sudah kita perbaiki, membuat chat tetap hilang.

### [EN] CLOSE ANTIGRAVITY IDE COMPLETELY
**IMPORTANT:** You **must fully close/exit Antigravity IDE** before running this script.
If the IDE is running while the script executes:
1. The IDE locks the `state.vscdb` database.
2. When the IDE exits, it will overwrite the database with its current in-memory state (which is empty), immediately wiping out the restored index.

---

## 🛡️ Keamanan & Backup Otomatis / Safety & Automatic Backup

[Indonesian]
Script ini memiliki fitur keselamatan ganda:
1. **Pencadangan Database:** Sebelum memodifikasi database, script secara otomatis membuat duplikat file database asli dengan nama `state.vscdb.backup` di folder yang sama. Jika ada kendala, Anda tinggal mengganti nama file tersebut kembali ke `state.vscdb`.
2. **Tanpa Penghapusan:** Script tidak pernah memodifikasi atau menghapus file `.pb` chat asli Anda.

[English]
This script features double-safety protection:
1. **Database Backup:** Before making any modifications, the script automatically copies your active database file to `state.vscdb.backup` in the same directory. If any issues occur, you can restore your original state simply by renaming that backup file back to `state.vscdb`.
2. **No Deletion:** The script never modifies or deletes your original `.pb` conversation files.

---

## Cara Menjalankan / How to Run

### 1. Tutup Antigravity IDE / Exit the IDE
* **macOS:** Tekan `Cmd + Q` atau Force Quit jika perlu.
* **Windows/Linux:** Pilih `File > Exit` atau tutup jendela aplikasi sepenuhnya.

### 2. Jalankan Script / Run the Script
Buka Terminal (macOS/Linux) or Command Prompt / PowerShell (Windows), lalu jalankan perintah berikut:

```bash
python3 restore_antigravity_2.0.py
```

### 3. Hasil & Verifikasi / Result & Verification
Setelah sukses dijalankan, script akan menampilkan:
```text
Found X conversations on disk for Antigravity 2.0
💾 Database file successfully backed up to: .../state.vscdb.backup
Building final index...
Backup of trajectorySummaries value saved to: trajectorySummaries_backup_2.0.txt

==========================================================
SUCCESS! Rebuilt index with X conversations.
==========================================================
```
Buka kembali Antigravity IDE Anda, riwayat chat Anda seharusnya sudah kembali muncul di sidebar.

---

## Lokasi Path Data (Antigravity 2.0) / Data Path Locations
Script ini secara otomatis mendeteksi path berikut berdasarkan sistem operasi Anda:

* **macOS:**
  * DB: `~/Library/Application Support/Antigravity IDE/User/globalStorage/state.vscdb`
  * Chats: `~/.gemini/antigravity-ide/conversations`
* **Windows:**
  * DB: `%APPDATA%\Antigravity IDE\User\globalStorage\state.vscdb`
  * Chats: `%USERPROFILE%\.gemini\antigravity-ide\conversations`
* **Linux:**
  * DB: `~/.config/Antigravity IDE/User/globalStorage/state.vscdb`
  * Chats: `~/.gemini/antigravity-ide/conversations`
