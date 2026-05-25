# Matter ပရိုတိုကော (Matter Protocol)

Matter သည် စက်မှုစံနှုန်းတစ်ခုဖြစ်သော smart home ဆက်သွယ်မှု ပရိုတိုကောတစ်ခု ဖြစ်သည်။ Tasmota ၏ Matter အကောင်အထည်ဖော်မှုသည် Berry scripting language ကို အသုံးပြုထားပါသည်။

## Compile Options

`USE_MATTER_DEVICE` ဖြင့် အခြေအနေအလိုက် compile ပြုလုပ်ပါသည်။

## အဓိက အစိတ်အပိုင်းများ

### Matter_Device Class
အခြား Matter အစိတ်အပိုင်းအားလုံးကို ပေါင်းစည်းပေးသော ဗဟိုအချက်အချာ (central hub) ဖြစ်သည်။

### Plugin စနစ်
`Matter_Plugin` ကို base class အဖြစ် အသုံးပြုပြီး အောက်ပါ plugin အမျိုးအစားများ ရှိသည်-

- **Root Plugin** — အခြေခံ node စီမံခန့်ခွဲမှု
- **Aggregator Plugin** — endpoint များကို စုစည်းပေးသည်
- **Device-Specific Plugin များ-**
  - **OnOff** — ရိုးရှင်းသော on/off ကိရိယာများ
  - **Light1/Light2** — မီးထိန်းချုပ်မှု
  - **Sensor** — အပူချိန် (Temp)၊ စိုထိုင်းဆ (Humidity)၊ ဖိအား (Pressure)၊ လူရှိနေခြင်း (Occupancy)
  - **Shutter** — ရှပ်တာ/ကာလိပ် ထိန်းချုပ်မှု

### Matter_UI
Web-based ဖွဲ့စည်းမှု အင်တာဖေ့စ်။

### Matter_Commissioning
Matter ကိရိယာကို network သို့ ချိတ်ဆက်ခြင်းအတွက် လိုအပ်သော လုပ်ငန်းစဉ်များ ပါဝင်သည်-

- **PASE** (Passcode Authenticated Session Establishment) — စက်ရှင်တည်ဆောက်ခြင်း
- **လက်မှတ်များ (Certificates)** — ကိရိယာ စစ်မှန်ကြောင်း အတည်ပြုခြင်း
- **Fabric Management** — Multi-controller ဖွဲ့စည်းမှုများအတွက်

## Bridge Mode

Bridge မုဒ်သည် အဝေးရှိ Tasmota ကိရိယာများကို Matter network သို့ ဖော်ထုတ်ပေးနိုင်သည်။ ၎င်းကို `SetOption151 1` ဖြင့် ဖွင့်အသုံးပြုသည်။

## Fabric Management

Matter fabric စီမံခန့်ခွဲမှုသည် ကိရိယာတစ်ခုကို controller အများအပြား (ဥပမာ - Google Home နှင့် Apple Home တစ်ပြိုင်နက်) မှ ထိန်းချုပ်နိုင်အောင် ပံ့ပိုးပေးပါသည်။

## အလိုအလျောက် ဖွဲ့စည်းမှု (Auto-Configuration)

`Matter_Autoconf` class သည် Tasmota ကိရိယာ၏ စွမ်းဆောင်ရည်များ (စွမ်းအင်စောင့်ကြည့်မှု၊ relay အရေအတွက်၊ အာရုံခံကိရိယာများ စသည်) ကို အလိုအလျောက် ထောက်လှမ်းပြီး သင့်လျော်သော Matter endpoint များကို ဖန်တီးပေးပါသည်။

## ပံ့ပိုးထားသော Matter Cluster များ

| Cluster | ဖော်ပြချက် |
|---------|------------|
| On/Off | အခြေခံ ခလုတ်ထိန်းချုပ်မှု |
| Level Control | အဆင့်လိုက် ထိန်းချုပ်မှု |
| Color Control | အရောင်ထိန်းချုပ်မှု |
| Temperature Measurement | အပူချိန်တိုင်းတာမှု |
| Humidity Measurement | စိုထိုင်းဆတိုင်းတာမှု |
| Pressure Measurement | ဖိအားတိုင်းတာမှု |
| Occupancy Sensing | လူရှိနေခြင်း အာရုံခံမှု |
| Window Covering | ရှပ်တာ/ကာလိပ် ထိန်းချုပ်မှု |

Matter Protocol သည် Tasmota ကိရိယာများကို Apple HomeKit၊ Google Home၊ Amazon Alexa နှင့် Samsung SmartThings ကဲ့သို့သော အဓိက smart home ဂေဟစနစ်များနှင့် ချောမွေ့စွာ ချိတ်ဆက်နိုင်စေပါသည်။
