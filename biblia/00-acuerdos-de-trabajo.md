# 00 — Acuerdos de trabajo

Reglas permanentes entre **Tsukikage** (autor) y el asistente. Se escriben aquí para que no dependan de la memoria de ninguna de las dos partes.

---

## 1. El asistente no tiene capacidades de visión

**No puede ver imágenes.** Ninguna: pósteres, diseños de personaje, capturas de pantalla, referencias. Da igual el formato —`.webp`, `.png`, `.jpg`—: el resultado es siempre el mismo mensaje de sistema.

**Lo que sí puede hacer con una imagen:**

| Puede ✅ | No puede ❌ |
|---|---|
| Leer dimensiones, formato y modo de color | Ver qué aparece en ella |
| Extraer la paleta dominante | Reconocer caras, ropa o personajes |
| Convertir y redimensionar | Leer texto que esté *dentro* de la imagen |
| Generar mapas de luminancia por código | Juzgar si se ve bonita |

**Regla operativa:** **debe advertirlo antes** de que el autor invierta trabajo en una imagen. Todo lo visual tiene que entrar **por palabras**: el autor describe, el asistente anota. *(Regla añadida el 13 de octubre de 2026, después de que su omisión costara trabajo al autor.)*

## 2. Tres capas en los documentos de personaje

- **CANON** — lo que el autor ha establecido. No se modifica sin su decisión.
- **PROPUESTA** — interpretación o sugerencia del asistente. Se acepta, se corrige o se tira.
- **RESERVADO** — decisión que el autor ya tomó pero pidió mantener en secreto. **No se escribe en ningún archivo ni en ningún mensaje de commit.**

Nunca se mezclan las capas en silencio: lo que el asistente interpreta no puede parecer decisión del autor.

## 3. No publicar lore sin autorización

El autor puede congelar cualquier decisión. Mientras esté congelada, el trabajo vive como borrador local y **no se sube al repositorio** hasta que él lo apruebe explícitamente.

## 4. No empezar a escribir capítulos sin luz verde

**Vigente en lo esencial: no se escribe un capítulo sin que el autor lo pida.** Lo que quedó atrás es el método.

- ~~Primero se construye y se aprueba el **Plan de Acción**.~~ **Derogado el 13 de octubre de 2026.** El autor aprobó trabajar **un volumen a la vez y un capítulo a la vez**, sin estructura cerrada de la obra. El motivo es suyo y está escrito en `biblia/14-volumen-1.md`: un esquema cerrado se vuelve obsoleto en cuanto cambia una decisión importante.
- Lo que sustituye al Plan de Acción es la **ficha de cinco bloques** por capítulo (`biblia/14-volumen-1.md`, «Cómo se trabaja cada capítulo»). El autor puede saltársela diciendo *«comienza con el capítulo N»*, y lo ha hecho en los capítulos 4 y 5.

## 5. Cada capítulo es distinto

Los **28 capítulos** (dos volúmenes de 14) tendrán cada uno **su propio diseño y su propia estructura narrativa**. Ninguno repite la fórmula del anterior.

*(Corregido el 13 de octubre de 2026: decía 26. La extensión acordada es 14 + 14.)*

## 6. El regalo tiene fecha

Es para **Jesús**, hermano del autor. **No se abre hasta el 2 de marzo de 2027.** Nada del repositorio debe adelantarlo.

---

## 7. Formato obligatorio de los capítulos (13 de octubre de 2026)

Se aplica a **todo** archivo dentro de `novela/`. No son preferencias de estilo: son requisitos del lector que va a usar el autor.

1. **UTF-8 con BOM** (`utf-8-sig`), siempre. Sin BOM, **ElevenReader** no respeta las pausas. Comprobación obligatoria después de escribir cualquier archivo:
   `open(ruta,'rb').read(3) == b'\xef\xbb\xbf'`
2. **La raya (—) es de los diálogos y de nada más.** Ni incisos, ni apartes, ni énfasis. Para todo lo demás: comas, puntos, punto y coma, guiones cortos, paréntesis. El autor lo pidió literalmente: *«usar otros signos de puntuación para el resto del capítulo»*.
3. **Prosa limpia para el TTS.** Ni Markdown, ni tablas, ni corchetes, ni asteriscos, ni almohadillas: el lector de voz los pronuncia o se los salta mal. Lista negra: `# * _ [ ] ~ < > |`.
4. **Cero dígitos en el cuerpo del capítulo.** Todo número se escribe con letra, y los títulos también: `Capítulo seis:`, nunca `Capítulo 6:`. *(Regla del asistente, aplicada el 13 de octubre de 2026 a los cinco capítulos ya escritos.)*
5. **Firma.** Todo capítulo cierra con `Tsukikage (月影)` en su propia línea. *(Pedido del autor; el capítulo 1 se publicó sin ella y se le añadió después.)*

## 8. Autorevisión antes de entregar (13 de octubre de 2026)

**Antes de dar por terminado un capítulo, el asistente lo vuelve a leer entero.** Es un pedido explícito del autor: *«asegúrate de darle un vistazo tu mismo también para verificar que todo esté escrito correctamente y no se nos haya escapado algún error o inconsistencia respecto al lore»*.

Se hace en tres pasadas, en este orden:

1. **Formato.** BOM presente · recuento de palabras contra la medida acordada · la raya solo en diálogos · cero símbolos de la lista negra · firma presente · cero dígitos · cero ideogramas sueltos (los únicos permitidos son `月影`).
2. **Continuidad.** Cada cifra y cada nombre propio del capítulo se busca en **todos** los capítulos anteriores. Las escaleras, los centímetros, las semanas y las horas tienen que cuadrar. **El cotejo se hace en minúsculas**: comparar sin bajar a minúsculas produce falsos positivos.
3. **Lectura de las zonas editadas.** Después de cualquier inserción se relee el párrafo anterior y el posterior. Los contadores no bastan: en el capítulo 4 un ancla duplicó párrafos y los números seguían dando bien.

**Regla técnica de las inserciones:** toda edición va con `assert texto.count(ancla) == 1` antes de escribir, y el ancla **nunca** puede ser una frase que también aparezca dentro del texto insertado. Si el assert falla, el script muere sin escribir nada a medias.

**Correcciones de continuidad ya hechas con este método (13 de octubre de 2026):**

| Error | Corrección |
|---|---|
| «Tres semanas sin coser» (caps. 1 y 2) | **Cinco semanas**: llega a fines de marzo, la máquina a fines de abril |
| «Nueve noches», «cuarenta y ocho horas» (cap. 5) | **Cinco noches**, veintisiete horas |
| «Pasaron tres semanas» desde la promesa a Sofía (cap. 5) | **Más de un mes**: la promesa se hizo en el capítulo 2 |

El capítulo 3 se queda en «tres semanas», que es lo correcto para su fecha.

## 9. Consultar las fuentes antes de cada capítulo (13 de octubre de 2026)

Antes de escribir, se consulta la biblia investigada y/o internet, **capítulo por capítulo**. Hacerlo una sola vez para el capítulo 1 no cuenta. Lo que se averigüe y siga importando se anota en el apartado «Recursos usados» de `biblia/14-volumen-1.md`.

## 10. Nivel de ecchi — ACUERDO DEL AUTOR (13 de octubre de 2026)

> **Sin filtros.** 🔥

El autor lo decidió así, sin matices. No se censura la tensión, el deseo ni el cuerpo.

### Dónde pone la línea el asistente (PROPUESTA, pendiente de que el autor la mueva)

El autor dijo *sin filtros* y el asistente no se va a autocensurar en silencio: si pone un límite, lo pone **a la vista** para que él lo corra. Éste es el límite que se está usando:

- **Todo lo que se siente, se escribe.** Piel, temperatura, respiración, olor, reacciones del cuerpo, pensamientos que él mismo preferiría no tener. Sin eufemismos.
- **Se llega hasta la ropa interior.** Es lo que la escena pide: una prueba de vestido se hace sobre el cuerpo, y la ropa de calle cambia la caída de la tela.
- **No hay actos sexuales ni descripción anatómica explícita de menores.** Los personajes tienen entre quince y diecisiete años. El canon de *My Dress-Up Darling* es ecchi, no hentai, y ésa es la medida que se está siguiendo.

Si el autor quiere correr la línea, se corre: basta con decirlo, y se anota aquí.

### Cómo se sostiene el ecchi en esta obra

No es adorno: **siempre está haciendo trabajar a los personajes.**

- **Marin** es cómoda en su cuerpo, no exhibitionista por accidente. Enseña, pregunta, se ríe. Nunca se avergüenza de lo que quiere.
- **Jesús** **no** se azora con los cuerpos: lleva desde los trece años vistiendo modelos en el taller de su madre. Lo que lo quiebra es que **hoy sí se fija**, y que se fija en *ésta*. La grieta está en su profesionalismo, no en su inocencia. Es la inversión del canon: allá se azora el chico que nunca había tocado a una chica; acá se le rompe la mano al que ha tocado a cien.
- **La silla lo vuelve específico.** Ella tiene que bajar a su altura para que él le marque el ruedo. Ésa es la geometría que carga la escena: lo que debería ser romántico es exactamente lo que a él le duele, porque **la regla seis es pedir**, y pedir es lo único que no sabe hacer.

## 11. Markdown ahora, la web interactiva al final — ACUERDO DEL AUTOR (13 de octubre de 2026)

**Se sigue escribiendo en Markdown.** La Web Interactiva / Novela Visual **no se diseña desde ahora: se hace hasta el mero final**, cuando los 28 capítulos estén escritos.

**Consecuencia:** no se toma ninguna decisión de formato pensando en la web. Los capítulos se escriben para leerse —y para que ElevenReader los lea— en archivos de texto plano. Cuando llegue el momento, la web se construirá sobre la obra terminada, no al revés.
