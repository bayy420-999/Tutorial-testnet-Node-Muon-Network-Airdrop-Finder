# Tutorial testnet Node Muon Network Airdrop Finder

<p style="font-size:14px" align="right">
<a href="https://t.me/airdropfind" target="_blank">Join Telegram Airdrop Finder<img src="https://user-images.githubusercontent.com/50621007/183283867-56b4d69f-bc6e-4939-b00a-72aa019d1aea.png" width="30"/></a>
</p>

<p align="center">
  <img height="auto" width="auto" src="https://raw.githubusercontent.com/bayy420-999/airdropfind/main/NavIcon.png">
</p>

## Referensi

* [Dokumen resmi](https://docs.muon.net/muon-network/muon-nodes/joining-the-testnet-alice)
* [Server discord](https://discord.gg/muon)
* [Node dashboard](https://alice.muon.net/join/)
* [tBNB (BNB Testnet faucet)](https://testnet.bnbchain.org/faucet-smart)

## Spesifikasi Software & Hardware

### Persyaratan Hardware

| Komponen | Spesifikasi minimal |
|----------|---------------------|
|CPU|4 Cores|
|RAM|8 GB DDR4 RAM|
|Penyimpanan|1 TB HDD|
|Koneksi|10Mbit/s port|

| Komponen | Spesifikasi rekomendasi |
|----------|---------------------|
|CPU|32 Cores|
|RAM|32 GB DDR4 RAM|
|Penyimpanan|2 x 1 TB NVMe SSD|
|Koneksi|1 Gbit/s port|

### Persyaratan Software/OS

| Komponen | Spesifikasi minimal |
|----------|---------------------|
|Sistem Operasi|Ubuntu 16.04|

| Komponen | Spesifikasi rekomendasi |
|----------|---------------------|
|Sistem Operasi|Ubuntu 22.04|

## Setup Node



### Install docker

Jika kalian kalian pernah ikut Q-Blockchain dan testnet node lainnya kemungkinan kalian sudah pernah install docker, jadi bisa skip langkah ini.

1. Update `apt-get` dan install paket yang diperlukan
   ```console
   sudo apt-get update
   sudo apt-get install \
     ca-certificates \
     curl \
     gnupg \
     lsb-release
   ```
2. Tambahkan kunci GPG docker
   ```console
   sudo mkdir -p /etc/apt/keyrings
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
   ```
3. Setup repositori
   ```console
   echo \
   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```
4. Install docker
   ```console
   sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
   ```
5. Cek apakah docker sudah terinstall dengan benar
   ```console
   sudo docker run hello-world
   ```

### Download, install, dan jalankan Node

Pastikan kalian sudah install docker, jika belum ikuti tutorial diatas

1. Install dependensi Linux
   ```console
   apt-get install screen git
   ```
2. Download Node
   ```console
   git clone https://github.com/muon-protocol/muon-node-js.git --recurse-submodules --branch testnet
   ```
3. Pindah ke folder Node
   ```console
   cd muon-node-js
   ```
4. Build Node
   Pertama buka terminal baru dengan menggunakan screen (karena proses build Node lama)
   ```console
   screen -Rd moun-network
   ```
   Lalu build Node menggunakan perintah dibawah
   ```console
   docker-compose build
   ```
5. Jalankan Node
   ```console
   docker-compose up -d
   ```
  
### Daftar menjadi validator

1. Cek status Node
   ```console
   curl http://127.0.0.1:8000/status
   ```
   Nanti akan keluar output seperti ini di terminal
   ```console
   {"address":"0x06A85356DCb5b307096726FB86A78c59D38e08ee",
    "peerId":"Qma3GsJmB47xYuyahPZPSadh1avvxfyYQwk8R3UnFrQ6aP",
    "managerContract":{"network":"bsctest","address":"0x2efB53c11FC935f6114B3fC37AaFa6a76B263a4E"},
    "shield":{"enable":false,"apps":[]},"addedToNetwork":false}
   ```
   Salin `address` dan `peerId`
2. Pergi ke [dashboard](https://alice.muon.net/join/)
3. Connect wallet menggunakan Metamask
4. Switch Network ke `BSC Testnet`
5. Mint 1000 ALICE token (Kalian harus punya tBNB untuk fee transaksi)
6. Approve token (Konfirmasi di Metamask)
7. Nanti akan ada form pendaftaran, masukan `address` dan `peerId` yang disalin tadi
8. Klik `ADD NODE` (Konfirmasi di Metamask)
9. Cek apakah Node sudah terdaftar
   Balik ke VPS, terus ketik perintah ini
   ```console
   curl http://127.0.0.1:8000/v1/?app=tss&method=test
   ```
   Jika keluar output seperti ini di terminal berarti pendaftaran sukses
   ```console
   {"success":true,"result":{"confirmed":true, ... }}
   ```

## Troubleshoot
Nanti aja
