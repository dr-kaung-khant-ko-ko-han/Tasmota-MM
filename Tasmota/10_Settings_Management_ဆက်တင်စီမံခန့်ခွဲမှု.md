# ဆက်တင်စီမံခန့်ခွဲမှု (Settings Management)

Tasmota ၏ ဆက်တင်စီမံခန့်ခွဲမှုသည် အလွှာပေါင်းစုံ ဗိသုကာပုံစံ (multi-layered architecture) ကို အသုံးပြုထားပါသည်။

## ဆက်တင်အလွှာ သုံးခု (Three Configuration Layers)

### 1. `my_user_config.h` — Base Defaults
compile-time အခြေခံ default ဆက်တင်များ။ Tasmota firmware ၏ မူလနေရာမှ ပါရှိသော ပုံသေတန်ဖိုးများ ဖြစ်သည်။

### 2. `user_config_override.h` — Build-Specific
တည်ဆောက်မှု (build) အလိုက် သီးသန့် ဆက်တင်များ။ အသုံးပြုသူသည် default ဆက်တင်များကို ဤနေရာမှ override လုပ်နိုင်သည်။ နောက်ဆက်တွဲ configuration ဖိုင်ကို အစားမထိုးဘဲ သိမ်းဆည်းနိုင်သော အားသာချက်ရှိသည်။

### 3. `tasmota_configurations.h` — Feature Sets
ကြိုတင်သတ်မှတ်ထားသော feature set များ။ ဥပမာ - `tasmota-minimal`၊ `tasmota-sensors` စသည်ဖြင့်။

## CFG_HOLDER — Configuration Version Identifier

`CFG_HOLDER` တန်ဖိုးသည် ဖွဲ့စည်းမှုဖွဲ့စည်းပုံ၏ version identifier အဖြစ် ဆောင်ရွက်သည်။ ၎င်းကို အသုံးပြု၍-
- ဆက်တင်ဖွဲ့စည်းပုံသည် ပြောင်းလဲခဲ့သည်ကို အတည်ပြုနိုင်သည်
- Firmware အဆင့်မြှင့်သည့်အခါ settings migration လိုအပ်မှုကို ဆုံးဖြတ်နိုင်သည်

## Flash Storage စနစ်

- **ESP8266** — EEPROM-emulated flash storage ကို အသုံးပြုသည်
- **ESP32** — NVS (Non-Volatile Storage) စနစ်ကို အသုံးပြုသည်

## TasmotaGlobal — Active Runtime State

`TasmotaGlobal` structure သည် အောက်ပါ active runtime state များကို ထိန်းသိမ်းသည်-
- **ပါဝါ အခြေအနေ** (power state) — relay များ၏ on/off အခြေအနေ
- **ကိရိယာ သတ်မှတ်ချက်များ** (devices) — module type၊ GPIO mapping
- **MQTT အခြေအနေ** — ချိတ်ဆက်မှု အခြေအနေ၊ topic များ
- **အချိန်ကိုက်မှု** (timing) — uptime၊ timer များ

## Save Triggers (သိမ်းဆည်းမှု အစပျိုးချက်များ)

ဆက်တင်များကို flash memory သို့ သိမ်းဆည်းသည့် အခြေအနေများ-

| Trigger | ဖော်ပြချက် |
|---------|------------|
| Time-based | `SAVE_DATA` timer — ဆက်တင်ပြောင်းလဲပြီးနောက် သတ်မှတ်ထားသော အချိန်အတွင်း သိမ်းဆည်းသည် |
| Change-based | Command များဖြင့် ဆက်တင်ပြောင်းလဲသည့်အခါ သိမ်းဆည်းသည် |
| Power events | ပါဝါကျဆင်းခြင်း သို့မဟုတ် restart ဖြစ်မည့်အခါ |
| Manual | `SaveData` command ဖြင့် ကိုယ်တိုင်သိမ်းဆည်းခြင်း |

## Version Migration (ဗားရှင်း ကူးပြောင်းခြင်း)

Firmware အဆင့်မြှင့်သည့်အခါ settings များကို အဆင့်မြှင့်သည့် လုပ်ငန်းစဉ်-

1. **Validate** — ဆက်တင်ဖွဲ့စည်းပုံ တရားဝင်မှုကို စစ်ဆေးသည်
2. **Apply incremental updates** — ဗားရှင်းအလိုက် အဆင့်ဆင့် မွမ်းမံမှုများ ပြုလုပ်သည်
3. **Preserve user data** — အသုံးပြုသူ၏ ကိုယ်ပိုင်ဆက်တင်များကို ထိန်းသိမ်းသည်
4. **Update version marker** — `CFG_HOLDER` ကို ဗားရှင်းအသစ်သို့ မွမ်းမံသည်

## SetOption စနစ်

`SetOption` သည် runtime အမူအကျင့်ကို ထိန်းချုပ်ရန် နံပါတ်တပ်ထားသော option များကို အသုံးပြုသည့် စနစ်ဖြစ်သည်။

ဥပမာ-
```
SetOption0 1   // ပါဝါပြန်လာလျှင် relay အခြေအနေ သိမ်းဆည်းခြင်း
SetOption19 1  // Home Assistant auto-discovery
SetOption151 1 // Matter ပံ့ပိုးမှု ဖွင့်ခြင်း
```

## Driver မှတ်ပုံတင်ခြင်း (Driver Registration)

Driver များသည် Tasmota ၏ settings lifecycle နှင့် ပေါင်းစည်းရန် မိမိတို့ကိုယ်ကို ကွဲပြားသော entry point များတွင် register လုပ်ကြသည်-

```
FUNC_SETTINGS_LOAD     — ဆက်တင်များ load လုပ်သည့်အခါ
FUNC_SETTINGS_SAVE     — ဆက်တင်များ save လုပ်သည့်အခါ
FUNC_SETTINGS_DEFAULTS — default သို့ ပြန်သွားသည့်အခါ
FUNC_SETTINGS_APPLY    — ဆက်တင်များ apply လုပ်သည့်အခါ
```

ဤအလွှာပေါင်းစုံ ဗိသုကာပုံစံသည် firmware update ပြုလုပ်စဉ်တွင်လည်း အသုံးပြုသူ၏ ကိုယ်ပိုင်ပြင်ဆင်မှုများကို လုံခြုံစွာ ထိန်းသိမ်းနိုင်စေပါသည်။
