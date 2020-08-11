FreeDict.org
===========

Este es el código fuente del sitio web <https://freedict.org>.
Si encuentra errores por favor ...
[diganos](https://freedict.org/community) o envienos una petición o un parche.

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
2.  Si no está familiarizado con Gettext, por favor contactenos a nuestra 
    [lista de correo](https://www.freelists.org/list/freedict) y agregaremos 
    el idiioma para UD. A continuación recivira un fichero ".po".

    Abra el fichero `.po` en un editor de texto. El primer parrafo puede ser ignorado.
    Los parrafos siguientes son los textos que deben ser traducidos. La
    primera linea siemre empieza con un "hash" `#`, por favor ignore está linea y
    no la modifique. La siguiente linea tiene un `msgid` con el texto en
    comillas. Este es el texto en Inglés que sirve de base para la traducción.
    Debajo hay una línea con un `msgstr` y comillas vacias. Coloque la traducción 
    entre las comillas.

    Si ve un texto más largo, como el siguiente:

    ````
    msgid ""
    "This is a long text that contains so little content that it is a hard task"
    "to extend over multiple lines."
    ```

    Su traducción debe ser formateada de la misma manera, especialmente su traducción debe
    empezar con `msgstr ""` y el texto raducido debe ir en la
    siguiente linea.

    Cualquier caracter especial, como `%s` o `\n` debe ser copiado sin modificación alguna.
    Tambien, de ser posible limite la longitud de la linea a 80 caracteres.

    ¡Desde ya gracas por su rtabajo! Envienos por favor su fichero traducido a,
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
-   una version reciente de la API de FreeDict
    -   Si tiene los derechos de acceso, eche una mirada a nuestra wiki
        <https://github.com/freedict/fd-dictionaries/wiki/FreeDict-API> como 
        construir la API más reciente.
    -   Para todos los demás: solo descargue
        <https://freedict.org/freedict-database.json> y coloquelo en el directorio raiz
        de su proyecto (el mismo en el que está el fichero README).

### Construir localmente

Invoking lektor build does require a internet connection to fetch items for the
"news" section. Setting the environment variable DEBUG (to any value) prevents
this. Building with a network connection, a file databags/news.pickle will be
created. Subsequent (DEBUG) runs will make use of this file, avoiding 403 by the
GitHub API.

### Building On The Server

Please see the head of `update_website` for document on the requirements, but in
general, it's enough to execute this script.

Extending
----------


All sites are written in markdown. Please only edit the contents.lr files,
because the contents+LANGCODE.lr files are auto-generated!

Also please do not use "------" for underlining headings, but instead "## TEXT",
because the plugin won't be able to handle dashed headings correctly.

Quirks
------

Some of these below are a repitition of what has been written below, but
sometimes it's better to have a separate section.

-   If you get errors from jinja telling you that `_` wasn't found, something
    went wrong with the Lektor cache. Do a friendly `rm -rf ~/.cache/lektor` and
    re-run.
-   Again, you need the FreeDict API files, namely the freedict-database.json in
    the root of this directory. If you are just testing the design, feel free to
    grab a copy from <https://freedict.org/freedict-database.json>
-   Please don't use dashed markdown headings:

        A Heading
        ---------

    These look very similar to a block delimiter in Lektor. Even though the
    lektor-i18n plugin tris not to interpret these, it might fail. Using `## A
    Heading` is safer.
