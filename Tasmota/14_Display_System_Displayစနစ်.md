# Display စနစ် (Display System)

Display စနစ်သည် LCD, OLED, e-paper, TFT ဖန်သားပြင်များအတွက် I2C, SPI, parallel, RGB အင်တာဖေ့စ်များမှတစ်ဆင့် စုစည်းထားသော framework တစ်ခုကို ပေးအပ်သည်။

## Core Classes (အဓိက Class များ)

- **Renderer** — အခြေခံ class ဖြစ်ပြီး `Adafruit_GFX` မှ အမွေဆက်ခံထားသည်။ ပုံဆွဲခြင်း၊ စာသားရေးခြင်း၊ ဂရပ်ဖစ် လုပ်ဆောင်ချက်များ ပါဝင်သည်။
- **uDisplay** — hardware အလိုက် သီးသန့်ဖြစ်ပြီး descriptor အခြေပြု configuration ဖြင့် ပြင်ဆင်သတ်မှတ်သည်။

## Supported Interfaces (ပံ့ပိုးထားသော အင်တာဖေ့စ်များ)

| အင်တာဖေ့စ် | ဖန်သားပြင်အမျိုးအစား | Chipset ဥပမာများ |
|-------------|------------------------|-------------------|
| I2C | OLED | SSD1306, SH1106 |
| SPI | TFT | ILI9341, ST7789 |
| 8-bit/16-bit Parallel | ESP32-S3 အတွက် | — |
| RGB | ESP32-S3 အတွက် | — |

## Descriptor Format (Descriptor ဖော်မတ်)

Descriptor ကို အောက်ပါ prefix များဖြင့် အသုံးပြုသည်။

| Prefix | ရှင်းလင်းချက် |
|--------|---------------|
| `:H` | Header (ခေါင်းစီး) |
| `:S` | Splash (စတင်ဖန်သားပြင်) |
| `:I` | Init (စတင်သတ်မှတ်ချက်) |
| `:A` | Address (လိပ်စာ) |
| `:R` | Rotation (လှည့်ခြင်း) |
| `:0` – `:3` | Rotation modes (လှည့်ခြင်းမုဒ် ၄ ခု) |
| `:L` | LUT (e-paper အတွက် Look-Up Table) |
| `:U` | Touch config (ထိတွေ့မှု ပြင်ဆင်သတ်မှတ်ချက်) |

### Descriptor Sources Priority (Descriptor ရင်းမြစ် ဦးစားပေးအဆင့်)

constant string → filesystem (`/display.ini`) → script → rule3 → flash

## Display Commands (Display အမိန့်များ)

- `DisplayModel` — ဖန်သားပြင်မော်ဒယ် သတ်မှတ်ခြင်း
- `DisplayWidth` — ဖန်သားပြင် အကျယ်
- `DisplayHeight` — ဖန်သားပြင် အမြင့်
- `DisplayMode` — ဖန်သားပြင်မုဒ်
- `DisplayDimmer` — အလင်းမှိန်ခြင်း

### DisplayText Escape Codes (DisplayText Escape Code များ)

| Code | လုပ်ဆောင်ချက် |
|------|---------------|
| `[z]` | မျက်နှာပြင် ရှင်းလင်းခြင်း |
| `[i]` | Invert (အရောင်ပြောင်းပြန်) |
| `[x##]` | x ကိုဩဒိနိတ် သတ်မှတ်ခြင်း |
| `[y##]` | y ကိုဩဒိနိတ် သတ်မှတ်ခြင်း |
| `[c##]` | စာသားအရောင် |
| `[C##]` | နောက်ခံအရောင် |
| `[B##]` | နောက်ခံဖြည့်ခြင်း |
| `[p##]` | စာသားအနေအထား |
| `[r##,##]` | စတုဂံဆွဲခြင်း |
| `[R##,##]` | စတုဂံဖြည့်ဆွဲခြင်း |
| `[k##]` | စာသားဖောင့်အရွယ် |
| `[K##]` | စာသားဖောင့်မိသားစု |
| `[h##]` | အလျားလိုက်မျဉ်းဆွဲခြင်း |
| `[v##]` | ဒေါင်လိုက်မျဉ်းဆွဲခြင်း |
| `[L##,##]` | မျဉ်းဆွဲခြင်း |

## Multi-Display Support (ဖန်သားပြင်မျိုးစုံ ပံ့ပိုးမှု)

ဖန်သားပြင် ၃ ခုအထိ တစ်ပြိုင်နက် ပံ့ပိုးနိုင်သည်။

## Touch Controllers (ထိတွေ့ကိရိယာများ)

| Controller | အမျိုးအစား | အင်တာဖေ့စ် |
|------------|-------------|------------|
| GT911 | Capacitive | I2C |
| FT5206 | Capacitive | I2C |
| XPT2046 | Resistive | SPI |
| 4-wire Resistive | Resistive | ESP32-S3 ပေါ်ရှိ ဝါယာ ၄ ခု |
