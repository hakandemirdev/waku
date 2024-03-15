# Waku
<img src="https://github.com/hakandemirdev/waku/blob/fb0f1b4990da283c41fcddc6122b811ad23e5d77/waku_logo.jpg" width="auto">

[Waku Web Sitesi](https://waku.org) 

[Waku Twitter](https://twitter.com/Waku_org/)

[Waku Discord](https://discord.com/invite/gMPAzmcDER)


Öncelikle işletim sistemimizi güncelliyoruz.
```
sudo apt update && sudo apt upgrade -y
```
Temel paketleri yüklüyoruz.
```
sudo apt-get install build-essential git libpq5 jq -y
```
Rust Yüklüyoruz.
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source "$HOME/.cargo/env"
```
Docker Kurulumu
```
sudo apt install docker.io -y
sudo curl -L "https://github.com/docker/compose/releases/download/v2.24.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
Waku Kurulumu
```
git clone https://github.com/waku-org/nwaku-compose
cd nwaku-compose
cp .env.example .env
```
Gerekli ayarları yapıyoruz.
env dosyası içerisinde aşağıdaki kısımları düzenliyoruz.

ETH_CLIENT_ADDRESS = Infura veya Alchemy'den Sepolia RPC alıyoruz. https://www.infura.io/ - https://www.alchemy.com

ETH_TESTNET_KEY = Metamask adresimizin private key'ini buraya yazıyoruz.

RLN_RELAY_CRED_PASSWORD = Şifre belirleyip yazıyoruz.


```
nano .env
```
Waku ağında dahil olmak için kayıt oluyoruz.
```
./register_rln.sh
```
Port ayarlarımızı yapıyoruz.
```
sudo ufw enable
sudo ufw allow 22    
sudo ufw allow 3000   
sudo ufw allow 8545   
sudo ufw allow 8645   
sudo ufw allow 9005   
sudo ufw allow 30304  
sudo ufw allow 8645

```
Waku Node Başlatma

```
docker-compose up -d
```
Log Kontrolü. Bu komutlarla loglarınızı kontrol edebilirsiniz.
```
docker-compose ps
docker-compose logs nwaku
```

Kontrol. 
Aşağıdaki komutlar çıktı veriyorsa node'unuz doğru çalışıyor demektir.
```
curl --location 'http://127.0.0.1:8645/debug/v1/version'
curl --location 'http://127.0.0.1:8645/debug/v1/info
```

Monitoring
```
http://ip_address:3000/d/yns_4vFVk/nwaku-monitoring
```

