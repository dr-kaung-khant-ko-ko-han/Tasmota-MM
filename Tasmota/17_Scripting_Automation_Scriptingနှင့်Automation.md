# Scripting နှင့် Automation (Scripting & Automation)

Tasmota တွင် အခက်အခဲအဆင့်အမျိုးမျိုးအတွက် automation framework များစွာ ပါဝင်သည်။

## Berry Scripting

Lightweight VM တစ်ခုဖြစ်ပြီး `xdrv_52` မှတစ်ဆင့် ပေါင်းစည်းထားသည်။ Event dispatcher သည် MQTT, rules, teleperiod ဖြစ်ရပ်များကို လမ်းကြောင်းပေးသည်။

### ပံ့ပိုးသော လုပ်ဆောင်ချက်များ
- **LED Control**: `Leds` class ဖြင့် WS2812 LED များကို ထိန်းချုပ်ခြင်း
- **Web Server Handlers**: Web server တွင် handler များ စာရင်းသွင်းခြင်း

## Scripter Module (xdrv_10)

Sensor data processing အတွက် optimized လုပ်ထားသော module ဖြစ်ပြီး flash မှတ်ဉာဏ် ~17KB ခန့် အသုံးပြုသည်။

### Variables (Variable များ)

| Prefix | ရှင်းလင်းချက် |
|--------|---------------|
| `p:` | Persistent — reboot လုပ်ပြီးနောက်တွင်လည်း တန်ဖိုးမပျောက် |
| `t:` | Timer — အလိုအလျောက် auto-decrement လုပ်သည် |
| `i:` | Increment — အလိုအလျောက် auto-increment လုပ်သည် |
| `m:` | Median filter — median filter အဖြစ် အသုံးပြုသည် |
| `g:` | Global — UDP မှတစ်ဆင့် device များကြား မျှဝေသည် |

### Filter Arrays (Filter Array များ)

- **Moving average** — ရွေ့လျားပျမ်းမျှ
- **Median** — အလယ်တန်ဖိုး

## SML Integration (SML ပေါင်းစည်းမှု)

မီတာဖတ်ခြင်းအတွက် အောက်ပါ function များ ပါဝင်သည်။

- `SML_GetVal()` — တန်ဖိုး ရယူခြင်း
- `SML_GetSVal()` — စာသားတန်ဖိုး ရယူခြင်း

## Cross-System Integration (စနစ်ဖြတ်ကျော် ပေါင်းစည်းမှု)

မျှဝေထားသော ဖြစ်ရပ်များ (shared events)၊ MQTT နှင့် တိုက်ရိုက် function calls များမှတစ်ဆင့် စနစ်အချင်းချင်း ပေါင်းစည်းနိုင်သည်။

### Key Functions (အဓိက Function များ)

| Function | ရှင်းလင်းချက် |
|----------|---------------|
| `callBerryEventDispatcher()` | အဓိက ဖြစ်ရပ်များ လမ်းကြောင်းပေးခြင်း |
| `callBerryFastLoop()` | 5ms တိုင်း အပ်ဒိတ်လုပ်ခြင်း |
| `Run_Scripter1()` | Script ကို လုပ်ဆောင်ခြင်း |
