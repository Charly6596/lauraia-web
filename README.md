# lauraia-web

Web pública mínima de **Laura IA** (@lauu_ia), cuenta de noticias de IA. Existe sobre todo
porque TikTok pide, para la app de desarrollador que conecta Postiz, una web HTTPS verificada
con términos de servicio y política de privacidad.

Sitio estático sin build (HTML + CSS, sin JavaScript ni recursos de terceros), servido con
GitHub Pages desde `main`, carpeta `/`.

```
index.html             portada: quién es Laura IA, redes, contacto
terminos/index.html    términos de servicio (ES, con versión breve en EN)
privacidad/index.html  política de privacidad (ES, con versión breve en EN)
assets/estilo.css      la única hoja de estilos
assets/marca.svg       logotipo y favicon
.nojekyll              Pages sirve los ficheros tal cual, sin pasar por Jekyll
```

Los enlaces internos son relativos, así que el sitio funciona igual en
`https://charly6596.github.io/lauraia-web/` que en un dominio propio.

## Verlo en local

```sh
python3 -m http.server 8000   # y abrir http://localhost:8000/
```

## Fichero de verificación de TikTok

TikTok da un fichero con nombre `tiktok<código>.txt` para demostrar que la web es tuya. Se sube
**tal cual, sin cambiarle nombre ni contenido, a la raíz del repo** (junto a `index.html`), se
hace commit en `main` y, cuando Pages lo publique, se pulsa «Verify» en TikTok. Comprobar antes:

```sh
curl -fsS https://<dominio>/tiktok<código>.txt
```

No hay ninguno todavía: se añade cuando TikTok lo genere.

## Dominio propio (pendiente)

De momento la web vive en `https://charly6596.github.io/lauraia-web/`. Para pasarla a un dominio:

1. Los registros DNS del dominio apuntando a GitHub Pages (en el repo `homelab`, `dns/<dominio>/zone.json`).
2. Un fichero `CNAME` en la raíz con el dominio en una línea, o fijarlo en
   `gh api -X PUT repos/Charly6596/lauraia-web/pages -f cname=<dominio>` (GitHub suele hacer un commit con ese fichero: `git pull` después).
3. Cuando GitHub emita el certificado, activar «Enforce HTTPS»:
   `gh api -X PUT repos/Charly6596/lauraia-web/pages -F https_enforced=true`.
