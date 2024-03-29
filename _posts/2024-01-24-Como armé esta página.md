---
layout: post
title:  "Cómo armé esta página con Jekyll+Git+GitHub"
---

Este post, que es de hecho mi primer post en esta página, lo estoy usando a la vez de prueba como de tutorial para quienes necesiten desarrollar un sencillo blog personal en GitHub, o incluso para mi mismo si tuviera que repetir el proceso.

Para entender este "how to" es necesario ya tener algún conocimiento de Git y de Github. Asumo que en general, por puro contexto, quien esté leyendo este post conocerá en mayor o menor profundidad. Pero de no ser así, hay vasto y muy buen material para aprender a usar esas maravillosas herramientas.

Jamás había usado Jekyll, pero me gustaron algunas particularidades del framework:

* La idea de tener un blog al estilo Wordpress pero generando un sitio estático, sencillo, fácil de mantener
* Que puediera ser desplegado dentro del propio GitHub, ya que en principio el blog será sobre cuestiones de desarrollo informático.
* Poder redactar posteos en formato *markdown* 

En el proceso de aprendizaje y búsqueda, tuve que decidir entre cuatro maneras de hacer el proceso, que ordeno desde las mas prácticas (y menos personalizables) a las menos prácticas (y mas personalizables)

* Hacer un fork de algún otro proyecto o sitio hecho con Jekyll (licencias mediante) y desde allí, modificar el contenido a mi gusto.
* Utilizar la herramienta de GitHub pages para la creación de una página personal con Jekyll (https://docs.github.com/es/pages/quickstart)
* Desarrollar desde un template de Jekyll en local y luego subirlo a GitHub.
* Desarrollar desde cero un proyecto Jekyll en local y luego subirlo a GitHub.


Después de analizarlo y meter un poco de mano en todas las opciones, decidí hacer uso de la tercera, me interesaba "jugar" con el sitio de manera local, tocar, cambiar, probar cosas de manera muy dinámica, pero tampoco quería embarrarme desde el principio en las cuestiones estéticas o aspectos profundos de diseño web. Además, de esta manera no estamos limitados a utilizar solamente los _temas_ o los _plugins_ que utiliza por defecto [GitHub Pages](https://docs.github.com/es/pages), aunque para quienes necesitan salir del paso rápidamente o no tienen tanta predisposición a "ensuciarse las manos" es una excelente alternativa 

Expongo a continuación los pasos que seguir:

<br>

---
---
---

## Instalar las herramientas necesarias para renderizar y desplegar localmente el sitio:


  **ATENCIÓN: Los pasos que daré son exclusivos para el sistema operativo Debian Linux. Para otros sistemas operativos, [la página oficial de Jekyll](https://jekyllrb.com/) provee la información necesaria y abarca muchos otros aspectos que no serán tratados en este tutorial.**



* Abrimos una terminal y desde allí instalamos las dependencias y los paquetes necesarios utilizando los siguientes comandos:

            sudo apt update
            sudo apt-get install ruby-full build-essential zlib1g-dev
            gem install jekyll bundler
            echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
            echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
            echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc source ~/.bashrc
            gem install jekyll bundler
 
<br>
* Creamos nuestro proyecto de blog:

        jekyll new myblog

Se creará una carpeta *myblog* con todos los archivos necesarios para desplegar el blog

<br>

* Entramos a la carpeta *myblog* (la cual consideraremos de aquí en mas nuestra carpeta raíz o root) y ya podemos desplegar el sitio en forma local

        cd myblog
        bundle exec jekyll serve

Si todo salió bien se nos indicará que el servidor está corriendo, dejaremos esa terminal abierta y aparte para mantener el servidor corriendo, o reiniciarlo cuando sea necesario.
Ahora podemos abrir nuestro blog en el navegador con la siguiente url: http://localhost:4000 se verá algo como esto:

![image](/static/img/first_blog.png)

Excelente, ya tenemos nuestro blog vivito y coleando. Ahora podemos empezar a personalizarlo:



<br>
---
---
---

## Iniciar el control de versiones con Git

Ahora que tenemos el blog funcionando, es un buen momento para instalar el control de versiones.Situados en la carpeta raíz del proyecto ejecutamos:

        git init
        git add .
        git commit -m "Commit Inicial"

De aquí en mas el control de flujo de las versiones queda a criterio y entendimiento de cada uno. Cabe aclarar que desde la creación del proyecto, nuestra carpeta ya tiene configuradas sus correspondientes archivos .gitignore para excluir rutas específicas del seguimiento de Git. Es posible que tengamos que agregar alguna ruta extra vinculada a nuestro editor, en el caso de vscode, sería la carpeta _.vscode/_ 

<br>
---
---
---
## Personalizar los datos del blog

Como comenté anteriormente, uno de los puntos altos de Jekyll es la posibilidad de utilizar  markdown para formatear nuestros posteos o cualquier información visible del sitio. Por supuesto que también puede usarse html y hasta combinar ambos, tal cual sucede con los típicos archivos READ\.ME que solemos escribir en nuestros repos.

Comenzaremos con las cuestiones mas generales y mas estáticas de nuestro sitio, para ello nos dirigimos al archivo __config.yml_ ubicado en el directorio raíz de nuestro proyecto. Las primeras líneas, comentadas con #, nos indican justamente el carácter estático del archivo, donde se configurarán los aspectos globales del sitio, que se supone no deberemos modificar con frecuencia. Nos advierte también que tendremos que reiniciar nuestro servidor para que los cambios se vean reflejados en el sitio, cosa que no sucederá luego con el contenido variable de la página, como por ejemplo, los posteos. 
Unas líneas mas abajo ya aparecen parámetros que podemos empezar a personalizar:

        title: Your awesome title
        email: your-email@example.com
        description: >- # this means to ignore newlines until "baseurl:"
        Write an awesome description for your new site here. You can edit this
        line in _config.yml. It will appear in your document head meta (for
        Google search results) and in your feed.xml site description.
        baseurl: "" # the subpath of your site, e.g. /blog
        url: "" # the base hostname & protocol for your site, e.g. http://example.com
        twitter_username: jekyllrb
        github_username:  jekyll

Aquí no hay mucho secreto, ya que cada línea nos viene con una explicación de cuál es su funcionalidad, es cuestión de cambiar los datos por los que nosotros querramos que se muestren en el blog, por ejemplo:

        title: El blog de Pablo Alí
        email: pavloali@gmail.com
        description: >-
        Crear, desarrollar, pensar, divertirse e innovar
        baseurl: ""
        url: "http://pabloaliargentina.github.io"
        #twitter_username: jekyllrb
        github_username:  pabloaliargentina

Nótese que mientras quité los comentarios en las líneas para mayor claridad, por otro lado comenté la línea de twitter_username, ya que no quiero mostrar esa información. Una vez realizados los cambios guardamos el archivo.

Ahora vamos a la terminal donde está corriendo nuestro servidor local.
Detenemos el servidor presionando CRTL+C
Y lo volvemos a arrancar con:

        bundle exec jekyll serve

Nos fijamos por las dudas si el servidor no encontró errores, si todo va bien, nuestro blog debería haber cambiado.

![image](/static/img/first_blog_01.png)

Ahora nos situamos arriba a la derecha y hacemos click en _about_

Nos aparecerá algo como esto:

![image](/static/img/first_blog_about.png)

Ahora nos dispondremos a generar nuestro propio _about_. Abrimos el archivo about.markdown en la raíz de nuestro proyecto.

Nos encontramos en las lineas iniciales una sección encasillada entre tres lineas consecutivas:

        ---
        layout: page
        title: About
        permalink: /about/
        ---

este encabezado se llama bloque _front matter_ y permite definir variables que le servirán al render para crear nuestro sitio, lo volveremos a ver mas adelante.
Por ahora nos limitaremos a reescribir la linea

        title: About

por

        title: Acerca de mi. 

Mas abajo estará el cuerpo del texto que querramos escribir. Podemos ver ya algunas líneas con caracteres especiales de markdown. No entraremos en detalle acerca de Markdown, hay suficiente información en la web para aprender a utilizarlo convenientemente.
Borramos todo ese texto y lo reescribimos a nuestro antojo. Finalmente guardamos el archivo y vamos al navegador a recargar la página, notando los cambios efectuados.
Nótese que en esta ocasión, no tuvimos necesidad de reiniciar el servidor, ya que automáticamente detectó los cambios y volvió a renderizar el sitio.

![image](/static/img/first_blog_about_01.png)

Ya tenemos personalizados los datos del blog, Por supuesto que quedan muchas cosas por mejorar, sobre todo referidas al estilo de la página, pero por ahora dejaremos eso para mas adelante, ahora toca dar el siguiente paso.

<br>
---
---
---
## Escribir el primer posteo

Bueno, ahora toca la parte mas divertida, que es empezar a publicar posteos. Ya que esta será la tarea mas frecuente, uno esperaría que también sea la mas sencilla, y por suerte lo es.
Vayamos ahora a la carpeta _/\_posts/_
Allí nos encontraremos con un archivo con extensión markdown, que es ni mas ni menos que el archivo que genera el post de ejemplo de nuestro sitio: "Welcome to Jekyll". Si hacemos click en el enlace dentro del blog, nos llevará a mostrarnos el posteo asociado a esa entrada.
De aquí en mas, cada posteo que querramos subir al blog consistirá simplemente en escribir un nuevo archivo .md o .markdown dentro de esta carpeta. El nombre de ese archivo debe tener el formato

AAAA/MM/DD-título.md.

En mi caso, el archivo de ejemplo es:

_2024-01-24-welcome-to-jekyll.markdown_

Al abrirlo nos volvemos a encontrar con el encabezado o _front matter:_

        ---
        layout: post
        title:  "Welcome to Jekyll!"
        date:   2024-01-24 11:30:25 -0300
        categories: jekyll update
        ---

Nuestros posts deberán replicar al menos las variables layout y title para mostrarse correctamente en el blog. El resto del archivo es ni mas ni menos que el cuerpo de texto de nuestro posteo.
Con esto en mente, hagamos nuestro propio posteo, creando un archivo nuevo, por ejemplo:

_2024-01-24-El-primer-post\.md_


_NOTA: Se recomienda utilizar algún editor de texto con soporte para archivos markdown, a fin de tener una vista previa en tiempo real de lo que se está escribiendo, en mi caso uso el propio vscode que ya tiene incorporada esa funcionalidad_

Dentro de nuestro archivo escribimos lo siguiente:

        ---
        layout: post
        title: El Primer Post
        ---

        # Y finalmente lo hemos logrado, tenemos nuestra primera publicación en el blog!!!!!

        O al menos eso es lo esperado...

Guardamos los cambios.

Aprovechamos y renombramos el archivo de ejemplo agregándole un carácter "_" al principio, nos quedaría: _2024-01-24-welcome-to-jekyll.markdown

Y ahora recargamos nuestra página

![image](/static/img/first_post_link.png) 

Nótese que el posteo de ejemplo ya no está en la lista, debido a que renombramos el archivo en cuestión.
Ahora  click en el enlace a nuestro post y...

![image](/static/img/first_blog_post.png)

Voilá! Nuestro primer post está publicado.

Sin embargo, hay algo ahí que me molesta un poco, la verdad que por el momento no quiero ver esa leyenda de "suscribe via RSS" al final del listado de entradas. No fue fácil dar con la solución a esta cuestión, pero de esa búsqueda, como suele suceder, aprendí mas a fondo cómo funcionan los _temas_ de Jekyll, y como se pueden personalizar hasta el último detalle. Dentro de nuestras carpeta de usuario, nuestro /home, hemos instalado una carpeta _/gem_ que contiene mucha información que nuestro framework usa para construir el blog. En mi caso particular (porque eso puede depender de la versión que se tenga instalada y del sistema operativo) me voy a referir a la carpeta 

_'usuario'/gems/gems/minima-2-5-1/\_layouts/_

Allí se encuentran algunos archivos _html_ que constituyen las plantillas básicas sobre las que se formará el sitio web. Podríamos simplemente editar el archivo necesario para quitar nuestra molesta línea de suscripción, pero ese cambio sólo aplicaría a nuestro sitio local, sin efecto alguno cuando subamos la página a GitHub. La solución consistirá entonces en copiar primero esta carpeta en nuestro proyecto, y ahí si, entonces, modificar lo necesario. Nos posicionamos en la carpeta raíz del proyecto y desde allí hacemos:

        cp ~/gems/gems/minima-2.5.1/_layouts/ .

Se creará la carpeta _/\_layouts_ en nuestro proyecto con algunos archivos .html.
Nos dirigimos al archivo _home.html_ y encontraremos una línea de código similar a ésta:


    <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | relative_url }}">via RSS</a></p>

simplemente la borramos o la comentamos por si decidimos utilizarla mas adelante.
Salvamos los cambios y ya que estamos, agregamos este mismo posteo al directorio, para ver la página un poco mas rellenita.
Nos queda así:

![image](/static/img/first_blog_02.png)

¡Bien hecho! Estamos en condiciones de dar otro paso importante.


<br>
---
---
---

## Crear un repositorio en GitHub y subir nuestro blog.

Con lo hecho hasta acá, estaríamos en condiciones entonces de subir nuestra primera versión potable del nuestro sitio. Empecemos por actualizar nuestro repo con git en local:

        git add .
        git commit -m "Listo para subir"

---
<br>
Ahora nos toca crear el repositorio en github.
Entramos en nuestro GitHub y [armamos un repositorio nuevo](https://github.com/new).

**ATENCIÓN: El nombre del repositorio tiene que ser exactamente así:** 

_nombre_de_usuario.github.io_

GitHub nos proveerá de esta manera el dominio https://nombre_de_usuario.github.io para nuestro blog. Aunque si disponemos de un dominio propio luego podremos utilizarlo también.

En mi caso sería, entonces:

 _pabloaliargentina\.github.io_

 ![image](/static/img/create_repository.png)

Agregamos una descripción de nuestro agrado y dejamos el resto como tal cual está.
Vamos abajo a la derecha y pulsamos en el botón _"crear repositorio"_ 

Una vez creado el repositorio, GitHub nos brindará el enlace para usar en git a efectos de subir nuestro sitio: En mi caso uso autenticación SSH, así que la elijo y copio el nombre del repositorio.

Ahora vamos desde la consola a la raíz de nuestro proyecto y ejecutamos los comandos git necesarios para hacer la subida:

        git remote add origin git@github.com:PabloAliArgentina/pabloaliargentina.github.io.git
        git branch -M main
        git push -u origin main

Si todo salió bien, nuestros archivos estarán ya en el repositorio de GitHub

---

Nos toca ahora configurar GitHub, para que renderice nuestro blog cada vez que hagamos un cambio, para ello dentro de nuestro proyecto en GitHub vamos al botón _"Settings"_

En la siguiente página vamos a _Pages ->  Build & Deployment -> Source -> GitHub Actions_ 

![image](/static/img/setting_actions.png)

Y luego hacemos click en _"Browse all workflows"_


En la barra de búsqueda ponemos _Jekyll_ iniciamos la búsqueda, y nos quedaremos con la opción Jekyll (a secas). Le damos click a configure

![image](/static/img/setting_actions_workflow.png)

Y en la siguiente página, sin alterar nada, le damos al botón verde de _"Commit Changes"_

![image](/static/img/actions_commit.png)

Confirmamos el commit en la ventana emergente y veremos que nos creó un archivo jekyll.yml que son las instrucciones para el deploy automático de nuestro blog.

Ahora volvemos a la página de nuestro repositorio en GitHub y veremos a la derecha una sección _"Deployments"_ y debajo el texto _"github-pages"_

![images](/static/img/deployment_display.png)

Si todo marchó bien, estará con un tilde color verde, caso contrario, veremos una X roja. Para ver los detalles del deployment podemos hacerle click y nos llevará a otra pantalla donde podemos ver los detalles.

En caso positivo, nuestro blog debería estar finalmente operativo, esto puede tardar desde unos pocos segundos hasta algunos minutos, en mi caso fue casi automático.

Abrimos otra pestaña y escribimos la url de nuestro blog, en mi caso:

https://pabloaliargentina.github.io

![imagen](/static/img/first_blog_online.png)

y finalmente nuestro blog ya está online!

Ahora podemos escribir nuevos posts creando nuevos archivos en la carpeta _/\_posts_ de nuestro repositorio, ya sea desde la página de GitHub, o desde nuestra copia local con su posterior push al repositorio. Nuestra _Action_ se pondrá en marcha automáticamente y en pocos segundos el blog estará actualizado.

Creo que hasta acá este tutorial ha hecho suficiente. En breve empezaré a hacer cambios al blog e iré mostrando en una segunda parte cómo es ese proceso. Espero que esta info resulte util para alguien y de ser así, se agradece cualquier feedback, sobre todo si es para corregirme errores o sugerir apuntes pero también para sumarle una estrellita al [repo](https://github.com/PabloAliArgentina/pabloaliargentina.github.io)
