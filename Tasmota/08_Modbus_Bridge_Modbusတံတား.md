# Modbus တံတား (Modbus Bridge)

Modbus Bridge သည် Tasmota တွင် စွမ်းအင်မီတာများနှင့် စက်မှုဆိုင်ရာ ကိရိယာများအတွက် ယေဘုယျ Modbus RTU/TCP ပံ့ပိုးမှုကို ပေးပါသည်။ JSON အခြေပြု register မြေပုံထုတ်ခြင်းကို အသုံးပြုပါသည်။

## အဓိက အစိတ်အပိုင်းများ

- **EnergyModbus** — ပင်မ driver၊ Modbus ကိရိယာများနှင့် ဆက်သွယ်မှုကို စီမံခန့်ခွဲသည်
- **TasmotaModbus** — အဆင့်နိမ့် Modbus ပရိုတိုကော အကောင်အထည်ဖော်မှု
- **NrgMbsParam** — ဖွဲ့စည်းမှုဆိုင်ရာ ပါရာမီတာများ (configuration parameters)
- **NrgMbsReg** — standard register အဓိပ္ပာယ်သတ်မှတ်ချက်များ
- **NrgMbsUser** — အသုံးပြုသူ သတ်မှတ်ထားသော register များ

## Standard စွမ်းအင်မီတာများအတွက် JSON ဖွဲ့စည်းမှု

ဖွဲ့စည်းမှုကို JSON format ဖြင့် ပြုလုပ်ပြီး အောက်ပါ အကွက်များ (fields) ပါဝင်သည်-

- **Name** — မီတာ၏ အမည်
- **Baud** — ဆက်သွယ်မှုအမြန်နှုန်း (baud rate)
- **Config** — Modbus ဆက်သွယ်မှု ဖွဲ့စည်းမှု (parity, stop bits စသည့်)
- **Address** — Modbus ကိရိယာ လိပ်စာ
- **Function** — Modbus function code (standard စွမ်းအင် register များအတွက်)

## ဒေတာ အမျိုးအစားများ (Data Types)

| အမျိုးအစား | Type ID | ဖော်ပြချက် |
|-----------|---------|------------|
| Float | 0 | 32-bit IEEE 754 floating point |
| Signed 16-bit | 1 | ±32,767 range |
| Signed 32-bit | 2 | ±2,147,483,647 range |
| Unsigned 16-bit | 3 | 0 to 65,535 range |
| Unsigned 32-bit | 4 | 0 to 4,294,967,295 range |

## လုပ်ဆောင်ချက် ယန္တရား

Modbus Bridge သည် polling-based ဆက်သွယ်မှုပုံစံကို အသုံးပြုပြီး register များကို အလှည့်ကျ စက်ဝန်းအတိုင်း ဖတ်ယူပါသည်။

- **Multi-phase ပံ့ပိုးမှု** — 3-phase မီတာများအတွက် phase တစ်ခုချင်းစီ၏ ဒေတာကို သီးခြားစီ စုဆောင်းသည်
- **Polling cycle** — register အားလုံးကို သတ်မှတ်ထားသော အချိန်ကာလအတွင်း အလှည့်ကျ ဖတ်ယူသည်

## User-Defined Register များ

အသုံးပြုသူ သတ်မှတ်နိုင်သော register များကို JSON အကွက်များဖြင့် သတ်မှတ်သည်-

- **R** — Register လိပ်စာ
- **J** — JSON key (web UI တွင် ပြသရန် သော့ချိတ်)
- **G** — GUI တွင် ပြသမည့် အမည်
- **U** — ယူနစ် (unit)
- **D** — ဒသမနေရာ အရေအတွက် (decimals)
- **T** — ဒေတာ အမျိုးအစား (type)
- **F** — အချိုးအဆ (factor)

## ပံ့ပိုးထားသော Modbus မုဒ်များ

- **Modbus RTU** — Serial (RS485/RS232) မှတစ်ဆင့်
- **Modbus TCP** — Network မှတစ်ဆင့် (Ethernet/WiFi)

## အသုံးပြုပုံ ဥပမာ

```json
{
  "MBAddress": 1,
  "MBbaud": 9600,
  "MBconfig": "8N1",
  "MBName": "Eastron SDM120"
}
```

Modbus Bridge သည် စက်မှုလုပ်ငန်းသုံး Modbus ကိရိယာများ၊ စွမ်းအင်မီတာများနှင့် အခြား Modbus-enabled အာရုံခံကိရိယာများကို Tasmota ဂေဟစနစ်တွင် ပေါင်းစည်းနိုင်ရန် စွယ်စုံသုံးနိုင်သော နည်းလမ်းကို ပေးအပ်ပါသည်။
