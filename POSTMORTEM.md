# Blameless Postmortem - Insiden Kegagalan Deployment Manual

## Ringkasan Insiden
Pada JOB 2 dilakukan proses deployment aplikasi secara manual dari Developer kepada Operations.
 Artefak yang diserahkan hanya berisi folder src/ dan HANDOVER.md tanpa requirements.txt.
 Operations harus menjalankan aplikasi berdasarkan instruksi serah-terima yang tersedia.
 Selama proses tersebut terjadi beberapa kegagalan sebelum aplikasi berhasil dijalankan.

## Kronologi (timeline)
1. Operations menerima artefak dan dokumen HANDOVER.md dari Developer.
2. Operations mencoba menjalankan aplikasi berdasarkan instruksi yang tersedia.
3. Proses deployment mengalami kegagalan karena informasi dependensi dan konfigurasi lingkungan belum lengkap.
4. Operations melakukan troubleshooting terhadap kegagalan yang ditemukan.
5. Setelah beberapa percobaan dan perbaikan, aplikasi berhasil dijalankan dan diverifikasi menggunakan curl.

## Dampak (waktu terbuang, jumlah kegagalan)

- Lead Time deployment manual: 1 menit 55 detik.
- Jumlah kegagalan (failed attempts): 2 kali.
- Status akhir deployment: berhasil.
- Terjadi waktu tambahan untuk troubleshooting karena artefak serah-terima belum lengkap.

## Akar Masalah pada SISTEM (bukan pada orang)
Akar masalah bukan terletak pada individu, tetapi pada desain proses deployment yang masih manual.
 Sistem serah-terima belum memastikan seluruh dependensi dan konfigurasi lingkungan terdokumentasi serta tersedia bersama artefak aplikasi. 
Selain itu, belum terdapat mekanisme otomatis untuk menyiapkan environment, memasang dependensi, menjalankan aplikasi, dan melakukan health check.

## Tindakan Perbaikan (action items) + penanggung jawab peran
- Developer: menyediakan requirements.txt yang lengkap dan terkontrol melalui version control.
- Developer: menyediakan setup.sh untuk mengotomasi proses setup dan deployment.
- Operations: menjalankan deployment menggunakan prosedur otomasi yang telah disediakan.
- Tim Dev dan Ops: memastikan dokumentasi dan artefak deployment tersimpan pada repository yang sama.
- Tim Dev dan Ops: menggunakan health check untuk memastikan aplikasi berhasil berjalan setelah deployment.

## Pelajaran yang Diambil
Deployment manual dapat menyebabkan pemborosan waktu dan meningkatkan kemungkinan kegagalan karena ketergantungan pada instruksi dan langkah manual. 
Otomasi membantu menciptakan proses deployment yang lebih konsisten, dapat diulang, dan mengurangi kebutuhan komunikasi tambahan antara Developer dan Operations. 
Kegagalan sebaiknya digunakan sebagai dasar untuk memperbaiki sistem kerja, bukan untuk menyalahkan individu.
