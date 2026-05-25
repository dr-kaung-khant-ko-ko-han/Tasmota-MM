# ဆက်သွယ်ရေးပရိုတိုကောများ (Communication Protocols)

Tasmota ၏ ဆက်သွယ်ရေးစနစ်သည် IoT စက်ပစ္စည်းများအား protocol အမျိုးမျိုးမှတစ်ဆင့် အပြန်အလှန် ဆက်သွယ်နိုင်စေသည်။ Modular driver framework သည် protocol implementation ကို message processing မှ ခွဲခြားပေးထားသည်။

## အဓိကအစိတ်အပိုင်းများ

### Command Processing Pipeline

Command processing pipeline သည် source အမျိုးမျိုးမှ ဝင်လာသော command များကို တစ်ပြေးညီ process လုပ်ပေးသည်။ Protocol driver တစ်ခုချင်းစီသည် incoming data ကို command format အဖြစ် ဘာသာပြန်ပေးပြီး central command handler သို့ ပို့ဆောင်သည်။

### Network Connectivity Management

WiFi၊ Ethernet၊ DNS နှင့် DHCP အပါအဝင် network connectivity ကို စီမံခန့်ခွဲသည်။ Multi-SSID fallback၊ static IP configuration၊ နှင့် hostname resolution တို့ကို ပံ့ပိုးထားသည်။

### MQTT Protocol

MQTT protocol ကို `xdrv_02_mqtt` driver မှတစ်ဆင့် အကောင်အထည်ဖော်ထားသည်။ Configurable topic template များဖြင့် publish/subscribe model ကို အသုံးပြုသည်။ TLS encryption၊ retained messages နှင့် birth/will messages များကို ပံ့ပိုးထားသည်။

### HTTP Web Server

HTTP web server ကို `xdrv_01_webserver` driver မှတစ်ဆင့် အကောင်အထည်ဖော်ထားသည်။ `WebServerDispatch[]` dispatch table ကို အသုံးပြု၍ URL path များကို handler function များနှင့် ချိတ်ဆက်ပေးသည်။ Web UI၊ REST API၊ နှင့် file serving တို့ကို ပံ့ပိုးပေးသည်။

### Serial Bridge

Serial bridge သည် MQTT နှင့် serial port အကြား transparent forwarding ပြုလုပ်ပေးသည်။ ဤနည်းအားဖြင့် serial-only စက်ပစ္စည်းများကို MQTT network တွင် ပေါင်းစည်းနိုင်သည်။

### Modbus Support

Modbus protocol (RTU နှင့် TCP) ကို ပံ့ပိုးထားပြီး industrial sensor များနှင့် actuator များနှင့် ဆက်သွယ်နိုင်သည်။ Modbus register mapping ကို configuration ပြုလုပ်နိုင်ပြီး Tasmota command system နှင့် ပေါင်းစည်းထားသည်။

### WiFi Management

WiFi network scanning ကို `WifiBegin()` နှင့် `WifiBeginAfterScan()` function များမှတစ်ဆင့် လုပ်ဆောင်သည်။ `WifiBeginAfterScan()` သည် ရရှိနိုင်သော network များကို scan လုပ်ပြီး configured SSID များထဲမှ အကောင်းဆုံးရွေးချယ်ချိတ်ဆက်သည်။ WiFi signal strength monitoring၊ auto-reconnect နှင့် WiFi power-saving mode များကိုလည်း ပံ့ပိုးထားသည်။
