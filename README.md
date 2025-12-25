# Dokumentasi Project SA-MP Server

## 📋 Daftar Isi
1. [Gambaran Umum](#gambaran-umum)
2. [Struktur Project](#struktur-project)
3. [Instalasi & Setup](#instalasi--setup)
4. [Konfigurasi](#konfigurasi)
5. [Sistem Gamemode](#sistem-gamemode)
6. [Filterscripts](#filterscripts)
7. [Plugin](#plugin)
8. [Database](#database)
9. [NPC Modes](#npc-modes)
10. [Panduan Development](#panduan-development)
11. [Troubleshooting](#troubleshooting)

---

## 🎯 Gambaran Umum

Project ini adalah server SA-MP (San Andreas Multiplayer) berbasis roleplay dengan fitur-fitur lengkap termasuk sistem ekonomi, faction, kendaraan, properti, dan integrasi Discord.

### Teknologi yang Digunakan
- **Platform**: SA-MP 0.3.7 / 0.3DL
- **Bahasa**: Pawn
- **Database**: MySQL
- **Voice**: Sampvoice (Voice Over IP)

---

## 📁 Struktur Project

```
ARIPIN/
├── .vscode/              # Konfigurasi VS Code
├── database/             # File database
├── filterscripts/        # Script filter tambahan
│   ├── mapping/         # Map custom
│   │   ├── ext/
│   │   └── int/
│   └── voiceavtr/       # Sistem voice chat
├── gamemodes/           # Mode permainan utama
│   ├── core/            # Sistem inti
│   │   ├── account/
│   │   ├── activity/
│   │   ├── admin/
│   │   ├── anims/
│   │   ├── anticheat/
│   │   ├── ask/
│   │   ├── avtreasure/
│   │   ├── balloon/
│   │   ├── beanbag/
│   │   ├── carsteal/
│   │   ├── casino/
│   │   ├── clothes/
│   │   ├── cmds/
│   │   ├── crafting/
│   │   ├── damagelog/
│   │   ├── dealer_showroom/
│   │   ├── death_system/
│   │   ├── discord/
│   │   ├── DMV/
│   │   ├── donator/
│   │   ├── dynamic/
│   │   ├── event/
│   │   ├── factions/
│   │   ├── fader/
│   │   ├── family/
│   │   ├── fivem_notify/
│   │   ├── fuel_system/
│   │   ├── gangzone/
│   │   ├── gun/
│   │   ├── gym/
│   │   ├── inventory/
│   │   ├── inventory_old/
│   │   ├── invoice/
│   │   ├── jobs/
│   │   ├── modshop/
│   │   ├── phone_system/
│   │   ├── report/
│   │   ├── robbery_static/
│   │   ├── salary/
│   │   ├── stall/
│   │   ├── stuff/
│   │   ├── systems/
│   │   ├── tackle/
│   │   ├── taser/
│   │   ├── timers/
│   │   ├── toll/
│   │   ├── toys/
│   │   ├── user-interface/
│   │   ├── vehicles/
│   │   └── voice/
│   └── utils/           # Utility functions
└── include/             # Header files
└── logs/                # Log files
└── npcmodes/            # Mode NPC
    └── recordings/      # Rekaman NPC
└── pawno/               # Compiler Pawn
└── plugins/             # Plugin server
└── properties/          # File properti
    └── vehicles/        # Data kendaraan
└── scriptfiles/         # File skrip tambahan
    └── YSI/
```

---

## 🚀 Instalasi & Setup

### Prasyarat
- SA-MP Server 0.3.7 atau lebih baru
- MySQL Server 5.7+
- Compiler Pawn (sudah termasuk dalam folder `pawno/`)

### Langkah Instalasi

1. **Clone atau Extract Project**
   ```bash
   # Extract file project ke folder server
   ```

2. **Setup Database**
   - Buat database MySQL baru
   - Import file SQL dari folder `database/`
   - Edit konfigurasi database di `server.cfg`

3. **Konfigurasi Server**
   - Edit file `server.cfg`
   - Sesuaikan setting:
     - `hostname` - Nama server
     - `maxplayers` - Maksimal pemain
     - `port` - Port server (default: 7777)
     - `gamemode0` - Gamemode utama

4. **Compile Gamemode**
   - Buka `pawno/pawno.exe`
   - Buka file `gamemodes/main.pwn`
   - Tekan F5 untuk compile
   - File `main.amx` akan muncul di folder `gamemodes/`

5. **Jalankan Server**
   - Windows: `samp-server.exe`
   - Linux: `./samp03svr`

---

## ⚙️ Konfigurasi

### server.cfg
```ini
echo Executing Server Config...
lanmode 0
rcon_password [password_anda]
maxplayers 100
port 7777
hostname [Nama Server Anda]
gamemode0 main 1
filterscripts bone flint gl_messages gl_spawns
announce 1
chatlogging 1
weburl www.sa-mp.com
onfoot_rate 40
incar_rate 40
weapon_rate 40
stream_distance 300.0
stream_rate 1000
maxnpc 50
logtimeformat [%H:%M:%S]
```

### Database Connection
Edit koneksi MySQL di file `gmcore.inc`:
```pawn
#define MYSQL_HOST "localhost"
#define MYSQL_USER "root"
#define MYSQL_PASS "password"
#define MYSQL_DATA "database_name"
```

---

## 🎮 Sistem Gamemode

### Core Systems

#### 1. Account System (`account/`)
- Registrasi dan login pemain
- Manajemen data karakter
- Sistem level dan experience
- Statistik pemain

#### 2. Admin System (`admin/`)
- Command admin
- Moderasi server
- Panel administrasi
- Log aktivitas admin

#### 3. Faction System (`factions/`)
- LSPD (Police Department)
- LSMD (Medical Department)
- Government
- Criminal Organizations
- Sistem ranking dan duty

#### 4. Family System (`family/`)
- Pembuatan dan manajemen family
- Territory control
- Family wars
- Bank family

#### 5. Vehicle System (`vehicles/`)
- Ownership kendaraan
- Spawn dan parkir
- Modifikasi kendaraan
- Sistem bahan bakar (`fuel_system/`)

#### 6. Property System
File konfigurasi di `properties/`:
- `banks.txt` - Data bank
- `businesses.txt` - Bisnis
- `houses.txt` - Rumah
- `interiors.txt` - Interior custom

#### 7. Job System (`jobs/`)
- Trucker
- Taxi Driver
- Mechanic
- Farmer
- Dan lainnya

#### 8. Inventory System (`inventory/`)
- Sistem item
- Crafting system
- Trading antar pemain

#### 9. Phone System (`phone_system/`)
- Call dan SMS
- Kontak
- Aplikasi phone

#### 10. Discord Integration (`discord/`)
- Bot Discord
- Notifikasi in-game ke Discord
- Webhook integration

---

## 🎨 Filterscripts

### Mapping
Lokasi: `filterscripts/mapping/`

**Exterior Maps** (`ext/`):
- Map tambahan untuk area outdoor

**Interior Maps** (`int/`):
- Custom interior untuk bisnis, rumah, dll

### Voice System
Lokasi: `filterscripts/voiceavtr/`

Files:
- `cmds.pwn` - Command voice
- `funcs.pwn` - Functions voice
- `AC_Black_Diamond.amx` - Voice plugin
- `hotkeys.pwn` - Hotkey configuration
- `mainan.amx` - Voice animations

---

## 🔌 Plugin

Lokasi: `plugins/`

### Plugin List

1. **mysql.so/dll** - Database connector
2. **streamer.so/dll** - Object streaming
3. **sscanf.so/dll** - String scanner
4. **discord-connector.so/dll** - Discord integration
5. **FileManager.dll** - File operations
6. **crashdetect.so/dll** - Crash debugging
7. **gvar.so/dll** - Global variables
8. **pawn-memory.so/dll** - Memory management
9. **samp_bcrypt.so/dll** - Password hashing
10. **sampvoice.so/dll** - Voice chat
11. **SKY.so/dll** - Custom plugin
12. **textdraw-streamer.so/dll** - Textdraw optimization

### Loading Order
Edit di `server.cfg`:
```ini
plugins crashdetect mysql streamer sscanf FileManager discord-connector gvar pawn-memory samp_bcrypt sampvoice textdraw-streamer
```

---

## 💾 Database

### Tabel Utama

1. **accounts** - Data akun pemain
2. **characters** - Data karakter
3. **vehicles** - Kendaraan pemain
4. **houses** - Properti rumah
5. **businesses** - Bisnis
6. **factions** - Data faction
7. **bans** - Daftar banned player
8. **items** - Item inventory
9. **logs** - Activity logs

### Backup Database
```bash
mysqldump -u username -p database_name > backup.sql
```

---

## 🤖 NPC Modes

Lokasi: `npcmodes/recordings/`

### NPC Recordings
- `animtest1.rec` - Test animasi
- `at400_ls_to_lv_x1.rec` - Penerbangan pesawat
- `mission_1.rec` - NPC mission
- `ship.rec` - Kapal
- `train_ls_to_sf.rec` - Kereta api

### Setup NPC
1. Compile NPC mode di `npcmodes/`
2. Tambahkan di `server.cfg`:
```ini
maxnpc 10
```
3. Connect NPC via script

---

## 👨‍💻 Panduan Development

### Struktur Code

#### Include Order
```pawn
#include <a_samp>
#include <a_mysql>
#include <streamer>
#include <sscanf2>
// ... includes lainnya

// Defines
#define MAX_PLAYERS 100

// Enums
enum PlayerData {
    pID,
    pName[MAX_PLAYER_NAME],
    // ...
}

// Variables
new PlayerInfo[MAX_PLAYERS][PlayerData];

// Functions
forward LoadPlayer(playerid);
public LoadPlayer(playerid) {
    // code here
}
```

### Naming Convention
- **Variables**: `pVariableName`, `gVariableName`
- **Functions**: `FunctionName()`
- **Commands**: `CMD:commandname`
- **Callbacks**: `OnCallbackName()`

### Adding New Feature

1. **Buat folder baru** di `gamemodes/core/nama_fitur/`
2. **Buat file .pwn** untuk code
3. **Include di main.pwn**:
```pawn
#include "core/nama_fitur/file.pwn"
```
4. **Compile dan test**

### Command System
```pawn
CMD:mycommand(playerid, params[]) {
    if(PlayerInfo[playerid][pAdmin] < 1) 
        return SendClientMessage(playerid, -1, "No access");
    
    // Command code here
    return 1;
}
```

### Database Query Example
```pawn
// Load data
new query[256];
mysql_format(MySQL, query, sizeof(query), 
    "SELECT * FROM accounts WHERE Username = '%e'", 
    PlayerName(playerid));
mysql_tquery(MySQL, query, "OnPlayerLoad", "d", playerid);

// Save data
mysql_format(MySQL, query, sizeof(query), 
    "UPDATE accounts SET Money = %d WHERE ID = %d", 
    PlayerInfo[playerid][pMoney], 
    PlayerInfo[playerid][pID]);
mysql_tquery(MySQL, query);
```

---

## 🐛 Troubleshooting

### Server Tidak Start
- Check `server_log.txt`
- Pastikan semua plugin ada
- Check `server.cfg` configuration

### Crash saat Runtime
- Enable `crashdetect` plugin
- Check log di `logs/`
- Periksa script yang baru ditambahkan

### Database Connection Failed
- Verify MySQL service running
- Check username/password
- Verify database exists

### Plugin Load Failed
- Pastikan plugin compatible dengan server
- Check architecture (32-bit vs 64-bit)
- Linux: check file permissions

---

## 📝 Log Files

Lokasi: `logs/`

- `discord-connector.log` - Discord activity
- `mysql.log` - MySQL queries
- `errors.log` - Error logging
- `log-core.log` - Core system logs
- `warnings.log` - Warning messages
- `plugins/` - Plugin-specific logs

### Log Monitoring
```bash
# Linux
tail -f logs/log-core.log

# Windows - gunakan text editor dengan auto-refresh
```

---

## 🔐 Security Best Practices

1. **Password Hashing**
   - Gunakan bcrypt untuk password
   - Jangan simpan plaintext password

2. **SQL Injection Prevention**
   - Selalu gunakan `mysql_format` dengan `%e`
   - Validasi input user

3. **RCON Password**
   - Gunakan password kuat
   - Jangan share RCON password

4. **Admin Commands**
   - Log semua admin activities
   - Implement permission levels

---

## 📚 Resources

### Documentation
- [SA-MP Wiki](https://wiki.sa-mp.com)
- [SA-MP Forum](https://forum.sa-mp.com)
- [Pawn Language Guide](https://github.com/pawn-lang/pawn)

### Tools
- [Pawno Editor](https://github.com/pawn-lang/compiler)
- [Map Editor](https://github.com/Yursa/MED)
- [MySQL Workbench](https://www.mysql.com/products/workbench/)

---

## 🤝 Contributing

### Cara Berkontribusi
1. Fork project
2. Buat branch baru (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push ke branch (`git push origin feature/AmazingFeature`)
5. Buat Pull Request

### Code Review Checklist
- [ ] Code tested dan working
- [ ] No memory leaks
- [ ] Follow naming convention
- [ ] Documentation updated
- [ ] No SQL injection vulnerabilities

---

## 📞 Support

Untuk bantuan lebih lanjut:
- Buat issue di repository
- Hubungi team development
- Check forum SA-MP

---

## 📄 License

Project ini menggunakan lisensi sesuai dengan ketentuan SA-MP dan plugin yang digunakan.

---

**Terakhir diupdate**: Desember 2025
**Versi Dokumentasi**: 1.0
