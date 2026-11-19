# Traktör yanlış konumu doğru sanırsa ne olur?

Uydu alıcısının sustuğunu fark etmek kolay. Daha zor durum, alıcının düzenli veri göndermeye devam edip hem konumu hem hızı yanlış göstermesi. Ekrandaki işaret ilerler ve yazan hız bu harekete uyar. Peki tekerlekler gerçekten o kadar yol aldı mı?

Bu soruyu Raspberry Pi 5 üzerinde **312 simülasyon koşusuyla** sınadım. Silindir, gübre ve ilaç işleri için düz sürüşü ve dönüşü, her birinde dört farklı sensör gürültüsü örneğiyle denedim. Böylece 13 durumun her biri için 24 koşu elde ettim. Pi gerçek kabin bilgisayarıydı. Deney, traktör hareketini ve sensör okumalarını yazılımda üretti.

## Dümen izni ne zaman kesildi?

| Deneyde olan | Dümen izni kesilen koşu | Hatanın başlamasından iznin kesilmesine kadar |
| --- | ---: | ---: |
| Normal sürüş | 0 / 24 | Yanlış alarm görülmedi |
| Uydu verisi kesildi | 24 / 24 | 0,46–0,54 saniye |
| Uydu verisi dondu | 24 / 24 | 0,46–0,54 saniye |
| Konum ve hız birlikte yanlıştı. Yalnız uydu verisi kontrol edildi. | 0 / 24 | Hata fark edilmedi |
| Aynı hata, hareket sensörü (IMU), teker hızı ve direksiyon açısıyla karşılaştırıldı. | 24 / 24 | 1,82–4,70 saniye |

Son iki satır aynı soruya iki yanıt veriyor. Alıcının bildirdiği hız ve konum birbiriyle uyuştuğu için ilk kontrol bunları kabul etti. Tekerleklerden ve hareket sensöründen gelen bağımsız ölçüler işin içine girince 24 koşunun hepsinde uyuşmazlık görüldü. En uzun örnekte karar **4,70 saniye** sürdü. Bu süre, gerçek traktörde ayrıca ölçülmesi gereken gecikmelerden biri.

**Harita baştan beri kayıksa** başka bir sorun var. Traktör ekranda yan sıradan başlıyor, sonra her metreyi ve dönüşü doğru izliyorsa tekerleklerin anlattığı hareket haritayla hâlâ uyuşur. Bu deneyde başlangıçtan beri sabit kalan konum hatası tespit edilemedi. İlk konumu doğrulamak için yeri bağımsız olarak bilinen bir referans gerekir.

**Dümen izni kesilince traktör duruyor mu?** Sanal sürücünün fren müdahalesini kaldırdığım 48 koşunun hepsinde model ilerlemeye devam etti. Yazılım dümen komutlarını kesebildi. Gerçek frenleme, durma mesafesi ve operatörün direksiyonu devralması saha deneyi bekliyor.

## Pi kapanıp açılınca iş nereden sürüyor?

Ayrı bir deneyde kabinde iki iş kaydı açtım. Pi yeniden başlatılırken gübre işi moladaydı, ilaç işi sürüyordu. Açılışta ikisi de **molada** geldi. İki kaydın da rotasını, hat üzerindeki son noktasını, süresini ve işlenen alanını kapanış öncesiyle karşılaştırdım. Her biri kendi kaydıyla eşleşti. Kabinde devam komutu verilince iki iş de kendi rotasında tamamlandı.

[Proje tanıtımına dön](../README.md)
