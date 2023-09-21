# Dokumentasi Socket.my.id

Website: [socket.my.id](https://socket.my.id)

## Daftar Isi
1. [Memulai Koneksi ke Websocket](#memulai-koneksi-ke-websocket)
2. [Mengirim Pesan](#mengirim-pesan)
3. [Mengirim Ping](#mengirim-ping)
4. [Menentukan Admin](#menentukan-admin)
5. [Menyetujui Koneksi Pengguna](#menyetujui-koneksi-pengguna)

## Memulai Koneksi ke Websocket
Untuk memulai koneksi ke websocket, gunakan URL yang telah Anda buat di [dashboard](https://socket.my.id) Anda. Saat aplikasi Anda terhubung ke server, server akan mengirim pesan berisi ID koneksi Anda. ID ini dapat digunakan oleh pengguna lain untuk mengirim pesan secara langsung ke Anda.

**Catatan**: Setiap pengguna akan secara otomatis terputus dalam 15 detik kecuali disetujui oleh admin atau jika pengguna tersebut mengubah statusnya menjadi admin. Setiap kali ada pengguna baru yang terhubung, sistem akan mengirimkan ID koneksi pengguna tersebut ke admin.

**Contoh Respon**:

`{"from":"system","id":"20d2e4f5-2986-427c-bc85-3d2c10fa564b"}`

## Mengirim Pesan
Untuk mengirim pesan, gunakan format JSON dengan properti `to` dan `body`.

- `to`: Tujuan pengiriman pesan. Bisa ke satu pengguna dengan ID koneksi atau ke semua pengguna dengan isian "all".
- `body`: Bisa berisi string atau objek yang akan dikirim.

**Contoh Pesan**:

```json
{"to":"all","body":"pesan percobaan"}
```

```json
{"to":"20d2e4f5-2986-427c-bc85-3d2c10fa564b","body":"pesan percobaan"}
```

```json
{"to":"20d2e4f5-2986-427c-bc85-3d2c10fa564b","body":{"event":"join"}}
```

## Mengirim Ping
Untuk mengirim ping, gunakan format string dengan isian "ping". Server akan merespons dengan JSON `{"data":"pong","from":"system"}`.

## Menentukan Admin
Admin memiliki kemampuan untuk menyetujui koneksi dari setiap pengguna yang terhubung. Untuk menjadi admin, kirimkan pesan dengan format JSON berikut:

- `to`: Diisi dengan "system".
- `event`: Diisi dengan "admin".
- `key`: Diisi dengan kunci yang terdapat di dashboard Anda.

**Contoh Pesan**:

```json
{"to":"system","event":"admin","key":"hfB2ZCr8PtlRPrv4i8fVOp0Zr9ChEWoPaCYjGFHr"}
```

**Contoh Respon**:

`{"from":"system","event":"admin","status":"success"}`

## Menyetujui Koneksi Pengguna
Untuk menyetujui koneksi pengguna, kirimkan pesan dengan format JSON berikut:

- `to`: Diisi dengan "system".
- `event`: Diisi dengan "approved".
- `id`: Diisi dengan ID pengguna yang ingin disetujui.

**Contoh Pesan**:

```json
{"to":"system","event":"approved","id":"20d2e4f5-2986-427c-bc85-3d2c10fa564b"}
```

**Contoh Respon**:

`{"from":"system","event":"approved","id":"20d2e4f5-2986-427c-bc85-3d2c10fa564b","status":"success"}`
