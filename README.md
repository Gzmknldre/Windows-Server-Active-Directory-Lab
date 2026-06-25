# Windows-Server-Active-Directory-Lab
Bir şirketin Ankara merkez ofisi için Active Directory altyapısının kurulması.
## 🌐 Network ve TCP/IP Topolojisi

Sistemlerin birbiriyle güvenli ve kararlı çalışabilmesi için uygulanan network ve IP adresleme planı şu şekildedir:

| Cihaz / Rol | İşletim Sistemi | IP Adresi | Alt Ağ Maskesi (Subnet) | Varsayılan Ağ Geçidi (GW) | DNS Adresi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Primary Domain Controller (DC)** | Windows Server | 192.168.10.10 | 255.255.255.0 (/24) | 192.168.10.1 | 127.0.0.1 (Loopback) |
| **DHCP Server** | Windows Server | 192.168.10.10 | 255.255.255.0 (/24) | 192.168.10.1 | 127.0.0.1 |
| **Client / Kullanıcı Bilgisayarı**| Windows 10/11 Pro | DHCP (Dinamik) | 255.255.255.0 (/24) | 192.168.10.1 | 192.168.10.10 |

### Network Servis Detayları:
* **DNS (Domain Name System):** Active Directory entegre DNS kurulmuştur. Forward ve Reverse Lookup Zone tanımlamaları yapılandırılmıştır.
* **DHCP Dağıtım Aralığı (Scope):** `192.168.10.50` - `192.168.10.200` arası dinamik olarak dağıtılmaktadır. Server ve network cihazları için `192.168.10.1` - `192.168.10.49` arası statik kullanım için rezerve edilmiştir.

---

## 🏛️ Active Directory ve OU (Organizational Unit) Mimarisi

Şirket hiyerarşisini mantıksal bir düzende yönetmek ve yetkilendirmeleri kolaylaştırmak adına kurulan OU yapısı:

```text
[Sanal Sirket Mimarisi] (Root Domain)
└── Ankara-Merkez (Merkez OU)
    ├── Departmanlar
    │   ├── Bilgi İşlem (IT)
    │   ├── Mühendislik
    │   └── İnsan Kaynakları (HR)
    ├── Kullanicilar (Kullanıcı Hesapları)
    └── Bilgisayarlar (Domain'e Bağlı Clientlar)
