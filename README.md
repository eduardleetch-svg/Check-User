# checkuser-panel

por [@EduardLeetch](https://github.com/eduardleetch-svg)

API de **solo lectura** que consulta el estado real de una cuenta SSH: si
existe, cuántos días le quedan y cuántas conexiones tiene abiertas ahora mismo
frente a su límite. No crea, edita ni borra nada.

Binario estático para `amd64`/`arm64`, sin dependencias en el servidor.

## Instalación

Una sola línea, en tu VPS (Ubuntu/Debian):

```bash
curl -L https://github.com/eduardleetch-svg/Check-User/archive/refs/heads/main.tar.gz | tar xz && cd Check-User-main && sudo ./install.sh
```

El panel FENIX usa el modo automático (`--auto --domain … --cert-url … --cert-token …`).

## API

```
GET /details/{username}                # formato compatible con paneles tipo DTunnel
GET /checkuser/{username}              # alias del anterior
GET /check/{username}?deviceId=…      # diálogo nativo de la app DTunnel (url_check_user)
GET /api/public/checkuser/{username}   # sin API key (10 consultas/min por IP)
GET /api/checkuser/{username}          # requiere header X-API-Key
GET /count                             # total global de conexiones activas
GET /healthz
```

Todas las respuestas llevan CORS (`Access-Control-Allow-Origin: *`), así que un
tema HTML puede consultarlas con `fetch` desde el WebView.

## Qué lee (v3.2)

- **Usuario / límite / vencimiento:** primero `/etc/adm-lite/userDIR/<usuario>`
  (`limite:` y `data:`; fechas `AAAA-MM-DD` o `DD/MM/AAAA`). Si no existe ese
  archivo, usa el respaldo para otros menús: la cuenta del sistema (solo
  UID ≥ 1000 con shell sin login) y su vencimiento de `/etc/shadow`.
- **Conexiones abiertas:** procesos `sshd`, `sshd-session` (OpenSSH 9.8+) y
  `dropbear` que pertenecen al usuario.

## Compilar

```bash
./build.sh
```
