# Scripter Module (Scripter Module)

Scripter Module (`XDRV_10`) သည် ESP8266 နှင့် ESP32 အတွက် ပေါ့ပါးသော scripting engine ဖြစ်ပြီး flash မှတ်ဉာဏ် ~17KB ခန့်သာ အသုံးပြုသည်။

## Language Design (ဘာသာစကား ဒီဇိုင်း)

RAM အသုံးပြုမှု အနည်းဆုံးဖြစ်စေရန် ဒီဇိုင်းထုတ်ထားသော custom language ဖြစ်သည်။

## Variable Type System (Variable အမျိုးအစား စနစ်)

`T_INDEX` structure နှင့် `SCRIPT_TYPE` union ကို အသုံးပြု၍ အမျိုးအစား ၁၁ မျိုး ပံ့ပိုးထားသည်။

## Filter System (Filter စနစ်)

`M_FILT` structure ကို အသုံးပြု၍ အောက်ပါ filter များ ရရှိနိုင်သည်။

| Syntax | ရှင်းလင်းချက် |
|--------|---------------|
| `m:name=0 5` | Moving average filter — နောက်ဆုံးတန်ဖိုး ၅ ခု၏ ပျမ်းမျှ |
| `M:name=0 5` | Median filter — နောက်ဆုံးတန်ဖိုး ၅ ခု၏ အလယ်တန်ဖိုး |

## Script Sections (Script အပိုင်းများ)

| Section | အသုံးပြုပုံ |
|---------|-------------|
| `>D` | Definitions (အဓိပ္ပာယ်သတ်မှတ်ချက်များ) |
| `>S` | Script (အဓိက script လုပ်ဆောင်ချက်) |
| `>W` | Web display (ဝဘ်ဖန်သားပြင် ပြသမှု) |
| `>M` | MQTT (MQTT မက်ဆေ့ခ်ျများ) |

## Execution (လုပ်ဆောင်ခြင်း)

`Run_Scripter1()` function သည် သက်ဆိုင်ရာ section သို့ လုပ်ဆောင်မှုကို လမ်းကြောင်းပေးသည်။

## Integration (ပေါင်းစည်းမှုများ)

| ပေါင်းစည်းမှု | ရှင်းလင်းချက် |
|----------------|---------------|
| **SML Smart Meter** | `smltab` function pointers မှတစ်ဆင့် မီတာဖတ်ခြင်း |
| **Web Interface Display** | ဝဘ်ဖန်သားပြင်တွင် ဒေတာပြသခြင်း |
| **File System** | `USE_SCRIPT_FATFS` ဖြင့် ဖိုင်စနစ် လုပ်ဆောင်ချက်များ |
| **Network** | TCP, UDP ဆက်သွယ်ရေး |

## Unishox Compression

Script များကို သိမ်းဆည်းရန် နေရာချွေတာရန်အတွက် Unishox compression ကို စိတ်ကြိုက် အသုံးပြုနိုင်သည်။

## Variable Attributes (Variable Attribute များ)

| Prefix | ရှင်းလင်းချက် |
|--------|---------------|
| `p:` | Persistent — reboot လုပ်ပြီးသည့်တိုင် တန်ဖိုး ထိန်းသိမ်းထားသည် |
| `t:` | Timer — အချိန်ကုန်ဆုံးမှုကို ရေတွက်သည် |
| `i:` | Increment — အလိုအလျောက် တိုးပွားသည် |
| `m:` | Filter — filter မှတစ်ဆင့် တန်ဖိုးကို စီမံသည် |
| `g:` | Global — UDP မှတစ်ဆင့် device များကြား မျှဝေသည် |

## Common Use Cases (အသုံးများသော အခြေအနေများ)

- စွမ်းအင်မီတာ ဒေတာ စီမံဆောင်ရွက်ခြင်း
- Sensor တန်ဖိုးများ တွက်ချက်ခြင်း
- Custom display formatting (စိတ်ကြိုက် ဖန်သားပြင် ဖော်မတ်ချခြင်း)
