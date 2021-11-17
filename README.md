
# POSTMAN COLLECTIONS for PAYTR APIs

PayTR tarafından yayınlanmış olan servislerin testlerini daha kolay bir şekilde gerçekleştirmenize imkan tanıyan "Postman" programına ait Collections dosyalarını kullanmaya başlayabilirsiniz.

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
- Request penceresinde bulunan form alanlarındaki değerleri kendi isteğinize göre değiştiriebilir, sonrasında **Send** butonuna tıklayarak servisi çağırabilirsiniz.
- Ekranının alt kısmındaki Response panelinde, servisten dönen cevap olarak başarılı/hatalı çıktılar gösterilecektir.

> **Tüm işlemler bu kadardı... PayTR servislerini test etmeye hemen başlayabilirsiniz.**

