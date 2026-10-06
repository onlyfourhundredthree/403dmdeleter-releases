<div align="center">

<img src="./src/assets/icon.png" alt="403 DM Deleter Logo" width="130" style="border-radius: 28px; box-shadow: 0 12px 35px rgba(46, 109, 255, 0.45); margin-bottom: 16px;" />

# ⚡ 403 DM Deleter ⚡

**Gelişmiş Masaüstü Discord Gizlilik, Mesaj Temizleme, Medya Kasası ve Hayalet Mesaj Arşivleyicisi**  
*Ultra-fast, native, lightweight & rate-limit protected Discord privacy & management suite powered by Tauri v2 & Rust.*

<p align="center">
  <a href="https://github.com/onlyfourhundredthree/403dmdeleter-releases/releases"><img src="https://img.shields.io/github/v/release/onlyfourhundredthree/403dmdeleter-releases?style=for-the-badge&color=2e6dff&label=v1.0.60%20(Latest)" alt="Latest Release" /></a>
  <a href="https://tauri.app/"><img src="https://img.shields.io/badge/Tauri_v2-Rust_Powered-24C8DB?style=for-the-badge&logo=tauri&logoColor=white" alt="Tauri v2" /></a>
  <a href="https://react.dev/"><img src="https://img.shields.io/badge/React_18-TypeScript-61DAFB?style=for-the-badge&logo=react&logoColor=black" alt="React 18" /></a>
  <a href="https://tailwindcss.com/"><img src="https://img.shields.io/badge/Tailwind_CSS-Design_Tokens-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white" alt="Tailwind CSS" /></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/Lisans-MIT-a855f7?style=for-the-badge" alt="License" /></a>
</p>

<p align="center">
  <a href="#-genel-bakış-overview">Genel Bakış</a> •
  <a href="#-temel-özellikler-features">Özellikler</a> •
  <a href="#-modül-detayları">Modül Detayları</a> •
  <a href="#-teknoloji-mimarisi-tech-stack">Mimari</a> •
  <a href="#-kurulum--geliştirici-rehberi-installation">Kurulum</a> •
  <a href="#-otomatik-yayınlama-sistemi-release-pipeline">Yayınlama</a> •
  <a href="#-güvenlik--yasal-uyarı-disclaimer">Güvenlik & Yasal Uyarı</a>
</p>

</div>

---

## 📖 Genel Bakış (Overview)

**403 DM Deleter**, yüzlerce megabayt RAM harcayan hantal tarayıcı eklentileri ve Electron scriptlerinin aksine; **Rust ve Tauri v2** mimarisiyle inşa edilmiş bağımsız, hafif ve üstün performanslı bir masaüstü Discord yönetim aracıdır.

- 🚀 **Ultra Düşük Kaynak Tüketimi:** Ortalama yalnızca **~35-45 MB RAM** ile sessizce çalışır.
- 🛡️ **Akıllı Hız Limiti Koruması:** Discord'un `X-RateLimit-Reset` ve `Retry-After` yanıtlarını milisaniyelik hassasiyetle yöneterek hesabınızı korur.
- 🎨 **Sıfırdan Tasarlanan UX/UI Sistemi:** Özelleştirilebilir cam teması (glassmorphism), özel duvar kağıdı motoru ve dinamik renk paletleri.
- 🔒 **Sıfır Dış Sunucu Bağımlılığı:** Tokenleriniz, mesaj geçmişiniz ve ayarlarınız asla üçüncü parti bir sunucuya iletilmez; tamamıyla yerel makinenizde saklanır.

---

## 🌟 Temel Özellikler (Features)

| Modül | Açıklama |
| :--- | :--- |
| 🧹 **Akıllı Mesaj Temizleyici** | DM'ler, Grup Konuşmaları ve Sunucu kanallarındaki mesajlarınızı akıllı filtreler, gecikme jitter'ı ve hayalet düzenleme (ghost edit) ile siler. |
| 🚫 **Gelişmiş Hayalet Mesaj (Sniper)** | WebSocket Gateway üzerinden silinen/düzenlenen mesajları anında yakalar. Kalıcı önbellek motoruyla oturum başlamadan önceki mesajları dahi tespit eder. |
| 🏰 **Sunucu (Guild) Yönetimi** | Rol/Yetki filtreleri (Sahip, Yönetici, Üye), ikon filtreleri ve tek tıkla toplu sunucudan ayrılma/silme mekanizması. |
| 👥 **Gelişmiş İlişki & Arkadaş Yöneticisi** | Rozet/Nitro durumu, avatar durumu, Snowflake ID yaş sıralaması ve tek tıkla toplu istek/engel yönetimi. |
| 🎙️ **Sesli Mesaj Kasası (Voice Vault)** | DM'lerdeki ses kayıtlarını (`.ogg`, `.mp3`) ayıklar; oynatma hızı (1x - 2x) ve ekolayzır animasyonlu dahili çalarla dinletip yerel diske arşivler. |
| 🖼️ **Medya Kasası & Galeri** | Sohbetteki tüm görselleri ve videoları toplar; tam ekran Lightbox ile inceler ve orijinal kalitede toplu olarak indirir. |
| 🎭 **Tepki Temizleyici (Reactions)** | Konuşmalarda bıraktığınız tüm emoji tepkilerini tespit edip otomatik olarak temizler. |
| 🎨 **Özel Tema & Duvar Kağıdı Motoru** | Kendi renk paletinizi oluşturun, özel arka plan görseli ekleyin; şeffaflık (%15-%95) ve bulanıklık (blur) ayarıyla cam efekti uygulayın. |
| 📊 **Discord Wrapped & İnfografik** | Sohbet analitiği üretir; en çok kullanılan kelimeleri ve saatlik aktivite grafiğini 1080x1350 PNG hikaye kartı olarak dışa aktarır. |
| 🔔 **Webhook Bildirimleri & HTML Yedek** | Silme operasyonlarının sonuçlarını belirlediğiniz Discord Webhook'una şık embed olarak iletir ve sohbeti Discord arayüzü görünümünde HTML olarak yedekler. |

---

## 🔍 Modül Detayları

### 🧹 1. Akıllı Mesaj Temizleyici
* **Dinamik Hız Limiti Yönetimi:** Discord API'sinin 429 yanıtlarını otomatik olarak yakalar ve kısıtlamaya uğramadan en ideal silme hızını korur.
* **İnsansı Rastgele Gecikme (Jitter Delay):** İstekler arasına ±200ms doğal insan dalgalanması serpiştirerek bot tespit algoritmalarını bertaraf eder.
* **Hayalet Düzenleme (Ghost Edit):** Mesaj silinmeden hemen önce içeriğini `.` veya boş karakterle güncelleyerek Discord önbelleklerinde eski mesajın kalmasını engeller.
* **Sabitlenmiş Mesajları Koruma (Keep Pinned):** Yıldızlanan / iğnelenen mesajları otomatik korur.
* **Grup DM Desteği:** Çoklu katılımcılı grup sohbetlerini tam isim, katılımcı sayısı ve grup simgeleriyle sorunsuz listeler ve temizler.
* **Akıllı Filtre Şablonları:**
  * 🤖 *Bot Komutları:* `!`, `/`, `.`, `?`, `-`, `$` gibi önekli komutları hedefler.
  * 🖼️ *Sadece Medya:* Fotoğraf, video ve dosya eklerini hedefler.
  * 🔗 *Sadece Bağlantılar:* URL ve Discord davet linklerini hedefler.
  * 📝 *Sadece Metin:* Medyasız salt metin mesajlarını seçer.

---

### 🚫 2. Gelişmiş Hayalet Mesaj (Sniper) & Önbellek Motoru
* **Canlı Gateway Dinleyicisi:** `wss://gateway.discord.gg` WebSocket hattına bağlanarak gerçek zamanlı mesaj akışını izler.
* **Kalıcı Önbellek (Persistent Cache):** Yakalanan ve taranan son 5.000 mesaj `localStorage` üzerinde saklanır; uygulama yeniden başlatılsa bile önbellek kaybolmaz.
* **Oturum Başlamadan Önce Silinen Mesajları Yakalama:**
  * Oturum açıldığında aktif DM kanallarını arka planda otomatik önbelleğe alır.
  * **"Geçmiş Mesajları Tara"** butonuyla açık konuşmaların geçmiş 50-100 mesajını tek tıkla hafızaya çekerek, sonradan silinen eski mesajların da yakalanmasını sağlar.
* **Kapsam ve Bildirim Filtreleri:**
  * Kapsam: *Tümü*, *Yalnızca DM'ler* veya *Yalnızca Sunucular*.
  * Sesli Uyarı ve Masaüstü Bildirimi seçeneklerini bağımsız açıp kapatabilme.
* **HTML Raporu:** Silinen ve düzenlenen tüm mesajları yazar bilgisi, zaman damgası ve ekleriyle birlikte tek tıkla HTML formatında dışa aktarma.

---

### 🏰 3. Sunucu (Guild) Yönetimi & Gelişmiş Filtreleme
* **Rol ve Yetki Filtreleri:**
  * 👑 *Sunucu Sahibi Olduklarım (Owner)*
  * 🛡️ *Yönetici / Admin Yetkim Olanlar*
  * 👤 *Normal Üye Olduğum Sunucular*
* **İkon Filtreleri:** Yalnızca özel ikonu olan sunucuları veya varsayılan harf simgeli ikonsuz sunucuları listeleme.
* **Akıllı Sıralama:** Sunucu adı (A-Z / Z-A), En Yeni Sunucu (Snowflake ID'ye göre) ve En Eski Sunucu.
* **Hızlı Seçim Kısayolları:**
  * ⚡ *Sahip Olmadıklarım:* Sahip olmadığınız tüm sunucuları tek tıkla seçerek toplu çıkış yapmayı kolaylaştırır.
  * 👤 *Normal Üyeler:* Yetkinizin olmadığı sunucuları otomatik işaretler.
  * 🔘 *İkonsuzlar:* Görseli bulunmayan sunucuları ayıklar.
  * 🔄 *Seçimi Tersine Çevir:* Seçilen ve seçilmeyen sunucuları yer değiştirir.

---

### 👥 4. Gelişmiş İlişki & Arkadaş Yöneticisi
* **Rozet & Nitro Filtreleri:** Nitro kullanıcıları, HypeSquad üyeleri, Erken Destekçi ve Onaylı Bot Geliştiricisi rozetlerine sahip arkadaşları filtreleme.
* **İsim Türü Filtresi:** Özel Takma Ad (Display Name) kullananlar ile orijinal kullanıcı adını kullananları ayırma.
* **Hesap Yaşı Sıralaması:** Snowflake ID algoritmasıyla arkadaş listenizi hesap oluşturulma tarihine göre (En Yeni / En Eski) kronolojik sıralama.
* **Toplu İlişki Aksiyonları:**
  * Bekleyen gelen arkadaşlık isteklerini toplu reddetme.
  * Giden tüm arkadaşlık isteklerini tek tıkla iptal etme.
  * Engellenen kullanıcılar listesini toplu olarak açma.
  * Silmeden önce arkadaş listenizi Discord HTML biçiminde yedekleme.

---

### 🎨 5. Özel Tema Motoru & Duvar Kağıdı (Glassmorphism)
* **3 Sekmeli Tema Stüdyosu:**
  * 🎨 **Renk Paleti:** Canvas, Primary ve Accent renklerini canlı Color Picker veya Hex kodu ile belirleme.
  * 🖼️ **Arka Plan & Duvar Kağıdı:** Küratörlü hazır duvar kağıtları (Cyberpunk, Midnight Neon, Deep Space, Abstract Minimal) veya harici görsel URL'si ekleme.
  * 💾 **Kayıtlı Temalar:** Kendi tasarladığınız temaları isim vererek kaydetme ve tek tıkla geri yükleme.
* **Cam Şeffaflığı & Bulanıklık:** Duvar kağıdı aktifken arka plan opaklığını (%15 - %95) ve arka plan bulanıklığını (0px - 16px Blur) gerçek zamanlı kaydırıcılarla ayarlayabilme.
* **Donanım Hızlandırmalı Geçişler:** CSS Transform ve hardware-accelerated geçişler sayesinde sıfır layout kayması ve akıcı UI deneyimi.

---

### 🎙️ 6. Sesli Mesaj Kasası (Voice Vault)
* DM veya Grup konuşmalarındaki tüm sesli mesajları anında tespit eder.
* Entegre oynatıcı ile dinleme imkanı:
  * Oynatma / Duraklatma ve hassas süre kaydırıcı (Seekbar).
  * Hızlandırılmış dinleme çarpanları: **1.0x**, **1.25x**, **1.5x**, **2.0x**.
  * Dinleme anında canlı ses dalgası (Waveform/Equalizer) animasyonu.
* Seçilen veya tüm ses kayıtlarını tek tıkla `Belgeler/403Deleter/VoiceMessages/` klasörüne orijinal formatında kaydetme.

---

## 🛠️ Teknoloji Mimarisi (Tech Stack)

```
┌────────────────────────────────────────────────────────┐
│                   403 DM Deleter                       │
├──────────────────────────┬─────────────────────────────┤
│      Frontend Katmanı    │      Backend & Sistem       │
├──────────────────────────┼─────────────────────────────┤
│  • React 18 & TypeScript │  • Rust & Tauri v2 Shell    │
│  • Tailwind CSS (Tokens) │  • Windows WebView2 Core    │
│  • Framer Motion         │  • Discord WebSocket Gateway│
│  • Lucide React Icons    │  • Native File System API   │
│  • Canvas HTML5 Engine   │  • SQLite / Local Storage   │
└──────────────────────────┴─────────────────────────────┘
```

| Katman | Teknoloji | Görev & İşlev |
| :--- | :--- | :--- |
| **Backend & Shell** | [Tauri v2](https://tauri.app/) • [Rust](https://www.rust-lang.org/) | Minimum bellek tüketimi, güvenli yerel dosya yönetimi ve native Windows entegrasyonu |
| **Frontend** | [React 18](https://react.dev/) • [TypeScript](https://www.typescriptlang.org/) | Tip güvenliği, modüler mimari ve reaktif state yönetimi |
| **Derleyici (Bundler)** | [Vite 5](https://vitejs.dev/) | Anlık HMR geliştirme ortamı ve optimize edilmiş üretim derlemesi |
| **Tasarım Sistemi** | [Tailwind CSS](https://tailwindcss.com/) | Tasarım tokenleri (`tokens.css`), glassmorphic cam efektleri ve CSS değişkenleri |
| **Animasyonlar** | [Framer Motion](https://www.framer.com/motion/) | Donanım hızlandırmalı pürüzsüz kart, modal ve bildirim geçişleri |
| **Ağ Geçidi** | Discord Gateway (v9 WebSocket) | Hayalet mesajların anlık tespiti ve canlı durum izleme |
| **Dosya Sistemi** | `@tauri-apps/plugin-fs` | Belgeler dizinine doğrudan, güvenli yerel dosya ve yedek yazma |

---

## 🚀 Kurulum & Geliştirici Rehberi (Installation)

### Ön Gereksinimler
* **Node.js:** `v20.x` veya üzeri ([nodejs.org](https://nodejs.org/))
* **Rust & Cargo:** Güncel kararlı sürüm ([rustup.rs](https://rustup.rs/))
* **C++ Build Araçları:** Windows için *Visual Studio C++ Build Tools*

### 1. Depoyu Klonlayın
```bash
git clone https://github.com/onlyfourhundredthree/403dmdeleter.git
cd 403dmdeleter
```

### 2. Bağımlılıkları Yükleyin
```bash
npm install
```

### 3. Geliştirici Modunda Çalıştırın (Tauri + React HMR)
```bash
npm run tauri dev
```

### 4. Kurulum Paketi Derleyin (.exe Installer)
```bash
npm run tauri build
```
*Derlenen imzalı kurulum sihirbazı `src-tauri/target/release/bundle/nsis/` dizininde oluşturulur.*

---

## 🔄 Otomatik Yayınlama Sistemi (Release Pipeline)

Proje, tek bir komutla sürüm yükseltme, Git etiketleme ve GitHub Actions CI/CD derlemesini tetikleyen otomatik bir yayınlama altyapısına sahiptir:

```bash
npm run publish
```

Bu otomasyon scripti (`publish.mjs`):
1. `package.json` ve `tauri.conf.json` içerisindeki sürüm numarasını otomatik olarak artırır (örn. `v1.0.59` ➔ `v1.0.60`).
2. Değişiklikleri otomatik commit eder ve `main` dalına pushlar.
3. Yeni sürüm etiketi (`vX.X.XX`) oluşturup remote depoya gönderir.
4. GitHub Actions iş akışını tetikleyerek Windows kurulum dosyasını (`.exe`) ve otomatik güncelleme bildirisini (`updater.json`) Releases deposuna teslim eder.

---

## 📂 Yerel Depolama ve Yedek Dizinleri

Uygulamanın ürettiği tüm rapor ve yedekler Windows kullanıcı belgeleri dizininde kategorize edilmiş halde saklanır:

```text
📁 Belgeler / 403Deleter /
├── 📄 Yedek_DM_[Kullanıcı-Kanal]_[Tarih].html   <-- Discord temalı interaktif sohbet yedeği
├── 📄 Yedek_Arkadaslar_[Tarih].html            <-- İlişki ve arkadaş listesi yedeği
├── 📄 Sniper_Raporu_[Tarih].html               <-- Silinen / düzenlenen mesaj raporu
├── 🖼️ Wrapped_[Kullanıcı]_[Tarih].png          <-- 1080x1350 PNG Discord Wrapped kartı
├── 📁 Media / [Kanal] /                        <-- Orijinal kalitede indirilen fotoğraflar/videolar
└── 📁 VoiceMessages / [Kanal] /                <-- Yerel olarak kaydedilen ses kayıtları (.ogg/.mp3)
```

---

## ⚠️ Güvenlik & Yasal Uyarı (Disclaimer)

> [!WARNING]
> Bu yazılım yalnızca **kişisel veri gizliliği, GDPR / KVKK hakları ve eğitim amaçları** doğrultusunda geliştirilmiştir.  
> Kullanıcı tokenlerinin otomatik istemciler aracılığıyla kullanılması Discord Hizmet Şartları'na (Terms of Service) aykırı olabilir.  
> Uygulamanın kullanımından doğabilecek tüm sorumluluk son kullanıcıya aittir.

> [!NOTE]
> **Tam Gizlilik Garantisi:** 403 DM Deleter **hiçbir kullanıcı verisini, hesap tokenini veya mesaj içeriğini dış sunuculara iletmez**.  
> Tüm kimlik doğrulama anahtarları ve veriler yalnızca yerel tarayıcı hafızanızda (`localStorage`) ve yerel makinenizde tutulur.

---

## 📄 Lisans

Bu proje [MIT Lisansı](LICENSE) kapsamında lisanslanmıştır.

<div align="center">
  <br />
  <sub>Geliştirici: <b><a href="https://github.com/onlyfourhundredthree">onlyfourhundredthree</a></b> • Güçlü, Hızlı ve Güvenli Discord Gizliliği</sub>
</div>
