# Instrucciones — Auditor de Calidad y Ventas · Instituto Continental

## Requisitos

- **Claude Code** instalado ([claude.ai/code](https://claude.ai/code))
- Conversaciones exportadas desde Genesys (HTML, TXT, CSV)
- **Git** instalado si deseas publicar en enlace público ([git-scm.com](https://git-scm.com))
- **Cuenta en GitHub** (gratuita) si deseas publicar en enlace público ([github.com](https://github.com))

---

## Modo 1 — Auditoría individual (1 conversación)

**1.** Abre esta carpeta en Claude Code

**2.** Comparte el archivo de Genesys:
```
Aquí el archivo: C:\auditorias\conversacion_001.html
```

**3.** Claude genera `docs/reporte-auditoria-[id].html` con:
- Los 19 criterios evaluados con evidencia textual
- Score global y nivel del asesor
- Barras de desempeño por área
- Feedback: fortalezas, mejoras y frases correctivas exactas
- JSON listo para copiar al sistema de reportes

---

## Modo 2 — Dashboard global (2 o más conversaciones)

**1.** Comparte todos los archivos juntos:
```
Audita estas 5 conversaciones: [adjunta o lista las rutas]
```

**2.** Claude audita cada una y genera `docs/dashboard-calidad-[mes-año].html` con:
- Ranking de asesores ordenado por score
- Criterios más fallados del equipo (análisis colectivo)
- Tarjeta por conversación con los 19 criterios en píldoras de color
- Recomendaciones para el equipo basadas en patrones detectados

---

## Publicar en enlace público (GitHub Pages)

Para compartir los reportes con un enlace como `https://tu-usuario.github.io/auditorias-continental/`:

### Primera vez (configuración única)

**Paso 1 — Crea un repositorio en GitHub**
1. Ve a [github.com/new](https://github.com/new)
2. Nombre: `auditorias-continental`
3. Visibilidad: **Public** (necesario para GitHub Pages gratuito)
4. Haz clic en **Create repository**
5. Copia la URL del repositorio (ej: `https://github.com/tu-usuario/auditorias-continental`)

**Paso 2 — Dile a Claude que publique**
```
Publica el reporte en GitHub Pages.
Mi repositorio es: https://github.com/tu-usuario/auditorias-continental
```

Claude ejecutará automáticamente:
```bash
git init
git checkout -b main
git add docs/
git commit -m "Reportes de auditoría - [fecha]"
git remote add origin [tu URL]
git push -u origin main
```

**Paso 3 — Activa GitHub Pages (una sola vez)**
1. Ve a tu repositorio en GitHub
2. Haz clic en **Settings** → **Pages** (menú lateral)
3. En "Source": selecciona **Deploy from a branch**
4. Branch: **main** · Folder: **/docs**
5. Haz clic en **Save**

En 1–2 minutos tu enlace estará activo:
```
https://tu-usuario.github.io/auditorias-continental/
```

### Actualizar reportes (siguientes veces)

Cada vez que generes nuevos reportes, solo di:
```
Actualiza el repositorio con los nuevos reportes
```

Claude ejecuta:
```bash
git add docs/
git commit -m "Nuevas auditorías - [fecha]"
git push
```
El enlace se actualiza automáticamente en ~30 segundos.

---

## Los 19 criterios del formulario

| # | Criterio | Regla clave |
|---|---|---|
| 1.1 | Atiende en los primeros 30 seg (PEC) | Diferencia de timestamps ≤ 30 seg |
| 1.2 | Se presenta con nombre e instituto | Nombre + "Instituto Continental" en saludo |
| 1.3 | Preguntas de filtro (carrera/modalidad) | Al menos una indagación activa |
| 1.4 | Propuesta de valor (Instituto/Programa/Modalidad) | Beneficios pertinentes al perfil del cliente |
| 1.5 | Registra correctamente la info del prospecto | Nombre, DNI, carrera, modalidad, ciudad |
| 1.6 | Brinda info de admisión y precios | Inscripción, matrícula, cuotas, total |
| 1.7 | Ventajas de la carrera / certificaciones progresivas | Diferenciadores específicos de la carrera |
| 1.8 | Información correcta y completa de la carrera | Sin errores ni contradicciones |
| 1.9 | Atento a la información del prospecto | Adapta discurso según lo que el cliente comparte |
| 1.10 | Responde acertadamente las inquietudes | Respuestas precisas y completas |
| 1.11 | Maneja objeciones correctamente | Clasifica, argumenta y ofrece alternativas |
| 1.12 | Ortografía profesional | Sin errores de tildes, gramática o redacción |
| 1.13 | Personaliza la interacción (mín. 2 veces) | Usa el nombre u datos personales del cliente |
| 1.14 | Es amable en toda la comunicación | Tono cordial, sin respuestas bruscas |
| 1.15 | Uso adecuado de plantillas | Sigue formato y contenido institucional |
| 1.16 | Estilo dinámico y empático | Emojis, mensajes cortos, genera rapport |
| 1.17 | Tipifica correctamente | Código de conclusión refleja el resultado real |
| 1.18 | Speech de cierre correcto | Resumen + próximos pasos + despedida estructurada |
| 1.19 | Genera agendamiento | Fecha y hora concreta para el siguiente contacto |

---

## Comandos de consulta rápida

| Lo que escribes | Lo que hace Claude |
|---|---|
| `"Ver historial de [asesor]"` | Tabla con todas sus auditorías y resultados |
| `"Ver perfil de [asesor]"` | Tasas por criterio, nivel y tendencias |
| `"Plan de mejora para [asesor]"` | Plan personalizado con frases exactas |
| `"Ranking de asesores"` | Comparativa de todos los asesores registrados |
| `"Actualiza el repositorio"` | Push automático a GitHub Pages |

---

## Estructura de archivos

```
kit-auditor-calidad-continental/
├── CLAUDE.md                              ← Configuración del kit
├── INSTRUCCIONES.md                       ← Este archivo
├── docs/                                  ← Carpeta publicada en GitHub Pages
│   ├── index.html                         ← Índice de todos los reportes
│   ├── reporte-auditoria-[id].html        ← Reportes individuales
│   └── dashboard-calidad-[mes].html       ← Dashboards globales
├── historial/                             ← Historial acumulado por asesor
│   ├── [nombre-asesor].json
│   └── [nombre-asesor]-perfil.json
└── .claude/
    └── skills/
        └── auditor-calidad-continental.md
```

---

## Preguntas frecuentes

**¿Cuántas conversaciones puedo auditar a la vez?**
No hay límite técnico. Claude procesa cada archivo secuencialmente y los consolida en el dashboard.

**¿El enlace de GitHub Pages es permanente?**
Sí, mientras el repositorio exista y sea público. Puedes actualizar el contenido sin que cambie el enlace.

**¿El historial se acumula entre sesiones?**
Sí. Los archivos `historial/*.json` persisten y Claude los lee en cada nueva sesión.

**¿Puedo añadir más criterios?**
Sí, edita `.claude/skills/auditor-calidad-continental.md` en el Paso 3. El dashboard se adapta automáticamente.

**¿Funciona con transcripciones de llamadas?**
Sí, siempre que incluyan timestamps y estén en texto plano.
