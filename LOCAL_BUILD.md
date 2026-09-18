# ZMK lokal bauen

Die lokale Umgebung verwendet dieselbe ZMK-Version `v0.3` wie der GitHub-Build.
Alle heruntergeladenen Quellen und Werkzeuge liegen in `.zmk-workspace/` und
`.venv/`; die Firmware landet in `build-local/`. Diese Verzeichnisse werden von
Git ignoriert.

Beide Hälften bauen:

```sh
./scripts/build-zmk-local
```

Nur eine Hälfte bauen:

```sh
./scripts/build-zmk-local left
./scripts/build-zmk-local right
```

Die fertigen Dateien liegen direkt in `build-local/` und sind nach der jeweiligen
Hälfte benannt:

- `build-local/piantor_pro_bt_left.uf2`
- `build-local/piantor_pro_bt_right.uf2`

Das gilt auch, wenn nur eine Hälfte gebaut wird. Die technischen
Build-Zwischendateien bleiben außerhalb des Ausgabeordners in
`.zmk-workspace/local-build/`.

## Hinweis zum iCloud-Pfad und ZMK Studio

Zephyr 3.5 kann Devicetree- und Protobuf-Dateien nicht zuverlässig aus einem
Pfad mit Leerzeichen verarbeiten. Das Skript legt deshalb automatisch den
temporären Alias `/private/tmp/piantor-zmk-local` an. Quellen, Build-Verzeichnis
und Ergebnisse bleiben physisch in diesem Repository.

ZMK Studio wird im lokalen Build deaktiviert, weil dessen Protobuf-Generator
den Alias wieder zum iCloud-Pfad mit Leerzeichen auflöst. Bluetooth, USB-HID,
Keymap, Display, Mausbuttons und Scrollen werden normal gebaut. Der GitHub-Build
aus `build.yaml` bleibt davon unberührt und enthält weiterhin ZMK Studio.
