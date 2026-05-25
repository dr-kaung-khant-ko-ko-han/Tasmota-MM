# SML အာရုံခံကိရိယာ ပံ့ပိုးမှု (SML Sensor Support)

SML (Smart Message Language) အာရုံခံကိရိယာ ပံ့ပိုးမှုသည် Tasmota တွင် utility meter များကို `XSNS_53` driver မှတစ်ဆင့် ဖတ်ယူနိုင်စေပါသည်။

## မီတာ ပမာဏ

`MAX_METERS` ဖြင့် သတ်မှတ်ထားပြီး default အားဖြင့် မီတာ **၅** ခုအထိ ပံ့ပိုးပါသည်။

## Protocol ပံ့ပိုးမှု

| Protocol | Identifier | ဖော်ပြချက် |
|----------|-----------|------------|
| **SML** | `s` | Smart Message Language — ဂျာမန် လျှပ်စစ်မီတာ စံနှုန်း |
| **OBIS** | `o` | Object Identification System — စွမ်းအင်မီတာ ဒေတာကုဒ် |
| **EBUS** | `e` | Energy Bus — အပူပေးစနစ် ဆက်သွယ်မှု |
| **VBUS** | `v` | Virtual Bus — နေရောင်ခြည်စွမ်းအင် စနစ်များ |
| **RAW** | — | Raw data stream |
| **CAN** | `C` | CAN bus (ESP32 တွင်သာ) |

## Feature Flags

| Flag | ဖော်ပြချက် |
|------|------------|
| `USE_SML_SCRIPT_CMD` | Scripter မှ SML command များ အသုံးပြုနိုင်ခြင်း |
| `USE_SML_MEDIAN_FILTER` | Median filter ဖြင့် ဒေတာချောမွေ့စေခြင်း |
| `USE_SML_DECRYPT` | AES 256-bit စာဝှက်ဖြေခြင်း ပံ့ပိုးမှု |
| `USE_SML_TCP` | Network မှတစ်ဆင့် SML ဒေတာ ဖတ်ယူနိုင်ခြင်း |
| `USE_SML_CANBUS` | CAN bus မှတစ်ဆင့် SML ဖတ်ယူခြင်း (ESP32) |

## Buffers နှင့် Configuration

- **Serial Buffer Size** — `SML_BSIZ = 48` (default)
- **Transaction Buffer** — `SML_TRX_BUFF_SIZE = 1024` (default)

## အထူး Options များ

- **Direction Bit Handling** — import/export ဒေတာအတွက် direction bit ကိုင်တွယ်မှု
- **DWS74 Fix Flags** — DWS74 မီတာအတွက် သီးသန့် ပြင်ဆင်မှု flags များ
- **Decryption Key** — 16-byte hex string အဖြစ် သတ်မှတ်ရသော AES decryption key

## စာဝှက်ဖြေခြင်း (Decryption)

`USE_SML_DECRYPT` ဖွင့်ထားပါက AES 256-bit encryption ဖြင့် စာဝှက်ထားသော SML ဒေတာများကို ဖြေနိုင်သည်။

## Scripter ပေါင်းစည်းမှု

Scripter (`>B`) သည် SML ဒေတာကို function pointer `SML_TABLE` မှတစ်ဆင့် ရယူအသုံးပြုနိုင်သည်-

| Function Pointer | ဖော်ပြချက် |
|-----------------|------------|
| `SML_SetBaud` | Baud rate သတ်မှတ်ခြင်း |
| `SML_Read` | SML ဒေတာ ဖတ်ယူခြင်း |
| `SML_Write` | SML ဒေတာ ရေးသားခြင်း |
| `SML_GetVal` | OBIS code ဖြင့် တန်ဖိုးရယူခြင်း (float) |
| `SML_GetSVal` | OBIS code ဖြင့် တန်ဖိုးရယူခြင်း (string) |
| `SML_Decode` | SML telegram decode ပြုလုပ်ခြင်း |

## OBIS Codes အသုံးများသော ဥပမာများ

| OBIS Code | ဖော်ပြချက် |
|-----------|------------|
| `1-0:1.8.0` | စွမ်းအင်သုံးစွဲမှု (import) စုစုပေါင်း |
| `1-0:2.8.0` | စွမ်းအင်ထုတ်လွှတ်မှု (export) စုစုပေါင်း |
| `1-0:16.7.0` | လက်ရှိ စုစုပေါင်းပါဝါ |
| `1-0:31.7.0` | Phase L1 လျှပ်စီးကြောင်း |
| `1-0:51.7.0` | Phase L2 လျှပ်စီးကြောင်း |
| `1-0:71.7.0` | Phase L3 လျှပ်စီးကြောင်း |

SML ပံ့ပိုးမှုသည် Tasmota ကို အထူးသဖြင့် ဥရောပတွင် အသုံးများသော smart utility meter များနှင့် တိုက်ရိုက်ချိတ်ဆက်နိုင်စေပါသည်။
