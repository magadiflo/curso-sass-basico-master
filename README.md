# [Curso de SASS de básico a master](https://www.youtube.com/playlist?list=PLy7TtEmBFusKPlehbCaSyIl8OA2lf4Krh)
Tomado del canal de **Designicode**

## Instalando SASS
Abrir una terminal y ejecutar el siguiente comando para que se instale a nivel global:
```
npm install -g sass
```

## Ver versión de sass instalada
```
sass --version
```

## Creación del proyecto
Ubicados mediante cmd en la directorio que será nuestro proyecto, ejecutamos el siguiente comando:

    ```
    npm init
    ```
No pedirá los siguientes datos
- nombre del paquete: *sass_course*
- versión: *0.0.1*
- Descripción: *Curso de sass*
- Entry point (index.js): *[no escribimos nada, le damos enter]*
- Test command: *[no escribimos nada, le damos enter]*
- Git repository: *[le damos enter, le agregaremos un repositorio después]*
- Keywords *[no escribimos nada, le damos enter]*
- Autor: *Coloco mi nombre*
- Licencia: *[no escribimos nada, le damos enter]*
- ¿It is OK?: *Presionamos enter*

Con esto nos habrá creado un **package.json**

## Ejecutando proyecto

Con el siguiente comando compilamos el archivo sass a css, y también
hacemos que esté pendiente de los cambios para que en automático lo compile a css
```
npm run sass
```

## Recomendaciones
- Debemos crear hojas de estilos de SASS individuales, para que estos
  solo apliquen a ciertos componentes. Para eso en el directorio 
  /scss podemos crear archivos por ejmplo: /components/tarjeta.scss, 
  luego eso deberían ser importado, de esa manera tendremos separado los
  estilos para cada componente.

---

## @import [deprecado]

Básicamente, **carga miembros (mixins, variables y funciones) dentro de otro módulo.** Las principales diferencias con las nuevas reglas (@use y @forward) es cómo manejan a los miembros. **@import hace que todo sea accesible globalmente en el archivo de destino.** Esto permite una cadena interminable de archivos importados donde es difícil rastrear de dónde provienen sus variables y mixins. También permite la superposición y hace que sea difícil rastrear por qué se rompe su CSS perfecto. Este es un problema especialmente con estructuras de archivos complejas y proyectos con múltiples contribuyentes y bibliotecas globales, **por lo que Sass ya no recomienda @import.** 

**NOTA**
> Se tomó la decisión de [abandonar definitivamente @import](https://www.redradix.com/insights/use-y-forward-en-sass) y los viejos módulos internos de SASS a más tardar el 1 de octubre de 2022.

## @use y @forward

**@use y @forward vienen para reemplazar a @import** y que van a eliminar el ámbito global en el que vivían las utilidades.

Con el nuevo sistema de módulos, cuando un parcial quiera acceder a alguna utilidad tendrá que importarla explícitamente, de manera que tendremos más control y de un simple vistazo sabremos qué código que no pertenece a ese parcial se está utilizando y de dónde viene, algo muy parecido a los import de JavaScript.

## @use

**Se declara al principio del archivo** en el que se quiere tener **acceso a esos miembros (variables, mixins y funciones)** para poder utilizarlos.

Por defecto están encapsulados con el nombre del fichero, de modo que si queremos acceder a la variable **$primary-color de theme.scss,** tendremos que hacerlo como **theme.$primay-color.**

Además, podemos **renombrar los namespaces usando as.**

```css
@use "theme" as defaultTheme;
@use "../3rd-party-library/theme" as externalTheme;

.box {
	color: defaultTheme.$primary-color;
	background-color: externalTheme.$primary-color;
}
```

## @forward

Sirve para traer a un fichero el contenido de otro. Por ejemplo, el índice en el que importamos parciales a través de @import.

Como con @use, tenemos protección ante duplicidad de código si tratamos de llamarlo dos veces pero, a diferencia de éste, @forward no añade namespaces.

```css
// Ajustes generales
@forward "base/reset";
@forward "base/reset"; // no duplicamos código
@forward "base/common";

// Componentes comunes
@forward "../components/";
```

**La regla @forward carga una hoja de estilo Sass y hace que sus mixins, funciones y variables estén disponibles cuando su hoja de estilo se carga con la regla @use.** Hace posible organizar bibliotecas Sass en muchos archivos, al tiempo que permite a sus usuarios cargar un único archivo de punto de entrada.

La regla se escribe @forward "<url>". Carga el módulo en la URL dada como @use, pero hace que los miembros públicos del módulo cargado estén disponibles para los usuarios de su módulo como si estuvieran definidos directamente en su módulo. Sin embargo, esos miembros no están disponibles en su módulo; si lo desea, también deberá escribir una regla @use. ¡No se preocupe, solo cargará el módulo una vez!

```css
// src/_list.scss
@mixin list-reset {
  margin: 0;
  padding: 0;
  list-style: none;
}
```
```css
// bootstrap.scss
@forward "src/list";
```
```css
// styles.scss
@use "bootstrap";

li {
  @include bootstrap.list-reset;
}
```
