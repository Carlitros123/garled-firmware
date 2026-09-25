# garled-firmware

Canal público de actualización remota (OTA) del firmware GarLed.

- `esp32-main/manifest.json` — versión vigente: `{version, url, sha256, size, publishedAt}`.
- `esp32-main/garled-esp32-<versión>.bin` — imagen de aplicación ESP32.

Los nodos consultan el manifiesto por HTTPS (CA verificada) cada 6 h o a pedido,
y solo aceptan binarios bajo este repositorio. Una imagen nueva arranca "a prueba":
si no recupera conectividad en 10 min, el bootloader vuelve a la anterior.

**Los binarios no contienen credenciales.** WiFi y MQTT viven en la memoria NVS de
cada nodo. El script de publicación compila sin `secrets.h` y aborta si detecta
algún valor secreto dentro del binario.

Código fuente y guía: repositorio privado `garled`, `firmware/esp32-main/`.
Publicar: `pwsh firmware/esp32-main/publish-ota.ps1 -Version X.Y.Z`.
