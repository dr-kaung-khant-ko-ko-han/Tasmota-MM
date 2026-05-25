# Tasmota ခြုံငုံသုံးသပ်ချက်

> မူရင်းစာမျက်နှာ — https://deepwiki.com/arendst/Tasmota/

---

Tasmota သည် ESP8266 နှင့် ESP32 အခြေပြု စက်ပစ္စည်းများအတွက် open-source firmware တစ်ခုဖြစ်ပြီး၊ စီးပွားဖြစ် IoT စက်များကို ဒေသတွင်းထိန်းချုပ်နိုင်သော smart home အစိတ်အပိုင်းများအဖြစ် ပြောင်းလဲပေးပါသည်။ Arduino framework အတွက် C++ ဖြင့် ရေးသားထားပြီး PlatformIO ဖြင့် တည်ဆောက်ထားကာ၊ cloud မှီခိုမှုကို ရှောင်ရှားပြီး ကျယ်ပြန့်သော စိတ်ကြိုက်ပြင်ဆင်မှုနှင့် automation စွမ်းရည်များကို ပေးအပ်ပါသည်။

## မိတ်ဆက်

Tasmota သည် ESP8266/ESP32 စက်များကို အောက်ပါ interface များမှတစ်ဆင့် ဒေသတွင်းထိန်းချုပ်မှု အပြည့်အဝပေးသည်။

- **Web-based configuration interface** (`xdrv_01_webserver`)
- **MQTT ပေါင်းစည်းမှု** (`xdrv_02_mqtt`) — home automation စနစ်များအတွက်
- **Serial console** — တိုက်ရိုက် စက်ပစ္စည်းအသုံးပြုခွင့်
- **OTA (Over-The-Air) firmware အပ်ဒိတ်များ**
- **Rules Engine** (`xdrv_10_rules`) နှင့် **Berry scripting** (`xdrv_52_berry`) မှတစ်ဆင့် automation
- **Modular XDRV/XSNS driver** တည်ဆောက်ပုံဖြင့် ကျယ်ပြန့်သော hardware ပံ့ပိုးမှု
- Template နှင့် module အဓိပ္ပာယ်ဖွင့်ဆိုချက်များမှတစ်ဆင့် စက်အမျိုးအစား ၆၀၀+ အတွက် ပံ့ပိုးမှု

## အဓိက ဗိသုကာတည်ဆောက်ပုံ

Firmware ဗိသုကာသည် core လုပ်ဆောင်ချက်များ (`tasmota.ino` တွင်) ကို feature-specific driver များမှ ခွဲခြားထားပြီး၊ မတူညီသော hardware ကန့်သတ်ချက်များနှင့် အသုံးပြုမှုကိစ္စများအတွက် optimized builds များကို ဖန်တီးနိုင်သည်။

Core system သည် `setup()` မှတစ်ဆင့် စတင်ပြီး၊ `loop()` ထဲသို့ ဝင်ရောက်ကာ အချိန်ကိုက်မှုများနှင့် driver callback စနစ်မှတစ်ဆင့် စနစ်လုပ်ဆောင်ချက်အားလုံးကို စီမံခန့်ခွဲသည်။

## Driver စနစ်

Tasmota သည် XDRV (eXternal DRiVer) နှင့် XSNS (eXternal SeNSor) စနစ်များမှတစ်ဆင့် ပြောင်းလွယ်ပြင်လွယ်ရှိသော driver တည်ဆောက်ပုံကို အကောင်အထည်ဖော်ထားသည်။

- `I2cDriver<index> 0/1` — I2C driver များကို ဖွင့်/ပိတ်
- `Driver<index> 0/1` — သတ်မှတ်ထားသော XDRV driver များကို ဖွင့်/ပိတ်
- Moduler စနစ်သည် compile time တွင် `#define USE_*` flags များမှတစ်ဆင့် feature များကို ထည့်သွင်း/ဖယ်ရှားနိုင်သည်

## Configuration စနစ်

### Compile-time Configuration
- `my_user_config.h` တွင် အခြေခံ feature များနှင့် default များ
- `user_config_override.h` တွင် စိတ်ကြိုက်ပြင်ဆင်မှုများ (code update လုပ်စဉ် ထိန်းသိမ်းထားသည်)
- Build flags များမှတစ်ဆင့် feature ရွေးချယ်မှု

### Runtime Configuration
- User-specific settings များကို flash memory တွင် သိမ်းဆည်းသည်
- `Settings` structure မှတစ်ဆင့် အသုံးပြုခွင့်
- Web UI, MQTT, Serial တို့မှ configuration commands များ

## ဆက်သွယ်ရေး ပရိုတိုကောများ

1. **MQTT** — အိမ်သုံး automation ပေါင်းစည်းမှုအတွက် အဓိက protocol၊ TLS ပံ့ပိုးမှု၊ Home Assistant အတွက် auto-discovery
2. **HTTP/Web UI** — တပ်ဆင်ထားသော web server၊ mobile-friendly configuration၊ REST API
3. **Serial** — UART မှတစ်ဆင့် command console
4. **ထပ်တိုး Protocol များ** — KNX၊ Modbus၊ Matter

## Command စနစ်

- Unified command set — interface အားလုံးတွင် တူညီသော command များ အလုပ်လုပ်သည်
- Drivers များက command handler များ register လုပ်နိုင်သည်
- JSON-formatted responses
- Command အမျိုးအစားများ — Power control, Configuration, Information, Hardware-specific
- `Backlog` ကို အသုံးပြု၍ command များကို ဆက်တိုက်လုပ်ဆောင်နိုင်သည်

## Scripting နှင့် Automation

1. **Rules Engine** — Event-action စနစ် (`ON Power1#State DO...`)
2. **Berry Scripting** — Object-oriented scripting language၊ class များနှင့် method များ
3. **Scripter** — Sensor data processing အတွက် advanced scripting module
4. **Timers** — Configurable timer ၁၆ ခုအထိ

## Build System နှင့် Variants

**ESP8266 variants:** tasmota.bin (standard), tasmota-4M.bin (4MB+), tasmota-sensors.bin, tasmota-lite.bin (1MB), tasmota-display.bin, tasmota-ir.bin

**ESP32 variants:** tasmota32.bin (standard), tasmota32-bluetooth.bin, tasmota32-webcam.bin, tasmota32-lvgl.bin, tasmota32-nspanel.bin

---

*Tasmota သည် ဒေသတွင်းထိန်းချုပ်မှု၊ တိုးချဲ့နိုင်မှုနှင့် အသုံးပြုရလွယ်ကူမှုကို အာရုံစိုက်ထားသော ESP8266/ESP32 စက်များအတွက် ပြည့်စုံသော firmware ဖြေရှင်းချက်တစ်ခုဖြစ်သည်။*
