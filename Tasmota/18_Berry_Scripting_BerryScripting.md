# Berry Scripting (Berry Scripting)

Berry သည် Tasmota တွင် အပြည့်အဝ ပေါင်းစည်းထားသော ပေါ့ပါးသည့် scripting language တစ်ခု ဖြစ်သည်။

## Implementation (အကောင်အထည်ဖော်မှု)

`XDRV_52` driver မှတစ်ဆင့် အကောင်အထည်ဖော်ထားသည်။ VM ကို `BerryInit()` ဖြင့် စတင်သတ်မှတ်သည်။

### Integration Points (ပေါင်းစည်းမှု အချက်များ)

| Function | အသုံးပြုပုံ |
|----------|-------------|
| `callBerryEventDispatcher()` | MQTT, rules, teleperiod ဖြစ်ရပ်များ ကိုင်တွယ်ခြင်း |
| `callBerryFastLoop()` | 5ms ကြိမ်နှုန်းမြင့် အပ်ဒိတ်များ |
| `callBerryRunDeferred()` | နှောင့်နှေးလုပ်ဆောင်ရမည့် အလုပ်များ |

## Module Categories (Module အမျိုးအစားများ)

| အမျိုးအစား | Module များ |
|-------------|-------------|
| **Core Language** | `string`, `json`, `math`, `time` |
| **Hardware I/O** | `gpio`, `display`, `light`, `energy` |
| **Communication** | `webserver`, `mqtt`, `serial` |
| **Storage** | `persist`, `flash`, `path` |
| **Advanced** | `crypto`, `ULP`, `matter` |

## Automation (Automation လုပ်ဆောင်ချက်များ)

| Function | ရှင်းလင်းချက် |
|----------|---------------|
| `tasmota.add_rule()` | ဖြစ်ရပ် ကိုင်တွယ်မှုများ စာရင်းသွင်းခြင်း |
| `tasmota.add_timer()` | တစ်ကြိမ်တည်း သို့မဟုတ် cron အချိန်ဇယားဖြင့် လုပ်ဆောင်ချက် စီစဉ်ခြင်း |
| `tasmota.add_fast_loop()` | ကြိမ်နှုန်းမြင့် အပ်ဒိတ်များ လုပ်ဆောင်ခြင်း |

## Web Console (Web Console / REPL)

Browser မှတစ်ဆင့် Berry code ကို တိုက်ရိုက်စမ်းသပ်ရေးသားနိုင်သော interactive console ဖြစ်သည်။

## Memory Allocation (မှတ်ဉာဏ် ခွဲဝေမှု)

| မှတ်ဉာဏ်အမျိုးအစား | အသုံးပြုပုံ |
|----------------------|-------------|
| **PSRAM** | ကြီးမားသော object များ သိမ်းဆည်းခြင်း |
| **IRAM** | အချိန်အရေးကြီးသော လုပ်ဆောင်ချက်များ |
| **Standard malloc** | အထွေထွေ အသုံးပြုမှုများ |

## Commands (Command များ)

| Command | ရှင်းလင်းချက် |
|---------|---------------|
| `BrRun` | Berry code ကို လုပ်ဆောင်ခြင်း |
| `BrRestart` | VM ကို ပြန်လည်စတင်ခြင်း |

## BEC Loader

ကြိုတင် compile လုပ်ထားသော bytecode များကို ဖွင့်ရန် BEC loader ကို အသုံးပြုသည်။ ၎င်းသည် run-time parsing မလိုဘဲ လျင်မြန်စွာ လုပ်ဆောင်နိုင်သည်။
