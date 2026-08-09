# TA-IND-04 — Análisis de Rendimiento Paralelo aplicado al PFC

## Identificación

- **Universidad:** Universidad Técnica Estatal de Quevedo
- **Facultad:** Ciencias de la Computación
- **Carrera:** Ingeniería de Software
- **Asignatura:** Aplicaciones Distribuidas (ISR-701)
- **Unidad:** Unidad 4 — Cómputo Paralelo y Distribuido
- **Actividad:** TA-IND-04 — Informe Técnico Individual
- **Período académico:** 2026–2027 PPA
- **Docente:** Gleiston C. Guerrero-Ulloa, M.Sc.
- **Estudiante:** Jeremy Ruperto Gaibor Rodríguez
- **Equipo PE-U4:** Equipo C
- **PFC de referencia:** Tienda Tech
- **Transformación declarada como foco individual:** T1 — Filtrado y selección

## Origen de los datos (PE-U4)

Los datos experimentales de partida son los producidos en equipo durante la práctica
GA-SUM-05 / PE-U4 y son legítimamente compartidos. El análisis, la redacción, las
figuras y las conclusiones de este informe son estrictamente individuales.

- **Repositorio de origen (PE-U4, Equipo C):**
  `https://github.com/ffarinangog2/pe-u4-spark-equipo-c`
- **Commit exacto del que se toman las mediciones (incluye T1 con N=1 y N=2):**
  `6b363abdd30e57425fc8e49a9a13181c2cb2a5b9`
- **Archivos fuente de los tiempos:**
  `resultados/tiempos_crudos.csv` y `resultados/tiempos_resumen.csv` del repositorio anterior.
- **Copia local de los datos usados en este informe:** `datos/tiempos_base.csv`
- **Evidencia adicional de trazabilidad:** capturas en `figuras/` (`evidencia_commit_t1...`,
  `evidencia_tiempos_crudos...`, `evidencia_tiempos_resumen...`) que documentan el commit y
  los archivos CSV de origen.

## Estructura del repositorio

```
ta-ind-04-gaibor/
├── README.md              (este archivo)
├── LICENSE
├── datos/
│   └── tiempos_base.csv           (copia de los datos de PE-U4 usados)
├── docs/
│   ├── TA_IND_04_Informe.tex      (fuente LaTeX del informe)
│   ├── TA_IND_04_Informe.pdf      (PDF compilado, committeado)
│   └── references.bib             (bibliografía IEEE, gestionada con biblatex)
└── figuras/
    ├── fig_speedup.png                 (figura propia, 300 DPI: speedup de T1 vs. Amdahl)
    ├── evidencia_commit_t1.png         (evidencia del commit de origen de los datos)
    ├── evidencia_tiempos_crudos.png    (evidencia de tiempos_crudos.csv)
    └── evidencia_tiempos_resumen.png   (evidencia de tiempos_resumen.csv)
```

## Entorno de ejecución declarado

- **PySpark:** 3.5.0
- **Python:** 3.12.10
- **OpenJDK:** 17.0.20
- **Sistema operativo:** Windows 11
- **Modo de ejecución:** Spark Standalone, master `spark://127.0.0.1:7077`
- **Configuración por executor:** 1 core, 512 MiB de memoria
- **Número de executors evaluados:** 1, 2 y 4 (ajustando particiones, paralelismo por
  defecto y máximo de cores en cada configuración)

## Instrucciones exactas de compilación

El documento se compila con **pdflatex + biber**. Se requiere una distribución TeX Live
con los paquetes `biblatex`, `biber`, `siunitx`, `tikz` y `booktabs` disponibles.

Desde la raíz del repositorio:

```bash
cd docs
pdflatex -interaction=nonstopmode TA_IND_04_Informe.tex
biber TA_IND_04_Informe
pdflatex -interaction=nonstopmode TA_IND_04_Informe.tex
pdflatex -interaction=nonstopmode TA_IND_04_Informe.tex
```

**Secuencia obligatoria:** `pdflatex → biber → pdflatex → pdflatex`
(dos pasadas finales de pdflatex son necesarias para resolver referencias cruzadas
de ecuaciones, figura y bibliografía).

El resultado es `docs/TA_IND_04_Informe.pdf`, ya committeado en el repositorio como
respaldo, en caso de que el entorno de compilación del docente difiera del original.

### Verificación en máquina limpia

Antes de la entrega se verificó que la secuencia anterior reproduce el PDF clonando el
repositorio en un directorio nuevo, sin configuración previa distinta de una instalación
estándar de TeX Live (`texlive-full` o equivalente con `biber` instalado).

## Declaración de uso de inteligencia artificial generativa

Se utilizó ChatGPT como herramienta de apoyo para revisar la redacción, organizar el
contenido del informe y verificar cálculos (speedup, Karp-Flatt, eficiencia y el
diagnóstico del umbral de rentabilidad). Los datos experimentales, resultados y
conclusiones se elaboraron a partir de las mediciones registradas en el repositorio
PE-U4 citado arriba.
