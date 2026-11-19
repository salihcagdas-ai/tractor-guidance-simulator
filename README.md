# Mark 42 · Traktör dümenleme simülasyonu

**Salih Çağdaş · Tarım teknolojileri · Kasım 2026**

Bir traktörün planlanan hatları bitirmesi, aletin tarlanın tamamını işlediğini gösterir mi? Mark 42'yi bu farkı sürücüye göstermek için geliştirdim. Kabin ekranında aleti ve iş yönünü seçiyor, nereden ikinci kez geçildiğini ve geride nerede boşluk kaldığını görebiliyorsun.

![İki yapay tarlada silindir, gübre ve ilaç için hesaplanan iş izleri](gorseller/kapsama.png)

Dikdörtgen ve üçgen, bu karşılaştırma için çizilmiş iki örnek tarla. Yeşil işlenen alanı, turuncu birden fazla işlenen yeri, pembe ise iş kaydı bulunmayan bölgeyi gösteriyor. Aynı tarlada alet değişince bindirmenin yeri ve büyüklüğü de değişiyor.

## Bir koşunun sonucu

Üçgen tarlada 27 metrelik ilaç makinesinin iç rotası **26,27 dakikada** tamamlandı. Bu, simülasyondaki iş süresi. İç hedefte boşluk **0 m²** çıktı. Operatörün kenarlarda çalıştığına dair kayıt girilmediği için ekran, kenarlar dahil **30.030,22 m²** alanı hâlâ açık gösterdi. Tekrar ilaçlanan alan **92,10 m²**, parsel dışına taşan alan **0 m²** oldu.

![Kabin sonuç kartında işlenen, kalan, tekrarlanan ve dışa taşan alanlar](gorseller/is-sonucu.png)

## Neleri doğruladım?

| Deneme | Gözlem |
| --- | --- |
| Üç aletle sürüş | Silindir, gübre ve ilaç makinelerini iki farklı tarla şeklinde baştan sona oynattım. Silindir dönüşte kalktı, yeni iş hattında indi. |
| Moladan devam | İlaçlama işinde 60 sanal saniye sonra mola verdim ve kabin sunucusunu kapattım. Yeniden açınca rota, son konum, süre ve işlenen alan aynıydı. İşi aynı rotada bitirdim. |
| Bağlantı kesintisi | Sekiz sanal kesinti veya duraklama durumunda operatör yeniden izin verene kadar dümen izni kapalı kaldı. |

[Tablet boyutunda kabin ekranını aç](gorseller/kabin.png)

**Projenin aşaması.** Yazılım ve simülasyon doğrulaması tamamlandı. Sırada parçaların tezgâh üzerinde birlikte denenmesi ve traktöre montaj var. Gerçek alet izi, sahadaki dümenleme hassasiyeti ve operatörün direksiyonu devralması sonraki aşamada ölçülecek.

© 2026 Salih Çağdaş. Portföy metni ve görselleri üzerindeki haklar saklıdır.
