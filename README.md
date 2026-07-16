# Ev Gözü

Rıza temelli, **her zaman görünür** ev kamerası/mikrofon yayın sistemi.
Yayın açıkken telefon ekranında bunu belirten kırmızı bir gösterge sürekli görünür.
Gizli çalışmaz; kapatmak için tek tuş yeterlidir.

## Dosyalar

- `index.html` — Evdeki (yayıncı) telefonda açılacak sayfa. Kamera/mikrofon izni ister, "Yayını Başlat/Durdur" düğmesi ve daima görünür durum çubuğu içerir.
- `viewer.html` — Senin izleyeceğin sayfa. Yayıncı cihazın kimliğini girip bağlanırsın.
- `manifest.json` — Telefonda "ana ekrana ekle" ile uygulama gibi kurulmasını sağlar.
- `sw.js` — PWA'nın çevrimdışı da açılabilmesi için basit önbellek.
- `icons/` — Uygulama ikonları.

## 1) Kendi adını yaz

`index.html` içinde şu satırı bul ve kendi adınla değiştir:

```html
document.getElementById('ownerName').textContent = "AD SOYAD BURAYA";
```

## 2) GitHub Pages'e yükleme

1. GitHub'da yeni bir repo oluştur (ör. `ev-gozu`), **public** yap.
2. Bu klasördeki tüm dosyaları (`index.html`, `viewer.html`, `manifest.json`, `sw.js`, `icons/`) repoya yükle.
3. Repo **Settings → Pages** kısmına git.
4. **Source**: `Deploy from a branch` → branch `main`, klasör `/root` seç, kaydet.
5. Birkaç dakika sonra siten şu adreste yayında olur:
   `https://kullaniciadi.github.io/ev-gozu/`

## 3) Evdeki telefonda kurulum (arkadaşın yapacak)

1. Telefonda Chrome ile `https://kullaniciadi.github.io/ev-gozu/index.html` adresine girsin.
2. Kamera/mikrofon izni istendiğinde **izin ver** desin.
3. Chrome menüsünden **"Ana ekrana ekle"** seçeneğini kullanırsa, sayfa telefonda normal bir uygulama gibi ikonla durur.
4. İhtiyaç olduğunda **"Yayını Başlat"** butonuna bassın. Bastığı an ekranda büyük kırmızı bir "YAYIN AÇIK" uyarısı belirir — bu her zaman görünür kalır, gizlenemez.
5. Telefonu istediğin noktaya yerleştirsin, şarja taksın.

## 4) Senin tarafında (izleme)

1. `https://kullaniciadi.github.io/ev-gozu/viewer.html` adresine gir.
2. Evdeki telefonun ekranında görünen **cihaz kimliğini** (ör. `8f2a-91c3-...`) viewer sayfasındaki kutuya yapıştır.
3. **Bağlan**'a bas, canlı görüntü ve ses gelir.

## Nasıl çalışır

Bağlantı, WebRTC teknolojisi ve ücretsiz genel **PeerJS** sinyalleşme sunucusu üzerinden kurulur.
Görüntü/ses trafiği tarayıcılar arasında doğrudan (peer-to-peer) akar; GitHub Pages sadece statik dosyaları sunar.

## Önemli sınırlar (bilerek böyle tasarlandı)

- Yayın durumu **her zaman ekranda görünür** ve kapatılabilir. Bu, gizli izleme değil, rızaya dayalı bir güvenlik kamerası davranışıdır.
- Herkese açık PeerJS sunucusu kullanıldığından, cihaz kimliğini sadece güvendiğin kişilerle paylaş. Daha fazla gizlilik istersen kendi PeerServer'ını barındırabilirsin (bkz. [peerjs.com](https://peerjs.com/peerserver)).
- Sayfa arka planda (tarayıcı kapalıyken) çalışmaz; telefon ekranı açık ve sayfa aktif olmalı.
