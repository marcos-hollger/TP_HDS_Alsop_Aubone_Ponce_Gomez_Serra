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

## Integrantes
- Alsop Agustín
- Alexia Aubone
- Marcos Javier Gómez Hollger
- Germán Ponce
- Agustin Serra Rivero
