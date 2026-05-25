# စတင်အသုံးပြုခြင်း (Getting Started)

Tasmota သည် ESP8266 နှင့် ESP32 အခြေပြု စက်ပစ္စည်းများအတွက် အစားထိုး firmware တစ်ခုဖြစ်ပြီး webUI မှတစ်ဆင့် လွယ်ကူစွာ configuration ပြုလုပ်နိုင်ခြင်း၊ OTA updates များ ပြုလုပ်နိုင်ခြင်း၊ timer သို့မဟုတ် rules များဖြင့် automation ပြုလုပ်နိုင်ခြင်း၊ ချဲ့ထွင်နိုင်မှုရှိခြင်းနှင့် MQTT၊ HTTP၊ Serial သို့မဟုတ် KNX မှတစ်ဆင့် local control အပြည့်အဝရရှိခြင်းတို့ကို ပေးစွမ်းပါသည်။

## Installation ရွေးချယ်စရာများ
### ရွေးချယ်မှု ၁: Web Installer (အကြံပြုချက်)
WebSerial API မှတစ်ဆင့် tasmota.github.io/install ရှိ Tasmota WebInstaller ကို အသုံးပြုပါ။

### ရွေးချယ်မှု ၂: Pre-built Binaries များ
ESP8266/ESP32 အတွက် ota.tasmota.com မှ download ရယူပါ။ flashing ပြုလုပ်ရန် Tasmotizer ကို အသုံးပြုပါ။

### ရွေးချယ်မှု ၃: Source မှ Compile ပြုလုပ်ခြင်း
Repository ကို clone လုပ်ပါ၊ `user_config_override_sample.h` ကို `user_config_override.h` အဖြစ် copy ကူးပါ၊ `pio run` command ကို run ပါ။

## WiFi Setup
ပထမဆုံး boot လုပ်သည့်အခါ WiFi credential များ မရှိပါက AP mode အဖြစ် စတင်ပါသည်။ `tasmota-xxxx` သို့ password `12345678` ဖြင့် ချိတ်ဆက်ပါ၊ `192.168.4.1` သို့ သွားကာ WiFi credential များ ထည့်သွင်းပါ။

## Command Interface
Command များကို Console၊ MQTT၊ HTTP၊ Serial တို့မှတစ်ဆင့် အသုံးပြုနိုင်ပါသည်။ အသုံးများသော command များ: `Power ON/OFF`၊ `Status`၊ `SetOption`၊ `Restart`။

## Migration
အဆင့်မြှင့်တင်သည့်လမ်းကြောင်း: Sonoff-Tasmota 3.9.x → 4.x → 5.14 → 6.7.1 → 7.2.0 → 8.5.1 → 9.1 → Latest။
