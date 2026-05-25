# Command ကိုင်တွယ်မှု (Command Processing)

Tasmota ၏ unified command system သည် MQTT၊ HTTP၊ Serial၊ Web UI နှင့် Backlog စသည့် source အမျိုးမျိုးမှ command များကို တစ်ပြေးညီ စီမံခန့်ခွဲပေးသည်။

## Command Processing Pipeline

ဗဟို `CommandHandler` function သည် command string ကို command name နှင့် parameters များအဖြစ် ခွဲထုတ်သည်။ `XdrvMailbox` structure က ခွဲထုတ်ထားသော ဒေတာများကို driver များဆီသို့ သယ်ဆောင်ပေးသည်။

## Command Registration

Command များကို `kTasmotaCommands` string array တွင် register ပြုလုပ်ထားသည်။ ဤ array သည် driver များနှင့် core modules များမှ command တစ်ခုချင်းစီ၏ handler mapping ကို သတ်မှတ်ပေးသည်။

## Command အမျိုးအစားများ

- **Power Control** — စက်ပစ္စည်းကို ON/OFF လုပ်သည့် command များ
- **Network** — WiFi၊ IP configuration ဆိုင်ရာ command များ
- **MQTT** — MQTT broker connection နှင့် topic configuration
- **System** — Status၊ restart၊ reset စသည့် system command များ
- **GPIO** — GPIO pin configuration နှင့် control

## Response Format

Command response များကို JSON format ဖြင့် ပြန်ကြားပေးသည်။ Response တွင် command အောင်မြင်မှု၊ error message များ၊ နှင့် တောင်းဆိုထားသော ဒေတာများ ပါဝင်သည်။

## Source Tracking

Command ဝင်လာသည့် source ကို ခြေရာခံရန်အတွက် source identifier များ ရှိသည်:

| Identifier | Source |
|------------|--------|
| `SRC_MQTT` | MQTT message |
| `SRC_WEBGUI` | Web UI console |
| `SRC_SERIAL` | Serial port |
| `SRC_BACKLOG` | Backlog queue |
| `SRC_HTTP` | HTTP request |

## Backlog System

Backlog သည် command အများအပြားကို တန်းစီကာ အစဉ်လိုက် လုပ်ဆောင်နိုင်သော စနစ်ဖြစ်သည်။ `Backlog` command နောက်တွင် semicolon (`;`) ဖြင့် ခြားထားသော command များကို ရေးသားနိုင်သည်။ Command တစ်ခုချင်းစီကို အစဉ်လိုက် process လုပ်ပြီး ရလဒ်ကို ပေါင်းစည်း၍ response ပြန်ပေးသည်။
