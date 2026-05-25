# Driver စနစ် (Driver System)

Tasmota Driver System သည် လုပ်ဆောင်ချက်များအတွက် `XDRV` (drivers) နှင့် ဒေတာစုဆောင်းမှုအတွက် `XSNS` (sensors) မှတစ်ဆင့် အဓိက extension mechanism ကို ပေးအပ်သည်။ Function-based dispatch ကို အသုံးပြုသည်။

## အဓိကအစိတ်အပိုင်းများ

- **XdrvCall / XsnsCall Dispatch** — Driver နှင့် sensor function များကို lifecycle event အလိုက် dispatch ပြုလုပ်ပေးသော ယန္တရား
- **Function ID များ** — Lifecycle event များအတွက် function identifier များ
- **Driver Modules** — Handler function များပါဝင်သော driver module တစ်ခုချင်းစီ

## အသုံးများသော Function ID များ

| Function ID | အသုံးပြုပုံ |
|-------------|------------|
| `FUNC_INIT` | Driver စတင်သည့်အခါ ခေါ်သည် |
| `FUNC_LOOP` | Main loop တိုင်းတွင် ခေါ်သည် |
| `FUNC_EVERY_SECOND` | တစ်စက္ကန့်တိုင်း ခေါ်သည် |
| `FUNC_COMMAND` | Command တစ်ခုရောက်ရှိသည့်အခါ ခေါ်သည် |
| `FUNC_JSON_APPEND` | JSON status တွင် ဒေတာထည့်ရန် ခေါ်သည် |
| `FUNC_SAVE_BEFORE_RESTART` | Restart မလုပ်မီ settings သိမ်းရန် ခေါ်သည် |

## Command Processing

Command processing သည် driver နှင့် core အကြား ဆက်သွယ်ရန်အတွက် `XdrvMailbox` structure ကို အသုံးပြုသည်။ ဤ structure သည် command name၊ parameters နှင့် response data များကို သယ်ဆောင်ပေးသည်။

## Berry Integration

Berry scripting language ဖြင့် high-level scripting ပံ့ပိုးထားပြီး driver system နှင့် ပေါင်းစည်းကာ အဆင့်မြင့် automation နှင့် custom logic များ ရေးသားနိုင်သည်။

## I2C Driver Integration

I2C bus ပေါ်ရှိ sensor နှင့် peripheral များအတွက် driver များကို standard I2C interface မှတစ်ဆင့် driver framework ထဲသို့ ပေါင်းစည်းထားသည်။
