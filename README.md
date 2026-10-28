
# 🌐 Segmented Enterprise Network — CCNA Enterprise Lab
<img width="920" height="391" alt="Ekran görüntüsü 2026-10-28 154736" src="https://github.com/user-attachments/assets/e8c24c77-09a1-4a9e-89b7-3bc6e15936e4" />

**VLAN Segmentation · Inter-VLAN Routing · OSPF · WAN · DMZ Concepts**

Cisco CCNA 200-301 konularını kurumsal ağ senaryosu üzerinden çalışmak için hazırladığım laboratuvar ve ağ mimarisi dokümantasyonu. Hedefim; merkez ofis, dağıtım/erişim katmanları ve uzak şubeler arasındaki iletişimi tasarlamak, yapılandırmaları incelemek ve ağ sorunlarını sistematik biçimde gidermek.

> **Not:** Aşağıdaki Packet Tracer görüntüsü, paylaştığım **referans kurumsal ağ topolojisidir**. Görselde yer alan tüm protokollerin kendi PingMyNetwork Sandbox laboratuvarımda eksiksiz çalıştığı bu ekran görüntüsünden doğrulanamaz. Gerçek yapılandırma ve test çıktıları ayrıca kontrol edilmelidir.

## 🗺️ Ağ topolojisi

![Cisco Packet Tracer enterprise network topology](topology.png)

Görselde merkez (HQ), iki şube (BRA1, BRA2), çok katmanlı anahtarlar, erişim anahtarları ve farklı VLAN'larda uç cihazlar yer alır.

## 🏢 Mimari

### Merkez ofis (HQ)

- **R1 ve R2:** WAN/uç yönlendirme cihazları.
- **MLS4 ve MLS5:** Dağıtım/çekirdek rolünde çok katmanlı anahtarlar.
- **SW1, SW2, SW3:** Kullanıcı ve sunucuların bağlandığı erişim anahtarları.
- **SRV7 (1.1.1.1):** Topolojide gösterilen dış servis/test sunucusu.

### Şubeler

- **BRA1:** R3 ve SW6; VLAN 40 ve VLAN 50 uç cihazları.
- **BRA2:** R4 ve SW7; VLAN 60 uç cihazları.
- WAN bağlantıları çizimde /30 nokta-nokta ağları ile temsil edilir.

## 📋 VLAN ve IPv4 planı

| Konum | VLAN | Amaç / uç cihazlar | Ağ |
|---|---:|---|---|
| HQ | 10 | PC1, PC5 | `192.168.10.0/25` |
| HQ | 20 | PC2, PC3 | `192.168.20.0/26` |
| HQ | 30 | SRV4, SRV6 | `192.168.30.0/27` |
| BRA1 | 40 | PC8 | `192.168.40.0/29` |
| BRA1 | 50 | PC9 | `192.168.50.0/29` |
| BRA2 | 60 | Laptop0, Laptop1 | `192.168.60.0/29` |

**Görselde etiketlenen WAN ağları:** `172.16.0.0/30`, `172.16.0.4/30`, `172.16.0.8/30`, `172.16.0.12/30`, `172.16.0.16/30`.

## 🛠️ İncelenen teknolojiler

| Teknoloji | Laboratuvardaki çalışma konusu |
|---|---|
| VLAN / 802.1Q | Erişim portları, trunk bağlantıları ve segmentasyon |
| Inter-VLAN Routing | Farklı VLAN'lar arasında Layer 3 iletişim |
| OSPFv2 | Dinamik yönlendirme ve komşuluk kontrolü |
| VLSM / IPv4 | Alt ağ planlama ve IP adresleme |
| EtherChannel / STP | Yedeklilik ve Layer 2 döngü kontrolü |
| HSRP | Varsayılan ağ geçidi yedekliliği kavramı |
| NAT/PAT | Özel IP adreslerinin dış ağa erişimi |
| DHCP Relay | Farklı alt ağlarda otomatik IP dağıtımı |
| DMZ / ACL | Sunucu ağı segmentasyonu ve erişim kontrolü |

Bu başlıklar bir **öğrenme ve doğrulama kapsamıdır**; uygulanmış özelliklerin kesin listesi için cihaz konfigürasyonları incelenmelidir. DMZ yalnızca ayrı bir subnet değildir; erişim politikalarıyla desteklenmesi gerekir.

## ✅ Doğrulama ve testler

Aşağıdaki komutlar Cisco IOS ortamında, ilgili cihazın özelliklerine göre kullanılabilir:

```text
show ip interface brief
show ip route
show ip ospf neighbor
show ip route ospf
show vlan brief
show interfaces trunk
show spanning-tree
show etherchannel summary
show standby brief
show ip nat translations
```

**Kontrol senaryoları:**

1. Aynı VLAN içindeki cihazların haberleşmesini test et.
2. Farklı VLAN'lardan hedef IP'lere `ping` gönder.
3. OSPF komşuluklarını ve öğrenilen rotaları doğrula.
4. HQ–BRA1–BRA2 arasındaki yönlendirme yolunu `traceroute` ile incele.
5. Güvenlik politikası varsa yetkili/yetkisiz erişimi ayrı ayrı test et.
6. Link yedekliliği yapılandırılmışsa bağlantı kesintisi senaryosunu dene.

> **Test sonuçları:** Bu depoda henüz CLI çıktıları veya doğrulanmış başarı raporu bulunmuyorsa testlerin geçtiği varsayılmamalıdır.

## 🚀 Nasıl kullanılır?

1. Depoyu indir veya klonla.
2. Varsa `.pkt` dosyasını **Cisco Packet Tracer** ile; PingMyNetwork laboratuvar dosyasını kendi desteklediği ortamda aç.
3. `topology.png` üzerinden cihaz ve ağ segmentlerini incele.
4. Cihaz konfigürasyonlarını kontrol et ve yukarıdaki doğrulama testlerini gerçekleştir.
5. Gözlemlerini, çözümlerini ve gerekli ekran görüntülerini dokümante et.

## 👨‍💻 Hazırlayan

**Ferdi Birgül**  
IT Support · Network Infrastructure · Cybersecurity  
GitHub: [@Ferdibrgll](https://github.com/Ferdibrgll)

*Eğitim, laboratuvar pratiği ve teknik dokümantasyon amacıyla hazırlanmıştır.*
