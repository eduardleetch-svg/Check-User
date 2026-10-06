# checkuser-panel

por [@EduardLeetch](https://github.com/eduardleetch-svg)

API de **solo lectura** que consulta el estado real de una cuenta SSH
administrada con el menú **adm-lite**: si existe, cuántos días le quedan, y
cuántas conexiones tiene abiertas ahora mismo frente a su límite. No crea,
edita ni borra nada — eso sigue siendo trabajo del menú de siempre.

Binario estático para `amd64`/`arm64`, sin dependencias en el servidor.

## Instalación

Una sola línea, en tu VPS (Ubuntu/Debian):

```bash
curl -L https://github.com/eduardleetch-svg/Check-User/archive/refs/heads/main.tar.gz | tar xz && cd Check-User-main && sudo ./install.sh
```

El instalador te guía: puerto donde escuchar, si tienes dominio propio, y
detecta solo si los puertos 80/443 ya están ocupados por otro servicio para
elegir el camino correcto de HTTPS.

## Página web

El panel sirve una mini página en `/`: un campo para escribir el usuario y
un botón que muestra el estado.

## API

```
GET /api/checkuser/{username}          # requiere header X-API-Key
GET /api/public/checkuser/{username}   # sin API key, mismo límite que la página web
GET /details/{username}                # formato compatible con paneles tipo DTunnel
GET /checkuser/{username}              # alias del anterior
GET /count                             # total global de conexiones activas
```

## Administración

El instalador trae su propio menú (`sudo ./install.sh`) para instalar,
reinstalar, desinstalar, cambiar puerto, regenerar/ver la API key y
reconfigurar HTTPS — no hace falta recordar ningún comando ni editar
ningún archivo a mano.
