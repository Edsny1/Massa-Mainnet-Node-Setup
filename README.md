
![Massa jpeg](https://github.com/Edsny1/Massa-Mainnet-Node-Setup/assets/98622870/a06b01e1-c657-4cea-981d-b62a186b480c)



# Massa-Mainnet-Node-Setup
Massalabs Mainnet Installing a node
1-Öncelikle sunucumuzu güncelliyoruz ( We are updating our server )
-	sudo apt-get update
-	sudo apt-get upgrade

2-Screen açabilmek için screen yüklüyoruz. ( We are loading screen)
-	sudo apt install screen

Screen açıyoruz. ( We open the screen)
-	screen -S Massa

3-Portları açalım. ( Let’s open the Ports )
-	sudo apt install ufw -y
-	sudo ufw allow 22
-	sudo ufw allow ssh
-	sudo ufw allow 31244/tcp
-	sudo ufw allow 31245/tcp
-	sudo ufw enable

4-Kütüphaneden verileri yükleyelim ( Let’s load data from the library )
-	sudo apt install pkg-config curl git build-essential libssl-dev libclang-dev cmake

5-Rustup yükleyelim ( İnstall Rustup )
-	curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
-	source $HOME/.cargo/env
Versiyon Kontrol edelim ( Version Control )( Optional)
-	rustc –version
-	rustup toolchain install 1.74.1
-	rustup default 1.74.1
-	rustc –version (Çıktı 1.74.1 olmalı) (Optional)

6-Repoyu Kopyalayalım ( Clone this repo )
-	git clone https://github.com/massalabs/massa.git

7-Sunucu İp Adresimizi Kaydedelim ( Let’s save our Server Ip Address )
-	massa-node/config/config.toml

Açılan sayfada ( On the opened page );
-	[protocol]
routable_ip = "AAA.BBB.CCC.DDD" 

*** ( AAA.BBB.CCC.DDD Sunucu ip adresinizle değiştirilmelidir )
*** ( Should be replaced with your public IP address )
**** Sunucunuz destekliyorsa IPV6 kullanabilirsiniz. ( IPV6 is also supported. )

-	Ctrl X daha sonra Y ile kaydedip Enter ile çıkıyoruz. ( Ctrl X then save with Y and exit with Enter )
-	get_status (Kontrol Ediyoruz) (We Check)
-	Node's IP: AAA.BBB.CCC.DDD  (Çıktı bu şekkilde olmalı) ( The output should be like this )

*** “ No routable IP ” çıktısı alıyorsanız 7.adımı tekrar yapalım. ( If the output is like this, let’s repeat step 7. )

8-Düğümü Yapılandırma ( Configure the Node )
-	cd massa/massa-node/
-	./massa-node -p <PASSWORD> |& tee logs.txt

*** <PASSWORD>  kısmına unutmayacağınız bir şifre belirleyin.) (Replace <PASSWORD> with a password that you will need to keep to restart your node. You should leave the window open. )

9-İkinci bir Screen açalım ( Let’s open a second screen );
-	cd massa/massa-client/
-	./massa-client -p <PASSWORD>

*** <PASSWORD> 8. Adımda belirlediğimiz şifreyi kullanabiliriz. (Replace <PASSWORD> with a password that you will need to keep to restart your client)

10- Düğüm başlatma ( Start the node );
İlk Screen’e geri dönüyoruz ( In a first Window )
-	cd massa/massa-node/
-	RUST_BACKTRACE=full cargo run --release -- -p <PASSWORD> |& tee logs.txt
*** <PASSWORD> kısmına 8. Adımda belirlediğimiz şifreyi yazıyoruz. (We write the password we determined in step 8.)

Düğümümüzü başlattık.

 
11- Client Başlatma. (Start the Client)
İkinci Screen’e geri dönüyoruz. (In a second Window)
-	cd massa/massa-client/
-	cargo run --release -- -p <PASSWORD>
*** <PASSWORD> kısmına 9.Adımda belirlediğimiz şifreyi yazıyoruz. ( We write the password we determined in step 8.)

***** Screen’ler arası geçişi Ctrl A+P ile yapabilirsiniz.

12- Cüzdan Ekleme (Add Wallet);
Client’in olduğu screen giriyoruz. (We enter the window there the client is)
-	cd massa/massa-client/
-	cargo run
-	wallet_add_secret_keys <your_secret_key>
Cüzdanımızı ekledik. (Wallet Add)
13- Cüzdan bakiye ve bilgilerini kontrol etmek için ( Wallet info )
-	wallet_info
*Adres keyleri için ( Public key’s addresse)
-	wallet_get_public_key <Address1> <Address2>
-	wallet_get_secret_key <Address1> <Address2>

14- Roll Satın almak ve Stake işlemi( Buying Rolls and Staking)
-	wallet_info
-	buy_rolls <address> <roll count> <fee>
Örnek (Example): 
buy_rolls A12dr48yZaL2NpQkwsrpsNLGDpndFUCVSdYdSiQh4UfkYRMo17km 1 0

Saking:
-	node_start_staking <your_address>

Tebrikler Düğümünüz artık çalışıyor. ( Congratulations. Your node is now running)



