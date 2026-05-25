# အသုံးပြုသူ အင်တာဖေ့စ်များ (User Interfaces)

Tasmota သည် အသုံးပြုသူများအတွက် အင်တာဖေ့စ်အမျိုးမျိုးကို ပံ့ပိုးပေးထားသည်- ရုပ်ပိုင်းဆိုင်ရာ display များ၊ touch input များ၊ web-based tools များ၊ GPIO Viewer နှင့် HASPmota တို့ ဖြစ်သည်။

## Display စနစ်

Display စနစ်သည် အလွှာလိုက် ဗိသုကာပုံစံ (layered architecture) ကို အသုံးပြုထားသည်-

### Renderer (Base Layer)
- Adafruit_GFX library ကို inherit လုပ်ထားသည်
- အခြေခံ ဂရပ်ဖစ်ဆွဲခြင်းဆိုင်ရာ လုပ်ဆောင်ချက်များ ပါဝင်သည်

### uDisplay (Hardware-Specific Layer)
- Hardware အလိုက် သီးသန့် driver များ
- Display controller တစ်ခုချင်းစီအတွက် protocol-specific အကောင်အထည်ဖော်မှု

### xdrv_13_display (Main Driver)
- Tasmota ၏ ပင်မ display driver
- Display command များကို ကိုင်တွယ်ခြင်း၊ data display ပြုလုပ်ခြင်း

## Touch ပေါင်းစည်းမှု

`xdrv_55_touch` driver မှတစ်ဆင့် touch input ကို ပံ့ပိုးပါသည်။

### Capacitive Touch (I2C)
| Controller | ဖော်ပြချက် |
|-----------|------------|
| **GT911** | Goodix capacitive touch controller |
| **FT5206** | FocalTech capacitive touch controller |

### Resistive Touch (SPI)
| Controller | ဖော်ပြချက် |
|-----------|------------|
| **XPT2046** | Resistive touch screen controller (ADS7843 compatible) |

## GPIO Viewer

GPIO Viewer သည် web interface မှတစ်ဆင့် hardware pin များ၏ real-time အခြေအနေကို စောင့်ကြည့်နိုင်သော feature တစ်ခု ဖြစ်သည်-

- GPIO pin တစ်ခုချင်းစီ၏ အခြေအနေ (input/output/function) ကို ပြသသည်
- Pin တစ်ခုစီ၏ current value (HIGH/LOW) ကို real-time ပြသသည်
- Module configuration များကို visual ပုံစံဖြင့် ကြည့်ရှုနိုင်သည်

## HASPmota

HASPmota သည် LVGL (Light and Versatile Graphics Library) ကို အသုံးပြု၍ အဆင့်မြင့် ဂရပ်ဖစ်အင်တာဖေ့စ်များ ဖန်တီးနိုင်သော စနစ်ဖြစ်သည်-

- **LVGL** ကို အခြေခံထားသော အဆင့်မြင့် GUI framework
- Nextion နှင့် အခြား smart display panel များနှင့် တွဲဖက်အသုံးပြုနိုင်သည်
- Custom UI design များ ဖန်တီးနိုင်သည်

## Display Commands များ

| Command | ဖော်ပြချက် |
|---------|------------|
| `DisplayModel` | Display model သတ်မှတ်ခြင်း |
| `DisplayWidth` | Display width သတ်မှတ်ခြင်း |
| `DisplayMode` | Display mode (0=off, 1=on, 2=auto) သတ်မှတ်ခြင်း |
| `DisplayDimmer` | Display အတောက်အမှိန် သတ်မှတ်ခြင်း |
| `DisplayText` | Display ပေါ်တွင် စာသားပြသခြင်း |

## DisplayText Formatting Codes

`DisplayText` command တွင် အောက်ပါ formatting codes များကို အသုံးပြု၍ display layout ကို ထိန်းချုပ်နိုင်သည်-

| Code | အလုပ်လုပ်ပုံ |
|------|-------------|
| `[z]` | Display clear |
| `[i]` | Display mode သတ်မှတ်ခြင်း |
| `[x]` | X-position သတ်မှတ်ခြင်း (column) |
| `[y]` | Y-position သတ်မှတ်ခြင်း (row/page) |
| `[c]` | Text color သတ်မှတ်ခြင်း |
| `[C]` | Background color သတ်မှတ်ခြင်း |
| `[r]` | Row အလိုက် cursor ရွှေ့ခြင်း |
| `[R]` | Row အလိုက် cursor ရွှေ့ပြီး clear လုပ်ခြင်း |
| `[k]` | Column အလိုက် cursor ရွှေ့ခြင်း |
| `[K]` | Column အလိုက် cursor ရွှေ့ပြီး clear လုပ်ခြင်း |

## Web Interface

Tasmota ၏ web UI သည်-
- **Main Menu** — အဓိက configuration စာမျက်နှာများသို့ လမ်းညွှန်ချက်များ
- **Console** — Serial/Telnet ကဲ့သို့ command-line အင်တာဖေ့စ်
- **Information** — Firmware version၊ flash size၊ free memory စသည့် အချက်အလက်များ
- **Configuration** — Module၊ WiFi၊ MQTT၊ Template configuration များ
- **Tools** — Firmware upgrade၊ filesystem management စသည်များ

ဤအင်တာဖေ့စ်အမျိုးမျိုးသည် Tasmota ကို ကိရိယာတပ်ဆင်သူများနှင့် အဆုံးသုံးစွဲသူများ နှစ်ဖက်စလုံးအတွက် အဆင်ပြေစွာ အသုံးပြုနိုင်စေပါသည်။
