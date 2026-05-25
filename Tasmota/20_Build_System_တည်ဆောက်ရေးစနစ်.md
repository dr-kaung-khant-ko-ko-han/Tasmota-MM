# တည်ဆောက်ရေးစနစ် (Build System)

Tasmota ၏ build system သည် **PlatformIO** ကိုအခြေခံထားပြီး ESP8266 နှင့် ESP32 variant အမျိုးမျိုးအတွက် firmware များကို compile ပြုလုပ်ပေးသည်။

## INI ဖိုင်အလွှာများ (Hierarchical INI Configuration)

Build configuration အတွက် INI ဖိုင်များကို အလွှာလိုက် ဖွဲ့စည်းထားသည်။ အောက်ခြေအလွှာမှ အပေါ်သို့တစ်ဆင့်ချင်း override လုပ်သွားသည့်ပုံစံဖြစ်သည်။

| ဖိုင် | အလုပ်လုပ်ပုံ |
|---|---|
| `platformio.ini` | အခြေခံ global configuration နှင့် ESP8266 variant များအားလုံးအတွက် |
| `platformio_tasmota32.ini` | ESP32 အတွက် အခြေခံ configuration |
| `platformio_tasmota_env.ini` | ESP8266 variant တစ်ခုချင်းစီအတွက် သီးသန့် environment များ |
| `platformio_tasmota_env32.ini` | ESP32 variant တစ်ခုချင်းစီအတွက် သီးသန့် environment များ |
| `platformio_override.ini` | အသုံးပြုသူမှ မိမိစိတ်ကြိုက် override ပြုလုပ်ရန် (git-track မလုပ်ပါ) |

## ESP8266 Variant များ

| Variant | ဖော်ပြချက် |
|---|---|
| `tasmota` | Feature အပြည့်အစုံပါသော standard build |
| `tasmota-minimal` | အနည်းဆုံး feature များသာပါဝင်သော lightweight build |
| `tasmota-sensors` | Sensor အမျိုးအစားအားလုံးကို support လုပ်သော build |
| `tasmota-display` | Display/Monitor support ပါဝင်သော build |

## ESP32 Variant များ

| Variant | ဖော်ပြချက် |
|---|---|
| `tasmota32` | ESP32 အတွက် standard build |
| `tasmota32s3` | ESP32-S3 chip အတွက် build |
| `tasmota32c3` | ESP32-C3 (RISC-V core) အတွက် build |
| `tasmota32-webcam` | Webcam support ပါဝင်သော build |

## ဘာသာစကား Variant များ (Language Variants)

Firmware တစ်ခုစီအတွက် ဘာသာစကား variant များပါရှိသည်။ အဓိကဘာသာစကားများမှာ -

- `DE` — ဂျာမန် (German)
- `CN` — တရုတ် (Chinese)
- အခြား ဘာသာစကား **၂၅ မျိုးကျော်** ရှိသည်

## Build Pipeline

### Pre-build အဆင့်များ

1. **`pre_source_dir.py`** — Flash mode အတွက် source directory ကိုပြင်ဆင်ခြင်း
2. **`override_copy.py`** — User override ဖိုင်များကို build directory သို့ကူးယူခြင်း
3. **`compress-html.py`** — Web asset များ (HTML, CSS, JS) ကိုချုံ့ခြင်း
4. **`set_partition_table.py`** — ESP32 အတွက် partition table သတ်မှတ်ခြင်း

### Post-build အဆင့်များ

1. **`name-firmware.py`** — Firmware ဖိုင်များကို variant အလိုက် အမည်ပြောင်းခြင်း
2. **`gzip-firmware.py`** — OTA update အတွက် firmware ကို gzip ချုံ့ခြင်း
3. **`post_esp32.py`** — ESP32 အတွက် factory image များထုတ်လုပ်ခြင်း
4. **`metrics-firmware.py`** — Firmware size စာရင်းဇယားများ ထုတ်လုပ်ခြင်း

## CI/CD (GitHub Actions)

GitHub Actions မှတစ်ဆင့် အလိုအလျောက် build နှင့် release ပြုလုပ်သည်။

- **Branch နှစ်ခုအတွက် workflow များ** — `development` နှင့် `master`
- **Matrix builds** — Variant အားလုံးကို တစ်ပြိုင်နက် build ပြုလုပ်ခြင်း
- **Release ဖန်တီးမှု** — Build အောင်မြင်ပါက GitHub Release ကို အလိုအလျောက် ဖန်တီးပေးခြင်း
- **OTA server deployment** — OTA update အတွက် firmware ဖိုင်များကို server သို့ တင်ပို့ခြင်း

## Custom Build Targets

| Target | အလုပ်လုပ်ပုံ |
|---|---|
| `downloadfs` | Flash memory အတွင်းမှ filesystem ကို download ပြုလုပ်ခြင်း |
| `factory_flash` | Factory reset ပြုလုပ်ပြီး firmware အသစ်တင်ခြင်း |
| `external_crashreport` | Crash report ထုတ်ယူခြင်း |
| `reset_target` | Target device ကို reset ပြုလုပ်ခြင်း |

## OTA Upload နည်းလမ်းများ

Firmware ကို OTA (Over-the-Air) မှတစ်ဆင့် upload လုပ်ရန် နည်းလမ်းမျိုးစုံ ထောက်ပံ့ထားသည် -

- **HTTP** — HTTP protocol ဖြင့် firmware ကို device သို့ တိုက်ရိုက်ပို့ခြင်း
- **SFTP** — Secure FTP ဖြင့် firmware ပို့ခြင်း
- **esptool** — Serial connection ဖြင့် တိုက်ရိုက် flash လုပ်ခြင်း

## အကျဉ်းချုပ်

Tasmota build system သည် **၁၀၀ ကျော်သော build configuration** များကို support လုပ်ပေးနိုင်ပြီး၊ developer များအတွက် custom build ပြုလုပ်ရန်လည်း လွယ်ကူစွာ extension လုပ်နိုင်သောပုံစံဖြင့် တည်ဆောက်ထားသည်။
