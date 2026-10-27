# OPERACIÓN ISO 9001: LOS 7 MISTERIOS DE LA CALIDAD

Videojuego educativo de siete expedientes. Multijugador auténtico mediante backend Node.js, sincronización de eventos SSE, puntuación verificada en servidor, QR PNG, credenciales y exportación CSV.

## Ejecutar localmente

Necesitas Node.js 20+, Python 3 y paquete Python `qrcode` para generar los códigos QR. No hay dependencias npm. En terminal:

```bash
cd operacion-iso9001
ADMIN_PASSWORD='tu-contraseña-segura' npm start
```

Abre `http://localhost:3000`. En modo local puedes probar el juego por enlace desde el mismo equipo. **Un QR para participantes con celulares distintos requiere desplegarlo en una URL pública HTTPS**.

## Publicar para una clase

1. Sube esta carpeta a un repositorio Git privado o público según prefieras.
2. En Railway, Render (servicio con Docker) u otro alojamiento compatible, crea un servicio desde ese repositorio. El `Dockerfile` configura Node y Python QR.
3. Configura la variable secreta `ADMIN_PASSWORD` con una contraseña fuerte, no la publiques en Git.
4. Configura `DATA_FILE=/data/data.json` **y monta un volumen persistente en `/data`** (es imprescindible para no perder resultados en reinicios). Debe haber **una sola instancia** del servicio; este backend no sincroniza varias instancias.
5. Obtén la URL pública HTTPS que te dé el alojamiento, por ejemplo `https://TU-SITIO.ejemplo` (reemplázala con la real).
6. Entra en esa URL, pulsa «CREAR COMPETENCIA», inicia sesión con tu contraseña y crea la sesión.
7. Proyecta el QR real generado desde la URL pública, descarga el PNG y, si quieres, incorpóralo a Canva. Los alumnos escanean, escriben su alias y esperan el comienzo.
8. Inicia la misión desde el panel; exporta resultados CSV antes de eliminar el servicio.

## Limitaciones relevantes

- El almacenamiento compartido de esta versión es un **archivo JSON del servidor**, no Supabase. Es real y persistente **solo con volumen configurado**, y está pensado para una clase en una sola instancia, no para una plataforma a gran escala.
- No se entrega una URL pública operativa: exige despliegue y dominio provistos por el alojamiento.
- La contraseña administra una sesión de servidor; el login se conserva en `sessionStorage` del navegador. Usa HTTPS y contraseña fuerte.
- Las preguntas correctas y puntuación se verifican exclusivamente en el servidor. Una puerta solo aporta puntos una vez. El bono final solo se concede tras completar siete puertas.
- Los alias son seudónimos, no identidades reales; el filtro de lenguaje ofensivo es básico.
- Los eventos en vivo utilizan Server-Sent Events y el reloj se basa en las marcas de tiempo del servidor (sujeto a desfase horario del celular).
- El QR usa `python3-qrcode`, instalado en el Dockerfile, y por seguridad no se genera para localhost.
- El panel de resultados no presenta participantes ni puntos inventados.

## Fuente académica (APA 7)
International Organization for Standardization. (2026). *Quality management principles: Your foundation for success* (3rd ed.). https://www.iso.org/publication/PUB100080.html

Todos los casos empresariales son hipotéticos. El diploma NO constituye certificación ISO.
