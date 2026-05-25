# HASPmota အင်တာဖေ့စ် (HASPmota Interface)

HASPmota သည် OpenHASP နှင့် တွဲဖက်အသုံးပြုနိုင်သော compatibility layer ဖြစ်ပြီး LVGL ကို အသုံးပြု၍ အဆင့်မြင့် GUI ကို ပံ့ပိုးပေးသည်။ ထိတွေ့တုံ့ပြန်နိုင်သော ဖန်သားပြင်များကို declarative JSONL definitions နှင့် Berry scripting တို့ဖြင့် အသုံးပြုနိုင်သည်။

## Core Classes (အဓိက Class များ)

### lvh_root
အခြေခံ class ဖြစ်ပြီး အောက်ပါတို့ ပါဝင်သည်။
- Rule engine (စည်းမျဉ်းအင်ဂျင်)
- Color parsing (အရောင် ခွဲခြမ်းစိတ်ဖြာခြင်း)
- Font handling (ဖောင့် ကိုင်တွယ်ခြင်း)

### lvh_obj
အဓိက UI object ဖြစ်ပြီး အောက်ပါတို့ ပါဝင်သည်။
- Event handling (ဖြစ်ရပ် ကိုင်တွယ်ခြင်း)
- LVGL wrapping

## Screen Protection (ဖန်သားပြင် ကာကွယ်မှု)

| Feature | ရှင်းလင်းချက် |
|---------|---------------|
| **Antiburn** | ဖန်သားပြင် မီးလောင်ခြင်းမှ ကာကွယ်ရန် အရောင်များကို လည်ပတ်ပြောင်းလဲပေးသည် |
| **DimmedPanel** | ဖန်သားပြင်ကို မှိန်ချပေးသော အကန့် |

## Rule Types (စည်းမျဉ်း အမျိုးအစားများ)

| Rule Type | ရှင်းလင်းချက် |
|-----------|---------------|
| `val_rule` | ဂဏန်းတန်ဖိုး အပ်ဒိတ်များ |
| `val_rule_formula` | တန်ဖိုး ပြောင်းလဲခြင်း (value transformation) |
| `text_rule` | စာသား အပ်ဒိတ်များ |
| `text_rule_format` | ဖော်မတ်ချထားသော အထွက်စာသား |

## Event Mapping (ဖြစ်ရပ် မြေပုံထုတ်ခြင်း)

LVGL ဖြစ်ရပ်များကို JSON ဖော်မတ်ဖြင့် Tasmota ၏ rule system သို့ publish လုပ်သည်။

## Color Formats (အရောင်ဖော်မတ်များ)

| ဖော်မတ် | ဥပမာ |
|----------|------|
| Hex | `#RRGGBB` (ဥပမာ `#FF0000`) |
| Named colors | `red`, `blue`, `green` စသည် |
| Default | `0x000000` (အနက်ရောင်) |

## Font Hierarchy (ဖောင့်အဆင့်ဆင့်)

embedded fonts → TTF files → binary fonts

နဂိုပါဝင်သော ဖောင့်များကို ဦးစားပေးအသုံးပြုပြီး၊ မရှိပါက TTF ဖိုင်များကို ရှာဖွေကာ နောက်ဆုံးတွင် binary ဖောင့်များကို အသုံးပြုသည်။

## Widget Classes (Widget Class များ)

| Class | ရှင်းလင်းချက် |
|-------|---------------|
| `lvh_label` | စာသားတံဆိပ် |
| `lvh_btn` | ခလုတ် |
| `lvh_slider` | ဆလိုက်ဒါ |
| `lvh_chart` | ဇယား/ဂရပ်ဖ် |
| `lvh_btnmatrix` | ခလုတ်အကွက် |
| `lvh_dropdown` | Dropdown စာရင်း |
| `lvh_arc` | အဝိုင်းပိုင်း gauge |

## Berry Solidification

Berry code ကို စွမ်းဆောင်ရည်မြင့်မားစေရန် C structures အဖြစ်သို့ compile လုပ်ပေးသည်။ ၎င်းကို solidification ဟု ခေါ်ဆိုပြီး run-time တွင် parsing overhead ကို လျှော့ချပေးသည်။
