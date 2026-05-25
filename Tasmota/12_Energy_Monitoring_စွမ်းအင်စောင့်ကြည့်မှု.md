# စွမ်းအင်စောင့်ကြည့်မှု (Energy Monitoring)

Tasmota ၏ စွမ်းအင်စောင့်ကြည့်မှုစနစ်သည် `xdrv_03` energy driver ကို ဗဟိုပြုထားပြီး Tasmota ၏ အဓိကကျသော အင်္ဂါရပ်တစ်ခု ဖြစ်သည်။

## အဓိက ဒေတာဖွဲ့စည်းပုံ

`tEnergy` structure သည် phase အလိုက် array များဖြင့် စွမ်းအင်ဒေတာအားလုံးကို ထိန်းသိမ်းသည်။ Phase တစ်ခုစီတွင် အောက်ပါတို့ ပါဝင်သည်-
- Voltage (ဗို့အား)
- Current (လျှပ်စီး)
- Power (ပါဝါ)
- Apparent Power
- Reactive Power
- Power Factor
- Frequency (ကြိမ်နှုန်း)

## ပံ့ပိုးထားသော Energy IC များ

| IC | Interface | Channels | ဥပမာ ကိရိယာများ |
|----|-----------|----------|----------------|
| **ADE7953** | I2C / SPI | Dual channel | Shelly 2.5၊ Shelly EM |
| **CSE7761** | UART | Single | Sonoff S31၊ Sonoff POW |
| **BL09XX** | UART | Single | Gen3 ကိရိယာများ (BL0937, BL0942) |
| **ADE7880** | I2C | 3-phase | Shelly 3EM |

## External Modbus မီတာများ

Modbus Bridge မှတစ်ဆင့် ပြင်ပ Modbus စွမ်းအင်မီတာများကိုလည်း ပံ့ပိုးပါသည်-

| မီတာ | Protocol | Phase | ထုတ်လုပ်သူ |
|------|----------|-------|-------------|
| **SDM120** | Modbus RTU | Single | Eastron |
| **SDM630** | Modbus RTU | 3-phase | Eastron |
| **PZEM-014** | Modbus RTU | Single | Peacefair |
| **PZEM-004T** | Modbus RTU | Single | Peacefair |

## လုပ်ငန်းစဉ် (Process)

စွမ်းအင်စောင့်ကြည့်မှု လုပ်ငန်းစဉ်သည် အောက်ပါအဆင့်များအတိုင်း လည်ပတ်သည်-

1. **Initialization** — Energy driver စတင်ခြင်း၊ IC ထောက်လှမ်းခြင်း၊ ချိန်ညှိခြင်း တန်ဖိုးများ load လုပ်ခြင်း
2. **200ms Updates** — ၂၀၀ မီလီစက္ကန့်တိုင်း sensor data စုဆောင်းခြင်း
3. **Data Collection** — Voltage၊ Current၊ Power စသည်တို့ကို တိုင်းတာခြင်း
4. **Processing** — တန်ဖိုးများ တွက်ချက်ခြင်း၊ စုစည်းခြင်း
5. **Storage** — စွမ်းအင်သုံးစွဲမှုစုစုပေါင်း၊ ယနေ့စွမ်းအင်ကို flash တွင် သိမ်းဆည်းခြင်း
6. **Threshold Checking** — သတ်မှတ်ထားသော ကန့်သတ်ချက်များကို ကျော်လွန်မှု စစ်ဆေးခြင်း
7. **Midnight Reset** — ညသန်းခေါင်တွင် ယနေ့စွမ်းအင်တန်ဖိုး ပြန်လည်သုညပြုလုပ်ခြင်း

## Energy Commands များ

| Command | ဖော်ပြချက် |
|---------|------------|
| `PowerCal` | ပါဝါ ချိန်ညှိခြင်း |
| `VoltageCal` | ဗို့အား ချိန်ညှိခြင်း |
| `CurrentCal` | လျှပ်စီး ချိန်ညှိခြင်း |
| `PowerSet` | Power threshold သတ်မှတ်ခြင်း |
| `EnergyToday` | ယနေ့ စွမ်းအင်တန်ဖိုး သတ်မှတ်ခြင်း/ပြန်လည်သတ်မှတ်ခြင်း |
| `MaxPower` | ဤနေ့ အတွက် အမြင့်ဆုံးပါဝါ ပြသခြင်း |
| `PowerDelta` | ပါဝါပြောင်းလဲမှု ကန့်သတ်ချက် သတ်မှတ်ခြင်း |

## Margin Detection

Margin detection သည် ဗို့အား၊ လျှပ်စီး၊ နှင့် ပါဝါတန်ဖိုးများ၏ threshold ကို စောင့်ကြည့်ပြီး သတ်မှတ်ချက်ကျော်လွန်ပါက MQTT နှင့် web UI တွင် အကြောင်းကြားချက်များ ပေးပို့ပါသည်။

## ချိန်ညှိခြင်း (Calibration)

```
New_Cal = Current_Cal × (Actual / Tasmota)
```

အထက်ပါ ဖော်မြူလာကို အသုံးပြု၍ တိကျသော တိုင်းတာမှုများ ရရှိစေရန် ချိန်ညှိနိုင်ပါသည်။

## Phase ပံ့ပိုးမှု

- **ESP8266** — Phase ၃ ခုအထိ
- **ESP32** — Phase ၈ ခုအထိ

## Tariff ပံ့ပိုးမှု (နှုန်းထားအလိုက် ခြေရာခံခြင်း)

Dual-rate (နှစ်မျိုးနှုန်းထား) လျှပ်စစ်မီတာများအတွက် tariff အလိုက် စွမ်းအင်သုံးစွဲမှုကို သီးခြားစီ ခြေရာခံနိုင်သော ပံ့ပိုးမှု ပါဝင်သည်။ Tariff 1 နှင့် Tariff 2 အတွက် စွမ်းအင်တန်ဖိုးများကို သီးသန့်ထိန်းသိမ်းပါသည်။

## JSON Output

စွမ်းအင်ဒေတာကို MQTT နှင့် web UI တွင် JSON format ဖြင့် တွေ့မြင်နိုင်ပါသည်။ ဥပမာ Status 8 (SENSOR) နှင့် Status 10 (ENERGY) တွင် ကြည့်ရှုနိုင်ပါသည်။
