# Código Civil Peruano — Estructurado para IA

> Repositorio mantenido por [CÓDIGO51](https://codigo51.com) — Consultoría de IA para LATAM

Código Civil peruano (D.Leg. 295) estructurado artículo por artículo en formato Markdown,
diseñado para ser consumido por sistemas MCP, RAG y agentes de IA legal.

**Actualizado a:** Ley 32228 — 08 de enero de 2025

---

## ¿Para qué sirve este repositorio?

Permite conectar Claude (u otro LLM) directamente a la legislación civil peruana vigente
mediante un servidor MCP. El agente puede buscar, leer y citar artículos específicos
en tiempo real durante un análisis legal.

**Caso de uso típico:**
> Un abogado en Claude Desktop pregunta sobre derechos sucesorios.
> El plugin `claude-for-legal` llama al MCP server de este repositorio,
> que devuelve los artículos 660–880 con su estado de vigencia actualizado.

---

## Estructura

```
codigo-civil-peru/
├── README.md
├── titulo_preliminar/         # Art. I – X
├── libro_i/                   # Art.   1 –   139  Derecho de las personas
├── libro_ii/                  # Art. 140 –   232  Acto jurídico
├── libro_iii/                 # Art. 233 –   659  Derecho de familia
├── libro_iv/                  # Art. 660 –   880  Derecho de sucesiones
├── libro_v/                   # Art. 881 – 1,131  Derechos reales
├── libro_vi/                  # Art. 1132 – 1,350  Las obligaciones
├── libro_vii/                 # Art. 1351 – 1,988  Fuentes de las obligaciones
├── libro_viii/                # Art. 1989 – 2,007  Prescripción y caducidad
├── libro_ix/                  # Art. 2008 – 2,045  Registros públicos
└── libro_x/                   # Art. 2046 – 2,122  Derecho internacional privado
```

### Cada artículo es un fichero `.md` con frontmatter YAML:

```yaml
---
id:              "CC-L4-724"
libro_num:       4
libro_nombre:    "Derecho de sucesiones"
articulo:        "724"
sumilla:         "Herederos forzosos"
status:          "modificado"
version:         2
fuente_original: "D.Leg. 295 (DOEP 25-07-1984)"
fuente_texto:    "LP Derecho — actualizado Ley 32228 (08-01-2025)"
fecha_vigencia:  "1984-11-14"
modificaciones:
  - tipo:  "modificado"
    norma: "Ley 30007"
    fecha: "17 de abril de 2013"
tags: []
---

## Art. 724 — Herederos forzosos

Son herederos forzosos los hijos y los demás descendientes...
```

---

## Estados de un artículo

| Status | Significado |
|---|---|
| `vigente` | Texto aplicable actualmente |
| `modificado` | Texto vigente ya incorporado — historial en `modificaciones[]` |
| `derogado` | Sin efecto legal — el MCP server emite advertencia automática |
| `incorporado` | Artículo nuevo añadido por ley posterior al texto original |

---

## Actualizar codigo

### Clonar y arrancar

```bash
git clone https://github.com/infoiacodigo51/codigo-civil-peru.git
cd codigo-civil-peru
```

---

## Tools disponibles

### `search_legislation(query, libro?, solo_vigentes?, limite?)`
Busca artículos por materia o texto libre.
```
search_legislation("herederos forzosos")
→ 32 artículos del Libro IV
```

### `get_article(articulo)`
Texto completo + estado de vigencia.
```
get_article("724")
→ Art. 724 con advertencia: "modificado por Ley 30007"
```

### `update_article(articulo, nuevo_texto, norma, fecha, tipo?)`
Actualiza un artículo cuando cambia la ley.
```
update_article("724", "nuevo texto...", "Ley 32500", "15-06-2025")
```

---

## Índice de materias

| Materia | Libro | Artículos |
|---|---|---|
| Personas, capacidad, domicilio | I | 1 – 139 |
| Acto jurídico, nulidad, representación | II | 140 – 232 |
| Familia, matrimonio, divorcio, alimentos | III | 233 – 659 |
| Sucesiones, herencia, testamento, legítima | IV | 660 – 880 |
| Propiedad, posesión, usufructo, hipoteca | V | 881 – 1,131 |
| Obligaciones, pago, novación, extinción | VI | 1,132 – 1,350 |
| Contratos, compraventa, resp. extracontractual | VII | 1,351 – 1,988 |
| Prescripción y caducidad | VIII | 1,989 – 2,007 |
| Registros públicos | IX | 2,008 – 2,045 |
| Derecho internacional privado | X | 2,046 – 2,122 |

---

## Política de actualizaciones

- Solo se hacen **commits** — nunca se reescribe el historial
- Cada commit referencia la norma que motiva el cambio
- Los artículos derogados se conservan con `status: derogado` — nunca se borran
- Versiones etiquetadas por año: `v2025.01`, `v2025.06`...

---

## Cobertura actual

| | |
|---|---|
| Total artículos | 2,089 |
| Vigentes | 1,850 |
| Modificados | 188 |
| Derogados | 34 |
| Incorporados | 17 |
| Última ley incorporada | Ley 32228 (08-01-2025) |

---

## Próximos repositorios

- `codigo-penal-peru` — Código Penal (D.Leg. 635)
- `codigo-procesal-civil-peru` — CPC (D.Leg. 768)
- `codigo-procesal-penal-peru` — NCPP (D.Leg. 957)

---

## Fuente de los datos

El contenido de este repositorio fue extraído y estructurado a partir de
**[LP Derecho (lpderecho.pe)](https://lpderecho.pe)**, portal de referencia
legal peruano, y validado contra el texto oficial del D.Leg. 295
(DOEP 25-07-1984), incluyendo las modificaciones hasta la Ley 32228
(08-01-2025).

> Los datos son de acceso público. Este repositorio los estructura
> en formato Markdown + YAML para hacerlos consumibles por sistemas MCP y RAG.

## ¿Encontraste un error o falta un artículo?

Este repositorio es mantenido por la comunidad. Si detectas un error
en el texto de un artículo o un artículo que no está incluido:

### Reportar un error
1. Ve a la pestaña [Issues](https://github.com/infoiacodigo51/codigo-civil-peru/issues)
2. Crea un nuevo issue con el título: `[Error] Art. XXX — descripción breve`
3. Indica el texto incorrecto y la fuente correcta (LP Derecho, El Peruano, etc.)

### Agregar un artículo faltante
1. Haz fork del repositorio
2. Crea el fichero `.md` en la carpeta del libro correspondiente
   siguiendo el formato YAML del frontmatter
3. Envía un Pull Request con el título: `[Nuevo] Art. XXX — sumilla`

> Cada contribución se revisa antes de hacer merge.
> La fuente del texto debe ser siempre verificable.

Este repositorio es de libre uso. Si lo usas en tu bufete o proyecto,
una mención a https://codigo51.com es bienvenida.


### Plantilla para artículo nuevo
Usa la plantilla en [`CONTRIBUTING/plantilla_articulo.md`](./CONTRIBUTING/plantilla_articulo.md)
como base para el fichero `.md` del artículo nuevo.

## Créditos y mantenimiento

Desarrollado y mantenido por **[CÓDIGO51](https://codigo51.com)**
Consultoría de Inteligencia Artificial para América Latina

- Web: [codigo51.com](https://codigo51.com)
- LinkedIn: [CÓDIGO51](https://linkedin.com/company/codigo51)
