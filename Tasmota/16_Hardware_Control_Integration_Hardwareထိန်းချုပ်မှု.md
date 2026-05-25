# Hardware ထိန်းချုပ်မှုနှင့် ပေါင်းစည်းမှု (Hardware Control & Integration)

Hardware ထိန်းချုပ်မှုသည် XDRV (ထိန်းချုပ်ခြင်း) နှင့် XSNS (အာရုံခံခြင်း) modular architecture ကို အသုံးပြုသည်။

## GPIO — အခြေခံအင်တာဖေ့စ်

GPIO သည် relay များ၊ ခလုတ်များ၊ LED များ၊ PWM အတွက် အခြေခံ အင်တာဖေ့စ် ဖြစ်သည်။

## I2C Communication (I2C ဆက်သွယ်ရေး)

| Function | ရှင်းလင်းချက် |
|----------|---------------|
| `I2cBegin(sda, scl, bus, frequency)` | I2C bus စတင်သတ်မှတ်ခြင်း |
| `I2cSetBus(bus)` | Bus နံပါတ် သတ်မှတ်ခြင်း |
| `I2cValidRead` | မှန်ကန်သော ဖတ်ယူမှုရှိမရှိ စစ်ဆေးခြင်း |
| `I2cWrite` | I2C မှတစ်ဆင့် ဒေတာ ရေးသားခြင်း |
| `I2cScan` | I2C bus ပေါ်ရှိ ကိရိယာများကို စကင်ဖတ်ခြင်း |

## Major Systems (အဓိက စနစ်များ)

### Shutter Control (ရှပ်တာ ထိန်းချုပ်မှု)
- ESP32 တွင် ရှပ်တာ ၁၆ ခုအထိ ထိန်းချုပ်နိုင်
- Position calibration (အနေအထား ချိန်ညှိခြင်း)
- Tilt control (စောင်းချိန်ညှိခြင်း)

### DALI Lighting (DALI အလင်းရောင်)
- Command/query operations
- Groups (အုပ်စုများ)
- Brightness (အလင်းအား ထိန်းချုပ်ခြင်း)

### Energy Monitoring (စွမ်းအင် စောင့်ကြည့်ခြင်း)
သီးသန့်စာမျက်နှာတွင် အသေးစိတ် ကြည့်ရှုနိုင်သည်။

## External Integration (ပြင်ပစနစ် ပေါင်းစည်းမှု)

| စနစ် | ရှင်းလင်းချက် |
|------|---------------|
| **Modbus** | စက်မှုကိရိယာများနှင့် ဆက်သွယ်ရန်၊ configurable JSON ဖြင့် ပြင်ဆင်နိုင် |
| **Sonoff Devices** | SPM, TM1621 LCD ကိရိယာများ ပံ့ပိုးမှု |
| **Webcam** | ESP32 ပေါ်တွင် OV2640 အသုံးပြု၍ HTTP streaming, RTSP, motion detection |

## Environmental Sensors (ပတ်ဝန်းကျင် အာရုံခံကိရိယာများ)

I2C မှတစ်ဆင့် BMP/BME series အာရုံခံကိရိယာများ (ဥပမာ BME280, BMP280) — auto-detection (အလိုအလျောက်ရှာဖွေခြင်း) နှင့် အချိန်မှန်ဖတ်ယူခြင်း (regular polling) တို့ ပံ့ပိုးထားသည်။

## Rules for Automation (Automation အတွက် စည်းမျဉ်းများ)

- Sensor readings ပေါ်မူတည်၍ trigger ဖြစ်စေခြင်း
- အချိန်ဇယားဖြင့် လုပ်ဆောင်ချက်များ စီစဉ်ခြင်း
- Conditional logic (အခြေအနေအလိုက် ယုတ္တိဗေဒ)

## Home Assistant Discovery

MQTT မှတစ်ဆင့် Home Assistant တွင် အလိုအလျောက် discovery ပြုလုပ်နိုင်သည်။
