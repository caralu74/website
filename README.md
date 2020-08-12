FreeDict.org
===========

Este es el código fuente del sitio web <https://freedict.org>.
Si encuentra errores por favor ...
[díganos](https://freedict.org/community) o envíenos una petición o un parche.

Estamos buscando traductores. No es demasiado trabajo y el sitio web no
cambia con mucha frecuencia. Si puede traducirlo a algún otro idioma diferente a los listados al final de 
<https://freedict.org>, Considere por favor traducir la página para nosotros.

Discusiones tienen lugar en nuestra Wiki:

https://github.com/freedict/fd-dictionaries/wiki/Website-migration-to-Lektor

Traducciones de la página web
-----------------

Apreciaríamos su ayuda para traducir nuestra página web. No es mucho trabajo
y las actualizaciones son menores. Hay dos maneras de abordar esto:

1.  Si está familiarizado con Gettext,  ...por favor, entregue una petición. Añada su idioma
    tanto en [freedict-org.lektorproject](freedict-org.lektorproject) como en
    [configs/i18n.ini](configs/i18n.ini) e intente construir usando "Lektor build".
    Si no puede proceder, siéntase libre de enviarnos un [E-mail]
    (https://www.freelists.org/list/freedict) y arreglaremos
    las cosas  para UD. 
2.  Si no está familiarizado con Gettext, por favor contáctenos a nuestra 
    [lista de correo](https://www.freelists.org/list/freedict) y agregaremos 
    el idioma para UD. A continuación recibirá un fichero ".po".

    Abra el fichero `.po` en un editor de texto. El primer párrafo puede ser ignorado.
    Los párrafos siguientes son los textos que deben ser traducidos. La
    primera linea siempre empieza con un "hash" `#`, por favor ignore está línea y
    no la modifique. La siguiente linea tiene un `msgid` con el texto en
    comillas. Este es el texto en Inglés que sirve de base para la traducción.
    Debajo hay una línea con un `msgstr` y comillas vacías. Coloque la traducción 
    entre las comillas.

    Si ve un texto más largo, como el siguiente:

    ````
    msgid ""
    "This is a long text that contains so little content that it is a hard task"
    "to extend over multiple lines."
    ```

    Su traducción debe ser formateada de la misma manera, especialmente su traducción debe
    empezar con `msgstr ""` y el texto traducido debe ir en la
    siguiente linea.

    Cualquier carácter especial, como `%s` o `\n` debe ser copiado sin modificación alguna.
    También, de ser posible, limite la longitud de la línea a 80 caracteres.

    ¡Desde ya gracias por su trababajo! Envíenos por favor su fichero traducido a,
    nuestra [lista de correo](https://www.freelists.org/list/freedict).
3.  Use una herramienta como [Poedit](https://poedit.net/download) que le ayudara en el proceso
    de traducción.

Construcción
--------

Está generador de la página web depende de lo siguiente:

-   Python >= 3.4
-   gettext utilities
-   pybabel
-   Pandoc
-   Lektor; en Debian/Ubuntu use `apt install lektor` o `pip3 install lektor`
-   una versión reciente de la API de FreeDict
    -   Si tiene los derechos de acceso, eche una mirada a nuestra wiki
        <https://github.com/freedict/fd-dictionaries/wiki/FreeDict-API> como 
        construir la API más reciente.
    -   Para todos los demás: solo descargue
        <https://freedict.org/freedict-database.json> y colquelo en el directorio raíz
        de su proyecto (el mismo en el que está el fichero README).

### Construir localmente

Invocar lektor build requiere de una conección a internet para buscar artículos para 
la sección de "noticias". Ajustar la variable de entorno DEBUG (a cualquier valor) impide
esto. Al construir con una conexión a internet, se creara el fichero databags/news.pickle 
Las ejecuciones posteriores (DEBUG) harán uso de este archivo, evitando UN 403 por la
API GitHub.

### Construir en el servidor.

Vea por favor el encabezado `update_website` para documentarse sobre los requerimientos, pero en 
general, es suficiente con ejecutar este script.

Ampliando
----------


Todos los sitios están escritos en markdown. ¡Por favor edite solamente los ficheros contents.lr,
ya que los ficheros contents+LANGCODE.lr son auto generados!

También por favor no use "------" para subrayar encabezados, sino "## TEXT",
porque el plugin no será capaz de manejar correctamente los encabezados subrayados.

Particularidades
------

Algunos de estos a continuación son una repetición de lo que se ha escrito más abajo, pero
a veces es mejor tener una sección separada.

-   si tiene un error de jinja diciéndole que `_` no fue encontrado, algo 
    salio mal con la cache de Lektor. Hafa un amistoso `rm -rf ~/.cache/lektor` y 
    vuelva a correrlo.
-   De nuevo, Ud necesita los ficheros de la API de FreeDict, a saber freedict-database.json en
    el directorio raíz. Si solo está probando el diseño, siéntase libre de 
    obtener una copia de <https://freedict.org/freedict-database.json>
-   Por favor no use subrayados markdown en los encabezados:

        A Heading
        ---------

    Estos se ven muy similares a un delimitador de bloques en Lektor. Aunque el
    plugin lektor-i18n intenta no interpretar esto, podría fallar. Usar un
    `## A Heading` es más seguro.
