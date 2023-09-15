# Dokumentasi Websocket

## Daftar Isi
1. [Memulai Koneksi ke Websocket](#memulai-koneksi-ke-websocket)
2. [Mengirim Pesan](#mengirim-pesan)
3. [Mengirim Ping](#mengirim-ping)
4. [Menentukan Admin](#menentukan-admin)
5. [Menyetujui Koneksi Pengguna](#menyetujui-koneksi-pengguna)

## Memulai Koneksi ke Websocket
Untuk memulai koneksi ke websocket, gunakan URL yang telah Anda buat di dashboard Anda. Saat aplikasi Anda terhubung ke server, server akan mengirim pesan berisi ID koneksi Anda. ID ini dapat digunakan oleh pengguna lain untuk mengirim pesan secara langsung ke Anda.

**Catatan**: Setiap pengguna akan secara otomatis terputus dalam 1 menit kecuali disetujui oleh admin atau jika pengguna tersebut mengubah statusnya menjadi admin. Setiap kali ada pengguna baru yang terhubung, sistem akan mengirimkan ID koneksi pengguna tersebut ke admin.

**Contoh Respon**:
`{"from":"system","id":"20d2e4f5-2986-427c-bc85-3d2c10fa564b"}`

**Contoh Pesan ke Admin**:
`{"from":"system","new_id":"20d2e4f5-2986-427c-bc85-3d2c10fa564b"}`

## Mengirim Pesan
Untuk mengirim pesan, gunakan format JSON dengan properti `to` dan `data`.

- `to`: Tujuan pengiriman pesan. Bisa ke satu pengguna dengan ID koneksi atau ke semua pengguna dengan isian "all".
- `data`: Bisa berisi string atau objek yang akan dikirim.

**Contoh**:
`{"to":"all","data":"pesan percobaan"}`

`{"to":"20d2e4f5-2986-427c-bc85-3d2c10fa564b","data":"pesan percobaan"}`

`{"to":"20d2e4f5-2986-427c-bc85-3d2c10fa564b","data":{"event":"join"}}`

## Mengirim Ping
Untuk mengirim ping, gunakan format string dengan isian "ping". Server akan merespons dengan JSON `{"system":"pong"}`.

## Menentukan Admin
Admin memiliki kemampuan untuk menyetujui koneksi dari setiap pengguna yang terhubung. Untuk menjadi admin, kirimkan pesan dengan format JSON berikut:

- `to`: Diisi dengan "system".
- `event`: Diisi dengan "admin".
- `key`: Diisi dengan kunci yang terdapat di dashboard Anda.

**Contoh**:
`{"to":"system","event":"admin","key":"hfB2ZCr8PtlRPrv4i8fVOp0Zr9ChEWoPaCYjGFHr"}`

**Contoh Respon**:
`{"from":"system","event":"admin","status":"success"}`

## Menyetujui Koneksi Pengguna
Untuk menyetujui koneksi pengguna, kirimkan pesan dengan format JSON berikut:

- `to`: Diisi dengan "system".
- `event`: Diisi dengan "approved".
- `id`: Diisi dengan ID pengguna yang ingin disetujui.

**Contoh**:
`{"to":"system","event":"approved","id":"20d2e4f5-2986-427c-bc85-3d2c10fa564b"}`

**Contoh Respon**:
`{"from":"system","event":"approved","id":"20d2e4f5-2986-427c-bc85-3d2c10fa564b","status":"success"}`
