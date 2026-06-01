# TP: Docking Molecular

---

## Modelos físicos de unión

En el docking rígido se considera tanto el ligando como la diana como componentes rígidos, reduciendo el problema a rotaciones y traslaciones. Pero esta afirmación es demasiado simplista, ya que ambas entidades son de naturaleza flexible.

Como se vio previamente en clase, hay tres modelos físicos de unión que evolucionaron históricamente:

- **Modelo llave-cerradura** (Emil Fischer, finales del siglo XIX): El receptor se considera una cerradura que contiene una región con sitios activos y diferentes tipos de bolsillo, mientras que el ligando, como una llave, puede unirse a los receptores. Solo una llave correcta encaja en su cerradura; es una aproximación muy rígida.
- **Teoría del ajuste inducido** (Daniel Koshland, 1958): Se plantea que la unión del ligando induce un cambio conformacional en la proteína; la proteína se "moldea" alrededor del ligando. Esto implica sitios más flexibles; la afinidad puede depender de cambios estructurales posteriores al contacto inicial. La proteína ya no es un objeto estático: cambia su forma en respuesta al ligando.
- **Teoría de selección conformacional:** La proteína existe en un equilibrio de conformaciones; el ligando selecciona y estabiliza una de ellas. El ligando es quien selecciona, entre un conjunto de conformaciones accesibles, la más apropiada para su unión.

---

## Docking de diana rígida y ligando flexible

Asumiendo que la aproximación de llave-cerradura es aceptable como modelo de unión ligando-diana, la flexibilidad de la proteína se puede omitir. De esta manera la búsqueda conformacional del ligando se convierte en la parte más importante del problema a resolver.

En muchos casos la exploración sistemática no es siempre posible, debido al efecto de la **explosión combinatoria** que supone la enumeración de todas las posibles rotaciones de cada ángulo de torsional en el ligando. Por ello es necesario recurrir a otras aproximaciones. Los métodos o algoritmos se pueden clasificar en tres categorías principales:

- **Construcción incremental:** Implica el análisis conformacional *on the fly* dentro de las limitaciones del sitio de unión, por división del ligando en fragmentos y su posterior unión de manera secuencial. Programas: FlexX, Surflex.
- **Conformaciones del ligando pre-calculadas:** Las conformaciones del ligando son generadas antes de la operación de docking y guardadas en una base de datos para su uso posterior. Programas: CRDOCK, GLIDE.
- **Generación in situ:** La totalidad del ligando se adapta de forma continua al sitio activo de la diana. Las técnicas más empleadas son:
  - *Complementariedad de forma*: evaluación de la concordancia entre el ligando y el sitio activo en términos geométricos (DOCK).
  - *Algoritmos genéticos*: basados en la teoría de la evolución de Darwin o en la teoría de la herencia de Lamarck (GOLD, AutoDock).
  - *Algoritmo de Monte Carlo*: generación aleatoria de grupos de rotación, traslación y orientación de los ligandos, evaluados con una función de scoring (LigandFit).
  - *Búsqueda tabú*: generación de poses de forma aleatoria llevando una lista de sitios o conformaciones ya probadas (PRO LEADS).
  - *Algoritmos bio-inspirados*: basados en la inteligencia de enjambres o en las estrategias de las colonias de hormigas (PLANTS).

---

## Docking flexible

Con respecto a la diana, y siempre que se incluya la flexibilidad del ligando, los métodos se clasifican en función del grado de flexibilidad que ésta incorpore. En el docking flexible siempre se incluye la flexibilidad del ligando y, sobre esa base, se agregan distintos niveles de flexibilidad de la diana.

Las estrategias para el estudio del docking flexible incluyen:

### Soft docking

Consiste en relajar los potenciales de interacción, lo que trae como consecuencia una expansión en las dimensiones del centro activo. En términos prácticos, el sitio de unión de la proteína se hace artificialmente más grande y tolerante, simulando así el efecto del acoplamiento inducido: la proteína "cede" para acomodar al ligando sin modelar explícitamente cómo cambia átomo por átomo.

> No se modela realmente cómo se mueve la proteína; es una simplificación útil pero no una representación real de la flexibilidad.

### Algoritmo de Monte Carlo

Se utiliza una colección de rotámeros para probar los cambios en las cadenas laterales de la diana durante el docking. Las cadenas laterales de los aminoácidos no están fijas; pueden adoptar diferentes conformaciones (un **rotámero** es cada una de estas orientaciones posibles). El algoritmo de Monte Carlo prueba los rotámeros de forma aleatoria, evaluando cuál combinación de cadenas laterales genera mejores interacciones con el ligando. Es una representación más realista de la flexibilidad local de la proteína (aunque no se mueve el esqueleto proteico completo).

### Esquema del complejo relajado

Se puede usar si se dispone de varias estructuras de la misma diana; consiste en realizar diferentes experimentos de docking de forma individual sobre cada estructura disponible y luego hacer un promedio de los resultados. Tener un conjunto de estructuras que representen la variedad conformacional permite al método de docking encontrar cuál de esas conformaciones es la más favorable para cada ligando.

Este proceso también se puede emplear con estructuras generadas por simulaciones de dinámica molecular o análisis de modos normales.

### Simulaciones de dinámica molecular y análisis de modos normales

También se emplean para tener en cuenta la flexibilidad total de la diana, mientras que al mismo tiempo se hace el docking del ligando.

---

## Re-scoring

Durante el docking flexible se generan una gran cantidad de poses posibles, las cuales deben ser evaluadas y ordenadas por la función de scoring. Sin embargo, dado que esta evaluación debe realizarse sobre miles de configuraciones en un tiempo razonable, la función de scoring **sacrifica precisión en favor de la velocidad de cálculo**. Como consecuencia, la clasificación resultante no garantiza que la pose ubicada en el primer puesto corresponda realmente a la estructura experimental correcta.

Para abordar esta limitación, se incorpora una etapa posterior denominada **re-scoring**, en la cual se aplican funciones de puntuación más precisas y computacionalmente más costosas sobre el conjunto reducido de poses candidatas que sobrevivieron a la evaluación inicial. Al trabajar sobre un número menor de soluciones, es posible utilizar descripciones más detalladas del proceso de unión sin que el costo computacional resulte prohibitivo.

Algunos métodos usan una aproximación basada en factores de ponderación, de manera que la puntuación original es escalada por un factor que depende de aspectos geométricos o propiedades *drug-like*. El scoring inicial actúa como un filtro rápido pero aproximado, mientras que el re-scoring permite una selección más rigurosa y confiable entre las poses finalistas.

---

## Docking proteína–proteína

El punto de partida para estudiar el modo de unión entre dos proteínas mediante docking es conocer las estructuras tridimensionales de ambas. Los algoritmos empleados tienen como objetivo generar una lista ordenada de todas las poses posibles, entre las cuales debe haber al menos una lo más parecida posible a la estructura nativa del complejo. Para lograr esa ordenación se recurre a una función de puntuación (**scoring**) que produce un *ranking* de las soluciones.

Sin embargo, el docking proteína-proteína es un problema de **mayor complejidad** que el docking proteína-ligando, porque el número de grados de libertad es mucho mayor. Intentar reproducir en detalle las interacciones de cada pose usando métodos como dinámica molecular puede volverse computacionalmente inabordable. Aun así, si se conocen las zonas de unión en la superficie de las proteínas, el número de posibilidades se reduce drásticamente, aumentando las probabilidades de éxito.

A esta complejidad se suma un factor crítico: **las proteínas no son estáticas**. La estructura de una proteína antes y después de unirse a otra puede ser significativamente diferente, lo que implica que para predecir la unión de forma precisa es necesario tener en cuenta la flexibilidad de las estructuras.

### Docking flexible en interacciones proteína–proteína

Si las proteínas que forman el complejo experimentan cambios conformacionales apreciables, es muy difícil obtener una solución cercana a la nativa usando docking rígido, incluso aplicando un refinado posterior. Predecir esos cambios conformacionales es costoso computacionalmente y complejo desde el punto de vista físico; hasta el momento no se ha conseguido desarrollar una estrategia directa en la que se pueda confiar de forma general.

Cuando dos proteínas se unen, ambas pueden cambiar de forma. Si se realiza docking tomando la estructura de la proteína tal como está sola, puede que esa conformación nunca genere una solución correcta, porque en la realidad la proteína tendría una forma diferente al momento de unirse.

**Situación 1:** Aplica cuando el cambio conformacional es grande solo en una de las proteínas implicadas. Se reproducen sus conformaciones mediante técnicas de dinámica molecular, modos normales o RMN, generando un conjunto de estructuras iniciales (antes de hacer docking se generan muchas conformaciones posibles de la proteína con otras técnicas). Si la estructura nativa está dentro del conjunto de estructuras pre-generadas, se puede pasar a una aproximación de docking rígido sobre cada estructura del conjunto. Hay que tener en cuenta que se puede producir un número significativo de **falsos positivos**, ya que pueden aparecer poses con buena puntuación por buen ajuste de superficies pero que no corresponden a la estructura nativa real.

**Situación 2:** Se conoce el sitio de unión entre ambas proteínas o algunas interacciones que se establecen cuando se forma el complejo. Se pueden reducir el número de poses posible de forma significativa. Es más factible el uso simultáneo de docking y dinámica molecular, donde es posible incluir la flexibilidad de toda la proteína o de una cierta región durante el docking; es un método parecido al escenario real en el que se produce la formación de complejos entre proteínas.

---

## Evaluación de la validez de los resultados

Para probar la precisión de un nuevo programa de docking y su función de scoring se puede realizar una evaluación **estructural** y otra **energética**.

### Evaluación estructural

Se necesita contar con un conjunto de complejos con estructura 3D conocida y una medida que permita cuantificar el parecido entre los resultados de docking y las estructuras experimentales. En base a esto, se utiliza la **desviación cuadrática media (RMSD)**:

$$RMSD = \sqrt{\frac{\sum_{i=1}^{n}(x_{1,i} - x_{2,i})^2}{n}}$$

Donde:
- $x_{1,i}$ = coordenada del átomo *i* en la estructura experimental
- $x_{2,i}$ = coordenada del átomo *i* en la estructura predicha
- $n$ = número total de átomos

El procedimiento consiste en extraer los ligandos de un conjunto de complejos ligando-diana y hacer docking de cada uno de ellos en su propia diana. El RMSD se calcula para cada pose posible usando como referencia la estructura experimental.

- **Valor de corte:** 1,0 Å (aunque algunos autores consideran 1,5 Å o hasta 2 Å).
- Por debajo de este valor: resultado **aceptable**.
- Por encima: resultado **incorrecto**.
- **Porcentaje de acierto o éxito:** porcentaje de estructuras predichas con RMSD < 2,0 Å; suele rondar el **70–75%**.

### Evaluación energética

Se necesitan datos de afinidad o actividad experimental del ligando por la diana. De esta manera se puede evaluar la manera en que las funciones de scoring reproducen estos valores.

**Principales limitaciones:**

Aunque los algoritmos de docking suelen encontrar correctamente la posición (pose) del ligando dentro de la proteína, las funciones de scoring todavía presentan dificultades para predecir con precisión la afinidad real de unión. Presentan dos limitaciones importantes:

1. No siempre asignan la mejor puntuación a la pose más cercana a la estructura experimental (RMSD bajo).
2. Las energías calculadas suelen correlacionarse pobremente con las afinidades medidas experimentalmente.

Esto se debe a que simplifican fenómenos complejos como la entropía, los efectos del solvente y la flexibilidad proteica, además de que la función de scoring prioriza sacrificar precisión en favor de la velocidad de cálculo. Por ello, la predicción cuantitativa de afinidad sigue siendo uno de los principales desafíos del docking, aunque se esperan mejoras gracias al aumento de la capacidad computacional y al desarrollo de modelos más avanzados.

---

## Modelos computacionales y softwares

### Glide

Software **comercial** de docking proteína-ligando (Schrödinger), utilizado en diseño racional de fármacos y *virtual screening* debido a su alta precisión en la predicción de poses de unión y su capacidad de manejar distintos niveles de flexibilidad molecular.

Características principales:

- Utiliza una **estrategia jerárquica** de búsqueda y filtrado para generar y evaluar poses del ligando.
- Permite probar ligando flexible mediante exploración de conformaciones y rotaciones torsionales.
- Implementa estrategias de **soft docking**, relajando parcialmente las restricciones estéricas para simular el ajuste inducido.
- Incluye distintos niveles de precisión:
  - **HTVS** (*High Throughput Virtual Screening*): muy rápido para grandes bibliotecas.
  - **SP** (*Standard Precision*): equilibrio entre velocidad y precisión.
  - **XP** (*Extra Precision*): mayor exactitud, pero mayor costo computacional.
- Puede realizar **Induced Fit Docking (IFD)**, permitiendo cierta flexibilidad del receptor mediante reorganización de cadenas laterales cercanas al ligando.
- Posee funciones de scoring avanzadas para clasificar las poses según su afinidad de unión estimada.

### GOLD

GOLD (*Genetic Optimisation for Ligand Docking*) es un software de docking proteína-ligando desarrollado por el **Cambridge Crystallographic Data Centre (CCDC)**. Su principal característica es que utiliza **algoritmos genéticos (GA)** para explorar distintas orientaciones y conformaciones del ligando dentro del sitio activo de una proteína.

Los algoritmos genéticos están inspirados en la evolución biológica: generan múltiples soluciones posibles (poses), las evalúan mediante funciones de scoring y seleccionan las mejores para producir nuevas generaciones hasta encontrar configuraciones energéticamente favorables.

Características principales:

- Permite ligandos completamente flexibles durante el docking.
- Emplea cuatro funciones de scoring: **GoldScore, ChemScore, ASP, ChemPLP**.
- Incorpora flexibilidad parcial de la proteína, especialmente en cadenas laterales del sitio activo.
- Contiene varias restricciones definidas por el usuario (enlaces de hidrógeno, región hidrofóbica, estructura y similitud).
- Puede realizar *ensemble docking*, usando múltiples conformaciones de la proteína.
- Permite considerar moléculas de agua, metales y docking covalente en algunos protocolos.
- Todas las funcionalidades están disponibles a través de la **API de Python**.

### AutoDock

AutoDock es uno de los programas de docking molecular más utilizados en investigación académica. Es **gratuito y de código abierto**, desarrollado por el laboratorio de Arthur J. Olson en The Scripps Research Institute.

Características principales:

- Permite ligandos flexibles, explorando rotaciones de enlaces y diferentes conformaciones.
- Puede incorporar cierta flexibilidad del receptor, generalmente en cadenas laterales seleccionadas del sitio activo.
- Utiliza el **Algoritmo Genético Lamarckiano (LGA)**, que combina algoritmos genéticos con optimización local para mejorar la búsqueda conformacional.
- Emplea **mapas de energía precalculados (*grid maps*)**, lo que acelera significativamente los cálculos.
- Incluye una función de scoring semiempírica basada en contribuciones de: Van der Waals, interacciones electrostáticas, puentes de hidrógeno, desolvatación y entropía torsional.
- Permite realizar estudios de *virtual screening* sobre grandes bibliotecas de compuestos.
- Cuenta con una gran comunidad de usuarios y abundante documentación científica.

### FlexX

FlexX es uno de los programas históricos más utilizados, especialmente famoso por su **velocidad**. Está diseñado principalmente para el *virtual screening* de grandes bibliotecas de compuestos.

**Algoritmo: Construcción Incremental**

1. **Fragmentación:** FlexX toma el ligando y lo "corta" de forma lógica a través de sus enlaces rotables, dividiéndolo en varios fragmentos.
2. **Selección del fragmento base:** Elige el fragmento más rígido y con más átomos pesados (el *fragmento base*).
3. **Colocación (*Placement*):** Coloca ese fragmento base en el sitio activo de la proteína buscando interacciones favorables (puentes de hidrógeno, interacciones hidrofóbicas).
4. **Crecimiento:** Va añadiendo el resto de los fragmentos uno a uno, rotando los enlaces según una biblioteca de conformaciones preferidas, hasta reconstruir el ligando completo dentro del sitio activo.

- **Flexibilidad:** El ligando es flexible (gracias a la fragmentación y rotación), pero la proteína se considera rígida (aunque versiones modernas permiten definir flexibilidad en cadenas laterales específicas).
- **Función de puntuación (Scoring):** Utiliza una **función empírica modificada de Böhm**, que calcula la energía libre de unión (ΔG) sumando de forma aditiva las contribuciones de los puentes de hidrógeno, interacciones iónicas, interacciones aromáticas y la penalización por la pérdida de entropía conformacional del ligando.
- **Ventaja principal:** Es extremadamente rápido; ideal para filtrar millones de moléculas en poco tiempo.
- **Desventaja:** Al rigidizar la proteína, puede perder precisión si el receptor sufre cambios conformacionales importantes al unirse al fármaco.

### ICM

ICM es un software conocido por su **precisión**. Trabaja con **coordenadas internas** (ángulos de torsión, longitudes de enlace y ángulos de enlace).

**Algoritmo: Monte Carlo con Minimización (BPMC)**

- En lugar de mover cada átomo de forma independiente, ICM mantiene fijos los enlaces químicos y longitudes estándar, y solo rota los ángulos de torsión. Esto reduce drásticamente las variables que la computadora debe calcular.
- Utiliza un **Algoritmo de Monte Carlo con Probabilidad Sesgada (BPMC)**. El programa realiza cambios aleatorios en los ángulos de torsión del ligando, minimiza la energía localmente y decide si acepta o rechaza la nueva pose basándose en criterios energéticos.

- **Flexibilidad:** Es muy bueno manejando la flexibilidad total del ligando y, además, permite introducir flexibilidad en el receptor de forma mucho más natural (mediante mapas de potencial continuos o docking multi-conformacional/4D).
- **Función de puntuación (Scoring):** Utiliza una **función de base física muy robusta** que incluye términos de Van der Waals, electrostática (ecuación de Poisson-Boltzmann), enlaces de hidrógeno, energía de solvatación hidrofóbica y entropía conformacional.
- **Ventaja principal:** Es de los programas más precisos del mercado para predecir la pose real de unión, debido a su riguroso muestreo energético.
- **Desventaja:** Requiere un costo computacional mucho mayor (es más lento) que FlexX.
