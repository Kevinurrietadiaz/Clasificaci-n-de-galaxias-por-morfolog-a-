# Clasificaci-n-de-galaxias-por-morfolog-a-
Clasificacion de galaxias usando CNN y el dataset Galaxy Zoo
Clasificar la forma de las galaxias es fundamental para entender cómo evolucionan las estructuras cósmicas. Tradicionalmente, este trabajo ha dependido de miles de voluntarios en proyectos como Galaxy Zoo. Mi objetivo en este proyecto fue automatizar ese proceso utilizando Inteligencia Artificial, entrenando un modelo capaz de distinguir entre las formas fundamentales del universo: elípticas, espirales y lenticulares.
En el dataset utilice una selección de imágenes del Galaxy Zoo, proporcionado originalmente a través de Kaggle. Este dataset es particularmente retador porque no son fotos perfectas de telescopios de alta gama; son imágenes con ruido, rotaciones y diferentes niveles de brillo, lo que obliga al modelo a aprender características morfológicas reales en lugar de simplemente memorizar píxeles.

Para este clasificador, no empece desde cero. Implementamos Transfer Learning utilizando la arquitectura MobileNetV2 como base.

¿Por qué MobileNetV2? Necesitábamos un modelo que fuera eficiente pero potente. Al estar pre-entrenado en millones de imágenes (ImageNet), el modelo ya "sabe" detectar bordes, texturas y formas básicas.

Ajuste Personalizado: Añadi capas de GlobalAveragePooling y una capa densa con Dropout del 40% para evitar que la IA se volviera "perezosa" y memorizara el ruido (Overfitting).
Tambien se implementa un sistema de ReduceLROnPlateau, que reducía la velocidad de aprendizaje cuando el modelo dejaba de mejorar, permitiéndole afinar sus predicciones en las etapas finales.

El entrenamiento duró 15 épocas. A mitad del proceso, el modelo pudo reducir la tasa de aprendizaje, logrando estabilizar su error en niveles mínimos.
se logro alcanzar un ~75.9%, un resultado muy sólido considerando la enorme ambigüedad visual que existe entre algunas galaxias.

Al analizar la Matriz de Confusión, se nota algo que incluso a los astrónomos les sucede, la IA es experta identificando galaxias elípticas (lisas), pero a veces confunde las espirales lejanas con objetos circulares.

Este sesgo no es necesariamente un fallo del código, sino un reflejo de la realidad astronómica. Muchas galaxias espirales, cuando están muy lejos o tienen poca resolución, pierden la visibilidad de sus brazos y se ven visualmente idénticas a una elíptica.

Aunque todavía hay espacio para mejorar la distinción de estructuras finas (quizás con mayor resolución o balanceo de datos), el modelo actual ya es capaz de procesar miles de galaxias en segundos con una fiabilidad comparable a la clasificación humana inicial.
