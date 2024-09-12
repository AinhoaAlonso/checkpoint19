# CHECKPOINT 19

# ¿Qué es Redux?

Redux en sí es independiente de la interfaz de usuario: puedes usarlo con cualquier capa de interfaz de usuario (React, Vue, Angular, vanilla JS, etc.) o sin ninguna interfaz de usuario.

Dicho esto, Redux se usa más comúnmente con React. La biblioteca React-Redux es la capa de enlace de interfaz de usuario oficial que permite que los componentes de React interactúen con una tienda Redux leyendo valores del estado de Redux y enviando acciones. Por lo tanto, cuando la mayoría de las personas se refieren a "Redux", en realidad quieren decir "usar una tienda Redux y la biblioteca React-Redux juntas".

React-Redux permite que cualquier componente React de la aplicación se comunique con la tienda Redux

Su propósito principal es proporcionar un contenedor predecible del estado de la aplicación, lo que facilita la gestión y sincronización del estado a lo largo de toda la aplicación.

>
>
>**Redux es un patrón y una biblioteca para administrar y actualizar el estado de la aplicación mediante eventos denominados "acciones"**. Funciona como un almacén centralizado para el estado que se debe utilizar en toda la aplicación, con reglas que garantizan que el estado solo se pueda actualizar de manera predecible.
>**Redux le ayuda a gestionar el estado "global"**, es decir, el estado que se necesita en muchas partes de su aplicación.
>**Los patrones y herramientas proporcionados por Redux facilitan la comprensión de cuándo, dónde, por qué y cómo se actualiza el estado de su aplicación, y cómo se comportará la lógica de su aplicación cuando se produzcan esos cambios.**

### ¿Por qué usar Redux?
Cuando creamos aplicaciones en React, éstas se organizan como una serie de componentes anidados, su naturaleza es funcional. En otras palabras reciben información a través de sus argumentos (props) y pasan la información a través de sus valores de retorno y a esto se le llama: one-way binding, los datos sólo se transmiten de los componentes a sus hijos:
![](https://miro.medium.com/max/367/1*ZiO5GjYS43uzbrJezNwl7w.jpeg)

#### React sin Redux
Entonces, imaginemos que en nuestro componente D tenemos un input que almacena cierta información en un estado. Esta información estará disponible para todo el componente D y sus hijos, ¿pero qué pasaria si necesitamos que esa información también esté presente en el componente E?
![](https://miro.medium.com/max/367/1*80noTHl0f_GsuptOp9IeyA.jpeg)

Una solución sería declarar el estado en el componente B (padre), de esa forma tendremos acceso a la información desde el componente D y E (hijos):
![](https://miro.medium.com/max/367/1*rwFsVl7k9LvxF-3AIFSJlQ.jpeg)

Siguiendo la misma lógica, ¿qué pasaría si necesito tener acceso a esa información en toda mi aplicación? Bueno, entonces declaro el estado en el padre de todos los componentes:
![](https://miro.medium.com/max/367/1*sjgMqU03KTZn0ydPJ3GbBg.jpeg)

Cuando estés aprendiendo React, hacerlo así es una buena forma de entender cómo funcionan los props y los componentes, pero no es una práctica que quieras repetir para proyectos grandes,

#### React con Redux
Entonces, necesitamos tener toda esa información en un solo lugar, para que pueda estar disponible en todos nuestros componentes, algo como nuestra única fuente de la verdad:
![](https://miro.medium.com/max/525/1*laMKJPicQQeL6M0Dly_MIg.png)

Teniendo toda esa información en nuestros estados Redux todos nuestros componentes tendran acceso a la misma información en todo momento.

Más arriba mencionamos que Redux es un patrón de arquitectura y vimos a Redux como una caja azul que almacena los estados. Veamos ahora qué tenemos dentro de nuestra caja azul y cómo funciona:
![](https://miro.medium.com/max/730/1*hr7tJuwlM4aykoqM6yHp7A.png)

1. Tenemos unComponent que va a emitir un Action, que pueden ser llamadas por algún evento: un click, por ejemplo.
2. El Action pasa al Store que es donde se guardan todos los estados.
3. El Store comunica al Reducer el estado actual y cual fue el Action que se ejecutó.
4. Luego, el Reducer retorna un nuevo estado modificado por la acción que se acaba de ejecutar.
5. El estado se actualiza en el Store.
6. Y el Store devuelve el nuevo estado modificado al componente.

### Ventajas
- Redux te da una arquitectura consistente (la interfaz de usuario despacha acciones, los reductores aplican actualizaciones de estado, la interfaz de usuario se vuelve a renderizar, siempre sabes que debes buscar en la lógica del reductor para entender qué estado se está utilizando y cómo se puede actualizar)
- Escribir más código de tu aplicación como funciones puras predecibles hace que sea más fácil de entender y probar
- Redux es ampliamente utilizado y bien documentado
- Las Redux DevTools te ayudan a visualizar lo que ha sucedido en tu aplicación y cómo el estado ha cambiado con el tiempo
- Redux Toolkit hace que escribir código Redux moderno sea mucho más simple e incluye la capa de obtención de datos RTK Query
- Mejor comprensión de la evolución del estado en un momento dado
- Facilidad para incorporar nuevas características a la app
- Mejoras en el proceso de desarrollo, pudiendo reiniciar la ejecución a partir de un estado concreto.

### Desventajas
- Redux (y React) funcionan bien para el 80% de los casos de uso, pero nunca serán las herramientas más rápidas en absoluto

# ¿Qué es un HOC? 
Un HOC (Higher-Order Component) es una función que toma un componente y devuelve otro componente con funcionalidades adicionales o modificadas.
Los HOCs no forman parte del API de React, si no que son un patrón muy útil para programar con este framework dada su arquitectura.

### Ventajas
- **Reutilización de lógica:** Puedes aplicar la misma lógica a múltiples componentes sin duplicar el código.
- **Separación de responsabilidades:** El HOC puede encargarse de manejar la lógica adicional (autenticación, logs, etc.), mientras que el componente original se centra en la interfaz de usuario.
- **Composición:** Puedes combinar varios HOCs para añadir distintas funcionalidades.

##### Casos de uso comunes:
- Autenticación de usuarios.
- Manejo de errores.
- Validación de permisos.
- Registro de eventos o estadísticas.

### Problemas comunes
- **Problemas con el paso de propiedades (props)**
Los HOCs dependen en gran medida de pasar las propiedades (props) al componente envuelto. Si un HOC no maneja correctamente las propiedades que recibe o si sobrescribe accidentalmente alguna propiedad importante, puede ocasionar problemas inesperados. Además, puede ser confuso seguir qué propiedades vienen del HOC y cuáles son del componente original.
- **Difícil depuración**
Los HOCs pueden dificultar la depuración de problemas. Cuando el componente está envuelto por varios HOCs, puede ser difícil entender cuál de ellos está causando un error o afectando el comportamiento. Esto se debe a que, al inspeccionar el código o el árbol de componentes, el componente original está escondido dentro de varios componentes envueltos.
- **Inyección de refs**
Los HOCs no manejan bien las refs (referencias a elementos del DOM o componentes). Si necesitas pasar una ref a un componente envuelto por un HOC, la ref no funcionará directamente porque los HOCs no pasan las referencias por defecto. 


# ¿Qué es Heroku? 
Es una plataforma que ofrece soluciones sólidas para alojar y desplegar aplicaciones web.

### Alternativas
| |Heroku | Vercel | Render|
|---|---|---|---|
|Opciones de precios | No tiene versión gratuita | Versión free con limitaciones | Versión free con limitaciones|
|Frameworks| Soporta cualquier framework backend (Node.js, Ruby, Python)|Soporta frameworks frontend (Next.js, React, Vue.js, etc.)| Soporta backend y frontend (Node.js, Python, Ruby, etc.)|
|Almacenamiento|Depende de servicios externos y complementos para muchas funcionalidades, como bases de datos, almacenamiento en caché y monitoreo.| Servicios externos como PlanetScale | PostgreSQL autoadministrado y Redis|
|Deploy automático| Sí (repos GitHub, GitLab, y Bitbucket)|Sí (repos GitHub, GitLab, y Bitbucket)|Sí (repos GitHub y GitLab)
|Soporte| Ofrece opciones de soporte más completas, incluyendo niveles premium con soporte dedicado.| Ofrece soporte a través de foros y correo electrónico |Soporte limitado, principalmente a través de documentación y comunidad |
|Conexión a APIs|Sí, sin limitaciones (ideal para API RESTful y GraphQL)|Sí, pero principalmente para frontend o funciones serverless|Sí, sin limitaciones (ideal para API RESTful y GraphQL)|
|Dominios personalizados| Si| Si| Si|
|Fortalezas| Versatilidad y flexibilidad, permitiendo a los desarrolladores construir y desplegar aplicaciones en varios lenguajes y marcos, además de proporcionar un ecosistema extenso de complementos para mejorar la funcionalidad.| Simplicidad y velocidad de despliegue, con una integración estrecha con Git y capacidades de escalado automático que aseguran un rendimiento óptimo para proyectos centrados en el frontend.|Especialmente diseñado para frameworks de frontend como Next.js, proporcionando características que mejoran el rendimiento y la experiencia de desarrollo.|

##### Resumen por plataforma:
- **Heroku:** Heroku ya no tiene plan gratuito, lo que limita su uso a planes pagos. Fué una opción sólida para aplicaciones backend y full-stack con soporte para una amplia gama de lenguajes y frameworks, pero ahora requiere un plan pago para acceso y uso continuo.

- **Vercel:** Enfocado principalmente en aplicaciones frontend y frameworks como Next.js. Es ideal para sitios estáticos y funciones serverless, con despliegue continuo, pero está más limitado para proyectos full-stack. No tiene tiempos de suspensión en el plan gratuito.

- **Render:** Proporciona un entorno full-stack más flexible, con capacidades tanto para frontend como backend. Ofrece almacenamiento persistente y bases de datos (aunque pagas), pero entra en modo "sleep" tras 15 minutos de inactividad en el plan gratuito.

##### Otras alternativas
Además de las plataformas comparadas, existen otras alternativas con planes gratuitos como Railway, Netlify, Firebase,...
