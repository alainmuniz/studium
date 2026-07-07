# Arquitectura del proyecto

## Entidades del Sistema

1. Universidad:

Universidad es la institución que agrupa *Cursos* y *Asignaturas*. O sea, la arquitectura es:

Universidad X/
    Cursos/
        Grado en A/
        Grado en B/
        Grado en C/
    Asignaturas/
        Asignatura 1/
        Asignatura 2/
        Asignatura 3/

Sus metadatos son:
    - Nombre (e.g. "Universitat de Barcelona")
    - Abreviatura (e.g. "UB")
    - Descripción o información institucional (e.g. "La Universidad de Barcelona es una institución...)
    - País (e.g. "España")
    - Foto (a considerar)


2. Cursos

Un curso es una estructura curricular que organiza asignaturas dentro de sí mismo. O sea, referencia asignaturas existentes del catálogo de la Universidad.

Sus metadatos son:
    - Código
    - Nombre
    - Universidad
    - Referencias a asignaturas
    - Años o secciones

No contiene documentos, sino referencias a los mismos, una estructura posible es:

Código: GDRE
Nombre: Grado en Derecho
Años: 4

##### Primer curso
    20405
    20406
    20407

##### Segundo curso
    20408
    20409
    20410

3. Asignaturas:

Asignatura es la entidad central del sistema. Es una unidad autónoma, que encierra dentro de sí el conocimiento a través de una serie de documentos en Markdown. Tiene total autonomía interna para organizarse, aunque se recomendará una gramática interna común para mayor uniformidad.

Sus metadatos son:
    - Código (e.g. "20405")
    - Nombre (e.g. "Derecho Internacional Público")
    - Universidad (e.g. "Universitat de Barcelona")
    - Autores (e.g. "Juan Pérez, Carlos González, Jorge Ramírez")
    - Revisores (e.g. "María Gutiérrez, José Morales")
    - Fecha de última revisión (e.g. "27/07/2025")

Pueden contener:
    - Temas
    - Ejercicios
    - Casos prácticos
    - Exámenes de años anteriores
    - Material complementario
    - Etcétera

En esos casos, cada uno de los tipos de materiales estará agrupado en desplegables, o sea:

Temas/
    Tema 1
    Tema 2
    Tema 3
Ejercicios/
    Ejercicios del tema 1
    Ejercicios del tema 2
    Ejercicios del tema 3


4. Documentos:

Es la unidad básica de información. Es, literalmente, un documento de markdown. Cada *Asignatura* está compuesta por una serie de documentos, que pueden ser del mismo o distinto tipo. Esos tipos pueden constituir grupos coherentes de documentos. Por ejemplo, podemos tener varios temas (véase ejemplo arriba).


## Estructura y relaciones

La estructura del proyecto queda de la siguiente manera:

universidades/
    universidad-1/
        index.md
        cursos/
            grado 1
            grado 2
            grado 3
        asignaturas/
            asignatura-1/
                index.md
                metadata.yml
                temas/
                    tema 1
                    tema 2
                    tema 3
                ejercicios/
                    ejercicios tema 1
                    ejercicios tema 2
                bibliografia.md

Por tanto, la relación entre los componentes es la siguiente:
- La Universidad agrupa cursos
- Cada curso tiene una serie de referencias a Asignaturas (varios cursos pueden comprender la misma Asignatura, o sea, referenciar el mismo objeto)
- Las Asignaturas contienen Documentos