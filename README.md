# Optimización del Planograma de un Stand de Ventas — MILP

Modelo de Programación Lineal Entera Mixta (MILP) desarrollado para OXXO
que asigna productos a charolas y bandejas en el Cuarto Frío, maximizando
la afinidad histórica de cada producto con su posición en el planograma.

Proyecto del curso MA2008B — ITESM, Escuela de Ingeniería y Ciencias.
Ingeniería en Ciencias de Datos y Matemáticas.

## Descripción del modelo

La función objetivo maximiza la suma ponderada de probabilidades históricas
de las celdas ocupadas:

    máx Z = Σ φ_{p,c,b} · X_{p,c,b}

### Variables de decisión

| Variable     | Tipo    | Significado                                      |
|--------------|---------|--------------------------------------------------|
| `X[p,c,b]`  | Binaria | Producto `p` ocupa la celda `(c, b)`             |
| `Y[p,c,b]`  | Binaria | Producto `p` inicia su bloque en `(c, b)`        |

### Restricciones principales

- **R2** — Colocación exacta de `Nₚ` frentes por producto
- **R3** — Sin solapamiento entre productos en una misma celda
- **R4** — Capacidad de ancho físico por charola (con holgura δ = 1 cm)
- **R5** — Contigüidad estricta de frentes dentro de la charola asignada
- **R_fill** — Llenado mínimo por charola (opcional, umbral ρ_min)

## Resultados principales

Evaluado sobre 50 combinaciones (TAMANO × SEGMENTO) del mueble CF / Refrescos:

- Optimalidad alcanzada en el 100% de los casos
- Tiempo promedio de solución: 0.40 s
- Objetivo normalizado promedio: 93.9%
- Fill promedio con relleno codicioso: 80.9%

## Archivos de datos requeridos

| Archivo                      | Descripción                        |
|------------------------------|------------------------------------|
| `oxxo_1.csv`                 | Catálogo de productos OXXO         |
| `ejemplo_planograma.csv`     | Planograma histórico de referencia |
| `Caso de estudio TEC.xlsx`   | Especificaciones del mueble        |

## Dependencias

```bash
pip install pulp pandas numpy openpyxl
```

## Uso

Colocar los tres archivos de datos en el mismo directorio que el notebook
y ejecutar las celdas en orden en Jupyter Notebook o JupyterLab
con Python 3.13+.

## Autores

Carlos Cuéllar Solís · Francisco Moreno Alcocer · Luis Javier Jacobo Morimoto
Luis Roberto Campos Solis · Maria Paula Recinos Ríos

**Profesores:** Fernando Elizalde · Sofía Salinas · Mónica Elizondo · Salvador García  
**Socio Formador:** OXXO  
**Grupo:** MA2008B.603 — Junio 2026
