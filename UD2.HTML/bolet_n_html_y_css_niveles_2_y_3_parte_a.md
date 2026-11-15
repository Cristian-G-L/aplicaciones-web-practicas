# 🌐 Boletín de HTML y CSS básico: de cero a página completa
> **Unidad Didáctica 2 · Parte A (Comprobación y reflexión)**  
> **Módulo:** Aplicaciones Web · 2.º SMR  
> **Alumno/a:** *[Tu Nombre]* · **Fecha:** *[Fecha]*

---

## 🖼️ Nivel 2. Imágenes y enlaces

### ✅ A1. Verdadero o falso (corrige las falsas)

| N.º | Afirmación | Resultado | Corrección (si es falsa) |
| :---: | :--- | :---: | :--- |
| **1** | *"La etiqueta `<img>` se cierra con `</img>`."* | ❌ **F** | La etiqueta `<img>` no tiene etiqueta de cierre. |
| **2** | *"El atributo `alt` muestra un texto si la imagen no se puede cargar."* | ✅ **V** | — |
| **3** | *"Para dar ancho y alto a una imagen se recomienda usar `style` en lugar de `width` y `height`."* | ✅ **V** | — |
| **4** | *"La propiedad `float` permite que una imagen flote a la izquierda o a la derecha del texto, o que no flote."* | ✅ **V** | — |
| **5** | *"El rótulo de un enlace solo puede ser un texto."* | ❌ **F** | El rótulo de un enlace también puede ser una imagen (o una imagen junto a un texto). |
| **6** | *"`target="_blank"` hace que el enlace se abra en una ventana (pestaña) nueva."* | ✅ **V** | — |
| **7** | *"Por defecto, un enlace ya visitado se ve azul y uno por visitar, morado."* | ❌ **F** | Es justo al revés: por defecto, un enlace **por visitar se ve azul** y uno **ya visitado se ve morado**. |
| **8** | *"Un enlace relativo escribe la URL completa, incluido el dominio."* | ❌ **F** | Ese es un enlace absoluto. El enlace relativo solo pone la ruta desde la carpeta donde está tu archivo (por ejemplo, `imagenes/foto.jpg`). |

---

### 🔗 A2. Relaciona atributo y función

| Pareja | Elemento | Descripción |
| :---: | :--- | :--- |
| **1 - D** | `src` | Ruta del archivo de imagen. |
| **2 - G** | `alt` | Texto que se muestra si la imagen no carga. |
| **3 - B** | `href` | Indica el destino del enlace. |
| **4 - F** | `target` | Indica dónde se abrirá el destino del enlace. |
| **5 - A** | `id` | Crea un marcador (bookmark) dentro de la página. |
| **6 - E** | `float` | Propiedad CSS para que la imagen flote junto al texto. |
| **7 - C** | `_blank` | Valor de `target` que abre una pestaña nueva. |

---

### 🧭 A3. ¿Absoluto o relativo?

1. `https://www.w3.org/` $\rightarrow$ **Absoluto** (lleva la dirección web completa con `https://`).
2. `paginas/contacto.html` $\rightarrow$ **Relativo** (busca dentro de una carpeta local).
3. `/css/default.asp` $\rightarrow$ **Relativo** (no lleva dominio ni `http`, parte de la raíz del sitio).
4. `https://www.google.com/` $\rightarrow$ **Absoluto** (lleva la dirección web completa).
5. `./apuntes.pdf` $\rightarrow$ **Relativo** (busca el archivo en la misma carpeta actual).
6. `imagenes/logo.png` $\rightarrow$ **Relativo** (busca dentro de la carpeta `imagenes`).

---

### 🎨 A4. Formatos de imagen

| Abreviatura | Nombre completo | Extensión |
| :---: | :--- | :---: |
| **GIF** | Graphics Interchange Format | `.gif` |
| **JPEG** | Joint Photographic Experts Group | `.jpg` / `.jpeg` |
| **PNG** | Portable Network Graphics | `.png` |
| **SVG** | Scalable Vector Graphics | `.svg` |
| **ICO** | Icon Format (Windows Icon) | `.ico` |
| **APNG** | Animated Portable Network Graphics | `.apng` / `.png` |

---

### 🔍 A5. Caza los errores de la galería

#### 🐛 Errores detectados (5 fallos):
1. **Etiqueta `<img>` mal escrita y cerrada:** Los atributos `src` y `alt` se han quedado fuera de los símbolos `< >` y además se intenta cerrar con `</img>` (que no existe).
2. **Estilos CSS rotos:** Dentro de `style`, en lugar de usar dos puntos (`:`) para dar el tamaño, se ha usado el signo igual (`=`).
3. **Falta el atributo `alt`:** En la segunda imagen (`monte.jpg`) falta el texto alternativo `alt`.
4. **Comillas en el enlace:** El valor de `href` (`https://www.wikipedia.org`) debe ir entre comillas dobles.
5. **Enlace sin cerrar:** Falta cerrar la etiqueta del enlace con `</a>` al final del texto.

*(Nota: También falta la etiqueta `<meta name="author">` obligatoria según las normas generales del boletín).*

#### ✨ Código corregido:
```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="utf-8">
    <title>Mi galería</title>
    <meta name="author" content="Tu Nombre">
</head>
<body>
    <h1>Mi viaje de fin de curso</h1>
    <img src="playa.jpg" alt="Playa al atardecer">
    <img src="monte.jpg" alt="Paisaje de montaña" style="width: 300px; height: 200px;">
    <a href="https://www.wikipedia.org" target="_blank">Más información sobre el destino</a>
</body>
</html>
```

---

### 📂 A6. Rutas que no funcionan

* **`<img src="logo.png" alt="Logo">`**
  * ❌ **No funciona:** La imagen está dentro de la carpeta `imagenes`, no suelta junto a `index.html`.
  * **Corrección:** `<img src="imagenes/logo.png" alt="Logo">`
* **`<img src="imagenes/equipo.jpg" alt="Equipo">`**
  * ✅ **Funciona:** La ruta, el nombre y la extensión coinciden exactamente.
* **`<a href="Contacto.html">Contacto</a>`**
  * ❌ **No funciona:** El archivo se llama `contacto.html` en minúsculas, y aquí está escrito con la `C` en mayúscula.
  * **Corrección:** `<a href="contacto.html">Contacto</a>`
* **`<a href="apuntes.pdf">Apuntes</a>`**
  * ✅ **Funciona:** El archivo está en la misma carpeta que `index.html`.
* **`<a href="imagenes/apuntes.pdf">Apuntes</a>`**
  * ❌ **No funciona:** El archivo `apuntes.pdf` está fuera, no dentro de la carpeta `imagenes`.
  * **Corrección:** `<a href="apuntes.pdf">Apuntes</a>`
* **`<img src="imagenes/equipo.png" alt="Equipo">`**
  * ❌ **No funciona:** La extensión del archivo real es `.jpg`, no `.png`.
  * **Corrección:** `<img src="imagenes/equipo.jpg" alt="Equipo">`

---

### 🖥️ A7. ¿Qué verá el usuario?

* **(a) ¿Dónde aparece la imagen del gato respecto al texto?**  
  Aparece pegada a la **derecha** de la pantalla, y el texto del párrafo se coloca a su izquierda rodeándola.
* **(b) Si `gato.jpg` no existe, ¿qué se mostrará?**  
  Se mostrará un icono de imagen rota junto con el texto alternativo: **"Gato durmiendo"**.
* **(c) ¿Qué ocurre al hacer clic en el logo?**  
  Al pulsar sobre la imagen del logo, se abrirá la página web `https://www.w3.org/` en una **pestaña nueva** del navegador.

---
---

## 🔖 Nivel 3. Enlaces internos (bookmarks)

### ✅ A1. Verdadero o falso (corrige las falsas)

| N.º | Afirmación | Resultado | Corrección (si es falsa) |
| :---: | :--- | :---: | :--- |
| **1** | *"Para crear un bookmark se añade el atributo `id` a una etiqueta de la página."* | ✅ **V** | — |
| **2** | *"`<a href="#S4">` salta al elemento con `id="S4"` de la misma página."* | ✅ **V** | — |
| **3** | *"Dos elementos de la misma página pueden tener el mismo `id`."* | ❌ **F** | Cada `id` debe ser único en toda la página; no se puede repetir en dos elementos distintos. |
| **4** | *"`<a href="guia.html#wifi">` abre `guia.html` directamente en la sección con ese `id`."* | ✅ **V** | — |
| **5** | *"Los identificadores `Precios` y `precios` son el mismo."* | ❌ **F** | Son distintos porque HTML diferencia entre letras mayúsculas y minúsculas. |

---

### 🖱️ A2. ¿Qué pasa al hacer clic?

* **Caso A (`<a href="#precios">` $\rightarrow$ `<h2 id="precios">`)**  
  Funciona bien: la página baja automáticamente hasta colocarse justo en el título **"Precios"**.
* **Caso B (`<a href="#Precios">` $\rightarrow$ `<h2 id="precios">`)**  
  No hace nada (falla): el enlace busca `#Precios` con `P` mayúscula y el título tiene `precios` en minúscula, así que no coinciden.
* **Caso C (`<a href="guia.html#instalacion">`)**  
  Abre el archivo `guia.html` y salta directamente hasta la sección que tenga el identificador `id="instalacion"`.

---

### 💭 A3. Reflexiona

1. **¿En qué tipo de páginas resulta más útil un índice con bookmarks?**  
   En páginas muy largas y con mucho texto (como manuales, tutoriales, artículos extensos o preguntas frecuentes), para no tener que bajar todo el rato con la rueda del ratón.
2. **Al final de cada sección habrá un enlace de vuelta al índice. ¿A qué `id` debe apuntar y dónde tienes que ponerlo?**  
   Debe apuntar a un identificador que esté arriba del todo de la página (por ejemplo, `href="#inicio"` o `href="#indice"`), poniendo ese `id="inicio"` en el título principal (`<h1>`) o en el contenedor del índice.
3. **¿Qué pasaría si dos secciones tuvieran el mismo `id`?**  
   El enlace se liaría y siempre saltaría solo al **primer** elemento que encuentre con ese nombre, ignorando el segundo (además de dar error si validas el código).