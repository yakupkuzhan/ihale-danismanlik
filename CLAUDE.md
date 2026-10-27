# Proje notları (Claude Code için devir notu)

Kamu ihale danışmanlığı (yapım işleri) kurumsal web sitesi prototipi. Geçici marka: "İhale Danışmanlık". Tüm ziyaretçi metinleri Türkçe.

## Teknik
- Astro 7 (static) + TypeScript strict + Tailwind CSS 4 (`@tailwindcss/vite`) + `@astrojs/sitemap`. React yok.
- **Node.js >= 22.23.4 gerekir** (önerilen 24). Daha eski Node ile Astro çalışmaz.
- Komutlar: `npm ci`, `npm run dev`, `npm run check`, `npm run build`, `npm run images` (OG/favicon üretir).
- Yayın adresi/alt dizin: `site.config.mjs` (`SITE_URL`, `BASE_PATH` ortam değişkenleri). İç bağlantılar daima `src/lib/paths.ts` içindeki `href()` / `asset()` ile verilir; mutlak `/...` yol yazmayın.
- `trailingSlash: 'always'`, `build.format: 'directory'`.
- Merkezi içerik: `src/data/site.ts` (marka, iletişim, prototip bayrakları), `src/data/services.ts` (6 hizmet), `src/data/home.ts`, `src/data/about.ts`, makaleler `src/content/articles/*.md`.

## İçerik kuralları
- Uydurma istatistik, müşteri, ekip, kuruluş yılı, tarih, yazar veya iletişim bilgisi eklenmez. Bilinmeyen alanlar `null` kalır ve arayüzde gizlenir ya da "Yayından önce eklenecek" olarak işaretlenir.
- Hukuki temsil, resmî kurum adına işlem veya ihale kazanma garantisi vaat edilmez. KİK/EKAP ile resmî bağlantı ima edilmez.
- Mevzuat bilgisi doğrulanamıyorsa kesin oran/süre verilmez; resmî kaynaklara (ihale.gov.tr, ekap.kik.gov.tr, mevzuat.gov.tr) yönlendirilir.
- `prototype.noindex: true` bilerek açık (prototip dizine eklenmesin). Lighthouse SEO bu yüzden ~63; kapatıldığında 100 ölçüldü.

## Yapılan doğrulamalar (ilk sürüm)
- `astro check`: 0 hata. Build: 17 sayfa. 713 iç bağlantı + 109 çapa kırıksız; kök (`/`) ve farklı repo adıyla da test edildi.
- 360–1920 px arası 6 genişlikte yatay taşma/konsol hatası yok. Mobil menü, Esc, odak tuzağı test edildi.
- axe-core: 10 sayfa × 2 genişlik ihlalsiz. Lighthouse: performans 99–100, erişilebilirlik 100, best practices 100.

## Yayın durumu
GitHub deposu: `yakupkuzhan/ihale-danismanlik` (ad düzeltildi). Kod `main` dalında.
- Depo adı düzeltildi ve Pages kaynağı "GitHub Actions" olarak etkin.
- "GitHub Pages'e Yayınla" workflow'u #3 (manuel) ve #4 (push) çalıştırmalarında **derleme ve yayınlama başarılı**.
- Adres: https://yakupkuzhan.github.io/ihale-danismanlik/
- **Kalan:** canlı sitenin elle doğrulanması (sayfalar, görseller, stiller, bağlantılar). Bu bulut oturumunun ağ politikası `github.io` adresine erişimi engellediği için oturumda yapılamadı.

## Gerçek yayına geçmeden önce
- `src/data/site.ts`: `prototype.showNotice` ve `prototype.noindex` → `false`; doğrulanmış iletişim bilgileri.
- `/kvkk/` ve `/gizlilik/` taslaklarındaki "Yayından önce doldurulacak" alanları (hukuki destekle).
- Ayrıntılar: `README.md`.
