# MQTT ပေါင်းစည်းမှု (MQTT Integration)

MQTT သည် Tasmota ၏ အဓိက IoT ဆက်သွယ်ရေး protocol ဖြစ်သည်။ ၎င်းသည် lightweight publish/subscribe messaging protocol ဖြစ်ပြီး low-bandwidth၊ high-latency သို့မဟုတ် unreliable network များအတွက် ဒီဇိုင်းထုတ်ထားသည်။

## Core Driver

MQTT အဓိက driver ကို `xdrv_02_9_mqtt.ino` တွင် အကောင်အထည်ဖော်ထားသည်။ `Mqtt` struct သည် connection state၊ topic configuration၊ last will testament (LWT)၊ နှင့် message queue များကို စီမံခန့်ခွဲသည်။

## Topic စနစ်

Topic စနစ်သည် `%prefix%` နှင့် `%topic%` placeholder များကို အသုံးပြုကာ `GetTopic_P` function မှတစ်ဆင့် topic string များ တည်ဆောက်သည်။

### Prefix အမျိုးအစားများ

| Prefix | အမျိုးအစား | ရည်ရွယ်ချက် |
|--------|------------|-------------|
| `cmnd` | Command | စက်ပစ္စည်းသို့ command ပို့ရန် |
| `stat` | Status | Command ရလဒ်ကို ပြန်ကြားရန် |
| `tele` | Telemetry | အလိုအလျောက် ဒေတာပို့ရန် |

### Default Topic Pattern

```
cmnd/tasmota/POWER
stat/tasmota/POWER
tele/tasmota/STATE
```

## ဆက်သွယ်မှု သတ်မှတ်ချက်များ

MQTT ဆက်သွယ်မှုအတွက် အောက်ပါ setting များကို သတ်မှတ်ရသည်:

| Setting | ဖော်ပြချက် |
|---------|------------|
| `mqtt_host` | MQTT broker ၏ hostname သို့မဟုတ် IP လိပ်စာ |
| `mqtt_port` | MQTT broker ၏ port (default: 1883) |
| `mqtt_user` | Broker authentication အတွက် username |
| `mqtt_password` | Broker authentication အတွက် password |
| `mqtt_topic` | Device ၏ topic identifier |

## TLS Encryption

`USE_MQTT_TLS` compile-time option ဖြင့် MQTT over TLS (MQTTS) ကို အသုံးပြုနိုင်သည်။ Fingerprint validation နှင့် CA certificate verification တို့ကို ပံ့ပိုးထားသည်။ Port 8883 ကို default အဖြစ် အသုံးပြုသည်။

## Azure IoT Integration

Azure IoT Hub သို့ Device Provisioning Service (DPS) မှတစ်ဆင့် ချိတ်ဆက်နိုင်သည်။ X.509 certificate authentication ဖြင့် secure device provisioning ကို ပံ့ပိုးထားသည်။

## အဆင့်မြင့် လုပ်ဆောင်ချက်များ

### File Transfer

`FileUpload` နှင့် `FileDownload` command များမှတစ်ဆင့် MQTT protocol ကိုအသုံးပြု၍ file transfer ပြုလုပ်နိုင်သည်။ Configuration file များ၊ template များနှင့် Berry script များကို MQTT မှတစ်ဆင့် ဖလှယ်နိုင်သည်။

### Retained Messages

`PowerRetain` နှင့် `SensorRetain` option များဖြင့် MQTT retained messages ကို configure လုပ်နိုင်သည်။ Retained messages များသည် broker တွင် သိမ်းဆည်းထားပြီး client အသစ်တစ်ခု subscribe လုပ်သည့်အခါ ချက်ချင်းပို့ဆောင်ပေးသည်။

## SetOption Flags

MQTT အပြုအမူကို ထိန်းချုပ်ရန် အောက်ပါ `SetOption` flags များကို အသုံးပြုသည်:

| SetOption | ဖော်ပြချက် |
|-----------|------------|
| `SetOption3` | MQTT protocol ကို enable/disable လုပ်သည် |
| `SetOption4` | MQTT response ကို `%topic%` မပါဝင်စေဘဲ ပြန်ကြားစေသည် |
| `SetOption90` | Non-JSON MQTT messages များကို disable လုပ်ကာ JSON-only mode သို့ ပြောင်းသည် |
