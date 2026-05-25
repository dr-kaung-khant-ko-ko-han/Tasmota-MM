# ဘာသာစကားမျိုးစုံ ပံ့ပိုးမှု (Internationalization)

Tasmota သည် compile-time header files များမှတစ်ဆင့် ဘာသာစကား **၂၀** ကို support လုပ်ပေးသည်။ သက်ဆိုင်ရာ header files များသည် `tasmota/language/` directory အတွင်းတွင် ရှိသည်။

## ဖိုင်အမည်ပေးစနစ် (File Naming)

ဖိုင်အမည်များသည် `[language_code]_[country_code].h` ပုံစံအတိုင်း သတ်မှတ်ထားသည်။

**ဥပမာ:** `en_GB.h` (အင်္ဂလိပ် — ဗြိတိန်)

## Header File တစ်ခုတွင် သတ်မှတ်ရမည့် Definitions များ

Language header file တစ်ခုစီတွင် အောက်ပါအချက်အလက်များကို `#define` macro များအဖြစ် သတ်မှတ်ပေးရသည် -

### အခြေခံ Locale သတ်မှတ်ချက်များ

| Macro | ဖော်ပြချက် |
|---|---|
| `LANGUAGE_LCID` | Windows locale ID (ဘာသာစကားခွဲခြားရန်) |
| `D_HTML_LANGUAGE` | HTML lang attribute တန်ဖိုး |

### ရက်စွဲနှင့် အချိန် သတ်မှတ်ချက်များ

- ရက်စွဲ ခွဲခြားသင်္ကေတ (date separator)
- အချိန် ခွဲခြားသင်္ကေတ (time separator)
- အတိုကောက် နေ့အမည်များ (abbreviated day names)
- အတိုကောက် လအမည်များ (abbreviated month names)

### အသုံးများသော စာသားများ (Common Strings)

အသုံးများသော string များကို အောက်ပါ macro များဖြင့် သတ်မှတ်သည် -

- `D_ADMIN` — စီမံခန့်ခွဲမှု (Administration)
- `D_TEMPERATURE` — အပူချိန် (Temperature)
- `D_HUMIDITY` — စိုထိုင်းဆ (Humidity)
- နှင့် အခြား string အများအပြား

### Component-Specific Definitions

Web server UI နှင့် firmware အဓိက logic အတွက် သီးသန့် macro များ -

- `xdrv_02_webserver` — Web interface တွင်ပြသမည့် စာသားများ
- `tasmota.ino` — Core firmware တွင်အသုံးပြုမည့် စာသားများ

## Memory ချွေတာခြင်းနည်းလမ်းများ (Memory Optimization)

Tasmota ၏ internationalization system သည် memory ချွေတာရန် အောက်ပါနည်းလမ်းများကို အသုံးပြုသည် -

1. **UTF-8 encoding only** — Character encoding တစ်မျိုးတည်းကိုသာ အသုံးပြုခြင်း
2. **Shortest possible strings** — စာသားတိုင်းကို အတိုဆုံးဖြစ်အောင် ရေးသားခြင်း
3. **Compile-time macros** — `#define` macro အားလုံးကို compile လုပ်ချိန်တွင် resolve လုပ်ခြင်း (runtime overhead မရှိ)
4. **တစ်ကြိမ်လျှင် ဘာသာစကားတစ်မျိုး** — Firmware တစ်ခုတွင် ဘာသာစကားတစ်မျိုးတည်းသာ compile လုပ်ထားခြင်း

## Support လုပ်ထားသော ဘာသာစကားများ

| ဘာသာစကား | Language Code | ဖိုင် |
|---|---|---|
| အင်္ဂလိပ် | English | `en_GB.h` |
| ဂျာမန် | German | `de_DE.h` |
| စပိန် | Spanish | `es_ES.h` |
| ပြင်သစ် | French | `fr_FR.h` |
| အီတလီ | Italian | `it_IT.h` |
| ပိုလန် | Polish | `pl_PL.h` |
| ပေါ်တူဂီ (ဘရာဇီး) | Portuguese BR | — |
| ပေါ်တူဂီ | Portuguese PT | — |
| ရုရှား | Russian | — |
| ဒတ်ချ် | Dutch | — |
| ဂရိ | Greek | — |
| တရုတ် (ထိုင်ဝမ်) | Chinese TW | — |
| ဟန်ဂေရီ | Hungarian | — |
| ချက် | Czech | — |
| ယူကရိန်း | Ukrainian | — |
| ဆလိုဗက် | Slovak | — |
| ရိုမေးနီးယား | Romanian | — |
| တူရကီ | Turkish | — |
| ဆွီဒင် | Swedish | — |
| ကိုရီးယား | Korean | — |
| ဟီဘရူး | Hebrew | — |

## Runtime ဘာသာစကား ပြင်ဆင်နိုင်မှု (Runtime Customization)

Firmware ကို compile လုပ်ပြီးသည့်နောက်တွင်လည်း အောက်ပါ command များဖြင့် အချို့သော စာသားများကို runtime တွင် ပြောင်းလဲနိုင်သည် -

### StateText Command

Relay state ကိုဖော်ပြသော `ON`/`OFF`/`TOGGLE` စာသားများကို မိမိကြိုက်နှစ်သက်ရာ ဘာသာစကားသို့ ပြောင်းလဲနိုင်သည်။

```
StateText1 ON;OFF;TOGGLE
```

### Prefix Command

MQTT topic prefix များ (`cmnd`, `stat`, `tele`) ကို ပြောင်းလဲနိုင်သည်။

```
Prefix1 cmnd;stat;tele
```

## Developer များအတွက် လမ်းညွှန်

Tasmota အတွက် UI စာသားအသစ်များထည့်သွင်းရာတွင် အောက်ပါစည်းမျဉ်းများကို လိုက်နာရန် အရေးကြီးသည် -

1. **`D_` macro များကို အမြဲသုံးပါ** — UI တွင်ပြသမည့် စာသားတိုင်းကို `D_` prefix ဖြင့် macro သတ်မှတ်ပြီး အသုံးပြုပါ။ Hardcoded string များ တိုက်ရိုက်မသုံးရပါ။

2. **ဘာသာစကားဖိုင်အားလုံးတွင် ထည့်ပါ** — Macro အသစ်တစ်ခု ထည့်သည့်အခါ `tasmota/language/` directory အတွင်းရှိ **ဘာသာစကားဖိုင်အားလုံး** တွင် သက်ဆိုင်ရာဘာသာပြန်ဖြင့် ထည့်သွင်းပေးရပါမည်။

3. **စာသားများကို တိုတောင်းအောင်ရေးပါ** — ESP8266 ၏ memory ပမာဏကန့်သတ်ချက်ကြောင့် စာသားတိုင်းကို တတ်နိုင်သမျှတိုအောင်ရေးသားရန် လိုအပ်ပါသည်။

4. **Compile-time resolution** — Runtime တွင် string processing လုပ်ရန် memory အလုံအလောက်မရှိသောကြောင့် အားလုံးကို `#define` macro များဖြင့်သာ သတ်မှတ်ပြီး compile time တွင် resolve လုပ်ထားရပါမည်။
