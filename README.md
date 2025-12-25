# Dokumentasi Lengkap Gamemode SA-MP Server

## 📋 Daftar Isi
1. [Struktur Gamemode](#struktur-gamemode)
2. [System Core - Detail per Modul](#system-core---detail-per-modul)
3. [Panduan Variables & Functions](#panduan-variables--functions)
4. [Flow Pemrograman](#flow-pemrograman)
5. [Integrasi Antar System](#integrasi-antar-system)

---

## 📁 Struktur Gamemode

```
gamemodes/
├── core/                    # Sistem inti server
│   ├── account/            # ✅ Sistem akun & autentikasi
│   ├── activity/           # ✅ Sistem aktivitas pemain
│   ├── admin/              # ✅ Sistem administrasi
│   ├── anims/              # ✅ Sistem animasi
│   ├── anticheat/          # ✅ Sistem anti-cheat
│   ├── ask/                # ✅ Sistem pertanyaan newbie
│   ├── avtreasure/         # ✅ Event treasure hunt
│   ├── balloon/            # ✅ Sistem balon
│   ├── beanbag/            # ✅ Sistem beanbag (stun)
│   ├── carsteal/           # ✅ Sistem pencurian mobil
│   ├── casino/             # ✅ Sistem casino
│   ├── clothes/            # ✅ Sistem pakaian
│   ├── cmds/               # ✅ Command system
│   ├── crafting/           # ✅ Sistem crafting
│   ├── damagelog/          # ✅ Log damage pemain
│   ├── dealer_showroom/    # ✅ Dealer kendaraan
│   ├── death_system/       # ✅ Sistem kematian
│   ├── discord/            # ✅ Integrasi Discord
│   ├── DMV/                # ✅ Department of Motor Vehicles
│   ├── donator/            # ✅ Sistem donasi
│   ├── dynamic/            # ✅ Objek dinamis
│   ├── event/              # ✅ Event system
│   ├── factions/           # ✅ Sistem faction
│   ├── fader/              # ✅ Screen fader
│   ├── family/             # ✅ Sistem family/gang
│   ├── fivem_notify/       # ✅ Notifikasi style FiveM
│   ├── fuel_system/        # ✅ Sistem bahan bakar
│   ├── gangzone/           # ✅ Territory gangzone
│   ├── gun/                # ✅ Sistem senjata
│   ├── gym/                # ✅ Sistem gym/latihan
│   ├── inventory/          # ✅ Sistem inventory
│   ├── inventory_old/      # 📦 Backup inventory lama
│   ├── invoice/            # ✅ Sistem tagihan
│   ├── jobs/               # ✅ Sistem pekerjaan
│   ├── modshop/            # ✅ Workshop modifikasi
│   ├── phone_system/       # ✅ Sistem telepon
│   ├── report/             # ✅ Sistem report
│   ├── robbery_static/     # ✅ Perampokan statis
│   ├── salary/             # ✅ Sistem gaji
│   ├── stall/              # ✅ Sistem lapak/stand
│   ├── stuff/              # ✅ Utilities umum
│   ├── systems/            # ✅ Sistem global
│   ├── tackle/             # ✅ Sistem tackle
│   ├── taser/              # ✅ Sistem taser
│   ├── timers/             # ✅ Global timers
│   ├── toll/               # ✅ Sistem tol
│   ├── toys/               # ✅ Sistem toy/aksesoris
│   ├── user-interface/     # ✅ UI components
│   ├── vehicles/           # ✅ Sistem kendaraan
│   └── voice/              # ✅ Sistem voice chat
├── utils/                   # Utility functions
│   ├── utils_colours.inc   # Definisi warna
│   ├── utils_defines.inc   # Definisi global
│   ├── utils_variables.inc # Variable global
│   ├── utils_vehicles.inc  # Utilities kendaraan
│   └── utils.inc          # General utilities
├── gmcore.inc              # Core gamemode include
├── main.amx                # Compiled gamemode
└── main.pwn                # File gamemode utama
```

---

## 🎯 System Core - Detail per Modul

### 1. 👤 Account System (`account/`)

**File Structure:**
```
account/
├── account_assign.inc      # Assignment data
├── account_registr.inc     # Registrasi
├── account_update.inc      # Update data
└── account.inc            # Main account
```

**Variables Location:**
- **Global Variables**: `account.inc`
```pawn
enum PlayerAccountData {
    pID,                    // ID Database
    pName[MAX_PLAYER_NAME], // Nama pemain
    pPassword[129],         // Password (bcrypt)
    pEmail[64],            // Email
    pRegDate[32],          // Tanggal registrasi
    pLastLogin[32],        // Login terakhir
    pLevel,                // Level pemain
    pExp,                  // Experience
    pMoney,                // Uang di tangan
    pBank,                 // Uang di bank
    pGender,               // Gender (1=Male, 2=Female)
    pAge,                  // Umur
    pSkin,                 // ID Skin
    Float:pHealth,         // Health
    Float:pArmour,         // Armour
    pAdmin,                // Level admin
    pHelper,               // Level helper
    // ... dst
}
new PlayerInfo[MAX_PLAYERS][PlayerAccountData];
```

**Functions Location:**

**`account.inc`** - Main functions:
```pawn
// Core account functions
stock ResetPlayerAccount(playerid)
stock SavePlayerAccount(playerid)
stock LoadPlayerAccount(playerid)
stock IsPlayerLoggedIn(playerid)
stock GetPlayerAccountID(playerid)
```

**`account_registr.inc`** - Registration:
```pawn
// Registration dialog handlers
ShowRegisterDialog(playerid)
OnPlayerRegister(playerid, password[])
ValidateEmail(email[])
ValidatePassword(password[])
```

**`account_update.inc`** - Update functions:
```pawn
// Update specific data
UpdatePlayerMoney(playerid, amount)
UpdatePlayerLevel(playerid)
UpdatePlayerBank(playerid, amount)
GivePlayerScore(playerid, score)
```

**`account_assign.inc`** - Data assignment:
```pawn
// Assign default data
AssignDefaultStats(playerid)
AssignDefaultSpawn(playerid)
ResetPlayerVariables(playerid)
```

**Usage Flow:**
```
1. Player Connect -> ShowRegisterDialog()
2. Input Data -> OnPlayerRegister()
3. Create Account -> SavePlayerAccount()
4. Load Data -> LoadPlayerAccount()
5. Spawn -> AssignDefaultSpawn()
```

---

### 2. 🎮 Activity System (`activity/`)

**File Structure:**
```
activity/
├── fishing/          # Sistem mancing
├── forklift/         # Pekerjaan forklift
├── hunting/          # Berburu
├── mowing/           # Memotong rumput
├── pizzadelivery/    # Delivery pizza
├── sweeper/          # Penyapu jalan
├── trashcollector/   # Pengumpul sampah
└── activity.inc      # Main activity
```

**Variables Location:** (dalam masing-masing folder)

**`fishing/`**:
```pawn
enum FishingData {
    fishingActive,      // Status fishing
    fishingTimer,       // Timer ID
    fishingBait,        // Jumlah umpan
    Float:fishPosX,     // Posisi X
    Float:fishPosY,     // Posisi Y
    Float:fishPosZ      // Posisi Z
}
new PlayerFishing[MAX_PLAYERS][FishingData];

// Fishing spots
new Float:FishingSpots[][] = {
    {2099.5, -108.5, 2.4},  // Santa Maria Beach
    {-2187.9, -226.9, 35.3}, // Ocean Docks
    // ... dst
};
```

**Functions:**
```pawn
// fishing.inc
CMD:fishing(playerid, params[])
StartFishing(playerid)
StopFishing(playerid)
OnPlayerCatchFish(playerid)
ProcessFishing(playerid)  // Timer callback
```

**`forklift/`**:
```pawn
enum ForkliftJob {
    forkliftVehicle,    // Vehicle ID
    forkliftCheckpoint, // Checkpoint ID
    forkliftBoxes,      // Jumlah box
    forkliftPay         // Pembayaran
}
new PlayerForklift[MAX_PLAYERS][ForkliftJob];
```

---

### 3. 👮 Admin System (`admin/`)

**File Structure:**
```
admin/
├── admin_functions.inc    # Fungsi admin utama
├── admin_lv1.inc         # Command level 1
├── admin_lv2.inc         # Command level 2
├── admin_lv3.inc         # Command level 3
├── admin_lv4.inc         # Command level 4
├── admin.inc             # Main include
├── executive.inc         # Executive commands
├── manager.inc           # Manager commands
└── steward.inc          # Steward commands
```

**Admin Levels:**
```pawn
// Defined in utils_defines.inc
#define ADMIN_LEVEL_1    1  // Moderator
#define ADMIN_LEVEL_2    2  // Admin
#define ADMIN_LEVEL_3    3  // Senior Admin
#define ADMIN_LEVEL_4    4  // Head Admin
#define ADMIN_LEVEL_5    5  // Executive
#define ADMIN_LEVEL_6    6  // Manager
#define ADMIN_LEVEL_7    7  // Owner
```

**Variables Location: `admin_functions.inc`**
```pawn
enum AdminData {
    adminDuty,           // Status duty
    adminWarnings,       // Jumlah warning
    adminJail,          // Status jail admin
    adminMuted,         // Status mute
    adminFrozen,        // Status freeze
    adminSpec,          // Status spectate
    adminSpecID,        // ID yang di-spec
    adminCloaked,       // Invisible mode
    adminGodMode,       // God mode
    adminVehicle        // Vehicle spawned
}
new AdminInfo[MAX_PLAYERS][AdminData];

// Admin log
enum AdminLogData {
    logID,
    logAdmin[MAX_PLAYER_NAME],
    logAction[128],
    logTarget[MAX_PLAYER_NAME],
    logDate[32]
}
```

**Functions by Level:**

**`admin_lv1.inc`** - Moderator:
```pawn
CMD:kick(playerid, params[])        // Kick player
CMD:warn(playerid, params[])        // Beri warning
CMD:mute(playerid, params[])        // Mute player
CMD:unmute(playerid, params[])      // Unmute
CMD:spec(playerid, params[])        // Spectate
CMD:specoff(playerid, params[])     // Stop spectate
CMD:goto(playerid, params[])        // Teleport ke player
CMD:gethere(playerid, params[])     // Bawa player
CMD:aduty(playerid, params[])       // Admin duty
```

**`admin_lv2.inc`** - Admin:
```pawn
CMD:ban(playerid, params[])         // Ban player
CMD:unban(playerid, params[])       // Unban
CMD:kick(playerid, params[])        // Kick with reason
CMD:jail(playerid, params[])        // Jail player
CMD:unjail(playerid, params[])      // Unjail
CMD:freeze(playerid, params[])      // Freeze player
CMD:unfreeze(playerid, params[])    // Unfreeze
CMD:slap(playerid, params[])        // Slap player
CMD:explode(playerid, params[])     // Explode player
CMD:sethp(playerid, params[])       // Set health
CMD:setarmour(playerid, params[])   // Set armour
CMD:givegun(playerid, params[])     // Give weapon
CMD:setlevel(playerid, params[])    // Set level
```

**`admin_lv3.inc`** - Senior Admin:
```pawn
CMD:setmoney(playerid, params[])    // Set money
CMD:givemoney(playerid, params[])   // Give money
CMD:setstat(playerid, params[])     // Set statistik
CMD:respawncar(playerid, params[])  // Respawn semua mobil
CMD:veh(playerid, params[])         // Spawn vehicle
CMD:dv(playerid, params[])          // Delete vehicle
CMD:setvw(playerid, params[])       // Set virtual world
CMD:setint(playerid, params[])      // Set interior
```

**`admin_lv4.inc`** - Head Admin:
```pawn
CMD:setadmin(playerid, params[])    // Set admin level
CMD:givedonator(playerid, params[]) // Give donator
CMD:makeleader(playerid, params[])  // Set faction leader
CMD:gotols(playerid, params[])      // Teleport LS
CMD:gotosf(playerid, params[])      // Teleport SF
CMD:gotolv(playerid, params[])      // Teleport LV
CMD:gotocoord(playerid, params[])   // Teleport koordinat
```

**`executive.inc`** - Executive:
```pawn
CMD:gmx(playerid, params[])         // Restart gamemode
CMD:restart(playerid, params[])     // Restart server
CMD:agivelicense(playerid, params[]) // Give license
CMD:createfaction(playerid, params[]) // Create faction
CMD:deletefaction(playerid, params[]) // Delete faction
```

**Functions: `admin_functions.inc`**
```pawn
// Core admin functions
stock IsPlayerAdmin(playerid, level)
stock GetAdminLevelName(level)
stock SendAdminMessage(color, const message[])
stock SendAdminCommand(playerid, command[])
stock LogAdminAction(playerid, action[], target[])
stock ShowAdminPanel(playerid)

// Admin features
stock ToggleAdminDuty(playerid)
stock AdminSpectate(playerid, targetid)
stock AdminFreezePlayer(playerid, targetid)
stock AdminJailPlayer(playerid, targetid, time)
```

---

### 4. 💃 Animations System (`anims/`)

**File Structure:**
```
anims/
├── anims_cmds.inc     # Command animasi
└── anims.inc          # Definisi animasi
```

**Variables Location: `anims.inc`**
```pawn
enum AnimData {
    animID,             // ID Animasi
    animLib[32],        // Library animasi
    animName[32],       // Nama animasi
    Float:animSpeed,    // Kecepatan
    animLoop,           // Loop status
    animFreeze          // Freeze on finish
}

// Daftar animasi
new AnimList[][AnimData] = {
    {1, "DANCING", "dance_loop", 4.0, 1, 0},
    {2, "DANCING", "DAN_Down_A", 4.0, 1, 0},
    {3, "DANCING", "DAN_Left_A", 4.0, 1, 0},
    {4, "DANCING", "DAN_Loop_A", 4.0, 1, 0},
    {5, "SMOKING", "M_smklean_loop", 4.0, 1, 0},
    {6, "CARRY", "crry_prtial", 4.0, 0, 1},
    {7, "COP_AMBIENT", "Coplook_loop", 4.0, 1, 0},
    {8, "DEALER", "DEALER_IDLE", 4.0, 1, 0},
    {9, "CRACK", "crckdeth2", 4.0, 0, 1},
    {10, "GRAVEYARD", "mrnF_loop", 4.0, 1, 0},
    // ... dst total 50+ animasi
};

// Player animation state
enum PlayerAnimData {
    playerAnimActive,
    playerAnimID,
    playerAnimTimer
}
new PlayerAnim[MAX_PLAYERS][PlayerAnimData];
```

**Functions: `anims_cmds.inc`**
```pawn
// Animation commands
CMD:animlist(playerid, params[])    // Daftar animasi
CMD:anim(playerid, params[])        // Play animasi
CMD:stopanim(playerid, params[])    // Stop animasi

// Core functions
stock PlayPlayerAnim(playerid, animid)
stock StopPlayerAnim(playerid)
stock GetAnimationName(animid)
stock ShowAnimationList(playerid, page)
```

---

### 5. 🛡️ Anti-Cheat System (`anticheat/`)

**File Structure:**
```
anticheat/
├── anticheat.inc      # Main anti-cheat
├── ac_log.inc        # Logging system
└── ddos.inc          # DDoS protection
```

**Variables Location: `anticheat.inc`**
```pawn
enum AntiCheatData {
    // Money cheat detection
    acLastMoney,
    acMoneyWarnings,
    
    // Weapon cheat detection  
    acWeapons[13],           // Senjata yang valid
    acAmmo[13],              // Ammo yang valid
    acWeaponWarnings,
    
    // Health/Armour cheat
    Float:acLastHealth,
    Float:acLastArmour,
    acHealthWarnings,
    
    // Teleport/Position cheat
    Float:acLastPosX,
    Float:acLastPosY,
    Float:acLastPosZ,
    acTPWarnings,
    
    // Speed cheat
    acSpeedWarnings,
    acLastSpeed,
    
    // Airbreak detection
    acAirbreakWarnings,
    
    // Vehicle cheat
    acVehicleWarnings,
    
    // Rapid fire
    acLastShot,
    acRapidFireWarnings,
    
    // Timers
    acCheckTimer,
    acUpdateTimer
}
new AntiCheat[MAX_PLAYERS][AntiCheatData];

// Detection settings
#define AC_MAX_WARNINGS          3      // Max warning sebelum kick
#define AC_CHECK_INTERVAL        1000   // Check setiap 1 detik
#define AC_MONEY_TOLERANCE       1000   // Toleransi money
#define AC_SPEED_LIMIT          280     // Max speed
#define AC_TELEPORT_DISTANCE    50.0    // Max teleport distance
#define AC_RAPID_FIRE_TIME      100     // Min time between shots (ms)
```

**Functions:**
```pawn
// Main functions
stock InitAntiCheat(playerid)
stock AntiCheatCheck(playerid)
stock ResetACWarnings(playerid)
stock ACKickPlayer(playerid, reason[])

// Money cheat detection
stock CheckMoneyCheat(playerid)
stock ValidateMoney(playerid, amount)

// Weapon cheat detection
stock CheckWeaponCheat(playerid)
stock GiveValidWeapon(playerid, weaponid, ammo)
stock ResetPlayerWeaponsAC(playerid)

// Position/Teleport cheat
stock CheckTeleportCheat(playerid)
stock UpdatePlayerPosAC(playerid)

// Speed cheat detection
stock CheckSpeedCheat(playerid)
stock GetPlayerSpeed(playerid)

// Health/Armour cheat
stock CheckHealthArmourCheat(playerid)

// Airbreak detection
stock CheckAirbreak(playerid)

// Vehicle cheat
stock CheckVehicleCheat(playerid)

// Callbacks
forward OnPlayerCheatDetected(playerid, cheattype, warnings);
public OnPlayerCheatDetected(playerid, cheattype, warnings) {
    // Handle cheat detection
    new string[144];
    format(string, sizeof(string), "** AC ** %s detected using %s (Warning: %d/%d)", 
        GetPlayerNameEx(playerid), GetCheatName(cheattype), warnings, AC_MAX_WARNINGS);
    SendAdminMessage(COLOR_RED, string);
    
    if(warnings >= AC_MAX_WARNINGS) {
        ACKickPlayer(playerid, GetCheatName(cheattype));
    }
}
```

**Cheat Types:**
```pawn
#define CHEAT_MONEY         0
#define CHEAT_WEAPON        1
#define CHEAT_HEALTH        2
#define CHEAT_ARMOUR        3
#define CHEAT_TELEPORT      4
#define CHEAT_SPEED         5
#define CHEAT_AIRBREAK      6
#define CHEAT_VEHICLE       7
#define CHEAT_RAPID_FIRE    8
```

---

### 6. ❓ Ask System (`ask/`)

**File Structure:**
```
ask/
├── ask_cmds.inc       # Commands
├── ask_functions.inc  # Functions
└── ask.inc           # Main
```

**Variables Location: `ask.inc`**
```pawn
enum AskData {
    askCooldown,        // Cooldown timer
    askMuted,          // Status mute
    askMessages        // Jumlah pesan hari ini
}
new PlayerAsk[MAX_PLAYERS][AskData];

// Ask system config
#define ASK_COOLDOWN        60      // 60 detik cooldown
#define ASK_MAX_MESSAGES    10      // Max 10 pesan per hari
#define ASK_LEVEL_REQUIRED  3       // Min level 3
#define ASK_COLOR           0x33CCFFAA
```

**Functions: `ask_functions.inc`**
```pawn
stock CanUseAsk(playerid)
stock SendAskMessage(playerid, message[])
stock ResetAskCooldown(playerid)
stock MutePlayerAsk(playerid, time)
stock UnmutePlayerAsk(playerid)
stock GetAskMessages(playerid)
```

**Commands: `ask_cmds.inc`**
```pawn
CMD:ask(playerid, params[])         // Tanya ke helper
CMD:ans(playerid, params[])         // Jawab (helper only)
CMD:togask(playerid, params[])      // Toggle ask channel
CMD:mutask(playerid, params[])      // Mute ask (admin)
```

---

### 7. 🏴‍☠️ Faction System (`factions/`)

**File Structure:**
```
factions/
├── factions_automax/         # Automax dealership
├── factions_bengkel/         # Workshop
├── factions_ems/             # EMS/Medic
├── factions_fox11/           # News
├── factions_handover/        # Handover system
├── factions_pemerintah/      # Government
├── factions_pinkytiger/      # Business
├── factions_polisi/          # Police (LSPD)
├── factions_putriinc/        # Business
├── factions_srimersing/      # Business
├── factions_texas/           # Gang
├── factions_uber/            # Uber/Taxi
└── factions.inc             # Main faction
```

**Variables Location: `factions.inc`**
```pawn
enum FactionData {
    factionID,              // ID Faction
    factionName[64],        // Nama faction
    factionType,            // Tipe (1=LEO, 2=Medical, 3=Gov, 4=Gang)
    factionColor,           // Warna faction
    factionMembers,         // Jumlah member
    factionMaxMembers,      // Max member
    Float:factionSpawnX,    // Spawn X
    Float:factionSpawnY,    // Spawn Y
    Float:factionSpawnZ,    // Spawn Z
    Float:factionSpawnA,    // Spawn angle
    factionBank,            // Bank faction
    factionVault,           // Vault
    factionSkins[10],       // Skin yang diizinkan
    factionWeapons[10],     // Senjata yang diizinkan
    factionVehicles[50],    // Kendaraan faction
    factionRanks[15][32]    // Nama rank
}
new FactionInfo[MAX_FACTIONS][FactionData];

// Player faction data
enum PlayerFactionData {
    pFaction,               // ID Faction
    pFactionRank,          // Rank
    pFactionJoinDate[32],  // Tanggal join
    pFactionDuty,          // Status duty
    pFactionSkin,          // Skin saat duty
    pFactionPayday,        // Gaji
    pFactionWarns,         // Peringatan
    pFactionNote[128]      // Catatan
}
new PlayerFactionInfo[MAX_PLAYERS][PlayerFactionData];

// Faction types
#define FACTION_TYPE_LEO        1   // Law Enforcement
#define FACTION_TYPE_MEDICAL    2   // Medical
#define FACTION_TYPE_GOV        3   // Government
#define FACTION_TYPE_NEWS       4   // News
#define FACTION_TYPE_GANG       5   // Gang/Criminal
#define FACTION_TYPE_BUSINESS   6   // Business
```

**Functions:**
```pawn
// Core faction functions
stock CreateFaction(name[], type, color, maxmembers)
stock DeleteFaction(factionid)
stock LoadFactions()
stock SaveFaction(factionid)

// Member management
stock AddPlayerToFaction(playerid, factionid, rank)
stock RemovePlayerFromFaction(playerid)
stock SetPlayerFactionRank(playerid, rank)
stock GetPlayerFactionName(playerid)
stock GetPlayerFactionRankName(playerid)

// Faction features
stock IsPlayerInFaction(playerid, factionid)
stock IsPlayerFactionLeader(playerid)
stock GetFactionOnlineMembers(factionid)
stock SendFactionMessage(factionid, color, message[])
stock ToggleFactionDuty(playerid)

// Faction bank
stock GiveFactionMoney(factionid, amount)
stock TakeFactionMoney(factionid, amount)
stock GetFactionMoney(factionid)

// Vehicles
stock CreateFactionVehicle(factionid, modelid, Float:x, Float:y, Float:z, Float:a, color1, color2)
stock IsFactionVehicle(vehicleid)
stock GetVehicleFactionID(vehicleid)
```

**Police System (`factions_polisi/`):**
```pawn
enum PoliceData {
    policeWarrants,         // Jumlah warrant aktif
    policeCuffs,           // Status borgol
    policeTaser,           // Status taser equipped
    policeRadar,           // Speed radar
    policeTickets,         // Tiket diterbitkan
    policeArrests,         // Penangkapan
    policeDraggedBy        // ID yang men-drag
}
new PoliceInfo[MAX_PLAYERS][PoliceData];

// Commands
CMD:duty(playerid, params[])        // Toggle duty
CMD:su(playerid, params[])          // Wanted player
CMD:ar(playerid, params[])          // Arrest
CMD:ticket(playerid, params[])      // Beri ticket
CMD:cuff(playerid, params[])        // Borgol
CMD:uncuff(playerid, params[])      // Lepas borgol
CMD:tazer(playerid, params[])       // Taser
CMD:drag(playerid, params[])        // Drag player
CMD:mdc(playerid, params[])         // Mobile Data Computer
CMD:backup(playerid, params[])      // Minta backup
CMD:spike(playerid, params[])       // Spike strip
CMD:roadblock(playerid, params[])   // Roadblock
```

**Medical System (`factions_ems/`):**
```pawn
enum MedicData {
    medicCalls,            // Panggilan diterima
    medicHeals,            // Jumlah heal
    medicRevives,          // Jumlah revive
    medicMedkit,           // Jumlah medkit
    medicOnCall            // Status on-call
}
new MedicInfo[MAX_PLAYERS][MedicData];

CMD:heal(playerid, params[])        // Heal player
CMD:revive(playerid, params[])      // Revive player
CMD:medkit(playerid, params[])      // Beri medkit
CMD:accept(playerid, params[])      // Accept call
```

---

### 8. 👨‍👩‍👧‍👦 Family System (`family/`)

**File Structure:**
```
family/
├── family_cmds.inc        # Commands
├── family_functions.inc   # Functions
└── family.inc            # Main
```

**Variables Location: `family.inc`**
```pawn
enum FamilyData {
    familyID,               // ID Family
    familyName[64],         // Nama family
    familyTag[8],           // Tag [XXX]
    familyColor,            // Warna
    familyLeader[MAX_PLAYER_NAME],  // Leader
    familyMembers,          // Jumlah member
    familyMaxMembers,       // Max member (upgradeable)
    familyLevel,            // Level family
    familyExp,              // Experience
    familyBank,             // Bank family
    familyTurf,             // Jumlah turf dikuasai
    Float:familyHQX,        // HQ koordinat
    Float:familyHQY,
    Float:familyHQZ,
    familySkin[10],         // Skin family
    familyWeapons[10],      // Senjata
    familyVehicles[20],     // Kendaraan
    familyRanks[10][32],    // Nama rank
    familyType              // Type (Gang/Mafia/MC)
}
new FamilyInfo[MAX_FAMILIES][FamilyData];

// Player family data
enum PlayerFamilyData {
    pFamily,                // ID Family
    pFamilyRank,           // Rank (0-9)
    pFamilyJoinDate[32],   // Join date
    pFamilyInvitedBy[MAX_PLAYER_NAME],
    pFamilyKills,          // Kills untuk family
    pFamilyDeaths
