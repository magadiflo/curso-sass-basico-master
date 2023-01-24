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