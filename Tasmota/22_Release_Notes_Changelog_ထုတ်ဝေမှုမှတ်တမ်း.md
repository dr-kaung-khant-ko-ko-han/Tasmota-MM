# ထုတ်ဝေမှုမှတ်တမ်းနှင့် အပြောင်းအလဲများ (Release Notes & Changelog)

## ဗားရှင်းစီမံခန့်ခွဲမှုစနစ် (Version Management)

Tasmota သည် **32-bit version constant** ကိုအသုံးပြုပြီး အောက်ပါအတိုင်း version အဆင့်ဆင့်ကို encode လုပ်ထားသည် -

```
major.minor.patch.build
```

ဥပမာ — `13.0.0.1` ဆိုလျှင် major `13`, minor `0`, patch `0`, build `1` ဖြစ်သည်။

## Changelog ဖော်မတ်

Changelog ကို အလွှာလိုက်ဖွဲ့စည်းထားပြီး အောက်ပါကဏ္ဍများအလိုက် ခွဲခြားဖော်ပြထားသည် -

### ကဏ္ဍများ

| ကဏ္ဍ | အင်္ဂလိပ် | ဖော်ပြချက် |
|---|---|---|
| Breaking Changes | Breaking Changes | ယခင်ဗားရှင်းများနှင့် ကိုက်ညီမှုပျက်သွားသော အပြောင်းအလဲများ |
| New Features | New Features | အသစ်ထည့်သွင်းထားသော feature များ |
| Bug Fixes | Bug Fixes | ပြင်ဆင်ထားသော bug များ |
| Known Issues | Known Issues | လက်ရှိသိရှိထားသည့် ပြဿနာများ |

## Firmware ဖြန့်ဖြူးမှု (Distribution)

Release တစ်ခုစီတွင် hardware အမျိုးအစားအလိုက် firmware variant မျိုးစုံကို ဖြန့်ဖြူးပေးသည် -

- ESP8266 variant များ (`tasmota`, `tasmota-minimal`, `tasmota-sensors`, `tasmota-display`)
- ESP32 variant များ (`tasmota32`, `tasmota32s3`, `tasmota32c3`, `tasmota32-webcam`)
- ဘာသာစကား variant များ (DE, CN, အစရှိသည်)

## Major Upgrade အတွက် ကူးပြောင်းလမ်းကြောင်းများ (Migration Paths)

Major version အကူးအပြောင်းများတွင် data မပျက်စေရန် တိကျသော ကူးပြောင်းလမ်းကြောင်းများ သတ်မှတ်ထားသည်။ တစ်ဆင့်ချင်းစီ upgrade လုပ်ရန် လိုအပ်ပြီး ကျော်ခုန်၍မရပါ။

### ကူးပြောင်းလမ်းကြောင်း

```
Sonoff-Tasmota 3.9.x → 4.x → 5.14 → 6.7.1 → 7.2.0 → 8.5.1 → 9.1 → Latest
```

#### အရေးကြီးသော မှတ်တိုင်များ

| ဗားရှင်း | အရေးပါသည့်အကြောင်းရင်း |
|---|---|
| **7.2.0** | Storage system တွင် **အဓိကပြောင်းလဲမှု** ပါဝင်သည်။ ဤမှတ်တိုင်ကို ကျော်၍မရပါ။ |
| **8.5.1** | GPIO function အမည်ပေးစနစ် **အပြောင်းအလဲ** ပါဝင်သည်။ ဤမှတ်တိုင်ကို ကျော်၍မရပါ။ |

## CFG_HOLDER နှင့် Settings Migration

Firmware အသစ် flash လုပ်သည့်အခါ `CFG_HOLDER` တန်ဖိုးကို စစ်ဆေးသည်။ တန်ဖိုးမတူပါက settings migration ကို အလိုအလျောက် လုပ်ဆောင်သည် -

1. **တည်ဆောက်ပုံ စစ်ဆေးခြင်း** — Settings structure ၏ version ကို validate လုပ်ခြင်း
2. **အပ်ဒိတ်များ အသုံးပြုခြင်း** — Version အလိုက် လိုအပ်သော update များကို တစ်ဆင့်ချင်း apply လုပ်ခြင်း
3. **User data ထိန်းသိမ်းခြင်း** — သုံးစွဲသူ၏ နဂိုမူရင်း setting များကို မပျက်စေဘဲ ထိန်းသိမ်းခြင်း
4. **Version မွမ်းမံခြင်း** — `CFG_HOLDER` တန်ဖိုးကို ဗားရှင်းအသစ်သို့ update လုပ်ခြင်း

Settings migration logic သည် firmware source code အတွင်းတွင် တည်ဆောက်ထားပြီး version တစ်ခုမှ နောက်တစ်ခုသို့ ကူးပြောင်းရာတွင် compatibility ကိုထိန်းသိမ်းပေးသည်။

## Version Detection Tool များ

### decode-status.py

Firmware တွင်ပါဝင်သော feature များကို ခွဲခြမ်းစိတ်ဖြာရန်အတွက် Python script တစ်ခု ပါဝင်ထားသည်။ Status report မှရရှိသော bit-flag တန်ဖိုးများကို decode လုပ်ပြီး မည်သည့် feature များ enable လုပ်ထားသည်ကို ဖော်ပြပေးသည်။

### Status Command များ

Device မှ runtime information ရယူရန် console တွင် အောက်ပါတို့ကို အသုံးပြုနိုင်သည် -

- `status 0` — Basic status
- `status 1` — Detailed status (feature flags များပါဝင်)
- `status 2` — Full status dump

### Feature Detection Mapping

Bit-flag တစ်ခုစီကို သက်ဆိုင်ရာ feature description နှင့် mapping လုပ်ထားသည်။ ဥပမာ — flag `0x00000001` သည် "MQTT enabled" ကိုဆိုလိုပြီး flag `0x00000002` သည် "Web server enabled" ကိုဆိုလိုသည်။

## Build Variant Documentation

Build variant များအားလုံး၏ အသေးစိတ်အချက်အလက်များကို အောက်ပါဖိုင်များတွင် မှတ်တမ်းတင်ထားသည် -

| ဖိုင် | အကြောင်းအရာ |
|---|---|
| `BUILDS.md` | Build variant တစ်ခုချင်းစီ၏ feature အကျဉ်းချုပ် |
| `RELEASENOTES.md` | Release တစ်ခုစီ၏ changelog အပြည့်အစုံ |

## Community ပံ့ပိုးမှု

Release documentation များ (changelog, release notes, build documentation) ကို ထိန်းသိမ်းရာတွင် **community contributions** များကို အမြဲကြိုဆိုပါသည်။ Release note များရေးသားခြင်း၊ changelog format မြှင့်တင်ခြင်း၊ version migration guide များပြုစုခြင်းတို့တွင် community အဖွဲ့ဝင်များမှ ပါဝင်ကူညီနိုင်ပါသည်။

## အကျဉ်းချုပ်

Tasmota ၏ release system သည် အောက်ပါတို့ကို အာမခံချက်ပေးသည် -

- **Version tracking** — 32-bit constant ဖြင့် version တစ်ခုချင်းစီကို တိကျစွာ ခွဲခြားနိုင်ခြင်း
- **Safe migration** — ဗားရှင်းဟောင်းမှ အသစ်သို့ settings မပျက်စေဘဲ ကူးပြောင်းနိုင်ခြင်း
- **Variant management** — Hardware နှင့် language အလိုက် firmware အမျိုးအစား ၁၀၀ ကျော်ကို စနစ်တကျ စီမံခန့်ခွဲနိုင်ခြင်း
- **Transparency** — Changelog နှင့် release notes များမှတစ်ဆင့် အပြောင်းအလဲအားလုံးကို ပွင့်လင်းမြင်သာစွာ ဖော်ပြခြင်း
