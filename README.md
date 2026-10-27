# Port Log - Sprint 1

## Objetivo
Aplicar conocimientos de versionado, organización y análisis exploratorio de datos
con pandas sobre un dataset real de operaciones portuarias.

## Introducción y contexto
El registro de movimientos del Puerto Fluvial de Rosario fue migrado desde un sistema
heredado de los años '90 que acumuló inconsistencias de formato en fechas, matrículas y
valores numéricos fuera de rango. En este sprint analizamos, depuramos y caracterizamos
esos datos para detectar las infracciones por exceso de velocidad de ingreso a muelle.

## Estructura
```
port_log/
├── data/
│   ├── interim/     datasets procesados en pasos intermedios (y plots/)
│   ├── processed/   datasets finales para otra aplicación
│   └── raw/         datasets en crudo
└── reports/         resúmenes estadísticos y conclusiones
```


# Port Log - Sprint 2

## Objetivo
Aplicar conocimientos de tratamiento de imágenes y programación limpia sobre el
contexto del sistema portuario.

## Introducción y contexto
Los radares ubicados en los accesos a los muelles capturan evidencia fotográfica de
las infracciones de velocidad. Las cámaras asociadas toman fotografías de la zona de
proa donde está pintada la matrícula del buque. En algunos casos el sistema recorta
automáticamente la zona de matrícula (`plates`); en otros casos se conserva la imagen
completa en contexto amplio (`completes`). En este sprint procesamos esas imágenes
(escala de grises, ecualización de histograma, suavizado y detección de bordes),
extrajimos las matrículas mediante OCR y las cruzamos con el dataset de movimientos
del Sprint 1 para validar visualmente las infracciones detectadas.

## Estructura
```
port_log/
├── data/
│   ├── interim/
│   │   ├── imgs/                     imágenes preprocesadas por etapa
│   │   │   ├── 03_01_gray/           escala de grises (plates/completes)
│   │   │   ├── 03_02_equalized/      ecualización de histograma (plates/completes)
│   │   │   ├── 03_03_blur/           suavizado gaussiano (plates/completes)
│   │   │   └── 03_04_canny/          detección de bordes (plates/completes)
│   │   ├── group_images.json         metadatos de imágenes agrupadas en plates/completes
│   │   └── plots/
│   ├── processed/
│   │   └── port_movements_image.csv  movimientos cruzados con matrículas extraídas
│   └── raw/
│       └── imgs/                     imágenes originales (plates/completes)
└── reports/                          resúmenes estadísticos y conclusiones
```


# Port Log - Sprint 3

## Objetivo
Aplicar conocimientos de bases de datos relacionales (SQLAlchemy), versionado de datos
(DVC) y búsqueda por similitud visual (ChromaDB) para profesionalizar el sistema
portuario.

## Introducción y contexto
El sistema creció en volumen y complejidad, y el manejo de la información mediante
archivos CSV dejó de ser suficiente. En este sprint migramos los movimientos portuarios
a una base de datos relacional (`transito_portuario`) modelada con SQLAlchemy, con las
entidades Buque, Movimiento, Radar y Evidencia. Los radares son móviles: un mismo radar
puede registrar movimientos en distintos muelles, por lo que el muelle se asocia a cada
movimiento y no al radar. Para auditar qué versión de los datos se utilizó en cada
análisis, versionamos con DVC las imágenes, los gráficos y el dataset procesado final,
usando Supabase como almacenamiento S3. Por último, como el OCR no siempre logra leer
correctamente las matrículas, construimos una base vectorial (`buque_vectorial`) con
ChromaDB y embeddings de OpenCLIP que permite identificar un buque por similitud visual
de su imagen, sin depender del texto.

## Estructura
```
port_log/
├── data/
│   ├── interim/
│   │   ├── imgs/                         imágenes preprocesadas por etapa
│   │   ├── group_images.json             metadatos de imágenes agrupadas en plates/completes
│   │   └── plots.dvc                     gráficos versionados con DVC
│   ├── processed/
│   │   ├── port_movements_image.csv.dvc  dataset final versionado con DVC
│   │   ├── transito_portuario.db         base relacional SQLAlchemy
│   │   └── buque_vectorial/              base vectorial ChromaDB (OpenCLIP)
│   └── raw/
│       └── imgs.dvc                      imágenes originales versionadas con DVC
└── reports/                              resúmenes estadísticos y conclusiones
```

## Integrantes
- Alsop Agustín
- Alexia Aubone
- Marcos Javier Gómez Hollger
- Germán Ponce
- Agustin Serra Rivero
