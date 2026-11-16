<h1 align="center">🏠 Precio de la vivienda en el Gran Santiago</h1>

<p align="center">
  <b>¿Cuánto valora el mercado la cercanía a plazas y parques?</b><br/>
  Regresión hedónica, machine learning y validación espacial con 102.642 ventas de casas (2019–2023)
</p>

<p align="center">
  <img src="https://img.shields.io/badge/R-276DC3?style=for-the-badge&logo=r&logoColor=white" alt="R">
  <img src="https://img.shields.io/badge/sf-Análisis_espacial-589632?style=for-the-badge" alt="sf">
  <img src="https://img.shields.io/badge/Random_Forest-ML-F37626?style=for-the-badge" alt="Random forest">
  <img src="https://img.shields.io/badge/Leaflet-Mapa_interactivo-199900?style=for-the-badge&logo=leaflet&logoColor=white" alt="Leaflet">
</p>

---

## 📌 Resumen

El precio de una casa depende de sus características y también del lugar donde está. Este trabajo analiza cómo influyen la **accesibilidad a áreas verdes**, la **distancia a los centros de empleo** y el **perfil socioeconómico de la zona censal** en el precio de las casas vendidas en el Gran Santiago (Chile).

Trabajo final del módulo *Transporte y Hogares + Machine Learning* del **Diplomado en Análisis Espacial de Datos, Facultad de Arquitectura y Urbanismo, Universidad de Chile** (octubre de 2026).

📄 **[Leer el informe completo (PDF)](Informe_Precio_Vivienda_Santiago.pdf)**
🗺️ **[Abrir el mapa interactivo de plazas](mapa_plazas_interactivo.html)** (descargalo y abrilo en el navegador)

## 🗂️ Datos

| Fuente | Detalle |
|---|---|
| Ventas de casas 2019–2023 | 102.642 transacciones con precio en UF, superficies, antigüedad y coordenadas |
| Zonas censales (Región Metropolitana) | 1.865 polígonos |
| Plazas y parques (SIEDU) | 10.063 polígonos con su superficie |
| Censo 2017 (INE) | Escolaridad, densidad, % de personas de 65 años o más y personas por hogar |

Todas las capas se proyectaron a UTM 19S (EPSG:32719). Cada venta se unió a su zona censal mediante un cruce espacial punto en polígono.

## ⚙️ Métodos

- **Accesibilidad a áreas verdes** con el modelo gravitacional de Hansen (1959), con tres valores de β (regional, intermedio y local), hectáreas a 15 minutos caminando y tiempo a la plaza de 1 ha o más.
- **Cuatro modelos hedónicos anidados (MCO)** sobre log(UF): vivienda, accesibilidad, atributos zonales y efecto fijo por comuna.
- **Machine learning:** random forest (300 árboles), random forest con coordenadas y gradient boosting (1.500 árboles).
- **Separación por vivienda** (80/20), para que una casa revendida no quede en entrenamiento y prueba a la vez.
- **Validación cruzada espacial por bloques** (25 bloques k-means, 5 pliegues), para medir el error en barrios que el modelo no vio.
- **Autocorrelación de los residuos** con el I de Moran (vecindad tipo reina).

## 📊 Resultados

<p align="center"><img src="figuras/fig1_precios.png" alt="Precio mediano por zona censal en UF y en UF/m2" width="900"></p>
<p align="center"><sub>Precio mediano por zona censal. Los quintiles más altos se concentran en el cono oriente.</sub></p>

- 🎓 **Un año más de escolaridad promedio en la zona** se asocia con un precio **19 % mayor**.
- 🏢 **Cada kilómetro de distancia a Tobalaba** (centro financiero) reduce el precio un **2,6 %**.
- 🌳 La accesibilidad a áreas verdes tiene un **efecto pequeño y sensible a cómo se mide**: las medidas regionales pierden significancia al controlar por el nivel socioeconómico; las locales se mantienen.
- 🤖 El machine learning baja el error (MAE) de **921 a unas 750 UF** en barrios conocidos, pero **esa ventaja desaparece en sectores no vistos**, donde la regresión generaliza igual o mejor (R² 0,82).

<p align="center"><img src="figuras/fig6_residuos.png" alt="Residuos por zona: MCO 3 frente a random forest con coordenadas" width="900"></p>
<p align="center"><sub>Los residuos de la regresión están agrupados (I de Moran = 0,29); los del random forest con coordenadas, no (I = 0,01).</sub></p>

<details>
<summary>Ver más figuras</summary>

<p align="center"><img src="figuras/fig2_accesibilidad.png" alt="Medidas de accesibilidad a áreas verdes" width="800"></p>
<p align="center"><img src="figuras/fig3_zonales.png" alt="Atributos zonales del Censo 2017" width="800"></p>
<p align="center"><img src="figuras/fig5_importancia.png" alt="Importancia de variables del random forest" width="700"></p>

</details>

## 💡 Conclusiones

- Para **tasar casas en barrios con muchas ventas**, el machine learning es preferible.
- Para **anticipar precios en sectores nuevos** o poco observados, un modelo con estructura generaliza mejor.
- Solo la regresión permite medir el efecto en unidades: un minuto adicional a un parque de 1 ha o más se asocia con un precio **0,05 % menor**.
- La autocorrelación de los residuos señala variables locales omitidas. Un modelo espacial (SAR o SEM) sería la extensión natural.

## 📁 Contenido del repositorio

```
├── README.md
├── Informe_Precio_Vivienda_Santiago.pdf
├── mapa_plazas_interactivo.html
└── figuras/
```

Los datos de ventas y el material del curso no se incluyen porque fueron provistos por el diplomado (prof. Tomás Cox).

---

<p align="center">
  <b>Anabella Engelman</b> · Geógrafa · Análisis espacial de datos<br/>
  <a href="https://github.com/geografaengelman-dev">GitHub</a> ·
  <a href="https://www.linkedin.com/in/anabella-engelman-ab1aaa80/">LinkedIn</a> ·
  <a href="mailto:geografaengelman@gmail.com">geografaengelman@gmail.com</a>
</p>

<p align="center"><sub>© 2026 Anabella Engelman. Todos los derechos reservados.</sub></p>
