# Arthera-Node-Kurulum-Rehberi.

# Arthera Validator Node Setup

Bu rehber, Arthera platformunda bir doğrulayıcı düğümünün nasıl kurulacağını adım adım açıklar.

## Gereksinimler

- İşlemci: 4 çekirdek / 8 iş parçacığı, 2.6GHz veya daha hızlı
- RAM: 8GB veya daha fazla
- Disk: 500GB SSD depolama veya daha fazlası
- Ağ: 1GBps, Genel IP

## Adım 1: Docker'ın Kurulumu

İlk olarak, Docker'ı kurmanız gerekiyor. Docker kurulum kılavuzuna [buradan](https://docs.docker.com/get-docker/) ulaşabilirsiniz.

## Adım 2: Arthera Node Görüntüsünün Çekilmesi

Son Arthera node görüntüsünü çekin.

```bash
docker pull arthera/arthera-node:latest
````

# Adım 3: Arthera Node Verilerini Saklamak İçin Bir Klasör Oluşturma

- Arthera node verilerini saklamak için bir klasör oluşturun.
````
mkdir $HOME/arthera
````

# Adım 4: Doğrulayıcı İçin Cüzdan Oluşturma
- Doğrulayıcı için bir cüzdan oluşturun.
````
docker run -it -v $HOME/arthera:/data arthera/arthera-node:latest account new
````
- Oluşturulan doğrulayıcı kimliği anahtar dosyasını güvenli bir yere kopyalayın, public key'i kaydedin ve şifreyi hatırlayın.

# Adım 7: Doğrulayıcıyı Kaydetme. Doğrulayıcıyı kaydetmek için Arthera cüzdanını kullanmanız gerekmektedir:

- Oluşturduğunuz cüzdanın private key'ini Metamask'e ekleyin.
- Metamask'te doğrulayıcı için yeni bir cüzdan oluşturun.
- https://wallet-test.arthera.net adresine gidin.
- Metamask ile giriş yapın ve import ettiğiniz hesabı seçin.
- Arthera Cüzdan'ında "Account" menüsüne gidin.
- "Become a Validator" bölümünde oluşturduğunuz doğrulayıcı public key'ini girin.
- "Register" butonuna tıklayın.

## Başarılıysa, doğrulayıcı ID'niz görüntülenir.

# Adım 8: Şifre Dosyası Oluşturma
- Aşağıdaki komutu çalıştırarak bir şifre dosyası oluşturun:
````
echo "ŞİFRENİZ" > $HOME/arthera/keystore/validator/password
````
# Adım 9: Düğümü Başlatma
- Aşağıdaki komutu kullanarak doğrulayıcı düğümünüzü başlatın:
````
docker run -v $HOME/arthera:/data arthera/arthera-node:latest \
  --testnet \
  --nat extip:SİZİN_GENEL_IP_ADRESİNİZ \
  --validator.id ADIM_7DEN_ALINAN_VALIDATOR_ID \
  --validator.pubkey "ADIM_6DAN_ALINAN_PUBLIC_KEY" \
  --validator.password "/data/keystore/validator/password"
````
- Başarıyla Arthera doğrulayıcı düğümünüzü başlatmış olmalısınız.

# Lütfen beğenmeyi ve forklamayı unutmayın.
