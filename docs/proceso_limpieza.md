# Proceso de Limpieza y Transformación de Datos

## Contexto
El dataset original contenía **4,963 registros y 18 columnas**, combinando datos de ventas (VGChartz) y metadatos (RAWG API). El objetivo fue **preservar la mayor cantidad de datos posible** mientras se aseguraba la calidad para el análisis.

---

## Estrategia General
- **0 filas eliminadas** (se manejaron todos los nulos de forma estratégica)
- Se crearon **columnas auxiliares** para clasificar sin perder datos originales
- Las columnas numéricas se mantuvieron para cálculos estadísticos

---

## Transformaciones Aplicadas

### 1. Columnas Eliminadas
| Columna | Motivo |
|---------|--------|
| `Last Update` | 43.5% de valores nulos, sin valor analítico para el dashboard |

### 2. Columnas de Ventas
| Columna | Acción |
|---------|--------|
| `Total Sales`, `NA Sales`, `PAL Sales`, `Japan Sales`, `Other Sales` | Verificadas sin nulos. Se mantuvieron como base del análisis. |

### 3. Manejo de Nulos en Calificaciones

| Columna Original | Acción | Columna Creada |
|------------------|--------|----------------|
| `metacritic` | Se conservó para cálculos. Se creó columna categórica | `Categoría Metacritic` |
| `rating` | Se conservó para cálculos. Se creó columna categórica | `Categoría Rating` |
| `ratings_count` | Nulos reemplazados por `0` | — |

**Categorías Metacritic:**
- `Sin Metacritic` → valor nulo
- `Desfavorable` → < 50
- `Mixto` → 50 - 69
- `Favorable` → 70 - 89
- `Aclamado` → ≥ 90

**Categorías Rating:**
- `Sin rating` → valor nulo
- `Malo` → < 2
- `Regular` → 2 - 3.4
- `Bueno` → ≥ 3.5

### 4. Manejo de Nulos en Texto
| Columna | Acción |
|---------|--------|
| `genres` | Nulos reemplazados por `"Género no especificado"` |
| `platforms` | Nulos reemplazados por `"Plataforma no especificada"` |
| `Publisher` | Nulos reemplazados por `"Desconocido"` |
| `Developer` | Nulos reemplazados por `"Desconocido"` |

### 5. Manejo de Fechas
| Columna | Acción |
|---------|--------|
| `Release Date` | Se conservó para cálculos temporales |
| `Año Lanzamiento` | Columna creada extrayendo el año. Nulos → `"Año desconocido"` |

### 6. Consola PS5
Se decidió **conservar los datos de PS5** a pesar de su representación limitada (consola lanzada en 2020, dataset con solo 5 años de datos vs 15+ años de PS3/PS4). Esto se aborda en el dashboard mediante:
- Visualizaciones que contextualizan la diferencia temporal
- Anotaciones que explican la naturaleza preliminar de los datos

---

## Resultado Final
| Indicador | Valor |
|-----------|-------|
| Filas originales | 4,963 |
| Filas después de limpieza | 4,963 |
| Columnas finales | 18 (originales + nuevas) |
| Columnas eliminadas | 1 (`Last Update`) |
| Datos perdidos por eliminación de filas | 0% |

---

## Herramientas Utilizadas
- **Power Query Editor** → transformaciones, reemplazo de valores, columnas condicionales
- **DAX** → creación de columnas calculadas para categorías