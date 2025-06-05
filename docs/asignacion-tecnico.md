# Matriculación en talleres (detalles técnicos)

## Detalles técnicos de cómo funciona el proceso

La asignación se realiza por sorteo aleatorio que ordena la lista de socios. Se harán luego 4 rondas de asignación y finalmente, los resultados confirmados se podrán consultar y modificar en la aplicación de Playoff. Con todo esto, evitamos los problemas que nos ha dado en otros años el alto número de matriculaciones simultáneas.

De cara a evitar este problema, se propuso y se presentó ya en Familias en Acción la siguiente aproximación a la resolución del problema::

1. Los socios harían una lista priorizada de talleres a los que quieren asistir, una lista con tantos elementos como quisieran.
2. Algunas actividades no estarán disponibles si el socio no cumple, por ejemplo, con los requisitos de edad.
3. Se utilizaría el número agraciado en la ONCE o cualquier otro sorteo oficial como semilla del generador aleatorios del equipo donde se realizaría la asignación. Se utiliza una semilla o `seed` porque los ordenadores en realidad no saben hacer números aleatorios reales y usan algoritmos pseudoaleatorios para generarlos, por lo que si se usa el mismo número de semilla, el resultado es el mismo. En este caso, se usaría el número agraciado en la ONCE o cualquier otro sorteo oficial como semilla del generador aleatorio del equipo donde se realizaría la asignación.
4. Un [programa](https://github.com/asociacion-avast/inscripciones-assign/blob/main/asignar.py), ordenaría (método Durstenfeld) la lista de socios de forma aleatoria usando ese número de semilla y una vez realizada esa ordenación, comenzaría a coger la lista priorizada de cada socio e iría asignando por orden talleres de forma que:
   1. Se coge la lista de socios y se validan de forma que:
      1. El socio está en estado de ALTA y VALIDADO en PlayOff
      2. Que el socio está dado de alta en la modalidad con actividades
      3. Que el socio ha rellenado una lista de preferencias para talleres
   2. Se ordena la lista de socios como se ha explicado en el paso anterior
5. Cada día y por cada socio de la lista se realiza este proceso:
   1. Se procesa la lista de preferencias del socio, se cogen las opciones y se comprueba que:
      1. El taller tiene plazas libres
      2. Que el rango de edad corresponde con la edad del socio
      3. El socio no tiene conflictos de horario con otros talleres ya inscritos
      4. Que el socio no tiene ya inscrito un taller similar
      5. Si todo el paso anterior es correcto, se procede a asignar ese taller al socio, en caso contrario, se repite con la siguiente opción de su lista de preferencias hasta que o bien se inscribe en un taller o bien, no hay talleres compatibles.
   2. Se pasa al siguiente socio y se repite el proceso hasta procesar la lista completa.
   3. Al final de la ejecución, donde generalmente, cada socio ha recibido un taller de su lista, se acaba el proceso.

## Advertencias

- El código del proceso de asignación está indicado en el enlace anterior, cualquiera puede revisarlo para auditarlo
- El proceso de asignación es completamente aleatorio, no se tiene en cuenta el número de socio, ni la antigüedad, ni nada que no sea la lista de preferencias, el número de plazas libres, año de nacimiento y que no haya inscripciones en talleres similares.
