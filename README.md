# MarioKartPSP — MK-Style build 8

Bu proje PSP (480x272) icin 3D kart yarisi prototipidir. Bu surumde model gorunumu ve PSP performansi icin ek duzeltmeler yapildi:

- Pipe Frame 64 DAE nesnelerinin COLLADA transform matrisleri vertex'lere onceden islenmistir; tekerlek, koltuk, govde ve metal parcalar artik ortak orijinde ust uste binmez.
- Z-up kaynak modeli PSP'nin Y-up sahnesine tutarli bicimde donusturulur; kart zemine oturur.
- Tekerlekler kendi pivot merkezlerinde PSP GU matrisleriyle doner ve on tekerlekler direksiyona gore yonlenir. Her karede binlerce vertex kopyalama islemi kaldirildi.
- Mario, Luigi ve Yoshi icin farkli olcekler uygulanir; karakterler koltuk merkezine tasinir ve direksiyona dogru hafif one egilir.
- Her kart parcasi kendi PNG'sini kullanir; UV koordinatlari ilgili texture boyutlarina gore islenmistir. Lastik texture'i 128x128'e dusurulerek bellek/texture maliyeti azaltildi.
- Texture cache, canli texture pointer'larini LRU ile ezmez. Asset bankasi sabit slot kullanir.
- Skybox: gunduz/gun batimi/gece; hareketli bulut ve uzak dag katmanlari.
- Yarista mini-harita, sira/lap/zaman/hiz HUD'u, 3-2-1-GO geri sayimi, drift/boost efektleri ve item kutulari var.
- Ses mixer'i WAV motor, muzik ve efekt dosyalarini tek PSP audio kanalinda karistirir.
- Oyuncu ve en yakin bot ayrintili kart + karakter meshini cizer; diger botlarda daha hafif LOD kullanilir.
- Oyun kontrolleri, 4 pist, zorluk, kupa/kariyer, ozel gucler, time trial ve ghost sistemleri korunur.

## GitHub web yukleme

Repository kokune su dosyalari koy:

```text
main.c
char_models.h
kart_models.h
CMakeLists.txt
Makefile
assets_pack.zip
.github/workflows/main.yml
```

`assets_pack.zip` runtime icin gereken `assets/audio/` ve `assets/textures/` klasorlerini icerir. Her dosyayi GitHub web arayuzunde tek tek yuklemen gerekmez; workflow ZIP'i acar.

## PSP Memory Stick

Build bittiginde `MarioKartPSP-GAME` artifact'ini indir. Icindeki klasoru su konuma kopyala:

```text
PSP/GAME/MarioKartPSP/EBOOT.PBP
PSP/GAME/MarioKartPSP/assets/audio/...
PSP/GAME/MarioKartPSP/assets/textures/...
```

Yerel ortamda PSPDEV toolchain bulunmadigi icin bu dosya seti burada gercek PSP derlemesiyle test edilmedi. Derleme dogrulamasi GitHub Actions'ta yapilmalidir; PSP donaniminda son gorunum/FPS ayrica kontrol edilmelidir.
