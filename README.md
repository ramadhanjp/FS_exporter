# FS_exporter
#### _Monitoring Root Filesystem_

![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=Prometheus&logoColor=white) ![Grafana](https://img.shields.io/badge/grafana-%23F46800.svg?style=for-the-badge&logo=grafana&logoColor=white)

FS_exporter adalah sebuah tool atau exporter yang digunakan untuk memonitoring resource Root File System pada sistem operasi Linux menggunakan Prometheus dan Grafana. Dengan FS_exporter, kamu dapat mengumpulkan berbagai metrik terkait penggunaan storage pada file system root, seperti total storage, storage yang digunakan, storage yang tersedia, serta file system yang penuh. Exporter ini memungkinkan integrasi dengan Prometheus untuk scraping metrik, dan Grafana untuk visualisasi data tersebut dalam bentuk grafik atau dashboard yang mudah dipahami.

Fungsi utama FS_exporter antara lain:
- Mengumpulkan Metrik Storage: Total kapasitas storage, storage yang digunakan, dan storage yang tersedia pada root file system.
- Monitoring File System: Mengidentifikasi file system yang penuh dan file apa yang menyebabkan penuh.
- Integrasi dengan Prometheus dan Grafana: Memungkinkan pengumpulan data oleh Prometheus dan visualisasi di Grafana.

## Installation
#### Langkah 1: Konfigurasi FS_exporter
###### 1. Download *fs_exporter* menggunakan wget

```sh
wget https://github.com/ramadhanjp/FS_exporter/releases/download/prometheus/fs_exporter.linux-amd64.tar.gz
```

###### 2. Pindahkan file binary ke directory yang sesuai (misalnya /usr/local/bin)

```sh
mv fs_exporter /usr/local/bin
```
###### 3. Buat file *fs_exporter* menjadi executable
```sh
chmod +x /usr/local/bin/fs_exporter
```
###### 4. Buat file unit untuk fs_exporter
```sh
nano /etc/systemd/system/fs_exporter.service
```
Isi file dengan konfigurasi berikut
```sh
[Unit]
Description=Root Filesystem Exporter
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/fs_exporter
Restart=always

[Install]
WantedBy=default.target
```
###### 5.Reload systemd dan start *fs_exporter*
```sh
systemctl daemon-reload
systemctl enable fs_exporter
systemctl start fs_exporter
```
#### Langkah 2: Konfigurasi Prometheus
###### 1. Edit file konfigurasi Prometheus
*Biasanya, file konfigurasi Prometheus terletak di /etc/prometheus/prometheus.yml. Tambahkan job baru untuk fs_exporter di dalamnya. Misalnya:*
```sh
scrape_configs:
  - job_name: 'fs_exporter'
    static_configs:
      - targets: ['<IP_ADDRESS>:8000']
```
> Note: Gantilah `<IP_ADDRESS>` dengan alamat IP server di mana fs_exporter berjalan. Jika rootfs_exporter berjalan di server yang sama dengan prometheus, Anda bisa menggunakan localhost

###### 2. Restart Prometheus
```sh
systemctl restart prometheus
```

#### Langkah 3: Integrasi dengan Grafana
###### 2. Import Dashboard untuk rootfs_exporter
Pergi ke *Create > Import*. Cari dashboard fs_exporter dan pilih prometheus sebagai datasource nya.

###### 2. Contoh dashboard 
![dashboard_rootfs](https://github.com/ramadhanjp/RootFS_exporter/assets/173976735/1477bdeb-720b-4c17-a4f8-e6626eaee7ac)



## Docker



## License

MIT

**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
