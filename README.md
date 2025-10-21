
<a id="arriba" href="#arriba8">atrás</a> - Curso de Java de Babull - <a href="#arriba1">siguiente</a>  

## 🚧 Guía Paso a Paso: Java y Arquitectura Hexagonal
<ul>
<li><a href="#arriba1">  Fundamentos de Java (Conceptos Clave para la Arquitectura) $\leftarrow$ **(Empezaremos con este)**</a></li>  
<li><a href="#arriba2">  Preparación del Entorno de Desarrollo y Estructura Básica de Proyectos</a></li>  
<li><a href="#arriba3">  Introducción a la Arquitectura Hexagonal: El "Por Qué" y sus Principios Centrales</a></li>  
<li><a href="#arriba4">  Definición del **Dominio (Core)**: Entidades y Casos de Uso</a></li>  
<li><a href="#arriba5">  Implementación de los **Puertos (Ports)**: Interfaces de Entrada y Salida</a></li>  
<li><a href="#arriba6">  Implementación de los **Adaptadores de Lado Primario (Driving/Inbound Adapters)**: La Interfaz de Usuario/API</a></li>  
<li><a href="#arriba7">  Implementación de los **Adaptadores de Lado Secundario (Driven/Outbound Adapters)**: Persistencia de Datos</a></li>  
<li><a href="#arriba8">  Conexión y Ensamblaje de Componentes (Inversión de Dependencia)</a></li>  
</ul>

<a id="arriba1" href="#arriba">atrás</a> - Curso de Java de Babull - <a href="#arriba2">siguiente</a>  

## 1. Fundamentos de Java (Conceptos Clave para la Arquitectura)

Antes de hablar de la Arquitectura Hexagonal, necesitamos entender tres conceptos cruciales en Java que son la base para implementarla: **Clases y Objetos**, **Interfaces**, y el principio de **Inversión de Dependencia (Dependency Inversion Principle - DIP)**.

### 1.1. Clases y Objetos (La Base de Java)

Java es un lenguaje de **programación orientada a objetos (POO)**. Esto significa que todo se organiza alrededor de *objetos* que son instancias (ejemplares) de *clases*.

* **Clase:** Piensa en una clase como el **molde** o el **plano** para crear algo. Define las **propiedades** (datos) y los **comportamientos** (acciones o métodos) que tendrán los objetos creados a partir de ella.
    * *Ejemplo:* La clase `Coche` podría tener las propiedades `color`, `velocidadMaxima` y los comportamientos `acelerar()`, `frenar()`.

* **Objeto:** Es la **cosa real** creada a partir del molde. Es una instancia concreta de una clase.
    * *Ejemplo:* El objeto `miCoche` es un coche azul con velocidad máxima de $200$ km/h, creado a partir de la clase `Coche`.

**Relación con Hexagonal:** La Arquitectura Hexagonal se basa en modelar el **Dominio** (el corazón de la aplicación) con clases y objetos que representan el negocio (ej: `CuentaBancaria`, `Producto`, `Cliente`).

### 1.2. Interfaces (El Contrato Clave)

Las interfaces son el concepto **más importante** para entender la Arquitectura Hexagonal.

* **¿Qué es una Interfaz?** Es un **contrato** o una **promesa**. Una interfaz en Java es una colección de **métodos abstractos** (métodos sin implementación, solo la firma) y algunas constantes.
    * *Método Abstracto:* Solo dice *qué* hacer, pero no *cómo* hacerlo.
    * *Ejemplo:* La interfaz `AlmacenadorDeDatos` podría tener el método `guardar(datos)`.

* **¿Cuál es su Propósito?** Una interfaz define una **funcionalidad** sin especificar quién o cómo la va a realizar. Cualquier **Clase** que elija implementar esa interfaz está **obligada** a proporcionar el código (*el cómo*) para todos los métodos definidos en el contrato.
    * *Ejemplo:* La clase `BaseDeDatosSQL` y la clase `ArchivoCSV` pueden ambas implementar la interfaz `AlmacenadorDeDatos`. Ambas cumplen el contrato `guardar(datos)`, pero una lo hace escribiendo en una base de datos y la otra en un archivo.

**Relación con Hexagonal:** En la Arquitectura Hexagonal, los **Puertos (Ports)** son casi siempre **Interfaces**. Son los **puntos de entrada y salida** de tu aplicación, y están definidos como contratos (Interfaces) para mantener el **Dominio** (el negocio) completamente aislado de la tecnología externa (Bases de datos, Web, APIs, etc.).

### 1.3. Inversión de Dependencia (DIP)

El DIP es uno de los cinco principios **SOLID** (principios de diseño de software) y es el **motor** de la Arquitectura Hexagonal.

* **Dependencia Tradicional (La Forma Incorrecta):** Normalmente, un módulo de alto nivel (que contiene la lógica de negocio importante) depende directamente de un módulo de bajo nivel (que se encarga de detalles tecnológicos).
    * *Ejemplo Tradicional:* Tu clase de lógica de negocio (`ServicioDeClientes`) usa directamente la clase `BaseDeDatosMySQL`. Si quieres cambiar a PostgreSQL, tienes que modificar la clase `ServicioDeClientes`. **La lógica de negocio depende del detalle tecnológico.**

* **Inversión de Dependencia (DIP):** El principio dice:
    1.  Los módulos de alto nivel **no deben depender** de módulos de bajo nivel. **Ambos deben depender de abstracciones (Interfaces).**
    2.  Las abstracciones **no deben depender** de los detalles. Los detalles (**Clases concretas**) deben depender de las abstracciones (**Interfaces**).

* **La Solución con Interfaces:**
    1.  Creamos una **Interfaz** (`RepositorioClientes`) en el módulo de alto nivel (Dominio).
    2.  El módulo de alto nivel (`ServicioDeClientes`) **depende de la Interfaz**.
    3.  El módulo de bajo nivel (`BaseDeDatosMySQL`) **implementa la Interfaz**.

Ahora, la lógica de negocio (`ServicioDeClientes`) ya no sabe si está usando MySQL o un archivo CSV; solo sabe que está llamando al método `guardar()` definido en el **contrato (Interfaz)**. Hemos "invertido" la dependencia, haciendo que la lógica de negocio dependa de un contrato, y la tecnología dependa también de ese mismo contrato.



**Relación con Hexagonal:** La Arquitectura Hexagonal es, en esencia, la aplicación práctica del DIP. El **Dominio** (el hexágono, el módulo de alto nivel) define todos sus **Puertos (Interfaces)**. De esta forma, el **Dominio NUNCA** depende de la tecnología externa, sino que la tecnología externa (los **Adaptadores**) depende de las Interfaces definidas por el Dominio.

***

¡Con estos fundamentos de Java claros, estaremos listos para establecer el entorno y la estructura de un proyecto para la Arquitectura Hexagonal en el siguiente paso! ¿Estás listo para el **Paso 2**?

<a id="arriba2" href="#arriba1">atrás</a> - Curso de Java de Babull - <a href="#arriba3">siguiente</a>  

## 2\. Preparación del Entorno de Desarrollo y Estructura Básica de Proyectos

Antes de escribir el código de negocio, necesitamos una "casa" donde vivirán nuestras clases. Esto implica instalar herramientas y organizar el proyecto de una forma que refleje las capas de la Arquitectura Hexagonal.

### 2.1. Instalación y Herramientas Necesarias 🛠️

Si no tienes experiencia previa con Java, necesitarás lo siguiente:

1.  **Java Development Kit (JDK):** Es el corazón. Contiene el compilador, las librerías necesarias y el entorno de ejecución (JVM). Necesitas instalar una versión reciente, como **JDK 17** (la versión LTS o *Long Term Support*).
2.  **Entorno de Desarrollo Integrado (IDE):** Es la herramienta donde escribirás el código. El más común en el mundo Java y altamente recomendado es **IntelliJ IDEA Community Edition** (gratuito). Otras opciones populares son Eclipse o VS Code.
3.  **Herramienta de Construcción (Build Tool):** Para Java, no solo escribimos archivos `.java`, sino que necesitamos una herramienta que gestione:
      * La compilación del código.
      * La descarga de librerías externas (dependencias).
      * La creación del paquete final (el archivo `.jar` ejecutable).
        El estándar de facto para proyectos profesionales es **Maven** o **Gradle**. Usaremos **Maven** por su simplicidad inicial.

### 2.2. Creación del Proyecto Básico con Maven

Para crear un proyecto Java que respete las capas de la Arquitectura Hexagonal, la mejor práctica es usar **Módulos de Maven** (o subproyectos). Esto nos permite hacer cumplir las reglas de dependencia de la arquitectura a nivel de compilación:

| Módulo/Capa | Contenido (Dominio) | Dependencias Permitidas |
| :--- | :--- | :--- |
| **`app-core`** | Lógica de **Dominio** (el negocio puro), **Puertos (Interfaces)**. | **NINGUNA** (no puede ver ni Base de Datos ni Web). |
| **`app-infra`** | **Adaptadores** (Implementaciones de BD, Web, Archivos). | Depende de `app-core` (implementa sus Interfaces). |
| **`app-main`** | El punto de arranque de la aplicación (el **Ensamblador**). | Depende de `app-core` y `app-infra`. |

**Estructura del Directorio del Proyecto:**

```
proyecto-hexagonal/
├── pom.xml (Maven Principal)
├── app-core/
│   ├── src/main/java/com/miempresa/core/...
│   └── pom.xml (Maven del Core)
├── app-infra/
│   ├── src/main/java/com/miempresa/infra/...
│   └── pom.xml (Maven de la Infraestructura)
├── app-main/
│   ├── src/main/java/com/miempresa/main/Application.java
│   └── pom.xml (Maven del Main)
```

**📌 Explicación Detallada de la Estructura (El Por Qué):**

  * **Aislamiento del Core:** La carpeta `app-core` es la más sagrada. Por definición, **sólo contendrá lógica de negocio**. El `pom.xml` de `app-core` *no* listará librerías de bases de datos (como JDBC) o frameworks web (como Spring Web), forzando a que la lógica de negocio permanezca **agnóstica a la tecnología**.
  * **Encapsulamiento de Infraestructura:** La carpeta `app-infra` contendrá todo lo "externo" al negocio: el código que habla con la base de datos, el código que procesa las peticiones web, etc. Su `pom.xml` sí listará librerías externas.
  * **Rol del Main:** La carpeta `app-main` es donde se juntan todas las piezas (Adaptadores y Core) y se arranca la aplicación. Es el único lugar que conoce la existencia de la tecnología (Adaptadores) *y* el negocio (Core).

### 2.3. Estructura de Paquetes dentro del Core (Muy Importante)

Dentro del módulo `app-core` (el Dominio), es crucial dividir las responsabilidades usando paquetes de Java para reflejar las partes de la Arquitectura Hexagonal:

```
app-core/src/main/java/com/miempresa/core/
├── domain/            <-- Clases de negocio (Ej: Cuenta, Producto)
├── service/           <-- Casos de Uso (Lógica de negocio: transferirDinero, crearProducto)
└── port/              <-- Interfaces (Contratos de comunicación)
    ├── in/            <-- Puertos Primarios (Input/Driving)
    └── out/           <-- Puertos Secundarios (Output/Driven)
```

**📌 Resumen de responsabilidades del `app-core`:**

  * **`domain`:** Contiene las **Entidades** que representan la información de la empresa.
  * **`service`:** Contiene los **Casos de Uso** (*Use Cases*), que son la lógica de negocio pura (qué se puede hacer).
  * **`port`:** Contiene las **Interfaces** que definen los límites del Dominio. Esto es la parte clave de Hexagonal.

-----

Con esta estructura definida, ya tenemos la casa lista para empezar a construir el Dominio. El **Paso 3** será entender la teoría de la Arquitectura Hexagonal y cómo estos paquetes (Domain, Service, Port) encajan en el Hexágono.

¿Continuamos con el **Paso 3**?

<a id="arriba3" href="#arriba2">atrás</a> - Curso de Java de Babull - <a href="#arriba4">siguiente</a>  

## 3. Introducción a la Arquitectura Hexagonal: El "Por Qué" y sus Principios Centrales

La Arquitectura Hexagonal, creada por Alistair Cockburn, también se conoce como la arquitectura de **Puertos y Adaptadores (*Ports and Adapters*)**.

### 3.1. El Problema que Resuelve (El "Por Qué")

En las arquitecturas tradicionales (como la arquitectura de tres capas: Presentación, Lógica de Negocio, Datos), el código de negocio suele estar íntimamente ligado a la tecnología.

* **Problema:** Si tu lógica de negocio (por ejemplo, cómo se calcula una comisión) está escrita directamente dentro de clases que dependen de la tecnología web o de la base de datos, tienes problemas si:
    * Quieres cambiar de una base de datos MySQL a MongoDB.
    * Quieres probar la lógica de negocio sin levantar el servidor web.
    * Quieres usar la lógica de negocio desde una API REST, una línea de comandos o una interfaz gráfica, sin reescribir nada.

La Arquitectura Hexagonal resuelve esto **protegiendo el corazón de la aplicación (el Dominio) de la tecnología externa.**

### 3.2. El Hexágono (El Símbolo)

Piensa en la arquitectura como un **Hexágono** 

[Image of Hexagonal Architecture Diagram]
.

* **El Interior (El Core/Dominio):** Es la lógica de negocio pura. Contiene las reglas, los datos, y los casos de uso. **El Core no conoce NADA de la tecnología externa** (no sabe si hay una base de datos, una web o un archivo CSV). Es el lugar más importante y estable de la aplicación.
* **Los Bordes del Hexágono:** Son los **Puertos (Ports)**. Actúan como contratos que definen cómo se comunica el Core con el mundo exterior.
* **El Exterior:** Son los **Adaptadores (Adapters)**. Son el código que convierte la tecnología externa (Web, SQL, Ficheros) al formato que el Core espera.

### 3.3. Principios Centrales: Puertos y Adaptadores

La arquitectura se basa en dos componentes clave que definimos como interfaces (Puertos) y sus implementaciones (Adaptadores).

#### A. Los Puertos (*Ports*)

Los Puertos son las **Interfaces de Java** que definen un contrato de comunicación. Representan los límites del Core. Los dividimos en dos tipos:

| Tipo de Puerto | También llamado | Rol | ¿Dónde se usa? |
| :--- | :--- | :--- | :--- |
| **Puerto Primario** | *Driving Port* (Conduce) / *Input Port* | Define lo que el **mundo exterior quiere hacer** con el Core (los Casos de Uso). | **Llamado** por la interfaz de usuario/web. |
| **Puerto Secundario** | *Driven Port* (Es conducido) / *Output Port* | Define lo que el **Core necesita del mundo exterior** (generalmente, persistencia o servicios). | **Implementado** por la infraestructura (BD, Servicios externos). |

#### B. Los Adaptadores (*Adapters*)

Los Adaptadores son las **clases concretas** (implementaciones) que se sientan en el exterior del hexágono y se encargan de la "traducción" tecnológica.

| Tipo de Adaptador | Rol | Implementa... | Tecnología que usa |
| :--- | :--- | :--- | :--- |
| **Adaptador Primario** | **Interfaz de Usuario/Web.** Recibe peticiones del usuario y las traduce en llamadas al Puerto Primario. | El **Puerto Primario** llama a este Adaptador. | Spring Web, Java Swing, Consola, etc. |
| **Adaptador Secundario** | **Infraestructura/Persistencia.** Contiene la lógica para interactuar con bases de datos, APIs de terceros, etc. | El **Puerto Secundario** (la Interfaz) es implementado por este Adaptador. | JDBC, JPA, APIs REST, etc. |

### 3.4. El Motor de la Arquitectura: Inversión de Dependencia (DIP)

Este es el punto crucial y la razón por la que el Hexágono funciona: **Las dependencias siempre apuntan hacia adentro, hacia el Core.**

* **El Core (`app-core`) no depende de la Infraestructura (`app-infra`).**
* **La Infraestructura (`app-infra`) SÍ depende del Core (`app-core`).**

Esto se logra porque el Core define **TODOS** los contratos (Interfaces/Puertos).

1.  El Core dice: "Para guardar datos, necesito que alguien implemente mi interfaz `RepositorioClientes` (Puerto Secundario)".
2.  El Adaptador Secundario (`BaseDeDatosSQL` en `app-infra`) dice: "Yo implemento la interfaz `RepositorioClientes` del Core".

El resultado: El Core permanece completamente aislado y la tecnología es intercambiable, porque la única cosa que importa es el contrato (la Interfaz).

***

Con esta teoría clara, ya podemos empezar a programar la capa más interna y protegida: el Dominio. El **Paso 4** se centrará en definir la lógica de negocio pura, sin pensar en bases de datos ni peticiones web.

¿Listo para el **Paso 4**?

<a id="arriba4" href="#arriba3">atrás</a> - Curso de Java de Babull - <a href="#arriba5">siguiente</a>  

## 4\. Definición del Dominio (Core): Entidades y Casos de Uso

El Core es el corazón de la aplicación, donde reside la lógica de negocio **sin ninguna dependencia tecnológica**. Para este ejemplo, vamos a modelar un sistema muy simple de **Gestión de Cuentas Bancarias**.

### 4.1. El Dominio (`app-core/domain`) 🏦

Aquí definiremos las **Entidades** y los **Objetos de Valor** que representan el negocio. Usaremos clases Java simples (POJOs - *Plain Old Java Objects*).

#### a. Modelando el Dinero (Objeto de Valor)

Para evitar errores en cálculos monetarios, es buena práctica usar un objeto de valor.

**Ruta:** `app-core/src/main/java/com/miempresa/core/domain/Dinero.java`

```java
package com.miempresa.core.domain;

import java.math.BigDecimal; // Importamos esta clase para manejar el dinero con precisión
import java.util.Objects;

// La clase Dinero es inmutable (sus valores no cambian después de crearse)
public class Dinero {
    
    private final BigDecimal cantidad;

    // Constructor privado para forzar la creación a través de un método estático
    private Dinero(BigDecimal cantidad) {
        if (cantidad.compareTo(BigDecimal.ZERO) < 0) {
            throw new IllegalArgumentException("La cantidad no puede ser negativa.");
        }
        this.cantidad = cantidad;
    }

    // Método estático de fábrica para crear instancias
    public static Dinero de(double valor) {
        // Usamos BigDecimal para evitar problemas de precisión del tipo 'double'
        return new Dinero(BigDecimal.valueOf(valor)); 
    }

    public BigDecimal getCantidad() {
        return cantidad;
    }

    // Comportamientos específicos del dominio:
    public Dinero sumar(Dinero otro) {
        return new Dinero(this.cantidad.add(otro.cantidad));
    }

    public Dinero restar(Dinero otro) {
        BigDecimal resultado = this.cantidad.subtract(otro.cantidad);
        if (resultado.compareTo(BigDecimal.ZERO) < 0) {
            throw new IllegalStateException("Saldo insuficiente.");
        }
        return new Dinero(resultado);
    }
    
    // Métodos equals y hashCode para comparar objetos de forma correcta (omitidos por brevedad)
    // ...
}
```

#### b. Modelando la Cuenta Bancaria (Entidad)

Esta es nuestra entidad central. Contiene la lógica para las operaciones permitidas.

**Ruta:** `app-core/src/main/java/com/miempresa/core/domain/Cuenta.java`

```java
package com.miempresa.core.domain;

// El Core SÓLO usa clases de Java estándar o de su propio dominio
public class Cuenta {

    private final Long id;          // Identificador de la cuenta
    private Dinero saldo;           // El saldo actual

    public Cuenta(Long id, Dinero saldo) {
        this.id = id;
        this.saldo = saldo;
    }

    // Método de Negocio: Permite depositar dinero en la cuenta
    public void depositar(Dinero cantidad) {
        // La lógica de negocio está aquí: el saldo se suma.
        this.saldo = this.saldo.sumar(cantidad);
    }

    // Método de Negocio: Permite retirar dinero
    public void retirar(Dinero cantidad) {
        // La lógica de negocio está aquí: la validación de saldo insuficiente ocurre en la clase Dinero.
        this.saldo = this.saldo.restar(cantidad);
    }

    // Getters
    public Long getId() {
        return id;
    }

    public Dinero getSaldo() {
        return saldo;
    }
}
```

### 4.2. Los Casos de Uso (`app-core/service`) ⚙️

Los Casos de Uso (o Servicios de Aplicación) orquestan las operaciones entre las Entidades y definen lo que la aplicación puede hacer. Este es el código que los **Puertos Primarios** expondrán.

**Ruta:** `app-core/src/main/java/com/miempresa/core/service/TransferenciaService.java`

```java
package com.miempresa.core.service;

import com.miempresa.core.domain.Cuenta;
import com.miempresa.core.domain.Dinero;
// Importamos el Puerto Secundario (la Interfaz) que usaremos
import com.miempresa.core.port.out.CuentaRepositoryPort;

// Esta clase contiene la LÓGICA DE NEGOCIO pura
public class TransferenciaService {

    // Dependencia del Puerto Secundario (el contrato de persistencia)
    private final CuentaRepositoryPort cuentaRepository; 
    
    // Inyección de dependencia (usaremos un constructor, luego veremos cómo automatizar esto)
    public TransferenciaService(CuentaRepositoryPort cuentaRepository) {
        this.cuentaRepository = cuentaRepository;
    }

    // El Caso de Uso Central: Lógica de Transferencia
    public void transferir(Long origenId, Long destinoId, double monto) {
        
        Dinero cantidad = Dinero.de(monto);

        // 1. Obtener Cuentas (usando el PUERTO SECUNDARIO)
        Cuenta cuentaOrigen = cuentaRepository.obtenerCuenta(origenId)
                .orElseThrow(() -> new RuntimeException("Cuenta de origen no encontrada"));
        
        Cuenta cuentaDestino = cuentaRepository.obtenerCuenta(destinoId)
                .orElseThrow(() -> new RuntimeException("Cuenta de destino no encontrada"));

        // 2. Ejecutar la Lógica de Negocio (la llama a la Entidad)
        cuentaOrigen.retirar(cantidad);
        cuentaDestino.depositar(cantidad);
        
        // 3. Persistir (usando el PUERTO SECUNDARIO)
        cuentaRepository.actualizarCuenta(cuentaOrigen);
        cuentaRepository.actualizarCuenta(cuentaDestino);
        
        // NOTA: El TransferenciaService NO sabe si la persistencia es SQL, NoSQL o un archivo.
        // Solo sabe que usa el contrato (CuentaRepositoryPort).
    }
}
```

-----

**Resumen del Paso 4:** Hemos creado el **Dominio** (Entidades: `Dinero`, `Cuenta`) con la lógica esencial, y el **Caso de Uso** (`TransferenciaService`) que orquesta las operaciones.

**Lo más importante:** En el `TransferenciaService` notamos la necesidad de una forma de **obtener** y **guardar** cuentas. Esta forma es una **Interfaz**, a la que llamamos `CuentaRepositoryPort`.

El **Paso 5** se centrará en definir exactamente esta interfaz y la que usará el mundo exterior para llamar a nuestro `TransferenciaService`. Estamos listos para definir los **Puertos (Interfaces)**.

¿Continuamos con el **Paso 5**?

<a id="arriba5" href="#arriba4">atrás</a> - Curso de Java de Babull - <a href="#arriba6">siguiente</a>  

## 5\. Implementación de los Puertos (Ports): Interfaces de Entrada y Salida

En la Arquitectura Hexagonal, los puertos viven en la capa del Core y se definen como interfaces Java dentro del paquete `port/`.

### 5.1. Puertos Secundarios (Driven/Output Ports) 💾

Este tipo de puerto define lo que el **Core necesita** del mundo exterior. En nuestro caso de uso (`TransferenciaService`), el Core necesita guardar y obtener cuentas.

  * **Rol:** Son Interfaces implementadas por la infraestructura (`app-infra`).
  * **Definición:** El Core define el contrato que la tecnología de persistencia deberá cumplir.

**Ruta:** `app-core/src/main/java/com/miempresa/core/port/out/CuentaRepositoryPort.java`

```java
package com.miempresa.core.port.out;

import com.miempresa.core.domain.Cuenta;
import java.util.Optional; // Usamos Optional para manejar la posible ausencia de una cuenta

// Puerto Secundario (Output Port): El Core "pide" estos servicios a la Infraestructura
public interface CuentaRepositoryPort {

    // Contrato para obtener una cuenta por su ID
    Optional<Cuenta> obtenerCuenta(Long id);

    // Contrato para actualizar (o guardar) una cuenta
    void actualizarCuenta(Cuenta cuenta);

    // NOTA IMPORTANTE: Esta Interfaz NO tiene código SQL, JPA, o de archivos.
    // Solo define las operaciones que son relevantes para el negocio.
}
```

**Observación Clave:** El `TransferenciaService` que creamos en el Paso 4 solo conoce y depende de esta interfaz, lo que permite intercambiar la implementación de la base de datos sin tocar el servicio.

### 5.2. Puertos Primarios (Driving/Input Ports) 🌐

Este tipo de puerto define lo que el **mundo exterior quiere hacer** con el Core. Es la interfaz que expone los **Casos de Uso** a las interfaces de usuario (web, consola, etc.).

  * **Rol:** Son Interfaces implementadas por los servicios de aplicación (Casos de Uso) dentro del Core.
  * **Definición:** La interfaz de usuario/web llamará a estos métodos.

**Ruta:** `app-core/src/main/java/com/miempresa/core/port/in/TransferenciaServicePort.java`

```java
package com.miempresa.core.port.in;

// Puerto Primario (Input Port): Define las operaciones que se pueden llamar desde afuera
public interface TransferenciaServicePort {

    // Este contrato es la forma en que la Web/API llamará a nuestra lógica de transferencia
    void transferir(Long origenId, Long destinoId, double monto);
    
    // NOTA: Esta Interfaz es implementada por la clase TransferenciaService que creamos en el Paso 4.
}
```

### 5.3. Adaptando el Caso de Uso (La Implementación del Puerto Primario)

Para cerrar la pinza del Core, debemos asegurarnos de que nuestro `TransferenciaService` (creado en el Paso 4) ahora **implemente** el `TransferenciaServicePort`.

**Modificación en:** `app-core/src/main/java/com/miempresa/core/service/TransferenciaService.java`

```java
package com.miempresa.core.service;

// ... (otros imports)
import com.miempresa.core.port.out.CuentaRepositoryPort;
import com.miempresa.core.port.in.TransferenciaServicePort; // <-- Nueva Importación

// IMPLEMENTAMOS EL PUERTO PRIMARIO (Input Port)
public class TransferenciaService implements TransferenciaServicePort { 

    private final CuentaRepositoryPort cuentaRepository; 
    
    public TransferenciaService(CuentaRepositoryPort cuentaRepository) {
        this.cuentaRepository = cuentaRepository;
    }

    // El cuerpo del método transferir ya existía, pero ahora cumple el contrato (la Interfaz)
    @Override // Sobreescribimos el método de la interfaz TransferenciaServicePort
    public void transferir(Long origenId, Long destinoId, double monto) {
        
        // ... (resto de la lógica de transferencia que ya definimos)
        // ... (El código de negocio permanece aquí, inalterado)
        
        // 1. Obtener Cuentas (usando el PUERTO SECUNDARIO: cuentaRepository)
        // ...
        
        // 2. Ejecutar la Lógica de Negocio (Entidades)
        // ...
        
        // 3. Persistir (usando el PUERTO SECUNDARIO: cuentaRepository)
        // ...
    }
}
```

-----

**Resumen del Paso 5:** Hemos definido los **contratos** para entrar y salir del Core.

1.  **Puerto Secundario (`CuentaRepositoryPort`):** El Core lo usa para pedir datos.
2.  **Puerto Primario (`TransferenciaServicePort`):** El mundo exterior lo usa para llamar al Core.

La arquitectura del Core está terminada. El siguiente paso, el **Paso 6**, será construir el **Adaptador de Lado Primario**, la parte que vive afuera y permite que un usuario (por ejemplo, a través de una API REST) use nuestro Core.

¿Listo para el **Paso 6**?

<a id="arriba6" href="#arriba5">atrás</a> - Curso de Java de Babull - <a href="#arriba7">siguiente</a>  

## 6\. Implementación de los Adaptadores de Lado Primario (Driving/Inbound Adapters) 🌐

El **Adaptador Primario** (o *Driving Adapter*) es la capa externa que traduce las interacciones del mundo real (una petición HTTP, un clic, un comando de consola) en llamadas al **Puerto Primario** del Core.

Este adaptador vive en nuestro módulo de **Infraestructura** (`app-infra`).

### 6.1. El Rol del Adaptador Primario

  * **Recibir Input:** Escucha peticiones (ej: una solicitud HTTP POST a `/transferir`).
  * **Traducir:** Convierte los datos de la tecnología (ej: JSON/HTTP) en objetos del Core (ej: un `Long` para IDs, un `double` para monto).
  * **Llamar al Core:** Llama al **Puerto Primario** (`TransferenciaServicePort`) para ejecutar la lógica de negocio.
  * **Devolver Output:** Traduce la respuesta del Core (o la excepción) al formato de la tecnología (ej: un código HTTP 200 OK).

### 6.2. Creación del Adaptador Web (Controlador REST)

Usaremos un ejemplo de un **Controlador REST** (típico de una API web) que usa el *framework* **Spring Boot** (el estándar de Java para APIs modernas).

**Nota Importante:** Si no usáramos un *framework* como Spring Boot, tendríamos que manejar manualmente la creación de un servidor web, algo que es complejo y no es el foco de la Arquitectura Hexagonal. Por ello, en el mundo real, los Adaptadores Primarios siempre usan *frameworks*.

#### a. Configuración de Dependencias (Maven)

El módulo `app-infra` necesita saber de Spring Boot para ser un controlador web, **y** necesita poder ver el Core para usar sus Interfaces.

**Ruta:** `app-infra/pom.xml` (Fragmento clave)

```xml
<dependencies>
    <dependency>
        <groupId>com.miempresa</groupId> 
        <artifactId>app-core</artifactId>
        <version>1.0-SNAPSHOT</version> 
    </dependency>
    
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

#### b. Creación de la Clase del Adaptador

**Ruta:** `app-infra/src/main/java/com/miempresa/infra/adapter/in/web/TransferenciaController.java`

```java
package com.miempresa.infra.adapter.in.web;

import com.miempresa.core.port.in.TransferenciaServicePort; // Importamos el PUERTO PRIMARIO

// Imports específicos de la tecnología (Spring Web)
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;


// Definimos la estructura de datos que esperamos de la petición HTTP (DTO)
// Este objeto es puramente para la capa de Presentación/Infraestructura
class TransferenciaRequest {
    public Long origenId;
    public Long destinoId;
    public double monto;
    // Getters y Setters se omiten por brevedad
}


@RestController // Anotación de Spring que la define como un controlador REST
@RequestMapping("/api/v1/transferencia") 
public class TransferenciaController {

    // 1. Dependencia del PUERTO PRIMARIO (Interfaz del Core)
    private final TransferenciaServicePort transferenciaService;

    // Inyección del Puerto Primario (Spring lo maneja)
    public TransferenciaController(TransferenciaServicePort transferenciaService) {
        // Notar que el Controller NO depende del TransferenciaService (la clase concreta),
        // sino de la Interfaz TransferenciaServicePort.
        this.transferenciaService = transferenciaService;
    }

    // 2. Método que recibe la petición HTTP
    @PostMapping
    public ResponseEntity<String> transferir(@RequestBody TransferenciaRequest request) {
        try {
            // A. Traducción: Tomar datos del Request HTTP y pasarlos al formato del Core
            
            // B. Invocación al Core: Llama al Puerto Primario (el Contrato)
            transferenciaService.transferir(
                request.origenId, 
                request.destinoId, 
                request.monto
            );

            // C. Devolver Output: Responder con éxito (código 200)
            return new ResponseEntity<>("Transferencia realizada con éxito.", HttpStatus.OK);

        } catch (RuntimeException e) {
            // Manejo de errores: traducir la excepción de negocio a una respuesta HTTP 400
            return new ResponseEntity<>(e.getMessage(), HttpStatus.BAD_REQUEST);
        }
    }
}
```

-----

**Resumen del Paso 6:**
Hemos creado la puerta de entrada a nuestro sistema. El `TransferenciaController` es un Adaptador Primario que:

1.  Conoce la **tecnología web** (anotaciones `@RestController`, `ResponseEntity`).
2.  Solo conoce el **Core** a través del **Puerto Primario** (`TransferenciaServicePort`).

El único elemento que nos falta es la base de datos. El **Paso 7** se centrará en crear el **Adaptador de Lado Secundario** que implementará el contrato de persistencia (`CuentaRepositoryPort`).

¿Listo para el **Paso 7**?

<a id="arriba7" href="#arriba6">atrás</a> - Curso de Java de Babull - <a href="#arriba8">siguiente</a>  

## 7\. Implementación de los Adaptadores de Lado Secundario (Driven/Outbound Adapters) 💾

El **Adaptador Secundario** (o *Driven Adapter*) es responsable de implementar el contrato que el Core definió para la persistencia de datos.

### 7.1. El Rol del Adaptador Secundario

  * **Implementar el Contrato:** Implementa la interfaz **Puerto Secundario** (`CuentaRepositoryPort`) del Core.
  * **Manejar la Tecnología:** Contiene el código específico de la base de datos (SQL, NoSQL, o incluso una API externa).
  * **Traducir:** Convierte los objetos del **Dominio** (ej: `Cuenta`) a los objetos específicos de la tecnología (ej: una `Entity` de JPA o un `Document` de MongoDB) y viceversa.

### 7.2. Creación del Adaptador de Base de Datos (Simulación en Memoria)

Para mantener la simplicidad y no introducir un motor de base de datos complejo (como JPA/Hibernate) en este momento, implementaremos un adaptador que usa un simple mapa de Java (memoria) para simular la base de datos.

#### a. El Adaptador (Implementación del Puerto)

Este adaptador vive en el módulo de **Infraestructura** (`app-infra`).

**Ruta:** `app-infra/src/main/java/com/miempresa/infra/adapter/out/persistence/CuentaRepositoryAdapter.java`

```java
package com.miempresa.infra.adapter.out.persistence;

// Imports de la tecnología (aunque aquí es solo Java, sería JPA, JDBC, etc. en un proyecto real)
import java.util.HashMap;
import java.util.Map;
import java.util.Optional;
import org.springframework.stereotype.Component; // Anotación de Spring para gestión de componentes

// Imports del Core: Solo conoce los objetos del Dominio y la Interfaz del Puerto
import com.miempresa.core.domain.Cuenta;
import com.miempresa.core.domain.Dinero;
import com.miempresa.core.port.out.CuentaRepositoryPort; 

@Component // Con esto, Spring sabrá que esta clase debe ser instanciada y usada
// El Adaptador implementa la Interfaz (el Contrato) del Core
public class CuentaRepositoryAdapter implements CuentaRepositoryPort {

    // Simulación de la base de datos en memoria (ID -> Cuenta)
    private final Map<Long, Cuenta> baseDeDatosSimulada = new HashMap<>();

    // Constructor para inicializar algunas cuentas de prueba
    public CuentaRepositoryAdapter() {
        // Cuentas iniciales
        baseDeDatosSimulada.put(1L, new Cuenta(1L, Dinero.de(1000.00)));
        baseDeDatosSimulada.put(2L, new Cuenta(2L, Dinero.de(500.00)));
    }

    // 1. Implementación del contrato: obtenerCuenta
    @Override
    public Optional<Cuenta> obtenerCuenta(Long id) {
        // En un caso real: aquí iría el código SQL: SELECT * FROM cuentas WHERE id = ?
        
        // Traduce del formato de la "BD" al objeto de Dominio (la Cuenta ya lo es aquí)
        return Optional.ofNullable(baseDeDatosSimulada.get(id)); 
    }

    // 2. Implementación del contrato: actualizarCuenta
    @Override
    public void actualizarCuenta(Cuenta cuenta) {
        // En un caso real: aquí iría el código SQL: UPDATE cuentas SET saldo = ? WHERE id = ?
        
        // Simplemente sobrescribe la cuenta en el mapa
        baseDeDatosSimulada.put(cuenta.getId(), cuenta); 
        System.out.println("LOG: Cuenta " + cuenta.getId() + " actualizada. Nuevo saldo: " + cuenta.getSaldo().getCantidad());
    }
}
```

### 7.3. Confirmación de la Inversión de Dependencia (DIP)

Este es el momento de revisar que el **Principio de Inversión de Dependencia (DIP)** se cumple perfectamente:

| Componente | Depende de... | ¿Conoce la tecnología? |
| :--- | :--- | :--- |
| **TransferenciaService** (Core) | `CuentaRepositoryPort` (Interfaz) | **NO**. Solo conoce el contrato. |
| **CuentaRepositoryAdapter** (Infra) | `CuentaRepositoryPort` (Interfaz) | **SÍ**. Implementa el código de la BD. |

El código de negocio (`TransferenciaService`) está a salvo de los detalles técnicos. Si decidimos cambiar la `baseDeDatosSimulada` por un motor SQL real, solo tendríamos que modificar la clase `CuentaRepositoryAdapter` (y quizás sus dependencias en Maven), **sin tocar ni una línea del Core**.

-----

Ya tenemos todas las piezas:

  * **El Core:** Define la lógica y los contratos.
  * **Adaptador Primario (Web):** Recibe la solicitud y llama al Core.
  * **Adaptador Secundario (BD):** Es llamado por el Core para guardar datos.

El **Paso 8** es el último y crucial: el **Ensamblaje**. Necesitamos una capa de arranque (`app-main`) que le diga a la aplicación: "Oye, cuando el Core pida un `CuentaRepositoryPort` (Interfaz), usa esta implementación concreta: `CuentaRepositoryAdapter`."

¿Continuamos con el **Paso 8**?

<a id="arriba8" href="#arriba7">atrás</a> - Curso de Java de Babull - <a href="#arriba">siguiente</a>  

## 8\. Conexión y Ensamblaje de Componentes (Inversión de Dependencia)

El Ensamblaje es la única capa que **conoce y junta** el **Core** con la **Infraestructura**. Este código vive en el módulo de arranque (`app-main`).

### 8.1. El Rol del Ensamblador (El `Main`)

El Ensamblador (a menudo llamado **Composition Root** en patrones de diseño) tiene dos tareas vitales:

1.  **Instanciar la Infraestructura:** Crear los objetos de los **Adaptadores Concretos** (ej: `CuentaRepositoryAdapter`).
2.  **Inyectar las Dependencias:** Pasar estos adaptadores concretos a los servicios del Core que los necesitan, cumpliendo el contrato de las **Interfaces (Puertos)**.

En un proyecto con **Spring Boot**, el *framework* se encarga de este ensamblaje automáticamente, usando el concepto de **Inversión de Control (IoC)** o **Inyección de Dependencia (DI)**, que es la forma moderna de aplicar el DIP.

### 8.2. Creación del Punto de Arranque con Spring Boot

Necesitamos la clase principal que le dice a Spring dónde buscar componentes y cómo iniciar el servidor web.

#### a. Configuración del Módulo `app-main`

El módulo `app-main` debe depender del `app-core` (para usar el `TransferenciaService`) y del `app-infra` (para usar los adaptadores y las dependencias de Spring Boot).

**Ruta:** `app-main/pom.xml` (Fragmento clave)

```xml
<dependencies>
    <dependency>
        <groupId>com.miempresa</groupId> 
        <artifactId>app-core</artifactId>
        <version>1.0-SNAPSHOT</version> 
    </dependency>
    
    <dependency>
        <groupId>com.miempresa</groupId>
        <artifactId>app-infra</artifactId>
        <version>1.0-SNAPSHOT</version>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter</artifactId>
    </dependency>
</dependencies>
```

#### b. La Clase de Aplicación

**Ruta:** `app-main/src/main/java/com/miempresa/main/Application.java`

```java
package com.miempresa.main;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

// @SpringBootApplication le dice a Spring que esta es la clase principal y que debe
// escanear paquetes para encontrar componentes (@Component, @RestController, etc.).
// Spring escaneará los componentes de app-infra y app-core.
@SpringBootApplication(scanBasePackages = {"com.miempresa.infra", "com.miempresa.core"}) 
public class Application {

    public static void main(String[] args) {
        // Arranca la aplicación, que a su vez inicia el servidor web (gracias a la dependencia web en infra)
        SpringApplication.run(Application.class, args);
        System.out.println("LOG: Aplicación de Arquitectura Hexagonal iniciada en el puerto 8080.");
    }
}
```

### 8.3. ¿Cómo Ocurre la Inyección (El Milagro del DIP)?

Cuando Spring arranca, hace lo siguiente:

1.  **Busca el `TransferenciaController`** (Adaptador Primario en `app-infra`).
2.  Ve que su constructor pide un objeto de tipo **`TransferenciaServicePort`** (la **Interfaz** del Core).
    ```java
    // Adaptador Primario (en app-infra)
    public TransferenciaController(TransferenciaServicePort transferenciaService) { ... }
    ```
3.  Busca una clase que **implemente** esa Interfaz. Encuentra el **`TransferenciaService`** (el Caso de Uso en `app-core`).
4.  Luego, ve que el constructor de `TransferenciaService` pide un **`CuentaRepositoryPort`** (la **Interfaz** de persistencia del Core).
    ```java
    // Caso de Uso (en app-core)
    public TransferenciaService(CuentaRepositoryPort cuentaRepository) { ... }
    ```
5.  Busca una clase que **implemente** esta otra Interfaz. Encuentra el **`CuentaRepositoryAdapter`** (Adaptador Secundario en `app-infra`).
6.  **Ensambla:** Spring crea el objeto `CuentaRepositoryAdapter` y se lo pasa al `TransferenciaService`. Luego, crea el objeto `TransferenciaService` y se lo pasa al `TransferenciaController`.

| Componente (Se inyecta en...) | Tipo requerido (Puerto) | Clase concreta que se inyecta (Adaptador) | Módulo |
| :--- | :--- | :--- | :--- |
| `TransferenciaController` | `TransferenciaServicePort` | $\rightarrow$ `TransferenciaService` | `app-core` |
| `TransferenciaService` | `CuentaRepositoryPort` | $\rightarrow$ `CuentaRepositoryAdapter` | `app-infra` |

### 8.4. Verificación (Test de Integración)

Una vez que la aplicación está corriendo, puedes probarla usando una herramienta como cURL o Postman, enviando una petición HTTP al Adaptador Primario:

| Detalle | Valor |
| :--- | :--- |
| **Método:** | `POST` |
| **URL:** | `http://localhost:8080/api/v1/transferencia` |
| **Cuerpo (JSON):** | `{"origenId": 1, "destinoId": 2, "monto": 250.00}` |
| **Resultado esperado:** | **Código 200 OK** con el mensaje: "Transferencia realizada con éxito." |
| **Resultado en logs:** | Verás el log del `CuentaRepositoryAdapter` confirmando los nuevos saldos. |

-----

### **Conclusión de la Guía**

¡Felicidades\! Has desarrollado tu primer proyecto con la **Arquitectura Hexagonal en Java** desde cero. Hemos cubierto:

1.  **Fundamentos de Java:** Clases, Interfaces y DIP.
2.  **Estructura del Proyecto:** Aislamiento del **Core** e **Infraestructura** con módulos Maven.
3.  **Teoría Hexagonal:** Puertos Primarios y Secundarios.
4.  **Desarrollo del Core:** Entidades (`Cuenta`) y Casos de Uso (`TransferenciaService`).
5.  **Definición de Puertos:** Interfaces (`TransferenciaServicePort`, `CuentaRepositoryPort`).
6.  **Adaptador Primario:** `TransferenciaController` (la entrada web).
7.  **Adaptador Secundario:** `CuentaRepositoryAdapter` (la salida a la BD simulada).
8.  **Ensamblaje:** Conexión de todas las partes usando Spring Boot y la Inyección de Dependencia para aplicar el DIP.

El resultado es una aplicación donde la lógica de negocio (`TransferenciaService`) es completamente independiente de la tecnología (`TransferenciaController` o `CuentaRepositoryAdapter`). Puedes cambiar la web por una consola o la BD por otra, **sin tocar la lógica central del negocio.**

<a href="#arriba8">atrás</a>  - Curso de Java de Babull - <a href="#arriba">volver al inicio</a>
