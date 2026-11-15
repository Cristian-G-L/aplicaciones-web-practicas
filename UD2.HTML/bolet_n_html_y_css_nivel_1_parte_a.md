# 🌐 Boletín de HTML y CSS básico: de cero a página completa
> **Unidad Didáctica 2 · Parte A (Comprobación y reflexión)**  
> **Módulo:** Aplicaciones Web · 2.º SMR  
> **Alumno/a:** *[Tu Nombre]* · **Fecha:** *[Fecha]*

---

## 📘 Nivel 1. Estructura y formato de texto

### ✅ A1. Verdadero o falso (corrige las falsas)

| N.º | Afirmación | Resultado | Corrección / Justificación |
| :---: | :--- | :---: | :--- |
| **1** | *"HTML es un lenguaje de programación como Python: sirve para hacer cálculos y tomar decisiones."* | ❌ **F** | HTML es un lenguaje de **marcas** (de estructuración), no de programación; sirve para estructurar el contenido de la web, no para hacer cálculos ni tomar decisiones. |
| **2** | *"La etiqueta `<br>` no necesita etiqueta de cierre."* | ✅ **V** |  |
| **3** | *"El valor de un atributo siempre se escribe entre comillas."* | ✅ **V** | |
| **4** | *"Los atributos de una etiqueta se escriben en la etiqueta de cierre."* | ❌ **F** | Los atributos de una etiqueta se escriben **siempre en la etiqueta de apertura**. |
| **5** | *"El texto de `<title>` aparece en la pestaña del navegador."* | ✅ **V** |  |
| **6** | *"`<strong>` y `<b>` se visualizan igual."* | ✅ **V** |  |
| **7** | *"Todo lo que escribimos dentro de `<head>` se ve en la página."* | ❌ **F** | El contenido de `<head>` es **metainformación** para el navegador y buscadores (título, codificación, estilos); no se renderiza dentro del cuerpo visible de la página. |
| **8** | *"La etiqueta `<hr>` se cierra con `</hr>`."* | ❌ **F** | La etiqueta `<hr>` es un elemento vacío (crea una línea horizontal separadora) y **no tiene etiqueta de cierre**. |
| **9** | *"Un comentario HTML (`<!-- ... -->`) se muestra en pantalla como una nota gris."* | ❌ **F** | Un comentario HTML **no se muestra en pantalla** en absoluto; solo es visible al inspeccionar el código fuente. |
| **10** | *"`<span>` crea un bloque de texto que siempre empieza en una línea nueva."* | ❌ **F** | `<span>` es un contenedor de tipo **línea (*inline*)**, por lo que fluye junto al texto sin provocar saltos de línea. |

---

### 🔗 A2. Relaciona etiqueta y efecto

| Pareja | Etiqueta | Descripción del efecto |
| :---: | :---: | :--- |
| **1 - B** | `<mark>` | Texto remarcado, como con un fosforito. |
| **2 - A** | `<del>` | Texto tachado (precio antiguo de una oferta). |
| **3 - E** | `<sub>` | Texto en subíndice (como en $\text{H}_2\text{O}$). |
| **4 - F** | `<sup>` | Texto en superíndice (como en $\text{m}^2$). |
| **5 - D** | `<small>` | Texto más pequeño que el normal. |
| **6 - C** | `<em>` | Texto enfatizado (se visualiza en cursiva). |
| **7 - G** | `<ins>` | Texto insertado (se visualiza subrayado). |

---

### 🔍 A3. Caza los errores

#### 🐛 Errores detectados (5 fallos):
1. **Falta de cierre:** No se ha cerrado la etiqueta `</head>`.
2. **Estructura incompleta:** Faltan `<!DOCTYPE html>`, `<meta charset="utf-8">` y `<meta name="author">` (obligatorios según las normas del boletín).
3. **Título sin cerrar:** Falta la etiqueta de cierre `</title>`.
4. **Encabezado discordante:** Se abre con `<h1>` pero se intenta cerrar con `</h2>`.
5. **Mala anidación (*solapamiento*):** Se abre `<b>` dentro de `<p>`, pero se cierra primero `</p>` y luego `</b>`. La etiqueta que se abre última debe cerrarse primera.

#### ✨ Código corregido:
```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="utf-8">
    <title>Mi tienda de gadgets</title>
    <meta name="author" content="Tu Nombre">
</head>
<body>
    <h1>Ofertas de otoño</h1>
    <p>Auriculares con <b>cancelación de ruido</b>.</p>
</body>
</html>
```

---

### 🎨 A4. Estilos rotos

* **1. `<h1 style="color:red font-size:40px;">Directo esta noche</h1>`**
  * **Fallo:** Falta el punto y coma (`;`) para separar las dos declaraciones CSS.
  * **Solución:**
    ```html
    <h1 style="color: red; font-size: 40px;">Directo esta noche</h1>
    ```

* **2. `<p style="text-align=center;">Estreno de temporada</p>`**
  * **Fallo:** En CSS las propiedades y sus valores se separan con dos puntos (`:`), no con el signo igual (`=`).
  * **Solución:**
    ```html
    <p style="text-align: center;">Estreno de temporada</p>
    ```

* **3. `<p style="background-color:yellow;">Sorteo de una tarjeta gráfica<p>`**
  * **Fallo:** Al final de la línea se ha puesto una etiqueta de apertura `<p>` en lugar de la de cierre `</p>`.
  * **Solución:**
    ```html
    <p style="background-color: yellow;">Sorteo de una tarjeta gráfica</p>
    ```

---

### 💬 A5. Comentarios y anidación

#### 🐛 Errores detectados:
1. **Sintaxis del comentario:** Los comentarios en HTML requieren dos guiones tanto al abrir como al cerrar (`<!-- ... -->`), no uno solo (`<!- ... ->`).
2. **Etiquetas cruzadas:** En `<strong><em>...</strong></em>` las etiquetas no respetan el orden de anidamiento. Como `<em>` se abrió después de `<strong>`, debe cerrarse antes.

#### ✨ Código corregido:
```html
<!-- Revisar el texto antes de publicar -->

<p>Tu contraseña debe tener <strong><em>al menos 12 caracteres</em></strong>.</p>
```

---

### 🖥️ A6. ¿Qué verá el usuario?

Si abrimos el archivo en el navegador, el resultado visual de arriba abajo será el siguiente:

> # Resumen de la jornada
> Ha ganado el equipo local.  
> El rival se despide del torneo.
>
> ---
>
> #### Próximo partido
> Sábado a las 18:00

**Desglose elemento a elemento:**
1. Un encabezado grande y en negrita (`<h1>`) con el texto *"Resumen de la jornada"*.
2. Un párrafo donde la primera frase (*"Ha ganado el equipo local."*) queda arriba y, justo debajo sin dejar espacio extra de párrafo gracias al `<br>`, aparece *"El rival se despide del torneo."*
3. Una línea horizontal (`<hr>`) que divide visualmente el contenido de lado a lado.
4. Un subtítulo de cuarto nivel (`<h4>`) más pequeño con el texto *"Próximo partido"*.
5. Un párrafo normal con la hora: *"Sábado a las 18:00"*.
