# Şeytanın avukatı: İşin Garibi link-in-bio (2026-09-29)

Denetlenen: `index.html` @ `f4497fb`. Canlı sayfa kaynakla aynı, yalnız satır sonları farklı (CRLF/LF).
Ölçüm: headless Chrome, iframe içinde 360 / 390 / 430 px ve uygulama içi tarayıcıyı taklit eden 360x600 ile 390x670 pencere. Yanına referans olarak thetin-one.vercel.app kondu.

## (a) Hüküm

1. **Ana iş çalışıyor:** tek kırmızı YouTube butonu baskın, hiyerarşi net ve Berkay'ın referans aldığı Thetin sayfasından daha iyi. 3 saniye testini geçiyor ama kıl payı: 360 px'te CTA ekranın alt yarısında, önünde yaklaşık 9 satır daktilo metni var.
2. **Markayı yanlış taşıyor:** sayfa kanalın kendi tanıtım cümlesine GERÇEK damgası basıyor. Pilot kapak da aynı hatayla reddedilmişti. Üstüne "arşiv dosyası" kostümü (manila, ataş, daktilo, yeşil çuha) kanalın kapak/Shorts dilini değil, jenerik "gizli dosya" şablonunu taşıyor. Sayfada tek espri yok.
3. **Teknik kırıklar küçük ama gerçek:** og:image göreli yol, 390 px'te damga metnin üstüne biniyor, ataş logoyu kesiyor, "izle" diyen buton abone penceresi açıyor. Bugün kanalda herkese açık video da yok. **Yayında kalabilir, ama K1-K3 ve Y1-Y2 düzelmeden "en iyi referans" çıtasında değil.**

## İyi olanlar (koru)

- Hiyerarşi doğru kurulmuş: tek birincil eylem (kırmızı, Anton 24px, tam genişlik), ikinciller sade. Referans sayfada 6 eşit buton var, bunda yok.
- Hafif: 7 KB HTML, JS yok, ikon kütüphanesi yok (inline SVG), iz sürücü yok.
- Dokunma alanları yaklaşık 60 px yükseklikte ve tam genişlikte, aralarında 12 px boşluk var. Telefonda yanlış butona basmak zor.
- Temel erişilebilirlik var: `lang="tr"`, `prefers-reduced-motion` (s.117), dekoratif damga `aria-hidden`, maskot `alt=""`, profil fotoğrafında anlamlı alt metin.
- YouTube linkinde handle (`@İşinGaribibu`, ASCII dışı `İ`) yerine kanal ID'si kullanılmış, doğru tercih. Link 200 dönüyor, og:title "İşin Garibi".
- Kanal kimliği gerçekten üç yerde duruyor: sayaç logosu, damga maskotu ve damga basma mekaniği. Bunlar şablon değil.
- Gizlilik temiz: commit yazarı `noreply`, PNG'lerde metadata yok (yalnız IHDR/IDAT/IEND), dış kaynak olarak sadece Google Fonts var.

## (b) Bulgular (önem sırasıyla)

### KRİTİK

**K1. Kanal kendi reklamına GERÇEK damgası basıyor, tanım da "gerçek" diyerek fazla iddia ediyor.**
- s.133: `<span class="baski">GERÇEK</span>Uydurma yok. Gerçekse gerçek, efsaneyse efsane diyoruz…`
- s.130: `Tarihin en tuhaf gerçek hikâyeleri.`
- Neden sorun: Kanalın tek farkı damganın güvenilirliği. Kanal EFSANE de anlatıyor (pilotta Sigurd efsane, semla rivayet). Bir sonraki cümle "efsaneyse efsane" derken tanımın "gerçek hikâyeler" demesi kendi kendini yalanlıyor. Emsal zaten var, `videolar/01-kral-olumleri/yayin/BILGI.md`: *"A'nın ilk hali 'GERÇEK' etiketiyle reddedildi: listede efsane (Sigurd) ve rivayet (semla) var."* Aynı gerekçe burada da geçerli. İzleyicinin damgayı ilk gördüğü yerde damga pazarlama için basılıyor, bu da onu değersizleştirir.
- Öneri: tanımdan "gerçek" kelimesini çıkar. Damga ya **KAYNAKLI** olsun (pilot kapakta kabul edilen karşılık) ya da tek damga yerine üç etiket yan yana sergilensin (GERÇEK / ŞÜPHELİ / EFSANE). İkincisi kanalın farkını tek bakışta, kelimesiz anlatır. (Kapsam dışı not: YouTube banner'ındaki "EN TUHAF GERÇEK HİKÂYELER" de aynı sorunu taşıyor.)

**K2. `og:image` göreli yol olduğu için sosyal önizleme kırılır.**
- s.10: `<meta property="og:image" content="profil.png">`
- Neden sorun: Open Graph mutlak URL ister. WhatsApp, Telegram, X ve Facebook tarayıcılarının çoğu göreli yolu çözmez. Link DM'de ya da grupta paylaşılınca görselsiz, çıplak bir kart çıkar. `og:url`, `og:type` ve `twitter:card` da eksik.
- Öneri: mutlak URL kullan ve üç eksik etiketi ekle (düzeltme listesi 1).

**K3. "YouTube'da izle" diyor, abone penceresine götürüyor. Bugün izlenecek video da yok.**
- s.137-139: `…UC_WlPwSPPTOmfSWafbowehw?sub_confirmation=1` + `YouTube'da izle`
- Neden sorun: Instagram ve TikTok linkleri kendi uygulama içi tarayıcılarında açar. Orada kullanıcı çoğunlukla YouTube'a giriş yapmamıştır, `sub_confirmation` penceresi ya giriş ister ya da hiç çıkmaz. Kullanıcı "izle"ye basıyor ama karşısına izleme değil, giriş duvarı çıkıyor. Bugün (29 Eyl) kanalda herkese açık video yok: pilotun yayını 3 Eki 17:00, video 02'ninki 7 Eki 18:00. Yani bu hafta butona basan boş bir kanal görüyor. Asıl huni de şöyle işliyor: Short'tan gelen kişi *o hikâyenin tamamını* arıyor, kanal ana sayfasını değil. İzleme sayfası giriş istemez.
- Öneri: birincil buton **son video** olsun (`youtu.be/ID`), ikincil buton "Kanala abone ol" (`sub_confirmation` burada kalsın). Her yeni videoda bir satırlık elle güncelleme gerekir, bu yayın adımına eklenir. Başlık yazma: YouTube A/B testi 3 farklı başlık döndürüyor, sayfadaki başlık izleyicinin gördüğüyle çelişebilir. Konu adı ve süre yazmak yeter. 3 Eki'ye kadar buton "YouTube kanalı · ilk video Cumartesi" olarak kalabilir.

### YÜKSEK

**Y1. 390 px'te damga "kaynaklar." kelimesinin üstüne biniyor.**
- s.100-106 `.baski { position:absolute; right:4px; top:-26px; … rotate(-14deg) }`
- Neden sorun: 390 px iPhone 12-16 genişliği, yani en sık görülen ekran. 380 px üstünde `.kimlik` yatay dizildiği için tanımın son satırı kesik çizgiye kadar iniyor. Döndürülmüş damga yukarı doğru yaklaşık 25 px taşıp metni örtüyor. 430 px'te sınırda, 360 px'te sorun yok. Ekran görüntüsünde "kaynakla**r.**" damga çerçevesinin altında kalıyor.
- Öneri: K1'deki etiket şeridine geçilirse sorun kendiliğinden kalkar. Tek damga kalacaksa akışa alınmalı: `position:static; display:inline-block`.

**Y2. Ataş logoyu kesiyor ve ataş gibi de görünmüyor.**
- s.61-66 `.foto::before { position:absolute; top:-16px; left:18px; … }`
- Neden sorun: Mutlak konumlu sözde öğe, statik `img`'nin üstünde boyanıyor. Gri hap şekli her genişlikte sayacın başının/kulağının üstünde duruyor. Tek başına da ataş okunmuyor, sadece yuvarlak köşeli bir dikdörtgen çerçeve gibi görünüyor. Süs ekliyor ama kimlik eklemiyor.
- Öneri: sil. Silmek düzeltmekten ucuz.

**Y3. "Arşiv dosyası" teması kendi başına bir şablon ve kanalın gerçek görsel dilinden kopuk.**
- s.17-24 (yeşil çuha + manila), s.14/31 (Special Elite), s.60-66 (ataş), s.43-52 (dosya sekmesi).
- Neden sorun: Special Elite, "gizli belge / true crime / komplo" sayfalarının varsayılan Google fontu. Manila, ataş, daktilo ve damga birlikte binlerce "CLASSIFIED dosya" sayfasının kostümü. Kanalın gerçek dili `KAPAK.md`'de yazıyor: soğuk ve koyu zemin, sıcak sarı maskot ve arkasında hale, siyah konturlu dev beyaz kalın yazı, tek kırmızı vurgu, bilerek kaba MS Paint çizimi, Discord Türkçesi. Instagram'dan Shorts izleyip gelen biri (bulanık zemin, eğik kalın sarı-beyaz altyazı) önce bej bir büro dosyasına iniyor, oradan lacivert-sarı YouTube kapaklarına geçiyor: üç ekran, iki marka. Yeşil çuha da bilardo ya da poker masasıdır, arşiv değil. Sayfanın verdiği his "ciddi dedektif", kanalınki "kara mizah + kaba çizim".
- Adil karşı görüş: Tema sıcak, gri Linktree kutularından ve referans sayfanın neon şablonundan ayrışıyor. "Kaynaklı" iddiasıyla kavramsal bağı da var. Kötü yapılmış değil, yanlış marka için iyi yapılmış.
- Öneri: kostümü (çuha, ataş, daktilo gövde fontu, dosya sekmesi) at. Kapak paletini al: koyu lacivert zemin, sarı haleli sayaç, Anton başlık, kırmızı CTA, sert gölgeli buton (bu kısım zaten kaba çizime yakın, kalsın). Kimliği taşıyan üç öğe (sayaç, damga maskotu, damga basma) kalsın. **Bu bir zevk değil tutarlılık kararı; son söz Berkay'ın.**

**Y4. Sayfada tek espri yok. Kanalın yarısı mizah.**
- Neden sorun: `SEYTANIN-AVUKATI.md`'deki "tutan mizah" referansı somut: sayaç karakteri, e-Devlet, dilekçe, callback. Sayfanın metni ise müze broşürü gibi: "…diyoruz; her videonun kaynakları açıklamasında." Maskot sadece bir kez zıplıyor. Kimliği en ucuza taşıyacak şey tek bir iyi şaka; bütün dosya kostümünden fazlasını yapar.
- Öneri, tek gag (en güçlüsü, marka mekaniğini kullanıyor): yayın sıklığı iddiasının üstüne küçük bir **ŞÜPHELİ** damgası bas (O2 ile birleşir), ör. `Her Cumartesi yeni video [ŞÜPHELİ]`. Kendi iddiasını denetleyen kanal, "uydurma yok" demekten daha inandırıcıdır. Ritim tutarsa damga GERÇEK'e çevrilir, bu da ileride bir callback olur.

### ORTA

**O1. Aynı vaat üç kez söyleniyor ve CTA'yı aşağı itiyor.**
- Tanımda "sağlam kaynaklar", kural paragrafında "Uydurma yok…", damgada GERÇEK. Meta açıklama bunun dördüncüsü.
- 360x600'de (küçük Android, Instagram tarayıcısı) CTA y≈470-550'de, ekranın alt yarısında. Önünde logo ve yaklaşık 9 satır metin var. 390x670'te y≈375-455, orada iyi.
- Öneri: tanım tek satır, kural tek satır + etiket şeridi. CTA yaklaşık 150 px yukarı çıkar.

**O2. "her hafta" kanıtlanmış bir ritim değil.**
- s.139 `Uzun videolar, her hafta`
- Neden sorun: Bugün kanalda 0 herkese açık video var. "Haftada bir" Project.md'de 2026-09-27 tarihli bir *çalışma kararı*; Cmt 17:00 / Çrş 18:00 takvimi bir kez bile işlemedi. Doğruluk kuralının ruhu şu: sayfa da bir iddiadır. Ayrıca video 02 6:46, yani "uzun" ancak Shorts'a göre uzun.
- Öneri: ya sıklığı sil ("Kaynaklı, bölümlü videolar") ya da Y4'teki ŞÜPHELİ damgası şakasıyla bilerek söyle.

**O3. IG/TikTok butonları çift ve kısmen döngüsel.**
- s.145 ve s.151: ikisinde de `Kısa hikâyeler`. Aynı alt metin hiçbir bilgi taşımıyor.
- Instagram bio'sundan gelen birine Instagram butonu göstermek onu geldiği yere geri yollar. İki hesapta da henüz 0 gönderi var (Project.md, 2026-09-29).
- Öneri: ikisini ortalanmış küçük bir ikon satırına indir (48 px daire), alt metinleri sil. YouTube tek büyük buton olarak kalır.

**O4. Font yükü sayfanın kendisinden ağır.**
- s.14: Anton ve Special Elite. Türkçe karakterler latin-ext alt kümesi istediği için 4 woff2 iniyor: Anton 21+12 KB, Special Elite 25+53 KB, toplam ≈ **111 KB**. Karşılaştırma: HTML 7 KB, iki görsel 108 KB. Üstüne iki üçüncü taraf alan adı ve render'ı bloklayan CSS var.
- Neden sorun: Instagram tarayıcısında bağlantı soğuk açılır. Font gelene kadar metin Courier New ile çizilir, sonra değişir, ve 3 saniye tam bu pencereye denk geliyor. Android'de Impact yok, Anton gelene kadar CTA Roboto ile görünür. 13 px'te Special Elite'in dokulu harfi okunaklılığı da düşürüyor (O5).
- Öneri: Special Elite'i tamamen kaldır (gövde `system-ui`). Anton kalsın (≈33 KB). `&text=` ile alt küme alınabilir ama her metin değişikliğinde parametre güncellenmek zorunda, kırılgan; değmez.

**O5. Erişilebilirlik açıkları.**
- `h1` yok: kanal adı `<div class="sekme">` (s.127). Ekran okuyucu ve arama motoru başlık görmüyor.
- Odak çizgisi `#1f8a3a`, manila `#e3c587` üstünde **2.65:1**, gereken 3:1 (s.88).
- Kırmızı butondaki `small`, opacity .9 ile beyaz/kırmızı **4.28:1**, 14 px metin için gereken 4.5:1 (s.98).
- 13 px Special Elite + opacity .75 (s.90): kontrast 6.4:1 ile geçiyor ama dokulu font küçük boyutta zor okunuyor.

### DÜŞÜK

- **D1.** `footer { text-align:center; }` (s.118) ölü kural, sayfada footer yok. Şablondan kalmış.
- **D2.** `damga.png` 59 KB ama 84 px gösteriliyor. pngquant/oxipng ile yaklaşık 15-20 KB'a iner. Kritik değil.
- **D3.** 360 px'te maskot kartın dışında, masanın üstünde bağsız sallanıyor (`bottom:-92px`). 390+'da kartın köşesine oturuyor. Görmezden gelinebilir.
- **D4. Gizlilik (karar Berkay'ın):** `lahmacunor.github.io` adresi github.com/lahmacunor'a, oradan `bakim-proforma-panel-web` ve `bakim-fiyat-rehberi`'ne (iş hayatı) bağlanıyor. Sayfa yeni bir sızıntı değil: video açıklamalarındaki atıf gist'leri zaten `gist.github.com/lahmacunor` altında. Kanalın Berkay'dan ayrı durması önemliyse çözüm ayrı bir org ve gist'leri taşımak. Önemli değilse geç. Google Fonts ziyaretçi IP'sini Google'a gönderir (KVKK/GDPR tartışmalı), O4'teki self-host ya da font atma bunu da bitirir.
- **D5. Referans çıta değil.** thetin-one.vercel.app'te 6 ikon için tüm Font Awesome CSS'i, `user-scalable=no` (yakınlaştırma yasağı, erişilebilirlik hatası), 6 eşit ağırlıkta buton ve sonsuz animasyonlu ızgara var. Koyu kart + neon kenar kopyalanmamalı. Çıta, kanalın kendi kapak dili ve Short'tan uzun videoya giden huni.
- **D6. Eksik mi? (YAGNI)**
  - Son video kartı: küçük resim ya da API gerekmez, K3'teki tek satırlık elle link yeter.
  - Analitik: gerek yok. Instagram profesyonel panosu bio linki dokunmalarını sayıyor, YouTube Studio da "Harici" trafik kaynağını gösteriyor.
  - Dil: yalnız Türkçe doğru.
  - Favicon: 320 px PNG iş görür, `apple-touch-icon` gereksiz.

## (c) Somut düzeltme listesi (dosya değiştirilmedi)

**Zorunlu (K1-K3, Y1-Y2, O5):**

1. `<head>` (s.10'un yerine):
   ```html
   <meta property="og:type" content="website">
   <meta property="og:url" content="https://lahmacunor.github.io/isingaribi/">
   <meta property="og:image" content="https://lahmacunor.github.io/isingaribi/profil.png">
   <meta name="twitter:card" content="summary">
   ```
2. Tanım (s.130). "Gerçek" çıkar, "sağlam" yerine doğrulanabilir bir söz gelir. Öneri, internet dilinde bir "açık kaynak" cinası:
   `Tarihte yaşanmış, ya da yaşandığı iddia edilen, saçmalıklar. Çizimler kaba, kaynaklar açık.`
   Meta description ve og:description (s.7, s.9) de buna göre kısalır.
3. Kural paragrafı (s.133) etiket şeridine dönüşür, `.baski` silinir:
   ```html
   <p class="etiketler" aria-label="Etiketler: gerçek, şüpheli, efsane">
     <span class="e gercek">GERÇEK</span><span class="e supheli">ŞÜPHELİ</span><span class="e efsane">EFSANE</span>
   </p>
   <p class="kural">Her iddiaya bunlardan biri basılır. Kaynaklar videonun açıklamasında.</p>
   ```
   CSS: `.etiketler{display:flex;gap:10px;justify-content:center;margin:18px 0 6px}`
   `.e{font-family:Anton,Impact,sans-serif;font-size:20px;border:3px solid currentColor;border-radius:6px;padding:0 8px;transform:rotate(-6deg)}`
   Renkler videodaki damga renklerinden alınır ve zemine karşı en az 3:1 olmalı (büyük yazı). İstenirse mevcut `bas` animasyonu üçüne 0.5/0.7/0.9 sn gecikmeyle uygulanır. `.kural`'daki `position:relative; padding-top:40px` silinir. Tek damga kalacaksa: `.baski{position:static;display:inline-block}`.
4. CTA (s.136-141). 3 Eki 17:00'dan sonra:
   ```html
   <li class="ana"><a href="https://youtu.be/ggRvRLNnka8">[yt svg]<span>Son videoyu izle<small>Kral ölümleri · 17 dk</small></span></a></li>
   <li><a href="https://www.youtube.com/channel/UC_WlPwSPPTOmfSWafbowehw?sub_confirmation=1">[yt svg koyu]<span>Kanala abone ol</span></a></li>
   ```
   3 Eki'ye kadar tek buton, `sub_confirmation` olmadan: `YouTube kanalı` + `İlk video Cumartesi 17:00`. Yayın adımına şu satır eklenir: "link-in-bio: `.ana a` href + small güncelle". Video başlığı yazılmaz, çünkü A/B testi başlığı değiştiriyor.
5. Ataş: s.60-66 `.foto::before` bloğunu sil.
6. Başlık: s.127 `<div class="sekme">` → `<h1 class="sekme">`, CSS'e `margin:0; font-weight:400;` ekle. Anton'un yalnız 400 ağırlığı var; h1'in varsayılan kalınlığı sahte bold üretir.
7. Odak: s.88 `outline: 3px solid var(--murekkep);` olsun (10:1).
8. s.98 `.ana small` içindeki `opacity:.9` silinsin (tam beyaz 5.0:1).

**Önerilen (Y3-Y4, O1-O4):**

9. Fontlar: s.14 `family=Anton&display=swap` olsun (Special Elite çıkar). s.31 `font-family: system-ui, -apple-system, "Segoe UI", Roboto, sans-serif;`. s.98'deki `"Special Elite"` referansı da silinir.
10. Sıklık iddiası: `her hafta` silinir. Şaka tercih edilirse CTA altına tek satır: `Her Cumartesi yeni video` + yanında küçük, 8° dönük bir `.e.supheli` damgası (14 px). Ritim 4 hafta tutunca GERÇEK'e çevrilir.
11. IG/TikTok (s.142-153) → ikon satırı:
    ```html
    <nav class="sosyal" aria-label="Diğer hesaplar">
      <a href="https://www.instagram.com/isingaribibu/" aria-label="Instagram">[svg]</a>
      <a href="https://www.tiktok.com/@isingaribibu" aria-label="TikTok">[svg]</a>
    </nav>
    ```
    `.sosyal{display:flex;justify-content:center;gap:16px;margin-top:18px}`
    `.sosyal a{width:48px;height:48px;display:grid;place-items:center;border:2px solid var(--murekkep);border-radius:50%;box-shadow:2px 2px 0 var(--murekkep)}`
12. Tema (Berkay kararı). `:root`'u kapak paletine çevir:
    `--zemin:#0f1a2e; --zemin-2:#1b2a47; --kart:#16213a; --yazi:#f4f1e8; --sari:#f5b82e; --kirmizi:#d7261e;`
    - body: lacivert radial.
    - Kart: koyu, 3 px açık kenar, sert gölge (neon değil).
    - Sayacın arkasında sarı hale: `.foto{background:radial-gradient(circle,var(--sari) 0 55%,transparent 70%)}`.
    - Kanal adı Anton, beyaz, siyah kontur: `text-shadow:0 3px 0 #000`.
    - Butonlarda mevcut sert gölge kalsın.
    - Dosya sekmesi ve çuha gider.
    - Tüm renk çiftlerinin kontrastı yeniden ölçülür.
13. s.118 `footer{…}` silinir. `damga.png` sıkıştırılır (`pngquant --quality 70-90`).

Sıra: 1-8 tek oturumluk iş (yaklaşık 30 satır diff). Ardından 9-11. 12 ayrı karar.
