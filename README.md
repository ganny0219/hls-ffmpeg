Sebelumnya memulai Download dan Install FFMPEG

1. Buat folder dengan nama movie yang diinginkan

![napo-folder](https://github.com/ganny0219/hls-ffmpeg/assets/43429378/f3c077de-dc74-4e72-a035-2b97f81b6766)

2. masukan file film dengan format mp4

![napo-folder](https://github.com/ganny0219/hls-ffmpeg/assets/43429378/e927fe3d-cb96-4c72-87f1-378248ceb545)

3. Buat folder resolusi yang diinginkan

![napo-folder](https://github.com/ganny0219/hls-ffmpeg/assets/43429378/4cb4e914-4ee3-4c50-aa1e-102ea912cb2b)

5. buka cmd dan masuk ke folder directory yang sudah di buat tadi
  
![napo-folder](https://github.com/ganny0219/hls-ffmpeg/assets/43429378/cfe78c29-5815-4c56-9bd3-37cb45ef49ab)

6. Masukan comand line berikut:

240p
------------------------
ffmpeg -i [NAMA-FILE-INPUT].mp4 -vf "scale=426:240" -c:v libx264 -b:v 400k -profile:v main -level:v 3.1 -g 60 -keyint_min 60 -sc_threshold 0 -c:a aac -b:a 64k -ar 48000 -f hls -hls_time 10 -hls_list_size 0 -var_stream_map "v:0,a:0" -master_pl_name [NAMA-FILE-OUTPUT].m3u8 -y 240p/240p.m3u8

ffmpeg -i napo.mp4 -vf "scale=426:240" -c:v libx264 -b:v 400k -profile:v main -level:v 3.1 -g 60 -keyint_min 60 -sc_threshold 0 -c:a aac -b:a 64k -ar 48000 -f hls -hls_time 10 -hls_list_size 0 -var_stream_map "v:0,a:0" -master_pl_name napo.m3u8 -y 240p/240p.m3u8

480p
------------------------
ffmpeg -i [NAMA-FILE-INPUT].mp4 -vf "scale=854:480" -c:v libx264 -b:v 800k -profile:v main -level:v 3.1 -g 60 -keyint_min 60 -sc_threshold 0 -c:a aac -b:a 96k -ar 48000 -f hls -hls_time 10 -hls_list_size 0 -var_stream_map "v:0,a:0" -master_pl_name [NAMA-FILE-OUTPUT].m3u8 -y 480p/480p.m3u8

720p
------------------------
ffmpeg -i [NAMA-FILE-INPUT].mp4 -vf "scale=1280:720" -c:v libx264 -b:v 1500k -profile:v main -level:v 3.1 -g 60 -keyint_min 60 -sc_threshold 0 -c:a aac -b:a 128k -ar 48000 -f hls -hls_time 10 -hls_list_size 0 -var_stream_map "v:0,a:0" -master_pl_name [NAMA-FILE-OUTPUT].m3u8 -y 480p/720p.m3u8


Penjelasan Comand Line :

-i input.mp4: Ini adalah berkas masukan (MP4) yang akan digunakan sebagai sumber.
Kemudian, ada tiga blok yang hampir sama, satu untuk setiap resolusi:

-vf "scale=...: Ini adalah filter video untuk mengubah resolusi. Anda dapat mengganti angka-angka ini sesuai dengan resolusi yang diinginkan (480p, 720p, 240p).

-c:v libx264 -profile:v main -level:v 3.1 -g 60 -keyint_min 60 -sc_threshold 0: Ini mengatur parameter video seperti kodek, profil, tingkat, dll.

-map 0 -b:v:... -s:v:... -c:a aac -ar 48000 -b:a ...: Ini mengatur parameter untuk stream video dan audio.

-f hls -hls_time 5 -hls_list_size 0 -var_stream_map "v:...,a:..." output/....m3u8: Ini mengonversi ke HLS dengan potongan waktu 5 detik dan menghasilkan berkas m3u8.

7. Proses Extrac

![napo-folder](https://github.com/ganny0219/hls-ffmpeg/assets/43429378/fbe2e2b4-6faa-4894-82e8-6f355b90ad2f)

8. Setelah hasinya selesai

![napo-folder](https://github.com/ganny0219/hls-ffmpeg/assets/43429378/8a854316-f08b-4372-abeb-795c1b9d7450)

Contoh M3U8 File
---------------

![napo-folder](https://github.com/ganny0219/hls-ffmpeg/assets/43429378/26c0192d-52a1-4977-a35b-41e5a8fd0ad9)

Penjelasan:

#EXTM3U: Menandakan bahwa ini adalah file daftar putar M3U8.

#EXT-X-VERSION:3: Versi protokol HLS yang digunakan.

#EXT-X-TARGETDURATION:10: Durasi maksimum dari setiap segmen video.

#EXT-X-MEDIA-SEQUENCE:0: Urutan media awal.

#EXT-X-PLAYLIST-TYPE:VOD: Jenis daftar putar, dalam hal ini "Video on Demand".

#EXTINF:10.0,: Durasi dan nama segmen berikutnya.

video-segment-0.ts, video-segment-1.ts, dan seterusnya: Nama segmen-segmen video.
Setiap #EXTINF menandakan durasi segmen video dalam detik dan mengacu pada segmen .ts yang harus diputar selama durasi tersebut.

Anda harus menyesuaikan file daftar putar .m3u8 sesuai dengan segmen-segmen video yang Anda miliki. Ini adalah contoh sederhana, dan dalam situasi nyata, ini akan mengacu pada segmen-segmen video yang Anda hasilkan saat mengkode video ke format HLS.

Pastikan bahwa file daftar putar dan segmen-segmen .ts berada di lokasi yang dapat diakses oleh pemutar video dan mematuhi struktur protokol HLS yang benar.

CARA MEMBUAT MASTER M3U8
------------------------------

buat file master.m3u8 (ex. napo.m3u8)

lalu isikan dengan :

#EXTM3U

#EXT-X-VERSION:3

#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=800000,RESOLUTION=854x480,CODECS="avc1.4d401f,mp4a.40.2"

480p.m3u8 ---- ubah dengan path menuju file .m3u8 (ex. https://asdh.com/240p/240p.m3u8)

#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=1500000,RESOLUTION=1280x720,CODECS="avc1.4d401f,mp4a.40.2"

720p.m3u8

#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=400000,RESOLUTION=426x240,CODECS="avc1.4d401f,mp4a.40.2"

240p.m3u8

   
