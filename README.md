# Váltó

<p align="center">
  <a href="../../releases/latest">
    <img src="https://img.shields.io/badge/%E2%AC%87%EF%B8%8F_Let%C3%B6lt%C3%A9s-Windowsra-2ea44f?style=for-the-badge&logo=windows&logoColor=white" alt="Letöltés Windowsra" height="60">
  </a>
</p>

<p align="center">
  <sub>Kattints a gombra, majd a megnyíló oldalon az <b>Assets</b> résznél töltsd le a <code>.exe</code> telepítőt.</sub>
</p>

Asztali alkalmazás, amellyel fájlokat alakíthatsz át egyik formátumból a másikba (hang, videó, kép, dokumentum, táblázat, prezentáció, e-könyv, archívum, betűtípus), és YouTube-videókat tölthetsz le MP3 vagy MP4 formátumban, a kívánt minőségben. Electron alapú, az átalakítás a saját gépeden fut.

![Verzió](https://img.shields.io/badge/verzi%C3%B3-2.1.0-blue)
![Platform](https://img.shields.io/badge/platform-Windows-lightgrey)
![Electron](https://img.shields.io/badge/Electron-app-47848F)

<!-- TODO: Ide szúrj be egy képernyőképet az alkalmazásról, pl.: -->
<!-- ![Képernyőkép](docs/screenshot.png) -->

## Tartalom

- [Funkciók](#funkciók)
- [Támogatott formátumok](#támogatott-formátumok)
- [YouTube-letöltés](#youtube-letöltés)
- [Telepítés felhasználóknak](#telepítés-felhasználóknak)
- [Futtatás forráskódból](#futtatás-forráskódból)
- [Beállítások](#beállítások)
- [Telepítő készítése](#telepítő-készítése)
- [Projektstruktúra](#projektstruktúra)
- [Hibaelhárítás](#hibaelhárítás)
- [Hozzájárulás](#hozzájárulás)
- [Licenc](#licenc)

## Funkciók

- Fájlok átalakítása kilenc kategóriában: hang, videó, kép, dokumentum, táblázat, prezentáció, e-könyv, archívum és betűtípus
- Több fájl egyszerre: behúzás vagy kiválasztás után fájlonként választható a célformátum, és egy gombbal az összes átalakítható
- YouTube-linkek letöltése MP3 vagy MP4 formátumban, minőségválasztással, több link egyszerre
- Az átalakítás helyben, a saját gépeden történik, a fájlokat nem tölti fel külső szolgáltatásnak
- Az alkalmazás magától érzékeli, mely eszközök vannak telepítve, és csak azokat a típusokat kínálja fel, amelyeket valóban el tud végezni
- Az ideiglenes fájlok a letöltés vagy a megszakítás után törlődnek

> **Fontos:** A telepítő csak az **FFmpeg**-et tartalmazza. Ez a hang, a videó és az alapvető képformátumok átalakításához, valamint a YouTube-letöltéshez elég. A többi kategóriához külön programok kellenek, lásd a következő részt.

## Támogatott formátumok

A listában csak az szerepel, amit a program kódja ténylegesen támogat. Az alkalmazásban a **Támogatott típusok** menüpont mutatja, hogy a te gépeden pontosan mi érhető el, és hogy melyik program hiányzik.

| Kategória | Bemenet | Kimenet | Szükséges program |
|-----------|---------|---------|-------------------|
| Hang | MP3, WAV, FLAC, OGG, OGA, Opus, AAC, M4A, WMA, AIFF, AIF, AMR, MKA, WEBA | MP3, WAV, FLAC, OGG, Opus, M4A, AAC, AIFF | FFmpeg (benne van) |
| Videó | MP4, MOV, AVI, MKV, WebM, FLV, WMV, M4V, MPG, MPEG, 3GP, TS, OGV | MP4, MOV, MKV, WebM, AVI, GIF, valamint a hangformátumok (hang kinyerése) | FFmpeg (benne van) |
| Kép | JPG, PNG, WebP, GIF, BMP, TIFF, ICO | JPG, PNG, WebP, GIF, BMP, TIFF, ICO | FFmpeg (benne van) |
| Kép (bővítve) | HEIC, HEIF, AVIF, SVG, PSD, TGA, JP2, EPS, AI | PNG, JPG, WebP, GIF, BMP, TIFF, ICO, PDF, AVIF | [ImageMagick](https://imagemagick.org/) |
| Dokumentum | DOC, DOCX, DOT, DOTX, ODT, OTT, RTF, TXT, HTML, WPD, WPS, Pages | PDF, DOCX, DOC, ODT, RTF, TXT, HTML | [LibreOffice](https://www.libreoffice.org/) |
| Dokumentum | Markdown, HTML, DOCX, ODT, RST, TeX, Org | Markdown, HTML, DOCX, ODT, EPUB, RST, TeX, TXT, Org | [Pandoc](https://pandoc.org/) |
| PDF | PDF | PNG, JPG, TXT, SVG, valamint DOCX és ODT | [Poppler](https://poppler.freedesktop.org/) (képek, szöveg), LibreOffice (DOCX, ODT) |
| Táblázat | XLS, XLSX, XLSM, ODS, CSV, Numbers | XLSX, XLS, ODS, CSV, PDF, HTML | LibreOffice |
| Prezentáció | PPT, PPTX, PPS, PPSX, ODP, Key | PPTX, PPT, ODP, PDF, PNG, JPG | LibreOffice |
| E-könyv | EPUB, MOBI, AZW, AZW3, FB2, LIT, PDB, LRF, HTMLZ | EPUB, MOBI, AZW3, FB2, PDF, DOCX, TXT, RTF | [Calibre](https://calibre-ebook.com/) |
| E-könyv | DOCX, RTF, TXT, HTML, ODT, PDF | EPUB, MOBI, AZW3, FB2 | Calibre |
| Archívum | ZIP, 7z, TAR, TAR.GZ, TAR.BZ2, TAR.XZ, RAR, GZ, BZ2, XZ | ZIP, 7z, TAR, TAR.GZ, TAR.BZ2, TAR.XZ | [7-Zip](https://www.7-zip.org/) |
| Betűtípus | TTF, OTF, WOFF, WOFF2 | WOFF, WOFF2, TTF, OTF | [Python](https://www.python.org/) + `fonttools` |

Megjegyzések:

- A PDF → DOCX/ODT átalakítás szerkeszthető változatot készít, de a bonyolult elrendezést nem mindig tartja meg tökéletesen.
- A betűtípusoknál a WOFF/WOFF2 → TTF/OTF csak kicsomagolás: a betűtípus belső (kontúr)formátuma nem változik.
- A program a LibreOffice, a Calibre és a 7-Zip esetében a szokásos Windows telepítési mappákban is keres. A Pandoc, az ImageMagick (`magick`), a Poppler (`pdftoppm`) és a Python (`python`) a `PATH`-on kell legyen.

### Korlátok

- Fájlonként legfeljebb **300 MB** tölthető fel (módosítható, lásd a [Beállítások](#beállítások) részt)
- Egyszerre legfeljebb **2** átalakítás fut, a többi sorban vár
- Egy átalakítási lépés legfeljebb **15 percig** futhat, utána a program leállítja
- Archívumoknál a kicsomagolt tartalom legfeljebb 1,5 GB lehet
- A jelszóval védett vagy sérült fájlokat a program nem tudja átalakítani

## YouTube-letöltés

A YouTube-linkek letöltése a program tetején, a fájlfeltöltő alatt található.

1. Illessz be egy vagy több YouTube-linket (soronként egyet). A linkek a listára kerülnek.
2. Válaszd ki a formátumot és a minőséget. Ez soronként is módosítható.
3. Kattints az **Összes letöltése** gombra, vagy egyenként a sor **Letöltés** gombjára.

| Formátum | Minőség |
|----------|---------|
| MP4 (videó) | 1080p, 720p, 480p, 360p vagy Legjobb elérhető |
| MP3 (hang) | Legjobb, 192 kbps vagy 128 kbps |

- Ha a videó nem érhető el a kiválasztott felbontásban, a program a legjobb, ennél kisebb változatot tölti le.
- A 360p–1080p választás kompatibilis (H.264/AAC) MP4-et ad, ha van ilyen. A **Legjobb elérhető** felbontáskorlát nélkül tölt, ezért 1440p vagy 4K videónál olyan kódolású (VP9/AV1) fájl is lehet, amit néhány régebbi lejátszó nem játszik le.
- Az MP3 minősége nem lehet jobb az eredeti hangsávnál, ezért a 192 kbps-nél magasabb beállításnak nincs értelme.
- Lejátszási lista linkjénél csak az adott videó töltődik le.
- A letöltött fájlok a **Letöltések** mappába kerülnek, kérdezés nélkül. Ha már van azonos nevű fájl, a program sorszámot fűz a névhez.
- Elfogadott linkek: `youtube.com`, `music.youtube.com` és `youtu.be`.

**Tudnivalók:**

- A letöltéshez internetkapcsolat kell. Az első YouTube-letöltéskor az alkalmazás letölti a [yt-dlp](https://github.com/yt-dlp/yt-dlp) programot (kb. 15-20 MB) az adatmappájába, ezért az első alkalom hosszabb. Hiba esetén a program egyszer magától frissíti a yt-dlp-t, és újrapróbálja.
- A YouTube feltételei tiltják a tartalmak letöltését, kivéve ha a YouTube erre lehetőséget ad. **Csak olyan videót tölts le, amelyhez jogod van** (saját tartalom, szabad felhasználású vagy engedéllyel használható anyag). A felelősség a felhasználóé.
- Ha a YouTube megváltoztatja a működését, a letöltés átmenetileg nem működhet, amíg a yt-dlp frissítést nem kap.

## Telepítés felhasználóknak

1. Nyisd meg a repó **[Releases](../../releases)** oldalát.
2. Töltsd le a legfrissebb verzió telepítőjét (`.exe`).
3. Futtasd a letöltött fájlt, és kövesd a telepítő lépéseit.
4. Ha dokumentumokat, e-könyveket vagy más, a fenti táblázatban jelölt kategóriákat is át szeretnél alakítani, telepítsd a hozzájuk szükséges programokat.

> **Megjegyzés:** Mivel a telepítő nincs kódaláírással ellátva, a Windows SmartScreen figyelmeztetést jeleníthet meg ("Ismeretlen kiadó"). Kattints a **További információ**, majd a **Futtatás mindenképp** gombra.

## Projektstruktúra

```
.
├── main.js             # Electron főfolyamat: elindítja a helyi szervert és megnyitja az ablakot
├── server.js           # Helyi Express szerver: eszközkeresés, útvonaltábla, fájlátalakítás
├── youtube.js          # YouTube-letöltés (yt-dlp + FFmpeg)
├── public/
│   └── index.html      # Felhasználói felület
├── package.json        # Függőségek, szkriptek, build-beállítások
└── package-lock.json
```

## Hibaelhárítás

### `Electron failed to install correctly, please delete node_modules/electron and try installing again`

Az Electron futtatható fájlja nem töltődött le, mert a telepítési szkriptek le voltak tiltva. Megoldás:

```bash
rmdir /s /q node_modules\electron
npm install electron --foreground-scripts
```

Ha az npm a figyelmeztetésben jelzett módon kéri a szkriptek engedélyezését:

```bash
npm install-scripts approve electron
npm install-scripts approve ffmpeg-static
npm install
```

Ha a `package.json`-ban `allowScripts` szakasz van, a benne szereplő verziószámoknak **pontosan egyezniük** kell a telepített verziókkal (`npm ls electron`), különben az npm nem engedélyezi a szkripteket.

Ha még így sem működik:

- Ellenőrizd, hogy a tűzfal, VPN vagy vírusirtó nem blokkolja-e a letöltést (az Electron a GitHubról tölti le a binárisát).
- Töröld a `node_modules` mappát és a `package-lock.json` fájlt, majd futtasd újra az `npm install` parancsot.

### Egy fájltípus nem jelenik meg, vagy nem lehet átalakítani

- Nyisd meg az alkalmazásban a **Támogatott típusok** részt. Ha egy eszköz hiányzik, az alatta lévő figyelmeztetés felsorolja.
- Telepítsd a hiányzó programot a [támogatott formátumok](#támogatott-formátumok) táblázat szerint, majd indítsd újra az alkalmazást (a program induláskor keresi meg az eszközöket).
- Győződj meg róla, hogy a bemeneti fájl nem sérült, nem jelszóvédett, és nincs használatban másik programban.

### Az átalakítás hibával leáll

- Ellenőrizd, hogy a fájl nem nagyobb-e a megengedett méretnél (alapból 300 MB).
- Nagyon nagy vagy bonyolult fájlnál az átalakítás 15 perc után időtúllépéssel megszakad.

### A YouTube-letöltés nem működik

- Ellenőrizd az internetkapcsolatot. Az első használatkor a yt-dlp letöltéséhez is kell.
- Ha a víruskereső blokkolja a yt-dlp letöltését, vagy törli a fájlt, add hozzá kivételként az alkalmazás adatmappáját (`%APPDATA%` alatt, az alkalmazás nevével).
- A hibaüzenet a sor alatt jelenik meg. Az **Újra** gombbal megismételhető a letöltés. A program hiba esetén egyszer magától frissíti a yt-dlp-t.
- Privát, korhatáros vagy területhez kötött videókat a program nem tud letölteni.

## Hozzájárulás

Hibajelentéseket és javaslatokat az **Issues** menüpontban várunk. Pull requestek előtt kérjük, nyiss egy issue-t a tervezett változtatásról.

1. Fork-old a repót
2. Hozz létre egy új ágat (`git checkout -b uj-funkcio`)
3. Commit-old a módosításokat (`git commit -m "Új funkció"`)
4. Pushold az ágat (`git push origin uj-funkcio`)
5. Nyiss egy Pull Requestet

## Licenc

Ez a projekt a [MIT licenc](LICENSE) alatt érhető el.

## Köszönet

- [Electron](https://www.electronjs.org/)
- [FFmpeg](https://ffmpeg.org/) és az [ffmpeg-static](https://github.com/eugeneware/ffmpeg-static) csomag
- [yt-dlp](https://github.com/yt-dlp/yt-dlp) és a [yt-dlp-wrap](https://github.com/foxesdocode/yt-dlp-wrap) csomag
- [LibreOffice](https://www.libreoffice.org/), [Pandoc](https://pandoc.org/), [Calibre](https://calibre-ebook.com/), [ImageMagick](https://imagemagick.org/), [Poppler](https://poppler.freedesktop.org/), [7-Zip](https://www.7-zip.org/) és [fontTools](https://github.com/fonttools/fonttools) az átalakítási funkciókhoz
