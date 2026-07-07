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
    - Universidad (e.g. "Universitat de Barcelona", o un identificador de esa universidad)
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

También tienen metadatos:
    - Título (e.g. "Tema 1. Las fuentes del Derecho")
    - Tipo (e.g. "tema")
    - Asignatura (e.g. "20405")
    - Última revisión (e.g. "7/7/2026")
    - Autores (e.g. "Marta Rodríguez")


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
                subject.yml
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

## Invariantes del sistema

Los siguientes principios constituyen reglas fundamentales de la arquitectura de Studium y deberán respetarse en cualquier evolución futura del proyecto.

1. Toda Universidad contiene un catálogo de Cursos y un catálogo de Asignaturas.

2. Todo Curso pertenece exactamente a una Universidad.

3. Toda Asignatura pertenece exactamente a una Universidad.

4. Un Curso nunca contiene el contenido de una Asignatura; únicamente referencia Asignaturas existentes.

5. Una misma Asignatura puede ser referenciada por varios Cursos de una misma Universidad.

6. Toda Asignatura constituye una unidad autónoma de conocimiento y contiene exclusivamente sus propios Documentos.

7. Todo Documento pertenece exactamente a una Asignatura.

8. Los Documentos pueden clasificarse en distintos tipos (Temas, Ejercicios, Casos prácticos, Exámenes, Bibliografía, Material complementario, etc.), sin que dicha clasificación limite la organización interna de la Asignatura.

9. Studium no impone una estructura interna rígida para las Asignaturas; únicamente establece una gramática editorial común para favorecer la uniformidad.

10. Los Cursos organizan el recorrido académico. Las Asignaturas organizan el conocimiento.

11. Ningún contenido académico deberá duplicarse innecesariamente dentro de una misma Universidad cuando pueda ser referenciado.