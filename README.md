
# POSTMAN COLLECTIONS for PAYTR APIs

PayTR tarafından yayınlanmış olan servislerin testlerini daha kolay bir şekilde gerçekleştirmenize imkan tanıyan "Postman" programına ait Collections dosyalarını kullanmaya başlayabilirsiniz.

## Collections İçindekiler
- [iFrame API](#iframe-api)
- [Havale/EFT iFrame API](#havaleeft-iframe-api)
- [Link API](#linkle-ödeme)
    - [Link Create](#linkle-ödeme)
    - [Link Delete](#linkle-ödeme)
    - [Send SMS](#linkle-ödeme)
    - [Send E-mail](#linkle-ödeme)
- [Direkt API Servisleri](#direkt-api)
    - [Direkt API](#direkt-api)
    - [Taksit Oranları Sorgulama](#taksit-oranları-sorgulama)
    - [BIN Sorgulama Servisi](#bin-sorgulama-servisi)
    - [Kart Saklama API](#kart-saklama-api)
        - [Yeni Kart Ekleme](#kart-saklama-api)
        - [Kayıtlı Karttan Ödeme](#kart-saklama-api)
        - [Kayıtlı Kart Listesi](#kart-saklama-api)
        - [Kayıtlı Kart Silme](#kart-saklama-api)
        - [Kayıtlı Karttan Tekrarlayan Ödeme](#kart-saklama-api)
- [Platform Transfer Talebi](#platform-transfer-talebi)
    - [Transfer Talimatı Ver](#platform-transfer-talebi)
    - [Geri Dönen Transfer Listesi](#platform-transfer-talebi)
    - [Geri Dönen Ödemeleri Hesaptan Gönder](#platform-transfer-talebi)
- [İade API](#iade-api)
- [Durum Sorgu API](#durum-sorgu-api)
- [BKM Express iFrame API](#bkm-express-iframe-api)
- [İşlem Dökümü](#işlem-dökümü)
- [Test Kart Bilgileri](#test-kart-bilgileri)


## BAŞLARKEN
PayTR API'lerini kullanmak için aşağıdaki bilgilere sahip olmanız gerekmektedir. Bu bilgilere PayTR Mağaza panelindeki [Bilgi](https://www.paytr.com/magaza/bilgi) sayfasından ulaşabilirsiniz.
- PayTR Mağaza No (merchant_id)
- Mağaza Parola (merchant_key)
- Mağaza Gizli Anahtar (merchant_salt)

> Not: Bu bilgiler tamamen `sizin mağazanıza özeldir`, dışarıya paylaşmamalısınız.

## KURULUM & KULLANIM
Postman tarafında kullanmanız için önceden hazırlanmış olan 2 adet dosya bulunmaktadır. Bunlardan birisi global tanımlamaların bulunduğu **PAYTRENV.postman_environment.json** dosyası, diğeri ise  API servislerin bulunduğu **PAYTR APIs.postman_collection.json** dosyasıdır.

#### Adım 1 (Environment Dosyasının Kurulumu):
- Postman programını açın
- Sol menüde bulunan "Environments" butonuna tıklayın
- Import butonuna tıklayın
- İndirmiş olduğunuz **PAYTRENV.postman_environment.json** adlı dosyayı seçin ve Import edin
- Import edilen PAYTRENV adlı environmenti seçtikten sonra **merchant_id, merchant_key, merchant_salt, user_ip ve merchant_oid** alanlarındaki XXXXXX değerlerini kendi bilgileriniz ile değiştiriniz.

#### Adım 2 (Collections Dosyasının Kurulumu):
- Sol menüde bulunan "Collections" butonuna tıklayın
- Import butonuna tıklayın
- İndirmiş olduğunuz **PAYTR APIs.postman_collection.json** adlı dosyayı seçin ve Import edin
- PAYTR APIs klasör adıyla gelen Collenctions'a tıkladıktan sonra sağ üstte bulunan **No Environment** butonuna tıklayarak, az önce eklemiş olduğumuz **PAYTRENV** adlı environmenti bu Collections'ta kullanabilmek için seçiyoruz.

#### Adım 3 (API Kullanım Örneği):
- PayTR APIs adlı Collections içerisinden kullanmak istediğiniz API servisi seçin (Örneğin: iFrame API)
- **get-iframe-token** adlı POST Request'e tıkladıktan sonra **Body** butonuna tıklayın
- **form-data** kısmında önceden hazırlanmış verilere ek olarak, Environment kısmından gelen bazı global veriler bulumaktadır.
- Request penceresinde bulunan form alanlarındaki değerleri kendi isteğinize göre değiştirebilir, sonrasında **Send** butonuna tıklayarak servisi çağırabilirsiniz.
- Ekranının alt kısmındaki Response panelinde, servisten dönen cevap olarak başarılı/hatalı çıktılar gösterilecektir.
<br>

## SERVİSLER HAKKINDA BİLGİLER
> Aşağıdaki bilgiler, servislerin kısa tanıtımlarıdır. Servisler hakkında daha detaylı bilgiye ve örnek kodlara ulaşmak için [Buraya Tıklayın](https://dev.paytr.com/).

---

#### iFrame API
Bu servis ile iFrame ödeme ekranını açarken kullanılacak olan **iframe_token** değeri döner.

---

#### Havale/EFT iFrame API
Bu servis ile Havale/EFT iFrame ödeme ekranını açarken kullanılacak olan **iframe_token** değeri döner.

---

#### Linkle Ödeme 
PayTR Link; entegrasyona gerek olmadan ödemelerinizi tek tık ile almanızı sağlar.
 
- **Linkle Ödeme (Create)**
Create servisi ile Hizmet/Ürün veya Fatura/Cari tahsilatlarınız için ödeme linkleri oluşturabilirsiniz.
<br>
 
- **Linkle Ödeme (Delete)**
Delete servisi ile daha önce oluşturmuş olduğunuz ödeme linklerini silebilirsiniz.
<br>

- **Linkle Ödeme (Callback)**
Oluşturduğunuz ödeme linki üzerinden yalnızca başarılı bir ödeme yapıldığında, Create servisinde link için göndermiş olduğunuz callbak_url’e işlem sonucu bildirilir.
    > _**Not:** Eğer Create servisinde callbak_url belirlemediyseniz veya belirlemek istemiyorsanız, bu entegrasyonu yapmanıza gerek yoktur. Bu servis yalnızca "Create" servisinde gönderdiğiniz linkin (varsa) callback_url'sine istek atar._
<br>
 
- **Linkle Ödeme (SMS/Email)**
Bu servisi kullanarak belirttiğiniz cep telefonu numarasına/email adresine oluşturmuş olduğunuz linkle ödeme sayfasına ait linkin gönderimini sağlayabilirsiniz. 

---

#### Direkt API
iFrame API'ye alternatif olarak kendi ödeme formunuz ile birlikte ödeme almanızı sağlayan servistir. Direkt API çözümünde, kullanılacak olan tüm servislerin mağaza tarafından (siz/yazılımcınız) entegre edilmeli ve test edilmelidir. Direkt API çözümünde güvenlik başta olmak üzere tüm akış **mağaza sahibinin sorumluluğundadır.** Direkt API çözümünü kullanma talebiniz PayTR ilgili birimlerince incelenmekte ve tanımlanmaktadır. Direkt API çözümü 2 adımlıdır:

> 1. ADIMda ödeme/kart bilgileri form aracılığı ile PayTR sistemine aktarılır,

> 2. ADIMda ise PayTR'den gelecek olan ödeme sonucuna ait yanıtın aktarılacağı "Bildirim URL" sayfası hazırlanır. Bu sayfada bildirim sonucuna göre (başarılı/başarısız) siparişi onaylamalı veya iptal etmelisiniz. (Bu adımda PayTR tarafından dönecek olan sipariş durumu bilgisi, PayTR Mağaza'nızın ayarlar sayfasında bulunan **Bildirim URL** adresine yönlendirilecektir. Yani 2. adımda kodlama yapacağınız sayfa ile aynı adres olmalıdır.)

---

#### Taksit Oranları Sorgulama
Direkt API entegrasyonu yapılırken, girilen kart numarasına ait taksit oranlarını çekmek için bu API kullanılmalıdır. Oranlar günlük olarak değişebilir. Bu nedenle bu oranları günlük olarak taksit oranları sorgulama API aracılığıyla çekip veritabanına kaydedebilir, güncelleyebilirsiniz. Bu oranları taksitli işlemlerde ürün fiyatına göre uygulayabilirsiniz

---

#### BIN Sorgulama Servisi  
BIN sorgulama servisi ile bir BIN numarası (kart numarasının ilk 6 hanesi) gönderip kartın detaylı bilgilerine ulaşabilirsiniz.

---

#### Kart Saklama API  
- **Yeni Kart Ekleme**
Bu servisi kullanarak ödeme esnasında PayTR'de kayıtlı bir kullanıcı ve kullanıcıya ait bir kart oluşturabilirsiniz. Bunun için yapılması gereken süreç:
    > 1. Direkt API dökümanında belirtildiği şekilde ödeme sayfanızı oluşturun.
    > 2. Kart bilgilerinin girildiği ödeme formunda "Kartını Kaydet" seçeneği sunacağınız bir onay kutucuğu ekleyin ve bu kutu seçildiyse gerekli bilgileri POST içeriğine ekleyin.

    > 1. Kullanıcı adına ilk kez bir kart kaydediliyorsa yalnızca "store_card" parametresi gönderilir.
    > 2. Kullanıcıya ait daha önceden kayıtlı bir kart varsa VE yeni bir  kart kaydetmek istiyorsa, POST içerisinde "utoken" ve "store_card" parametreleri birlikte gönderilmelidir.

- **Kayıtlı Karttan Ödeme**
    İzlenecek adımlar:
    > 1. Ödeme yapacak olan kayıtlı kullanıcıya ait kayıtlı kartlar ekranda listelenir.
    > 2. Kullanıcı listelenen kayıtlı kartlardan ödeme yapacağı kartı seçer.
    > 3. Kullanıcın seçtiği karta ait "require_cvv" parametresi değeri "1" ise CVV gireceği input alanı gösterilir.
    > 4. Kullanıcın seçtiği karta ait "ctoken" bilgisi VE kullanıcının "utoken" bilgisi POST içerisinde gönderilir.

- **Kayıtlı Kart Listesi**
Ödeme formunda, kullanıcıya ait kayıtlı kartları göstermek için daha önceden yeni kart kayıt servisinden elde edilmiş olan "utoken" bilgisi ile bu servise istek atarak o kullanıcıya ait kayıtlı kartları listeleyebilirsiniz.
<br>

- **Kayıtlı Kart Silme**
Kullanıcıya ait kayıtlı olan bir kart bilgisini silmek için "utoken, ctoken, merchant_id, paytr_token" bilgilerini bu servise göndererek istek yapmalısınız.
<br>

- **Kayıtlı Karttan Tekrarlayan Ödeme**
    Kayıtlı Karttan Tekrarlayan Ödeme (Recurring Payment) servisi ile kullanıcıya ait kayıtlı kart bilgileri ile dilediğiniz zaman veya aralıklarla ödeme alabilirsiniz.
    > 1. Recurring Payment adımında belirtilen değerlerle birlikte ödeme istek bloğunu oluşturun. Ödeme işlemi, kendi oluşturacağınız yapı üzerinden, kayıtlı kart bilgileri ile servise göndereceğiniz istek sonucunda oluşacaktır. Bu sebepten dolayı kullanıcıyla etkileşime girecek form oluşturulmasına gerek bulunmamaktadır.
    > 2. İşlemler Non3D (Non Secure) olarak gerçekleşecektir. Kullanıcınız herhangi bir ek işlem yapmayacak veya işlem sırasında kendisinden herhangi bir bilgi talep edilmeyecektir (Kullanabilmek için mağazanızda Non3D yetkilerinin açık olması gerekmektedir).
    > 3. Kayıtlı Kart Listesi servisinden, ödeme gerçekleştirilecek kullanıcıya ait "utoken" verisi kullanarak kayıtlı kartın "ctoken" verisine ulaşmanız gerekmektedir. Daha sonrasında bu ve dökümanda belirtilen diğer tüm alanları POST içerisinde ilgili servise iletmelisiniz.

---

#### Platform Transfer Talebi
PayTR Pazaryeri Çözümü ile pazaryeri platformu sahipleri, aynı sepette birden fazla satıcının ürünü olduğu durumlar, parçalı iade yapılması, sipariş tutarının sonradan değişmesi, farklı satıcıya farklı komisyon uygulanması vb. gibi her ihtiyaçlarını özgürce karşılayabilirler.

- **Transfer Talimatı**
    İzlenecek adımlar:
    > **1. ADIM Platform Transfer Talimatının Verilmesi:**  Dökümanda belirtilen bilgiler, ilgili servise gönderilmelidir. 
    > <em>**Not:** Mağaza, ödeme yapılmasını istediği tarihte (aynı gün hariç) en geç saat 10:00'a kadar Transper API'si yoluyla isteği göndermelidir. Daha sonra gönderilen istekler, bir sonraki iş gününde işleme alınacaktır.</em>

    > **2. ADIM Transfer Talimatının Sonucunun Alınması (Opsiyonel):** PayTR sistemi, transfer işlemlerin sonuçlanması sonurası PayTR Mağaza Paneli > Ayarlar sayfasında "Platform Transfer Sonucu Bildirim URL" kısmında belirttiğiniz adrese bilgi verir. 

- **Geri Dönen Ödemeleri Listele**
Bu servis ile transfer talebi yapılmış ancak alıcı hesap hatası nedeniyle geri dönen ödemelerin listesine ulaşabilirsiniz. Geri dönen ödemeler mağazanıza ait bir alt hesaba bakiye olarak işlenir. Geri dönen bu ödemeleri tekrar göndermek için “Geri Dönen Ödemeler – Hesaptan Gönder” servisini kullanabilirsiniz.
<br>

- **Geri Dönen Ödemeleri Hesaptan Gönder**
Bu servis ile transfer talebi yapılmış ancak alıcı hesap hatası nedeniyle geri dönen ödemeler için tekrar ödeme isteği gönderebilirsiniz. Geri dönen bu ödemelerin listesine “Geri Dönen Ödemeler – Listele API” servisi ile ulaşabilirsiniz.
<br>

- **Geri Dönen Ödemeler Callback**
Geri dönen ödemelerden oluşturacağınız transfer talebi sonrasında Success yanıtı almanız ile birlikte hesaptan gönderme talebiniz PayTR sistemi tarafından başarılı olarak alınmış olur. PayTR sistemi talebinizi ortalama 5 dakika içerisinde işleme alacak, gönderdiğiniz trans_info içeriğini kontrol ederek transferleri gerçekleştirecektir. Kontrol sırasında hatalı bilgi tespiti halinde ilgili işlem başarısız olarak işaretlenir. Oluşan sonuç JSON formatında PayTR Mağaza Paneli > Ayarlar > Platform Transfer Sonucu Bildirim URL olarak tanımladığınız adrese POST edilerek bildirilir.

---

#### iade API
Bu servis aracılığıyla, siparişe ait tutarın bir kısmı veya tamamı için iade işlemi gerçekleştirebilirsiniz. Bunun için sipariş numarası, iade edilecek tutar VE dökümandaki diğer istenilen bilgilerin ilgili servise POST metodu ile istek atılması gerekmektedir.

---

#### Durum Sorgu API
Durum Sorgu servisi aracılığıyla, mağazanız üzerinde gerçekleştirilen işlemlerin durumunu sorgulayabilirsiniz. Mağaza Durum Sorgulama ve Pazaryeri Durum Sorgulama olarak iki kategoriye ayrılır. 

---

#### BKM Express iFrame API
BKM Express servisini kullanarak BKM Express sisteminde kayıtlı olan kartlar aracılığıyla ödeme alabilirsiniz. BKM Express Entegrasyonu iFrame ödeme yönteminde otomatik olarak ödeme ekranına gelmektedir. Ancak "Direkt API" çözümünde BKM Express entegrasyonu yaparken **$payment_type = "bex"** olarak gönderilmesi gerekmektedir. 

---

#### işlem Dökümü
İşlem dökümü servisi ile, iletilen tarih aralığındaki (en fazla 3 gün) yapılan satış ve iade işlemlerinin dökümünü alabilirsiniz.

---

#### Test Kart Bilgileri
> Aşağıdaki test kart bilgileri yalnızca **Direkt API** çözümü için geçerlidir. iFrame API yönteminde test kart bilgileri otomatik olarak gelmektedir.

| Kart bilgileri | Alabileceği değerler | Açıklama                               |
|----------------|----------------------|----------------------------------------|
| Adı Soyadı     | PAYTR TEST           | Dilediğiniz şekilde gönderebilirsiniz. |
| Kart No        | 4355 0843 5508 4358  | Bu değer zorunludur.                   |
| Son Kullanma   | 12 / 24              | Dilediğiniz şekilde gönderebilirsiniz. |
| CVV            | 000                  | Bu değer zorunludur.                   |


| Kart bilgileri | Alabileceği değerler | Açıklama                               |
|----------------|----------------------|----------------------------------------|
| Adı Soyadı     | PAYTR TEST           | Dilediğiniz şekilde gönderebilirsiniz. |
| Kart No        | 5406 6754 0667 5403  | Bu değer zorunludur.                   |
| Son Kullanma   | 12 / 24              | Dilediğiniz şekilde gönderebilirsiniz. |
| CVV            | 000                  | Bu değer zorunludur.                   |


| Kart bilgileri | Alabileceği değerler | Açıklama                               |
|----------------|----------------------|----------------------------------------|
| Adı Soyadı     | PAYTR TEST           | Dilediğiniz şekilde gönderebilirsiniz. |
| Kart No        | 9792 0303 9444 0796  | Bu değer zorunludur.                   |
| Son Kullanma   | 12 / 24              | Dilediğiniz şekilde gönderebilirsiniz. |
| CVV            | 000                  | Bu değer zorunludur.                   |


---

## Sosyal Medya Hesaplarımız :mailbox_with_no_mail:
[![Facebook](https://img.shields.io/badge/Facebook-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://facebook.com/paytrcom/)   [![Twitter](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/paytrcom)    [![Instagram](https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://www.instagram.com/paytrcom/)   [![LinkenIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://tr.linkedin.com/company/paytr)    [![YouTube](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/channel/UCX1trqvEZnXcLWXXFRG3Atg)    [![GooglePlay](https://img.shields.io/badge/Google_Play-414141?style=for-the-badge&logo=google-play&logoColor=white)](https://play.google.com/store/apps/details?id=com.magaza.paytr)   [![AppStore](https://img.shields.io/badge/App_Store-0D96F6?style=for-the-badge&logo=app-store&logoColor=white)](https://apps.apple.com/us/app/paytr-ma%C4%9Faza/id1559727339)
