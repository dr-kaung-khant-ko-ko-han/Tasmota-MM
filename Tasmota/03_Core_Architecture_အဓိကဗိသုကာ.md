# အဓိကဗိသုကာ (Core Architecture)

Tasmota သည် modular နှင့် event-driven architecture ကို လိုက်နာပြီး subsystem များကို standardized driver framework မှတစ်ဆင့် ညှိနှိုင်းဆောင်ရွက်ပေးသော main execution loop ကို ဗဟိုပြုထားသည်။

## Main Execution

Arduino ပုံစံ `setup()` နှင့် `loop()` ဖြင့် time-based scheduling ကို အသုံးပြုသည်။ Global state ကို `TasmotaGlobal` structure မှတစ်ဆင့် စီမံခန့်ခွဲသည်။

## Driver Framework

Driver framework သည် function pointer array များ (`XDRV` နှင့် `XSNS`) ကို အသုံးပြုသည်။ `XDRV` သည် drivers များ (လုပ်ဆောင်ချက်များ) အတွက်ဖြစ်ပြီး `XSNS` သည် sensors များ (ဒေတာစုဆောင်းမှု) အတွက် ဖြစ်သည်။

## Settings Management

Settings များကို flash storage တွင် migration ပံ့ပိုးမှုဖြင့် စီမံခန့်ခွဲသည်။ Firmware version အဆင့်မြှင့်သည့်အခါ settings format အပြောင်းအလဲများကို အလိုအလျောက် ကိုင်တွယ်ပေးသည်။

## Command System

Command system သည် JSON response များဖြင့် unified interface တစ်ခု ပေးအပ်သည်။ MQTT၊ HTTP၊ Serial၊ Web UI စသည့် source အမျိုးမျိုးမှ လက်ခံသော command များကို တစ်ပြေးညီ စီမံခန့်ခွဲပေးသည်။
