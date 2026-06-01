# TP3: Asignación por homología y filogenia molecular

**Profesora:** Dra. Ana Julia Velez Rueda

---

## Introducción

Las albúminas son las proteínas sanguíneas más abundantes en los mamíferos y cumplen la función principal de unir y transportar diversos compuestos endógenos y exógenos, en su mayoría hidrofóbicos. Esta proteína globular está compuesta por tres dominios homólogos (I, II y III), cada uno de los cuales contiene dos subdominios similares (A y B). En particular, los residuos **Lys 199, Arg 410, Tyr 411, Cys 34 y Lys 195** de HSA se describen como algunos de los importantes, no solo para la unión del ligando sino también para la catálisis. Esto la hace una proteína de interés farmacológico ya que se encuentra involucrada en el reparto (*delivery*) de fármacos.

A lo largo de los vertebrados, las albúminas se conservan evolutivamente, aunque muestran una notable diversidad estructural.

---

## DESAFÍO I: Asignación por homología

Utiliza la secuencia de albúmina humana (HSA) como consulta en BLASTp contra la base de datos de proteínas de vertebrados.

### a. ¿Qué especies presentan ortólogos más cercanos a la HSA?

A partir de los resultados de BLASTp, los ortólogos más cercanos a la albúmina humana corresponden a: **Gorila, Pan paniscus, Pongo abelii y Pongo pygmaeus**. Todos tienen cobertura del 100%, porcentajes de identidad entre el 98 y 99% y E-value de 0. Esto indica una alta conservación de la albúmina entre humanos y otros primates.

También se identifican otras especies, tales como *Nomascus leucogenys*, *Macaca Mulata*, *Papio anubis*, *Mus musculus*, *Bos taurus*, *Canis lupus familiaris* y *Felis catus*.

Como son los ortólogos se ignoran los resultados de *Homo sapiens* (porque queremos ver de otras especies) y los que sean sintéticos o parciales. Se buscó la secuencia FASTA en UniProt y con ello se realizó la búsqueda en BLASTp.

### b. ¿Qué criterios utilizaste para identificarlos?

Para buscar los ortólogos más cercanos se consideraron las secuencias con:

- alto porcentaje de identidad
- alta cobertura, es decir que se alinee casi toda la secuencia de HSA
- E-value bajo, que indica una similitud no azarosa

Se excluyeron secuencias *Homo sapiens* (porque es la misma especie), proteínas parciales y constructos sintéticos.

### c. ¿Podrías identificar al menos dos ortólogos y dos parálogos en la familia de albúminas?

**Ortólogos:** Son homólogos que están presentes dentro de diferentes especies y tienen funciones muy similares o idénticas. Los árboles filogenéticos son algo así como el árbol genealógico de las especies, e implican una hipótesis sobre las relaciones que existen entre los organismos. Mismo gen en especies distintas.

**Parálogos:** Que están presentes dentro de una especie y que suelen diferir en sus funciones bioquímicas. Genes relacionados dentro de una misma familia, originados por duplicación génica.

- **Ortólogos:** Albúmina sérica de *Gorilla gorilla*, Albúmina sérica de *Pan paniscus*. Estas proteínas fueron identificadas como ortólogos debido a su alto porcentaje de identidad de secuencia, elevado query cover y E-value cercano a 0 en comparación con la HSA.
- **Parálogos:** Alpha-fetoprotein (AFP), Afamin (AFM). Estas proteínas pertenecen a la misma familia génica que la albúmina humana, pero surgieron por eventos de duplicación génica y cumplen funciones diferentes, por lo que se consideran parálogos.

### d. Obtené secuencias de albúminas de al menos 50–90 especies diferentes de mamíferos desde UniProt y construí un alineamiento de proteínas ortólogas usando Clustal Omega

No se ven todas las proteínas en la imagen, pero alineamos **60 secuencias**.

### e. ¿Qué porcentaje de identidad comparten en promedio?

A partir de la matriz de identidad generada por Clustal Omega, se calculó una identidad promedio de **77,02%** entre las 60 secuencias de albúmina de mamíferos analizadas. Para el cálculo se excluyeron los valores de la diagonal de la matriz, ya que corresponden a la comparación de cada secuencia consigo misma.

Este resultado sugiere que las albúminas de mamíferos presentan una conservación importante.

Esta identidad promedio se calculó sumando los valores de las 3540 identidades (que son todas las celdas de la tabla menos la diagonal) y se divide por 3540 (es 3540 porque hay 60 secuencias y se consideraron 60 × 59 = 3540 comparaciones).

### f. ¿Qué regiones se encuentran más conservadas?

En el alineamiento múltiple se observa una alta conservación general, especialmente de la región N-terminal de las albúminas analizadas. Se identificaron puntualmente:

- el motivo **MKWVTF** en las posiciones 1–6
- **SSAYSRGVFRR** en las posiciones 38–41
- **KGLVLIAF** en las posiciones 44–51
- **QYLQQCP** en las posiciones 53–59

También se observa la conservación de residuos puntuales como **Cys58** y **Pro59**, que aparecen mantenidos en la mayoría de las secuencias visibles.

En conjunto, el alineamiento muestra que las albúminas de mamíferos están muy conservadas; si bien existen cambios puntuales entre especies, la mayor parte de la secuencia mantiene aminoácidos idénticos o muy similares (lo que concuerda con el alto promedio de identidad obtenido). Esto sugiere que la estructura y la función principal de la albúmina se mantuvieron fuertemente conservadas durante la evolución de los mamíferos.

---

## DESAFÍO II: Árbol filogenético

Usando el alineamiento del punto I.d construí un árbol filogenético mediante la herramienta IQ-tree.

### a. Visualiza el árbol usando iTOL o FigTree

🔗 https://itol.embl.de/tree/1902103227231561779649091

### b. Estudiá los clados y relacionalo con las observaciones del punto anterior

El árbol recupera agrupaciones que son totalmente consistentes con la clasificación taxonómica clásica, lo que valida la calidad del alineamiento y del análisis filogenético:

| Clado en el árbol | Especies incluidas | Grupo taxonómico |
|---|---|---|
| Clado basal superior | SHEEP, CAPHI, BOVIN, BALMU, MONMO | Artiodáctilos (rumiantes + cetáceos) |
| Junto a ellos | PIG, 9CETA | Suinos y cetáceos, Artiodactyla |
| Clado siguiente | HORSE, EQUAS | Perissodactyla |
| Clado carnívoros | FELCA, PANTA, CANLF, URSMA, AILME, NEOVI, MUSPF | Carnivora |
| Clado roedores/lagomorfos | MOUSE, RAT, MUSCR, MESAU, MERUN, CRIGR, RABIT | Rodentia + Lagomorpha |
| Clado primates | HUMAN, PANTR, PANPA, GORGO, PONAB, MACMU, MACFA, PAPAN, RHIBE, RHIRO, NOMLE, CEBIM, SAIBB, CALJA, AOTNA | Primates (Hominidae → Platyrrhini) |

El árbol filogenético construido con IQ-TREE a partir del alineamiento múltiple de secuencias de albúmina de 60 especies de mamíferos obtenidas de UniProt recupera una topología ampliamente consistente con la clasificación taxonómica clásica de este grupo. Este resultado constituye en sí mismo una validación de la calidad del alineamiento generado con Clustal Omega y de la utilidad de la albúmina como marcador filogenético en mamíferos.

**Organización en clados y concordancia taxonómica**

El árbol resuelve con claridad los principales órdenes de mamíferos incluidos en el análisis. Los primates forman un clado monofilético bien resuelto, con una estructura interna que refleja las relaciones conocidas entre haplorrinos y estrepsirrinos:

- Los **grandes simios** (*Homo sapiens*, *Pan troglodytes*, *Pan paniscus*, *Gorilla gorilla*, *Pongo abelii*) se agrupan con longitudes de rama mínimas entre sí, indicando escasa divergencia de secuencia.
- Los **monos del Viejo Mundo** (macacos, babuinos, *Cercocebus*) forman un clado hermano.
- Los **platirrinos** (*Callithrix*, *Saimiri*, *Aotus*, *Cebus*) se ubican más distantes, en concordancia con su separación evolutiva hace aproximadamente 40 millones de años.
- Los **lémures** (*Propithecus*, *Microcebus*) se posicionan como estrepsirrinos, correctamente separados del resto de los primates.

Los carnívoros, artiodáctilos, perisodáctilos y roedores junto con lagomorfos conforman cada uno sus propios clados monofiléticos. El **elefante africano** (*Loxodonta africana*), representante de Afrotheria, aparece como una rama divergente y relativamente larga, reflejando la antigüedad de este linaje.

La identidad promedio del 77,02% refleja la heterogeneidad de distancias evolutivas presentes en el dataset. Dentro de cada clado, las identidades son notablemente más altas: las secuencias de grandes simios comparten más del 98% de identidad con la albúmina humana, mientras que la comparación entre primates y roedores desciende a valores cercanos al 70%, y entre primates y artiodáctilos a valores similares o menores.

Las regiones identificadas en el alineamiento como más conservadas, particularmente el motivo N-terminal **MKWVTFI** y el segmento **SAYSRG**, aparecen prácticamente invariantes en todos los clados del árbol. Esta conservación universal es consistente con una fuerte **presión de selección purificadora** sobre estas posiciones. Los residuos funcionalmente críticos de la albúmina (Cys34, Lys195, Lys199, Arg410 y Tyr411) se encuentran precisamente en regiones de alta conservación, lo que respalda la hipótesis de que la función principal de la albúmina como transportador se mantuvo conservada a lo largo de toda la evolución de los mamíferos.

Los resultados del árbol son plenamente coherentes con los ortólogos más cercanos identificados mediante BLASTp: *Gorilla gorilla*, *Pan paniscus* y *Pongo abelii* son exactamente las que aparecen como ramas más próximas a *Homo sapiens* en el árbol filogenético.

---

## DESAFÍO III: Anotación de blancos moleculares

Consulta en bases de datos ChEMBL y DrugBank para identificar fármacos que se unan a la albúmina humana (HSA). Complementado con la publicación *"Albumin is a reliable drug-delivering molecule: Highlighting points in cancer therapy"*.

### a. ¿Qué tipo de moléculas suelen interactuar con la HSA?

La HSA tiene una notable afinidad por moléculas **hidrofóbicas y lipofílicas**. Entre los compuestos endógenos, transporta ácidos grasos de cadena larga, bilirrubina y hormonas esteroideas. En cuanto a fármacos (exógenos), interactúa principalmente con compuestos orgánicos de carácter ácido o neutro y con un alto grado de insolubilidad en agua (como el ibuprofeno, la warfarina, el diazepam y el paclitaxel).

Según la publicación mencionada, estas propiedades convierten a la albúmina en un excelente sistema natural de *drug delivery*. Su elevada biocompatibilidad, larga vida media plasmática y capacidad de acumularse en tejidos tumorales permiten mejorar el transporte y la biodisponibilidad de agentes anticancerígenos.

### b. ¿Qué importancia biomédica tiene esta interacción?

**Farmacocinética:** Al unirse a la albúmina, el fármaco se solubiliza y viaja protegido por el torrente sanguíneo. Solo la fracción libre (no unida a la proteína) es terapéuticamente activa; por ende, la albúmina determina la vida media, distribución y depuración de los medicamentos en el organismo.

**Terapia contra el cáncer:** Las células tumorales consumen grandes cantidades de albúmina para nutrir su rápido crecimiento. Esto se aprovecha biomédicamente para diseñar nanopartículas de albúmina cargadas con quimioterapéuticos, logrando que el tratamiento se dirija selectivamente al tumor (efecto EPR).

### c. ¿Qué diferencias se reportan entre la unión de fármacos en la albúmina humana y la bovina?

Aunque comparten una alta identidad de secuencia, la albúmina bovina presenta variaciones estructurales puntuales en los sitios de unión (Sitios de Sudlow I y II). Por ejemplo:

- La **BSA** posee **dos residuos de triptófano** (Trp134 y Trp214)
- La **HSA** solo tiene **uno** (Trp214)

Esto altera la flexibilidad del bolsillo molecular y provoca que ciertos fármacos tengan afinidades notablemente distintas o incluso cambien su estereoselectividad al unirse a una u otra proteína.

### d. ¿Cuáles son las principales diferencias entre especies en dichas regiones de interés?

Mientras que en primates los bolsillos de unión están conservados casi al 100%, al comparar humanos con roedores u otros mamíferos la identidad en estas regiones específicas cae. Pequeñas sustituciones de aminoácidos cambian el volumen, la carga electrostática o la hidrofobicidad del bolsillo, lo que explica por qué un fármaco que funciona eficazmente en los ensayos preclínicos con ratones a veces se comporta de forma muy distinta en humanos.

### 2. Identificar características comunes

#### a. ¿Qué motivo estructural ("andamiaje" o scaffold común) comparten?

```python
moleculas = {
    'CMP-1': 'CC1=CC=CC=C1O',
    'CMP-2': 'CCOc1ccc2nc(SCc3ccccc3)sc2c1',
}
resultados = analisis_completo(moleculas)
print(resultados['scaffolds'])
```

Ambas moléculas comparten un **anillo aromático bencénico** como andamiaje central. Este tipo de estructura es clave para encajar en los sitios de unión de la albúmina mediante interacciones de apilamiento hidrofóbico (pi-pi y fuerzas de Van der Waals).

#### b. ¿Qué sustituyentes (grupos químicos) están presentes en diferentes posiciones?

- **CMP-1:** posee sustituyentes simples: un grupo metilo (-CH₃) y un grupo hidroxilo (-OH) unido al anillo.
- **CMP-2:** es mucho más voluminoso; presenta un sistema bicíclico de benzotiazol, un grupo etoxi (-OCH₂CH₃) y una cadena con un puente tioéter (-S-) conectada a otro grupo bencilo.

#### c. ¿Qué diferencias y similitudes estructurales hay entre estos compuestos? ¿Cómo crees que deben ser las distintas proteínas en los sitios capaces de transportarlos?

Ambos compuestos son marcadamente lipofílicos, pero difieren en tamaño y complejidad espacial. Para poder albergar y transportar compuestos tan diversos, las cavidades de la albúmina deben ser **anfipáticas y flexibles**: el interior del bolsillo debe estar revestido de aminoácidos hidrofóbicos (como fenilalanina, leucina o valina) para estabilizar los anillos aromáticos, combinados con residuos cargados (como las lisinas y argininas conservadas) dispuestos estratégicamente en la entrada del bolsillo para actuar como "anclas" electrostáticas de los grupos polares.

---

## DESAFÍO IV: Identificación de sitios de interés

Utilizando las bases de datos UniProt e InterPro para identificar dominios y motivos conservados en la HSA.

### a. ¿Cuáles son los dominios principales identificados?

Se identifican claramente los **tres dominios globulares homólogos (I, II y III)**, subdivididos cada uno en los subdominios A y B.

### b. ¿Coinciden con los sitios conocidos de unión a ligandos descriptos en la introducción?

Sí, coinciden a la perfección:
- El **Sitio I de Sudlow** se localiza en el subdominio IIA (donde se encuentran las lisinas Lys195 y Lys199 críticas para la función).
- El **Sitio II de Sudlow** se ubica en el subdominio IIIA (asociado a la actividad de Arg410 y Tyr411).

### c. ¿Qué residuos resultan altamente conservados en ortólogos y podrían ser críticos para la función?

Los residuos más conservados entre los ortólogos de albúmina son:

- **Lys199, Arg410, Tyr411, Cys34 y Lys195**

Estos aminoácidos aparecen conservados en muchas especies de mamíferos dentro del alineamiento múltiple, lo que sugiere una fuerte presión evolutiva para mantener su función. Cys34 es el único residuo con un grupo tiol (-SH) libre, fundamental para el estado redox de la proteína y la unión covalente de fármacos.

### d. ¿Cómo se distribuyen los dominios principales a lo largo del árbol?

La arquitectura de los tres dominios se encuentra **universalmente distribuida** en todos los clados del árbol filogenético. Al equiparar el árbol con el alineamiento, se observa que la evolución no ha eliminado ni añadido dominios enteros en los mamíferos, sino que ha operado mediante **mutaciones puntuales en regiones expuestas al solvente o bucles externos**, resguardando el núcleo de los dominios funcionales.

### e. ¿Existen evidencias de interferencias farmacológicas o promiscuidad proteica de impacto farmacológico para la HSA?

La HSA es una proteína sumamente **promiscua** porque un mismo bolsillo (especialmente el Sitio I) puede alojar a decenas de fármacos estructuralmente distintos. Esto genera un alto riesgo de **interferencia farmacológica por competencia** en tratamientos polimedicados: si a un paciente se le administran simultáneamente dos fármacos que compiten por el mismo sitio (por ejemplo, warfarina e ibuprofeno), uno desplazará al otro, elevando drásticamente la concentración de fármaco libre en plasma y pudiendo causar efectos tóxicos o sobredosis.

> **Nota:** Los estudios del Grupo de Bioinformática Estructural de la UNQ refuerzan que esta promiscuidad es una propiedad evolutiva de la albúmina para lidiar con desechos metabólicos hidrofóbicos, pero se convierte en un desafío crítico en la farmacología moderna.

---

## 💡 Para investigar: Investigación de la UNQ

Investigación realizada en la Universidad Nacional de Quilmes (UNQ) por el Grupo de Bioinformática Estructural sobre la evolución de albúminas.

> **Promiscuidad:** capacidad de una proteína para catalizar reacciones diferentes de aquellas para las cuales evolucionó originalmente.

Las albúminas presentan conservación en su secuencia a lo largo de los vertebrados, a pesar de poseer gran diversidad estructural entre miembros de la familia. La HSA posee varios sitios de unión de alta afinidad; sin embargo, la mayoría de los fármacos y ligandos se unen a los denominados **Sitio I** (desde Met1 hasta Asn111) y **Sitio II** (desde Gln196 hasta Pro303).

### ¿Qué se plantea en la investigación?

Se plantea que las actividades promiscuas observadas en HSA, particularmente relacionadas a reacciones catalíticas, podrían no ser simples accidentes estructurales, sino el resultado de **adaptaciones evolutivas**. Se analizaron patrones evolutivos y estructurales de cinco tipos de albúmina: HSA, BSA, RabSA, PSA y RSA.

Para evaluar esta hipótesis, se utilizó la reacción de **condensación aldólica cruzada** entre acetona y p-formilbenzonitrilo.

### ¿Qué se encontró?

- Las posiciones asociadas al comportamiento promiscuo evolucionan bajo **presión de selección positiva** y se localizan en cavidades y túneles conservados.
- Las albúminas de mamífero analizadas son capaces de catalizar una reacción de condensación aldólica cruzada, demostrando que la actividad promiscua se encuentra **conservada evolutivamente**.
- Se identificaron residuos importantes para esta actividad: **Lys199, Arg218 y Arg222**, localizados en cavidades conservadas.
- Se observaron **corrimientos de pKa** en residuos clave, indicando adaptaciones fisicoquímicas específicas para sostener la actividad catalítica.
- Se identificaron **túneles conservados** que conectan cavidades internas con la superficie proteica.

### Relación con nuestro TP

En nuestro análisis bioinformático observamos que las albúminas presentan una elevada conservación evolutiva entre mamíferos, con un porcentaje de identidad promedio alto y clados filogenéticos coherentes con la clasificación taxonómica. El árbol filogenético construido mediante IQ-TREE mostró agrupamientos esperados de primates, roedores y otros mamíferos, mientras que el alineamiento múltiple permitió identificar regiones altamente conservadas, especialmente en zonas relacionadas con la unión de ligandos y cavidades funcionales. Esto coincide con los hallazgos del paper, donde se describe que las cavidades, túneles y residuos funcionales se mantienen conservados durante la evolución.

Tanto el paper como nuestro análisis sugieren que la conservación de las albúminas no responde únicamente a su función clásica de transporte, sino también a **propiedades estructurales y catalíticas promiscuas** que podrían tener relevancia fisiológica.
