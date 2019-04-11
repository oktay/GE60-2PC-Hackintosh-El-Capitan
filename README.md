# MSI GE60 2PC OS X El Capitan
This is a guide for install Mac OS X El Capitan on "MSI GE60 2PC" laptop.

## Yükleme 🚀
Öncelikle BIOS ayarlarından SATA mode AHCI olarak ayarlanmalı. VT-D disable olarak ayarlanmalı EHCI Hand-off enabled. Secureboot Disable olmalı.
Yükleme için Clover bootloader kullanılmalı.
Kurulum için gerekli Boot Argümanları nv_disable=1 ve dart=0 yeterli olacaktır. Clover seçeneklerinden ise KernelPM işaretli olmalıdır.

## Araçlar ⚒
Gerekecek tüm araçlar Tool klasörü içerisinde bulunmakta.

## Kextler ⚡️
Tüm PS2 kextleri ve var ise NullCPUPowerManagment.kext dosyası silinmeli.

### ACPI Dosyaları 💡
DSDT ve SSDT dosyaları CLOVER içerisindeki ACPI/Patched yoluna atılmalı.

### Grafikler 🖥
HD4600 içerisindeki FakePCIID kextlerini yükledikten sonra HDMI çıkışını çalıştırabilmek için Yamalar kısmındaki Port değişim yaması yapılmalı.

### Ses 🔊
Ses için Auido kısmındaki HDA kextleri kullanılmalı. Jaklar otomatik çalışmıyor kulaklık takıldığında Ses ayarlarındaki Çıkış seçeneklerinden seçim yapmak gerekiyor. Sadece harici mikrofon çalışıyor.

### Touchpad ve Klavye 💻
Öncelikle tüm PS2 kextleri sildikten sonra Touchpad PS2 içerisindeki Kextleri yüklemek yeterli olacaktır.

### Batarya Göstergesi 🔋
Battery içerisindeki ACPIBatteryManager.kext dosyasını yüklemek yeterli.

### Lan 📍
Wi-Fi & Lan içerisindeki AtherosE2200Ethernet.kext dosyasını yüklemek yeterli.

> ### Wi-Fi ☁️
Wi-Fi çalışmamakta.
Benim cihazımda AR9285 takılı olduğu için. AtherosWiFiInjector.kext ve IOath3kfrmwr.kext dosyalarını yükledikten ve Yamalar kısmındaki yamayı uyguladıktan sonra çalışmakta.  

## Yamalar 💊

### Ses 🔊

| Name* | Find* [HEX] | Replace* [HEX] | Comment |
| ------ | ----------- |---------------|---------|
| AppleHDA   | 8B19D411 | 9208EC10 | t1-10.9-10.11-AppleHDA/Realtek ALC892 |
| AppleHDA   | 786D6C2E7A6C | 7A6D6C2E7A6C | t1-AppleHDA/Resources/xml>zml |
| AppleHDA   | 8319D411 | 00000000 | Realtek ALC Codec Patch |

### Grafik 🖥

| Name* | Find* [HEX] | Replace* [HEX] | Comment |
| ------ | ----------- |---------------|---------|
| AppleIntelFramebufferAzul   | 010509000004000087000000 | 030603000008000006000000 | Replace port 5 with 7 |
| AppleIntelFramebufferAzul   | 0600260A01030303000000020000300100006000 | 0600260A01030303000000020000300100009000 | 0x0a260006 9MB cursor bytes patch |
| IOGraphicsFamily | 0100007517 | 010000EB17 | Boot graphics glitch |

### Wi-Fi ☁️

| Name* | Find* [HEX] | Replace* [HEX] | Comment |
| ------ | ----------- |---------------|---------|
| AirPortAtheros40   | 0000680C2A | 0000680C2B | Patch AR9285 |
