
# Jitsi (Video Bridge) Monitoring
> [Jitsi](https://jitsi.org/what-is-jitsi/) = Proyek opensource untuk solusi konferensi video yang aman.\
> [Jitsi Video Bridge](https://github.com/jitsi/jitsi-videobridge) = Router video untuk WebRTC.

###### Desclaimer
This repo's guide is written in Bahasa Indonesia. This repo is intended as learning purpose or trial.\
Petunjuk repo ini ditulis dalam Bahasa Indonesia. Repo ini ditujukan untuk tujuan pembelajaran atau percobaan.

## Daftar Cek Pekerjaan
- [x] REST
- [ ] XMPP MUC

## Dokumentasi Jitsi Statistics
- https://github.com/jitsi/jitsi-videobridge/blob/master/doc/statistics.md

## Cara Mencoba
1. Pastikan bahwa Docker dan Docker-Compose sudah terinstall.\
[Cara Install Docker](https://docs.docker.com/get-docker/) dan [Cara Install Docker-Compose](https://docs.docker.com/compose/install/)
2. Clone repo ini
     ```
      $ git clone https://github.com/haidlir/jitsi-monitoring.git
    ```
3. Hidupkan dengan mengeksekusi file up.sh
   ```
    $ ./up.sh
   ```
4. Buka Grafana di http://localhost:3000
5. Buat data source ke InfluxDB\
Username dan Pasword dapat dilihat di file ```.env```
6. Import Dashboard dari file ```fixtures/grafana-jvb.json```
7. Konfigurasi Jitsi Video Bridge (JVB)\
- file videobridge/config
```
# extra options to pass to the JVB daemon
JVB_OPTS="--apis=rest"
```
- file videobridge/sip-communicator.properties
```
# Additional Configuration
org.jitsi.videobridge.rest.private.jetty.port=8080
org.jitsi.videobridge.ENABLE_STATISTICS=true
org.jitsi.videobridge.STATISTICS_TRANSPORT=colibri
```
8. Ubah konfigurasi telegraf sesuai dengan komponen JVB yang ingin dimonitor\
Contoh:
```
  ...
  ## List of urls to query.
  urls = ["http://meet.example.com:8080/about/health"]
  ...
  ## URL of each server in the service's cluster
  urls = [
    "http://meet.example.com:8080/colibri/stats",
  ]
  ...
```

### Cuplikan Gambar
![Grafana-JVB](https://raw.githubusercontent.com/haidlir/jitsi-monitoring/master/img/grafana-jvb.png "Grafana-JVB")

## Credits
1. InfluxData
2. Grafana Labs
3. Jitsi

###### Notes
Bila butuh bantuan dalam mengimplementasikan hal serupa di lingkungan produksi atau operasional, kami terbuka untuk berkolaborasi. [Kontak kami](http://www.netmonk.id)