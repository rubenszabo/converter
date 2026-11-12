# Váltó

<p align="center">
  <a href="../../releases/latest">
    <img src="https://img.shields.io/badge/%E2%AC%87%EF%B8%8F_Let%C3%B6lt%C3%A9s-Windowsra-2ea44f?style=for-the-badge&logo=windows&logoColor=white" alt="Letöltés Windowsra" height="60">
  </a>
</p>

<p align="center">
  <sub>Kattints a gombra, majd a megnyíló oldalon az <b>Assets</b> résznél töltsd le a <code>.exe</code> telepítőt.</sub>
</p>

Asztali alkalmazás fájlok formátumok közötti konvertálására. Electron alapú, a médiafájlok feldolgozását beépített FFmpeg végzi, ezért használatához nincs szükség külön szoftver telepítésére.

![Verzió](https://img.shields.io/badge/verzi%C3%B3-2.0.0-blue)
![Platform](https://img.shields.io/badge/platform-Windows-lightgrey)
![Electron](https://img.shields.io/badge/Electron-app-47848F)

<!-- TODO: Ide szúrj be egy képernyőképet az alkalmazásról, pl.: -->
<!-- ![Képernyőkép](docs/screenshot.png) -->

## Tartalom

- [Funkciók](#funkciók)
- [Támogatott formátumok](#támogatott-formátumok)
- [Telepítés felhasználóknak](#telepítés-felhasználóknak)
- [Futtatás forráskódból](#futtatás-forráskódból)
- [Telepítő készítése](#telepítő-készítése)
- [Projektstruktúra](#projektstruktúra)
- [Hibaelhárítás](#hibaelhárítás)
- [Hozzájárulás](#hozzájárulás)
- [Licenc](#licenc)

## Funkciók

- Fájlkonvertálás különböző formátumok között
- Beépített FFmpeg, külső telepítés nélkül
- Egyszerű, asztali grafikus felület
- Offline működés, a fájlok nem hagyják el a számítógépet

<!-- TODO: Egészítsd ki a valós funkciókkal (pl. tömeges konvertálás, minőségbeállítás, húzd-és-ejtsd támogatás). -->

## Támogatott formátumok

<!-- TODO: Töltsd ki a ténylegesen támogatott formátumokkal. -->

| Kategória | Bemenet | Kimenet |
|-----------|---------|---------|
| Videó     | pl. MP4, MKV, AVI | pl. MP4, WebM |
| Hang      | pl. MP3, WAV, FLAC | pl. MP3, WAV |

## Telepítés felhasználóknak

1. Nyisd meg a repó **[Releases](../../releases)** oldalát.
2. Töltsd le a legfrissebb verzió telepítőjét (`.exe`).
3. Futtasd a letöltött fájlt, és kövesd a telepítő lépéseit.

> **Megjegyzés:** Mivel a telepítő nincs kódaláírással ellátva, a Windows SmartScreen figyelmeztetést jeleníthet meg ("Ismeretlen kiadó"). Kattints a **További információ**, majd a **Futtatás mindenképp** gombra.

## Futtatás forráskódból

### Előfeltételek

- [Node.js](https://nodejs.org/) (LTS vagy újabb verzió)
- npm (a Node.js-sel együtt települ)
- Git

### Lépések

```bash
# Repó klónozása
git clone https://github.com/FELHASZNALONEV/REPO-NEV.git
cd REPO-NEV

# Függőségek telepítése
npm install

# Alkalmazás indítása
npm run app
```

> **Fontos:** Az újabb npm verziók alapértelmezetten blokkolhatják a telepítési szkripteket. Az Electron és az `ffmpeg-static` viszont a telepítéskor tölti le a szükséges binárisokat. Ha az indításnál az `Electron failed to install correctly` hibát kapod, lásd a [Hibaelhárítás](#hibaelhárítás) szakaszt.

## Telepítő készítése

<!-- TODO: Ellenőrizd a package.json "scripts" részében a pontos parancsot, és írd át, ha eltér. -->

```bash
npm run build
```

A kész telepítő a `dist/` mappában jön létre. Terjesztéshez töltsd fel a GitHub **Releases** oldalára, ne a repóba.

## Projektstruktúra

<!-- TODO: Igazítsd a valós mappaszerkezethez. -->

```
.
├── package.json        # Függőségek és szkriptek
├── package-lock.json
├── main.js             # Electron főfolyamat (példa)
├── ...                 # Felület és egyéb forrásfájlok
└── README.md
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

Ha még így sem működik:

- Ellenőrizd, hogy a tűzfal, VPN vagy vírusirtó nem blokkolja-e a letöltést (az Electron a GitHubról tölti le a binárisát).
- Töröld a `node_modules` mappát és a `package-lock.json` fájlt, majd futtasd újra az `npm install` parancsot.

### A konvertálás nem indul el vagy hibával leáll

- Ellenőrizd, hogy az `ffmpeg-static` telepítése sikeres volt-e.
- Győződj meg róla, hogy a bemeneti fájl nem sérült, és nincs használatban másik programban.

## Hozzájárulás

Hibajelentéseket és javaslatokat az **Issues** menüpontban várunk. Pull requestek előtt kérjük, nyiss egy issue-t a tervezett változtatásról.

1. Fork-old a repót
2. Hozz létre egy új ágat (`git checkout -b uj-funkcio`)
3. Commit-old a módosításokat (`git commit -m "Új funkció"`)
4. Pushold az ágat (`git push origin uj-funkcio`)
5. Nyiss egy Pull Requestet

## Licenc

<!-- TODO: Válassz licencet (pl. MIT), és add hozzá a LICENSE fájlt. -->

Ez a projekt a [MIT licenc](LICENSE) alatt érhető el.

## Köszönet

- [Electron](https://www.electronjs.org/)
- [FFmpeg](https://ffmpeg.org/) és az [ffmpeg-static](https://github.com/eugeneware/ffmpeg-static) csomag
