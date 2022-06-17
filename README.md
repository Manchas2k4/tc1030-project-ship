![Tec de Monterrey](images/logotecmty.png)
# Situación problema: Simulación de un sistema de un sistema de gestión portuaria

## <span style="color: rgb(26, 99, 169);">¿Qué tengo que hacer?</span>
En este repositorio encontrarás una serie de carpetas y archivos que necesitarás para el desarrollo del proyecto.
* *test_cases*: En este directorio encontrarás los archivos de entrada (*input0.txt*, *input1.txt*, *input2.txt*, *input3.txt*, *input4.txt*) que utilizaremos para probar el sistema completo. Adicionalmente están las salida esperadas para cada uno de los archivos de entrada (*output0.txt*, *output1.txt*, *output2.txt*, *output3.txt*, *output4.txt*).
* *unit_test*: En este directorio se encuentran los archivos de pruebas de unidad para cada una de las clases que tienes que desarrollar. Estos archivos de prueba te permiten verificar si tu implementación es correcta.
* *archivos cabecera (o header)*: Archivos en los que se realiza la implementación de cada clase.
* *main.cpp*: Archivo que contiene la función *main*. En este archivo se realiza la lectura/escritura de archivos.

En estos archivos deberás desarrollar la implementación de cada una de las clases que integran la solución del problema presentado en esta actividad. En la parte superior de cada archivo coloca deberás, en comentarios, tus datos. Por ejemplo:
```
// =========================================================
// File: one_header.h
// Author: Edward Elric - A00123456
// Date: 01/01/2021
// Description: This file implements some functions.
// =========================================================
```

## <span style="color: rgb(26, 99, 169);">Introducción</span>
En este proyecto, debes implementar una simulación de un sistema de gestión portuaria. El objetivo principal es analizar las solicitudes proporcionadas en el archivo de entrada y llevar a cabo las acciones necesarias.

Hay *puertos*, y los *barcos* que navegan entre ellos. Los buques transportan los siguientes tipos de contenedores: *ligeros*, *pesados*, *refigerados* y *líquidos*, cada uno de ellos debe manejarse de manera diferente. Los contenedores en un puerto se pueden cargar en los barcos y, a la inversa, se pueden descargar de un barco a un puerto. Los barcos necesitan una cierta cantidad de combustible para navegar de un puerto a otro.

Ten en cuenta que no hay ninguna interacción con el usuario durante la ejecución. Tu solución tomará la entrada de un archivo de texto, realizará las operaciones e imprimirá la información necesario en un archivo de texto de salida. El nombre de ambos archivos, los tomará como argumento del programa. En otras palabras, **no habrá ninguna entrada dada con el teclado mientras se ejecuta el programa**.

Ten en cuenta que habrá varias clases. Por lo tanto, trabajarás con varios archivos cabecera (o header). Los nombres de las variables de instancia y métodos se proporcionarán en este documento, así como en el encabezado de la clase que se encuentra en cada archivo cabecera. Aunque esto no significa que no puedas agregar métodos o campos adicionales.

### <span style="color: rgb(26, 99, 169);">**Clases**</span>
Existen 8 clases interactuando entre sí en este proyecto:
* `Container`.
* `LightContainer` (derivado de `Container`)
* `HeavyContainer` (derivado de `Container`)
* `RefrigeratedContainer` (derivado de `HeavyContainer`)
* `LiquidContainer` (derivado de `HeavyContainer`)
* `SimpleShip`.
* `Port`.
* `Ship`.

Ten en cuenta que será necesario hacer los cálculos necesarios mediante el uso de los métodos correspondiente en las clases `Port`, `Container` (o derivados) o `Ship`, no en el programa principal.

#### <span style="color: rgb(26, 99, 169);">**Container**</span>
La clase `Container` cuenta con las siguientes variables de estado:
* `id`: Identificador del contenedor.
* `weight`: Peso del contenedor.
* `type`: Tipo de contenedor (ligero, pesado, rerigerado, líquido).

La clase cuenta con los siguientes métodos:
* Constructor con tres parámetro (identificador, peso y tipo del contenedor).
* Constructor de copia.
* Métodos de acceso para todas las variables de instancia. (Si consideras necesario agregar métodos de modificación, adelante).
* `bool operator==(const Container *right)`: Regresa `true`, si el id, peso y tipo de contenedor son los mismo.
* `bool operator==(const Container &right)`: Regresa `true`, si el id, peso y tipo de contenedor son los mismo.
* `bool operator<(const Container *right)`: Si ambos contenedores son de mismo tipo, regresa `true`si el identificador de nuestro contenedor es menor. Si los tipos son diferentes, regresa `true`, si el tipo de nuestro contenedor es menor.
* `bool operator<(const Container &right)`: Si ambos contenedores son de mismo tipo, regresa `true`si el identificador de nuestro contenedor es menor. Si los tipos son diferentes, regresa `true`, si el tipo de nuestro contenedor es menor.
* `virtual double getConsumption() const = 0`: Función abstracta. Se deberá implementar en las clases derivadas.

#### <span style="color: rgb(26, 99, 169);">**Light**</span>
La clase `Light`, derivada de `Container`, no tiene ninguna variable de instancia propia. Sin embargo, cuenta con los siguientes métodos:
* Constructor con dos parámetro (identificador y peso). Invoca al constructor de la clase superior, indicando el tipo de contenedor correcto.
* Constructor de copia. Invoca al constructor de la clase superior.
* Métodos de acceso para todas las variables de instancia. (Si consideras necesario agregar métodos de modificación, adelante).
* `double getConsumption() const`: El consumo de combustible por llevar este tipo de contenedor es 2.5 veces el peso del mismo.

#### <span style="color: rgb(26, 99, 169);">**Heavy**</span>
La clase `Heavy`, derivada de `Container`, no tiene ninguna variable de instancia propia. Sin embargo, cuenta con los siguientes métodos:
* Constructor con dos parámetro (identificador, peso). Invoca al constructor de la clase superior, indicando el tipo de contenedor correcto.
* Constructor de copia. Invoca al constructor de la clase superior.
* Métodos de acceso para todas las variables de instancia. (Si consideras necesario agregar métodos de modificación, adelante).
* `double getConsumption() const`: El consumo de combustible por llevar este tipo de contenedor es 3 veces el peso del mismo.

#### <span style="color: rgb(26, 99, 169);">**Liquid**</span>
La clase `Liquid`, derivada de `Heavy`, no tiene ninguna variable de instancia propia. Sin embargo, cuenta con los siguientes métodos:
* Constructor con dos parámetro (identificador, peso). Invoca al constructor de la clase superior, indicando el tipo de contenedor correcto.
* Constructor de copia. Invoca al constructor de la clase superior.
* Métodos de acceso para todas las variables de instancia. (Si consideras necesario agregar métodos de modificación, adelante).
* `double getConsumption() const`: El consumo de combustible por llevar este tipo de contenedor es 4 veces el peso del mismo.

#### <span style="color: rgb(26, 99, 169);">**Refrigerated**</span>
La clase `Refrigerated`, derivada de `Heavy`, no tiene ninguna variable de instancia propia. Sin embargo, cuenta con los siguientes métodos:
* Constructor con dos parámetro (identificador, peso). Invoca al constructor de la clase superior, indicando el tipo de contenedor correcto.
* Constructor de copia. Invoca al constructor de la clase superior.
* Métodos de acceso para todas las variables de instancia. (Si consideras necesario agregar métodos de modificación, adelante).
* `double getConsumption() const`: El consumo de combustible por llevar este tipo de contenedor es 5 veces el peso del mismo.

#### <span style="color: rgb(26, 99, 169);">**SimpleShip**</span>
La clase `SimpleShip` cuenta con las siguientes variables de estado:
* `id` : Identificador de la nave.

La clase cuenta con los siguientes métodos:
* Constructor con un parámetro (identificador de la nave).
* Constructor de copia.
* Métodos de acceso para todas las variables de instancia. (Si consideras necesario agregar métodos de modificación, adelante).
* `bool operator==(const Container *right)`: Regresa `true`, si el identificador de ambas naves es el mismo.
* `bool operator==(const Container &right)`: Regresa `true`, si el identificador de ambas naves es el mismo.
* `bool operator<(const Container *right)`: Regresa `true`, si el identificador de nuestra nave es menor.
* `bool operator<(const Container &right)`: Regresa `true`, si el identificador de nuestra nave es menor.
* `virtual std::string toString() const = 0`: Función abstracta. Se deberá implementar en las clases derivadas.

#### <span style="color: rgb(26, 99, 169);">**Port**</span>
La clase `Port` cuenta con las siguientes variables de estado:
* `id`: Identificador del puerto.
* `x`, `y`: Posición del puerto en un plano cartesiano.
* `containers`: Lista de los contenedores que están en el puerto.
* `history`: Lista de los barcos que han estado en el puerto.
* `current`: Lista de los barcos que actualmente están en el puerto.

La clase cuenta con los siguientes métodos:
* Constructor con tres parámetros (identificador, posición en `x` y `y` del puerto).
* Constructor de copia.
* Métodos de acceso para todas las variables de instancia. (Si consideras necesario agregar métodos de modificación, adelante).
* `double getDistance(Port *port)`: Regresa la distancia euclidiana entre nuestro puerto y `port`.
* `void incomingShip(SimpleShip *ship)`: Si la nave no se encuentra ya en el puerto, la agrega a la lista de naves que actualmente están en el puerto.
* `void outgoingShip(SimpleShip *ship)`: Sólo se debe ejecutar si la nave se encuentra en el puerto. Remueva la nave de la lista de naves que actualmente están en el puerto y, si la nave no se encuentra en la lista de naves que han estado en el puerto, la agrega.
* `bool contains(Container *container)`: Regresa `true`, si el contenedor se encuentra en el puerto.
* `void add(Container *container)` : Agrega el nuevo contenedor a la lista de contenedores del puerto.
* `void remove(Container *container)` : Remueve el contenedor de la lista de contenedores del puerto.
* `std::string toString() const`: Regresa un string con el siguiente formato: "Port #id : (x, y)", en seguido la lista de contendores lígeros, pesados, refrigerados y líquidos que hay en el puerto. A continuación, despliega las naves que se encuentra en el puerto (**VER LOS EJEMPLOS DE SALIDA**).

#### <span style="color: rgb(26, 99, 169);">**Ship**</span>
La clase `Ship`, derivada de `SimpleShip`, cuenta con las siguientes variables de estado propias:
* `currentWeight`, `totalWeight` : Peso actual y máximo total de los contenedores que puede llevar la nave.
* `currentNumberOfAllContainers`, `maxNumberOfAllContainers` : cantidad actual y máxima de contenedores que puede llevar la nave.
* `currentNumberOfHeavyContainers`, `maxNumberOfHeavyContainers` : cantidad actual y máxima de contenedores pesados que puede llevar la nave.
* `currentNumberOfRefrigeratedContainers`, `maxNumberOfRefrigeratedContainers` : cantidad actual y máxima de contenedores refrigerados que puede llevar la nave.
* `currentNumberOfLiquidContainers`, `maxNumberOfLiquidContainers` : cantidad actual y máxima de contenedores con líquidos que puede llevar la nave.
* `fuel` : Cantidad actual de combustible.
* `fuelConsumptionPerKM`: Consumo de combustible por kilómetro.
* `currentPort`: Puerto actual en que se encuentra la nave.
* `containers` : Una lista con los contenedores que lleva la nave actualmente.

La clase cuenta con los siguientes métodos:
* Constructor con ocho parámetro (identificador de la nave, puerto actual, peso total que puede llevar, máxima cantidad de contenedores (totales, pesados,refrigrerados y líquidos) que puede llevar la nave y el consumo por kilómetro. Debe invocar al constructor de la clase superior con los parámetros correctos. El resto de las variables de instancia se inicializan a cero.
* Constructor de copia.
* Métodos de acceso para todas las variables de instancia. (Si consideras necesario agregar métodos de modificación, adelante).
* `bool sailTo(Port *port)`: El método calcula combustible que se consumiría por ir de un puerto a otro con base al consumo que genera cada uno de los contenedores que lleva la nave en ese momento, la distancia al puerto destino y el consumo por kilómetro de esta nave. Si la cantidad de combustible es menor al combustible actual, resta la cantidad calculada al combustible actual, elmina la nave del puerto actual, agrega la nave al puerto destino, cambia el puerto actual al puerto destino y regresa `true`para indicar que si se pudo realizar el viaje.
* `void reFuel(double amount)`: Siempre la cantidad sea positiva, la aumenta al combustible actual.
* `bool load(Container *container)`: Este método deberá revisar varias condiciones. La primera, si el puerto actual no tiene el contenedor o si la cantidad actual de contenedores es mayor o igual a la cantidad máxima de contenedores o si el peso actual m+as el peso del contenedor excede el peso total que puede llevar la nave, no es posible cargar ese contenedor. A continuación, deberá verificar, de acuerdo al tipo de contenedor, que no se exceda de la cantidad máxima permitida de contenedores de un tipo determinado. En cualquier caso anterior, deberá regresar `false`. Si se puede hacer la carga, deberá remover el contenedor del puerto actual, agregar a la lista de contenedor, incrementar el número de contenedores que lleva la nave tanto en lo general, como en lo que respecta a un tipo determinado, regresando `true`para indicar que se realizó la carga del contenedor.
* `bool contains(Container *container)`: Indica si el contenedor se encuentra dentro de la lista de contenedores.
* `bool remove(Container *container)`: Remueve un contenedor determinado de la lista de contenedores.
* `bool unLoad(Container *container)`: Este método, primero, deberá revisar si lleva el contenedor indicado. Si es así, deberá remove el contenedor de la lista de contenedores agregarlo al puerto actual, reducir el número de contenedores que lleva la nave tanto en lo general, como en lo que respecta a un tipo determinado, regresando `true`para indicar que se realizó la descarga del contenedor. Si no, regresa `false`.
* `std::string toString() const`: Regresa un string con el siguiente formato: "Ship #id : fuel", en seguido "\n\t\tLight Containers: " y la lista de contenedores ligeros, a continuación "\n\t\tHeavy Containers: " y la lista de contenedores pesados; y así para el resto de los contenedores refigerados y líquidos (**VER LOS EJEMPLOS DE SALIDA**).

#### <span style="color: rgb(26, 99, 169);">**main.cpp**</span>
En el archivo *main.cpp* se realizarán las operaciones generales de entrada y salida. Leerás de un archivo de entrada las operaciones sobre la simulación, las deberás realizar e imprimirás los resultados en el archivo de salida.

Las operaciones se detallan más adelante. El nombre de los archivos de entrada y salida se darán como argumentos del programa a través de la línea de comandos. Si el archivo de entrada no existe, el programa termina.

Deberás manejar tres vectores, uno para apuntadores a objetos `Container`, otro para apuntadores de objetos `Port` y otro para apuntadores a objetos `Ship`. 

#### <span style="color: rgb(26, 99, 169);">**Entrada**</span>
Vas a leer el archivo de entrada elemento por elemento.

La primera línea tiene cuatro números enteros, `C`, `S`, `P` y `N`. El número `C` represnta el número de contenedores que estarán en la simulación. El segundo número, `S`, indica el número de naves en la simulación. El tercer número, `P`, indica el número de puertos en la simulación. Y, por último, `N`, representa el número de eventos a simular.

Las siguientes `N` líneas serán algunas de las siguientes operaciones:
1. Creando un contenedor.
2. Creando una nave.
3. Creando un puerto.
4. Cargar un contenedor a una nave.
5. Descargar un contenedor de una nave.
6. Un nave viaja del puerto actual a otro.
7. Una nave carga combustible.

##### <span style="color: rgb(26, 99, 169);">**1. Creando un contenedor**</span>
Esta línea contiene un 1, seguido id del puerto en el que está el contenedor, el peso y tipo de contenedor.
```
1 <idPort> <weight> <type>
```
Los tipos válidos son `B`, `R` y `L`. `R` indica que es un contenedor refrigerado, mientras que `L` indica que es un contenedor líquido. Caso espacial es `B`, el tipo de contenedor que se creará dependerá del peso del contenedor. Si es peso es menor o igual a 3000, se crea un contenedor ligero; si es mayo, se crea un contenedor pesado. Toma en cuenta que el identificador del contenedor será el orden de creación. Por ejemplo, el primer contenedor creado debe tener Id 0 y debe colocarse en la posición 0 del vector.

##### <span style="color: rgb(26, 99, 169);">**2. Creando una nave**</span>
Esta línea contiene un 2, seguido del identificador del puerto en que se encuentra la nave, el peso total que puede llevar la nave, en número máximo de contenedores, de contenedores pesados, refrigerados y líquidos que la nave puede llevar, así como el consumo de combustible por kilómetro. Recuerda agregar esta nueva nave al puerto correspondiente.
```
2 <idPort> <totalWeight> <maxNumberOfAllContainers> <maxNumberOfHeavyContainers> <maxNumberOfRefrigeratedContainers> <maxNumberOfLiquidContainers> <fuelConsumptionPerKM>
```
Toma en cuenta que el identificador de la nave será el orden de creación. Por ejemplo, la primera nave creada debe tener Id 0 y debe colocarse en la posición 0 del vector.

##### <span style="color: rgb(26, 99, 169);">**3. Creando un puerto**</span>
Esta línea contiene un 3, seguido de la posición `x` y `y` del puerto.

```
3 <x> <y>
```
Toma en cuenta que el identificador de la nave será el orden de creación. Por ejemplo, la primera nave creada debe tener Id 0 y debe colocarse en la posición 0 del vector.

##### <span style="color: rgb(26, 99, 169);">**4. Cargar un contenedor a una nave**</span>
Esta línea contiene un 4, seguido del id de la nave y el id del contenedor.

```
4 <idShip> <idContainer>
```

##### <span style="color: rgb(26, 99, 169);">**5. Descargar un contenedor de una nave**</span>
Esta línea contiene un 5, seguido del id de la nave y el id del contenedor.

```
5 <idShip> <idContainer>
```

##### <span style="color: rgb(26, 99, 169);">**6. Un nave viaja del puerto actual a otro**</span>
Esta línea contiene un 6, seguido del id de la nave y el id del puerto.

```
6 <idShip> <idPort>
```

##### <span style="color: rgb(26, 99, 169);">**7. Una nave carga combustible**</span>
Esta línea contiene un 7, seguido del id de la nave y la cantidad de combustible.

```
7 <idShip> <amount>
```

#### <span style="color: rgb(26, 99, 169);">**Salida**</span>
Debes calcular lo siguiente e imprimirlo en el archivo de salida.

Debés imprimir la información relacionada con cada puerto (contenedores y barcos).

Por último, deberás eliminar todos los apuntadores que existan y cerrar los archivos de entrada y salida.
