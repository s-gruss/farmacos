# Trabajo Práctico N°2 — Análisis Farmacológico In Silico
 
---
 
## 1. Selección de compuestos
 
### 1.a. Compuestos de uso común (PubChem)
 
| Compuesto | Canonical SMILES |
|-----------|-----------------|
| Aspirin | `CC(=O)OC1=CC=CC=C1C(=O)O` |
| Paracetamol | `CC(=O)NC1=CC=C(C=C1)O` |
| Caffeine | `CN1C=NC2=C1C(=O)N(C(=O)N2C)C` |
 
### 1.b. Fármacos seleccionados
 
#### Fármacos aprobados (anticáncer)
 
**Imatinib**
- SMILES: `CC1=C(C=C(C=C1)NC(=O)C2=CC=C(C=C2)CN3CCN(CC3)C)NC4=NC=CC(=N4)C5=CN=CC=C5`
- Inhibidor de quinasas de molécula pequeña que revolucionó el tratamiento del cáncer, particularmente la leucemia mieloide crónica. Aprobado por la FDA el 1 de febrero de 2001 y por la EMA el 7 de noviembre de 2001.
- PubChem CID: [5291](https://pubchem.ncbi.nlm.nih.gov/compound/5291)

**Temozolomide**
- SMILES: `CN1C(=O)N2C=NC(=C2N=N1)C(=O)N`
- Utilizado junto a radioterapia como estándar de cuidado para glioblastoma y astrocitoma anaplásico refractario. Aprobado por la FDA el 11 de agosto de 1999 (cápsula oral) y el 27 de febrero de 2009 (inyección intravenosa). Comercializado como TEMODAR® por Merck.
- PubChem CID: [5394](https://pubchem.ncbi.nlm.nih.gov/compound/5394)

**5-Fluorouracil**
- SMILES: `C1=C(C(=O)NC(=O)N1)F`
- Análogo de pirimidina utilizado como agente antineoplásico para tratar tumores sólidos incluyendo cáncer de colon, recto, mama, gástrico, pancreático, ovárico, vesical y hepático. Aprobado el 30 de septiembre de 1998.
- PubChem CID: [3385](https://pubchem.ncbi.nlm.nih.gov/compound/3385)
#### Fármacos experimentales
 
**Resveratrol**
- SMILES: `C1=CC(=CC=C1/C=C/C2=CC(=CC(=C2)O)O)O`
- Polifenol vegetal encontrado en altas concentraciones en uvas rojas. Propuesto como tratamiento para hiperlipidemia y prevención de hígado graso, diabetes, aterosclerosis y envejecimiento. En investigación; máximo alcanzado: Fase 3.
- PubChem CID: [445154](https://pubchem.ncbi.nlm.nih.gov/compound/445154)

**Curcumin**
- SMILES: `COC1=C(C=CC(=C1)/C=C/C(=O)CC(=O)/C=C/C2=CC(=C(C=C2)O)OC)O`
- Molécula altamente pleiotrópica con actividades antibacteriana, antiinflamatoria, hipoglucemiante, antioxidante, cicatrizante y antimicrobiana. Investigada para el tratamiento de mucositis, cáncer rectal, cáncer de próstata, esquizofrenia crónica y deterioro cognitivo leve (MCI). Su baja biodisponibilidad oral limita su eficacia terapéutica.
- PubChem CID: [969516](https://pubchem.ncbi.nlm.nih.gov/compound/969516)
---
 
## 2. Predicción de propiedades fisicoquímicas (SwissADME)
 
Propiedades obtenidas mediante [SwissADME](http://www.swissadme.ch) a partir de los SMILES de cada compuesto.
 
| Compuesto | MW (g/mol) | LogP | HBA | HBD | TPSA (Å²) | Rot. bonds |
|-----------|-----------|------|-----|-----|-----------|-----------|
| Aspirin | 180.16 | 1.28 | 4 | 1 | 63.60 | 3 |
| Paracetamol | 151.16 | 0.93 | 2 | 2 | 49.33 | 2 |
| Caffeine | 194.19 | 0.08 | 3 | 0 | 61.82 | 0 |
| Imatinib | 493.60 | 3.38 | 6 | 2 | 86.28 | 8 |
| Temozolomide | 194.15 | −0.92 | 5 | 1 | 108.17 | 1 |
| 5-Fluorouracil | 130.08 | 0.13 | 3 | 2 | 65.72 | 0 |
| Resveratrol | 228.24 | 2.48 | 3 | 3 | 60.69 | 2 |
| Curcumin | 368.38 | 3.03 | 6 | 2 | 93.06 | 8 |
 
> **MW**: peso molecular · **LogP**: índice de lipofilicidad · **HBA**: aceptores de puente de H · **HBD**: dadores de puente de H · **TPSA**: superficie polar topológica · **Rot. bonds**: enlaces rotables
 
---
 
## 3. Identificación de subestructuras indeseables (PAINS)
 
El análisis se realizó utilizando el módulo Python `admet_module` en Google Colab:
[https://colab.research.google.com/drive/1VjEV80n9U3faOHIQ-JusWDQd50qdHocO](https://colab.research.google.com/drive/1VjEV80n9U3faOHIQ-JusWDQd50qdHocO?usp=sharing)
 
```bash
pip install rdkit-pypi molvs requests pandas numpy matplotlib seaborn
pip install deepchem
```
 
```python
from admet_module import analisis_completo
mis_moleculas = {'molecula': 'COc1ccccc1C=O'}
resultados = analisis_completo(mis_moleculas)
```
 
### Resultados
 
**Compuestos del ítem 1.a (aspirin, paracetamol, caffeine):** no se detectaron subestructuras indeseables (PAINS) en ninguno de los tres compuestos.
 
**Compuestos del ítem 1.b (imatinib, temozolomide, 5-fluorouracil, resveratrol, curcumin):** no se detectaron alertas PAINS en ninguno de los cinco compuestos.
 
| Compuesto | PAINS_Alerts | PAINS_Details |
|-----------|-------------|---------------|
| Aspirin | 0 | — |
| Paracetamol | 0 | — |
| Caffeine | 0 | — |
| Imatinib | 0 | — |
| Temozolomide | 0 | — |
| 5-Fluorouracil | 0 | — |
| Resveratrol | 0 | — |
| Curcumin | 0 | — |
 
Todos los compuestos presentaron toxicidad predicha **Low** con LD50 estimado > 5000 mg/kg según el módulo.
 
**Datos ADMET (ítem 1.b):**
 
| Compuesto | Absorción | Penetración BBB | Unión a proteínas plasmáticas | Inhibición CYP | Clearance renal |
|-----------|----------|----------------|-------------------------------|----------------|----------------|
| Imatinib | High | No | High | Low | Low |
| Temozolomide | High | No | Low | Low | High |
| 5-Fluorouracil | High | Yes | Low | Low | High |
| Resveratrol | High | No | Medium | Low | Low |
| Curcumin | High | No | High | Low | Low |
 
---
 
## 4. Predicción de toxicidad in silico (ProTox-II)
 
Análisis realizado en [ProTox-II](https://tox-new.charite.de/protox_II/) con los SMILES de todos los compuestos.
 
### 4.a. LD50 predicho y clase de toxicidad
 
| Compuesto | LD50 predicho (mg/kg) | Clase de toxicidad |
|-----------|-----------------------|-------------------|
| Aspirin | 250 | Clase 3 |
| Paracetamol | 338 | Clase 4 |
| Caffeine | 127 | Clase 3 |
| Imatinib | 100 | Clase 3 |
| Temozolomide | 498 | Clase 4 |
| 5-Fluorouracil | 1923 | Clase 4 |
| Resveratrol | 1560 | Clase 4 |
| Curcumin | 2000 | Clase 4 |
 
> Las clases van de I (muy tóxico, LD50 ≤ 5 mg/kg) a VI (no tóxico, LD50 > 5000 mg/kg).
 
### 4.b. Hepatotoxicidad, mutagenicidad y carcinogenicidad
 
| Compuesto | Hepatotoxicidad | Carcinogenicidad | Mutagenicidad |
|-----------|----------------|-----------------|---------------|
| Aspirin | Inactive (0.51) | Inactive (0.86) | Inactive (0.97) |
| Paracetamol | **Active (0.74)** | Inactive (0.51) | Inactive (0.90) |
| Caffeine | Inactive (0.97) | Inactive (0.93) | Inactive (0.94) |
| Imatinib | **Active (0.71)** | Inactive (0.67) | Inactive (0.73) |
| Temozolomide | Inactive (0.58) | Inactive (0.50) | Inactive (0.61) |
| 5-Fluorouracil | Inactive (0.78) | **Active (0.85)** | Inactive (0.88) |
| Resveratrol | Inactive (0.74) | Inactive (0.71) | Inactive (0.92) |
| Curcumin | Inactive (0.61) | Inactive (0.84) | Inactive (0.88) |
 
> Entre paréntesis se indica la probabilidad predicha por el modelo.
 
### Conclusión
 
La molécula con menor toxicidad según ProTox-II es **curcumin**, con el LD50 más alto del conjunto (2000 mg/kg, Clase 4) y todas las alertas de toxicidad en estado Inactive. Resveratrol (1560 mg/kg) presenta un perfil similar. En el extremo opuesto, imatinib presenta el LD50 más bajo (100 mg/kg, Clase 3) y hepatotoxicidad predicha como activa.
 
---
 
## 5. Fichas técnicas
 
### Criterios evaluados
 
**Filtro de Lipinski (Regla de los 5):** MW ≤ 500 g/mol · LogP ≤ 5 · HBD ≤ 5 · HBA ≤ 10
 
**Filtro de Veber:** TPSA ≤ 140 Å² · enlaces rotables ≤ 10
 
---
 
### Aspirin
 
| Propiedad | Valor |
|-----------|-------|
| Categoría | Uso común |
| SMILES | `CC(=O)OC1=CC=CC=C1C(=O)O` |
| Peso molecular | 180.16 g/mol |
| LogP | 1.28 |
| HBA / HBD | 4 / 1 |
| TPSA | 63.60 Å² |
| Rot. bonds | 3 |
| LD50 estimado | 250 mg/kg (Clase 3) |
| Lipinski | ✓ Cumple (todos los criterios) |
| Veber | ✓ Cumple |
| PAINS | Sin alertas |
| Hepatotoxicidad | Inactive |
| Carcinogenicidad | Inactive |
| Mutagenicidad | Inactive |
 
---
 
### Paracetamol
 
| Propiedad | Valor |
|-----------|-------|
| Categoría | Uso común |
| SMILES | `CC(=O)NC1=CC=C(C=C1)O` |
| Peso molecular | 151.16 g/mol |
| LogP | 0.93 |
| HBA / HBD | 2 / 2 |
| TPSA | 49.33 Å² |
| Rot. bonds | 2 |
| LD50 estimado | 338 mg/kg (Clase 4) |
| Lipinski | ✓ Cumple (todos los criterios) |
| Veber | ✓ Cumple |
| PAINS | Sin alertas |
| Hepatotoxicidad | **Active** (prob. 0.74) |
| Carcinogenicidad | Inactive |
| Mutagenicidad | Inactive |
 
---
 
### Caffeine
 
| Propiedad | Valor |
|-----------|-------|
| Categoría | Uso común |
| SMILES | `CN1C=NC2=C1C(=O)N(C(=O)N2C)C` |
| Peso molecular | 194.19 g/mol |
| LogP | 0.08 |
| HBA / HBD | 3 / 0 |
| TPSA | 61.82 Å² |
| Rot. bonds | 0 |
| LD50 estimado | 127 mg/kg (Clase 3) |
| Lipinski | ✓ Cumple (todos los criterios) |
| Veber | ✓ Cumple |
| PAINS | Sin alertas |
| Hepatotoxicidad | Inactive |
| Carcinogenicidad | Inactive |
| Mutagenicidad | Inactive |
 
---
 
### Imatinib
 
| Propiedad | Valor |
|-----------|-------|
| Categoría | Anticáncer aprobado |
| SMILES | `CC1=C(C=C(C=C1)NC(=O)C2=CC=C(C=C2)CN3CCN(CC3)C)NC4=NC=CC(=N4)C5=CN=CC=C5` |
| Peso molecular | 493.60 g/mol |
| LogP | 3.38 |
| HBA / HBD | 6 / 2 |
| TPSA | 86.28 Å² |
| Rot. bonds | 8 |
| LD50 estimado | 100 mg/kg (Clase 3) |
| Lipinski | ✓ Cumple |
| Veber | ✓ Cumple |
| PAINS | Sin alertas |
| Hepatotoxicidad | **Active** (prob. 0.71) |
| Carcinogenicidad | Inactive |
| Mutagenicidad | Inactive |
 
---
 
### Temozolomide
 
| Propiedad | Valor |
|-----------|-------|
| Categoría | Anticáncer aprobado |
| SMILES | `CN1C(=O)N2C=NC(=C2N=N1)C(=O)N` |
| Peso molecular | 194.15 g/mol |
| LogP | −0.92 |
| HBA / HBD | 5 / 1 |
| TPSA | 108.17 Å² |
| Rot. bonds | 1 |
| LD50 estimado | 498 mg/kg (Clase 4) |
| Lipinski | ✓ Cumple |
| Veber | ✓ Cumple |
| PAINS | Sin alertas |
| Hepatotoxicidad | Inactive |
| Carcinogenicidad | Inactive |
| Mutagenicidad | Inactive |
 
---
 
### 5-Fluorouracil
 
| Propiedad | Valor |
|-----------|-------|
| Categoría | Anticáncer aprobado |
| SMILES | `C1=C(C(=O)NC(=O)N1)F` |
| Peso molecular | 130.08 g/mol |
| LogP | 0.13 |
| HBA / HBD | 3 / 2 |
| TPSA | 65.72 Å² |
| Rot. bonds | 0 |
| LD50 estimado | 1923 mg/kg (Clase 4) |
| Lipinski | ✓ Cumple (todos los criterios holgadamente) |
| Veber | ✓ Cumple |
| PAINS | Sin alertas |
| Hepatotoxicidad | Inactive |
| Carcinogenicidad | **Active** (prob. 0.85) |
| Mutagenicidad | Inactive |
 
---
 
### Resveratrol
 
| Propiedad | Valor |
|-----------|-------|
| Categoría | Experimental |
| SMILES | `C1=CC(=CC=C1/C=C/C2=CC(=CC(=C2)O)O)O` |
| Peso molecular | 228.24 g/mol |
| LogP | 2.48 |
| HBA / HBD | 3 / 3 |
| TPSA | 60.69 Å² |
| Rot. bonds | 2 |
| LD50 estimado | 1560 mg/kg (Clase 4) |
| Lipinski | ✓ Cumple (todos los criterios) |
| Veber | ✓ Cumple |
| PAINS | Sin alertas |
| Hepatotoxicidad | Inactive |
| Carcinogenicidad | Inactive |
| Mutagenicidad | Inactive |
 
---
 
### Curcumin
 
| Propiedad | Valor |
|-----------|-------|
| Categoría | Experimental |
| SMILES | `COC1=C(C=CC(=C1)/C=C/C(=O)CC(=O)/C=C/C2=CC(=C(C=C2)O)OC)O` |
| Peso molecular | 368.38 g/mol |
| LogP | 3.03 |
| HBA / HBD | 6 / 2 |
| TPSA | 93.06 Å² |
| Rot. bonds | 8 |
| LD50 estimado | 2000 mg/kg (Clase 4) |
| Lipinski | ✓ Cumple (MW < 500, LogP < 5) |
| Veber | ✓ Cumple |
| PAINS | Sin alertas |
| Hepatotoxicidad | Inactive |
| Carcinogenicidad | Inactive |
| Mutagenicidad | Inactive |
 
---
 
### Respuestas a las preguntas del ítem 5
 
**¿Qué compuestos cumplen mejor con los filtros de Lipinski y Veber?**
 
Todos los compuestos analizados cumplen con los filtros de Lipinski y Veber. Los que cumplen con mayor margen son aspirin, paracetamol, caffeine, 5-fluorouracil y resveratrol, ya que son moléculas de bajo peso molecular, con LogP moderado y todos sus parámetros claramente dentro de los límites. Curcumin e imatinib también cumplen, aunque con valores más cercanos a los límites (curcumin: rb = 8, HBA = 6; imatinib: MW = 493.6 g/mol). En la práctica, la baja biodisponibilidad oral del curcumin documentada en la literatura refleja que el cumplimiento formal de los filtros no siempre garantiza buen comportamiento farmacológico.
 
**¿Aparecieron moléculas con alertas PAINS?**
 
No. Ninguna de las 8 moléculas analizadas presentó alertas PAINS. Esto indica que ninguna contiene subestructuras asociadas a falsos positivos frecuentes en ensayos de screening de alta throughput (HTS), como quinonas reactivas, catecoles o grupos Michael aceptores problemáticos.
 
**¿Cuál es su toxicidad?**
 
Según ProTox-II, todos los compuestos se ubican en Clase 3 o Clase 4 de toxicidad. Las diferencias más relevantes son las siguientes: paracetamol e imatinib presentan hepatotoxicidad predicha como activa, lo que es consistente con sus perfiles clínicos conocidos. El 5-fluorouracil es el único compuesto con carcinogenicidad activa, en consonancia con su mecanismo de acción como antimetabolito que interfiere con la síntesis de ADN. Los compuestos experimentales resveratrol y curcumin son los que muestran menor toxicidad global, con los LD50 más altos (1560 y 2000 mg/kg respectivamente) y todas las alertas toxicológicas en estado Inactive.