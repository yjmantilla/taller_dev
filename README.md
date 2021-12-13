# taller_dev

hola
Este es el repositorio del taller de fecha 12 de Nov.


Los temas que vamos a tratar son los siguientes: 


Para grabar compartir pantalla en un google meet y grabar microfono
Cuando haya voluntarios, que ellos compartan pantalla.

Parte 1: 8 a 11

Break: 11 a 1

Parte 2: 1 a 4

Uso de visual code
    iniciar con conda: https://stackoverflow.com/questions/50360460/how-to-start-visual-studio-code-within-anaconda-env
    python extension
        select interpreter
    debugging
        just my code
        debug console
Git
    crear repositorio
        que nombre?
        publico o privado?
        gitignore --> usar el de python, ver que es lo que contiene
        para que el readme al inicio?
        link para clonar
    git bash for windows
        bashrc y profile
            crear .bashrc y .profile
            https://stackoverflow.com/questions/54501167/anaconda-and-git-bash-in-windows-conda-command-not-found
            . /c/Anaconda3/etc/profile.d/conda.sh
        winpty
            https://stackoverflow.com/questions/32597209/python-not-working-in-the-command-line-of-git-bash
            alias python='winpty python.exe'
        clonar repo
    abrir repo en vscode
    crear archivo fun.py (con una funcion inutil que solo imprima algo) para las funciones
        add
        commit
            yo lo pienso como que el commit empaqueta cambios con un mismo proposito y bajo un comentario que resuma cual es este.
            sin embargo lo pueden encontrar mas como guardar localmente una version del proyecto con esos cambios
            https://www.freecodecamp.org/espanol/news/el-comando-git-commit-explicado/
            
            Tambien se puede entender desde la diferencia entre el working directory y el staging directory.
            El working directory es el directorio en si donde continuamente estas trabajando en el codigo.
            
            El staging directory contiene solo los cambios que tu de verdad quieres en el proyecto. Este directorio va acumulado "commits" y va creando la historia
            de tu proyecto, cada commit representando un snapshot (una foto) del proyecto en ese momento.
            
            Por lo tanto, mientras mas atomicos los commits, mas control sobre a que punto del proyecto podrias volver en un futuro. Aunque siempre hay un balance para  no hacer un commit por cambios demasiado pequeños.
            
            En ese sentido, yo lo pienso como el conjunto de cambios que tienen un solo proposito son buenos para constituir un commit.
            
            https://www.gitkraken.com/learn/git/commit
            
        push
    dentro de github web añadir algo al readme
        pull dentro de visual code
    
Trabajo colaborativo
    fork: cada quien lo hace
    clone de SU fork a su pc
    asociar original y fork
        git remote -v
        git remote add upstream https://github.com/sappelhoff/pyprep
        git remote -v para checkear
        git pull upstream main para tener la ultima version del original
    crear una rama para trabajar
        git checkout -b nombrerama

    Funciones:
        Reto: Construir todo sin importar ninguna libreria auxiliar

        Division
        Multiplicacion
        n multiplos de un numero (142857)
        Potencia
        Factorial
        sumatoria
        productoria
        Promedio
        Maximo
        Minimo
        Valores Unicos de una lista
        N numero de fibonacci
        collatz
        recaman

    Cada quien hace un pull request, necesito un voluntario para mostrar el proceso
        hacer push a su fork
            probablemente en este punto haya problemas de login
                Configuracion del token
                    https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token
                    Configuracion de la cuenta
                        Developer settings
                            Personal Access Tokens
                                Agregar una nota
                                definir los dias
                                dar todos los permisos
                                copiar el token
                                Cuando se haga una operacion de git pedira login y se usa el username y luego el token como password
        pull request
            porque se llama asi
            como hacerlo
            el pull request desde el punto de vista del original
                comentarios y sugerencias de cambio
    
    Los demas probablemente necesiten hacer un rebase
        rebase
            https://github.com/sappelhoff/pyprep/blob/master/.github/CONTRIBUTING.md
            git checkout main
            git pull upstream main
            git checkout my_feature
            git rebase master
                Arreglar los conflicts...

Cuando todos hayan agregado su funcion al main se sigue...
Pero cada quien trabaja en su fork durante lo que viene, para que apliquen directamente...

A partir de ahora a medida que voy haciendo cambios, mostrar como uso git desde visual code... Quizas ellos deban instalar una extension. Not sure.


Estructuración de paquetes (instalables) en python
    Mostrar ejemplo de estructuracion de sklearn
    https://github.com/scikit-learn/scikit-learn
        repo
            paquete
            docs
            examples
            test
    Se replica este proceso cada quien por su parte, llaman el paquete como prefieran.
        paquete
            fun.py
        
        Probar importacion un nivel afuera (si funciona porque es relativa), cada quien usa su funcion
            paquete
                fun.py
            usar_paquete.py
                from paquete.fun import mifuncion
            Run usar_paquete.py con run python file terminal, con la consola parada en el root del repo
            este import es relativo, entonces no hay problemas
        
        Probar carpeta de test (toca path hack primero)
            Suponiendo que queremos hacer un test, se crea la carpeta de tests
            
            repo
                paquete
                    fun.py
                test
                    tests.py
                        from paquete.fun import mifuncion
                usar_paquete
                
            mismo RUN , esta vez deberia fallar, porque?
                se puede usando import relativo o patch hacks
                o volverlo un verdadero paquete de python
                
                PATHACK
                    tests.py
                        import sys
                        sys.path.insert(0, os.path.abspath('..'))
                        
                    porque no funciona? falta agregar un punto
                    
                    tambien probar con import relativo
                    
                    from ..paquete import fun.py
                    
                    
            Bueno ya funciona. Entonces... pero es un paquete?
                NO
                
                probar importarlo como numpy por ejemplo
                
                import paquete as pq
                
                print(pq.fun.mifuncion)
                
                pq.fun.mifuncion(x)
                
                funciona? no, porque todavia es un paquete.
                
            agregar __init__.py
                repo
                    paquete
                        __init__.py
                        fun.py

            funciona? NO ,todavia falta que reconozca el modulo de fun
            El __init__.py expone las partes de nuestro paquete al usuario
            https://github.com/numpy/numpy/blob/main/numpy/__init__.py como ejemplo
            
                repo
                    paquete
                        __init__.py
                            from . import fun
            
            
            volver a probar print(pq.fun.mifuncion), si deberia funcionar
            
            
            
        Volverlo un verdaro paquete instalable de python (setup.py)
        
        Se crea setup.py en el root del repo (al mismo nivel de la carpeta del paquete)
        
            repo
                paquete
                    fun.py
                setup.py
                    from setuptools import setup

                    setup(name='funniest',
                          version='0.1',
                          description='The funniest joke in the world',
                          url='http://github.com/storborg/funniest',
                          author='Flying Circus',
                          author_email='flyingcircus@example.com',
                          packages=['funniest'], # este es el nombre de la carpeta del paquete)
                          
            instalarlo
                parar la consola al mismo nivel que setup.py
                para no ensuciar el environment base crear un nuevo environment
                    conda create -n example python=3.9
                    conda activate example
                pip install .
                pip freeze
                
                
            Prueba usar paquete desde fuera de ese repositorio pero con el mismo environment
            
            Crear un archivo suelto .py que lo importe
            usarlo, deberia funcionar, el environment se debe activar
            posiblemente se necesite select interpreter:
                ctrl shift p --> select python interpreter , dar click en el nuevo environment para correrlo con RUN
            
            
            editar tu funcion para que imprima tu nombre al final de esta
            volver a probarlo desde fuera, los cambios se hacen ? NO
            
            se debe instalar en modo editable
            
            en el environment
                pip uninstall paquete
                pip install -e .
                probar con el archivo.py desde afuera
                hacer cambio de imprimir luego del nombre la edad
                volver a probar con el archivo .py desde afuera, deberia detectar el cambio
            
            EL MODO EDITABLE ES MUY UTIL SI ESTAS DESARROLLANDO.



Estandares de documentación de codigo
    el docstring
        el docstring no solo existe en el codigo sino como objeto dentro de python
    la funcion help retorna el docstring de un objeto
    
    numpy : https://numpydoc.readthedocs.io/en/latest/example.html#example ,https://numpydoc.readthedocs.io/en/latest/format.html#docstring-standard
    google : https://google.github.io/styleguide/pyguide.html#Comments
    
    comparacion : https://www.sphinx-doc.org/en/master/usage/extensions/napoleon.html?highlight=numpy
    The main difference between the two styles is that Google uses indentation to separate sections, whereas NumPy uses underlines.
    
    
    
    Ejercicio : Cada quien realiza el docstring de su funcion y lo sube a SU fork
    
    luego en un archivo.py le aplica el help(mifuncion)
    
- Estándares de estilo de código
    
    PEP8
        What is PEP 8
            https://siderlabs.com/blog/about-style-guide-of-python-and-linter-tool-pep8-pyflakes-flake8-haking-pyling-7fdbe163079d/#:~:text=to%20use%20flake8-,What%20is%20flake8,configuration%20file%20such%20as%20pep8.

            Before I explain about how to use pep8, I explain what is PEP 8.

            python has document group called PEP

            This is an aggregate of documents which explains about information, new features, process and environment settings for python community.

            Document №8 is PEP 8 — Style Guide for Python Code.

            As the title “Style Guide”indicates, it describes about code style of python.
            https://www.python.org/dev/peps/pep-0008/

    LINTERS
        Pero leer esta guia y tratar de cumplirla a mano es dificil, para esto tenemos los LINTERS.
        
            Estos son herramientas de analisis de codigo: https://en.wikipedia.org/wiki/Lint_(software).
            Lint, or a linter, is a static code analysis tool used to flag programming errors, bugs, stylistic errors and suspicious constructs.
            
        En este caso nos interesa un linter que nos diga donde incumplimos el PEP8
        
        Uno de estos linters es flake8
            en el environment deseado
                python -m pip install flake8
            
            https://code.visualstudio.com/docs/python/linting
            https://flake8.pycqa.org/en/latest/
            
            luego ctrl shift p select interpreter flake 8
            
            es posible que te diga para instalar algo.
            
            ya luego de esto el IDE deberia mostrar en el codigo los errores.
            
            tambien se puede correr con flake8 carpeta-de-analisis
            

    Autoformateo
        
        Tambien hay herramientas que dan formato al codigo de forma automatica, una de estas es black
        https://github.com/psf/black
        
        
        Ejemplos de formateo:
            https://black.vercel.app/
        
        En el environment deseado:
            pip install black
            
            correr black carpeta_a_formatear
            
            Aunque esto no quiere decir que haya inconsistencias entre formatos:
            https://black.readthedocs.io/en/stable/guides/using_black_with_other_tools.html
            
        Tambien es posible hacer que en VSC al guardar se formatee, pero no entrare en detalles:
            https://dev.to/adamlombard/how-to-use-the-black-python-code-formatter-in-vscode-3lo0
            
            

- Software testing: pytest y code coverage

    https://en.wikipedia.org/wiki/Test-driven_development
    https://en.wikipedia.org/wiki/Anti-pattern

    Dentro de la carpeta de test cada uno creara un archivo .py y probaran SU funcion con un caso de ejemplo
    
    Ejemplo:
    
    def suma(x,y)
        return x+y
        
    assert suma(1,4)==5
    
    https://stackoverflow.com/questions/5142418/what-is-the-use-of-assert-in-python
    
    Lo que haremos ahora es utilizar pytest como plataforma de testeo. Digamos que cada prueba será una funcion que comience con test_nombre_de_prueba
    
    y todos estas funciones estaran en un arhivo .py que a su vez se llamara test_categoria_de_pruebas.py
    
    
    instalacion
    https://docs.pytest.org/en/6.2.x/getting-started.html
    
    pip install -U pytest en el environment deseado
    
    repo
        paquete
        tests
            test_paquete.py
                import mifuncion
                test_mi_funcion():
                    assert mifuncion(A,B) == valorCorrecto
        
        
        luego correr parados en repo:
            pytest
            
        deberia aparecer el resultado del test
        
        
    testeo de excepciones:
    
    Ejercicio: Cada uno en su funcion valide que la entrada sea un numero o una lista segun el caso
    
    if x not isinstance(int):
        raise TypeError
        
        si mal no recuerdo se puede hacer
        
        raise TypeError('Se esperaba un entero pero se obtuvo ' + str(type(x)))
        
    Hay una multitud de excepciones que se pueden retornar:
        https://docs.python.org/3/library/exceptions.html
    
    
    En pytest se pueden probar estas excepciones con la clausula with:
    
    import pytest
    
    with pytest.raises(TypeError):
        assert mifuncion(data_tipo_erroneo)
        
    y volver a probar pytest.
    
    Ejercicio:
        Cada uno realiza el test de su excepcion.


    
    Code Coverage
    https://en.wikipedia.org/wiki/Code_coverage
    
    La idea es detectar las secciones de codigo no probadas por los tests.
    
    Herramienta: Coverage https://github.com/nedbat/coveragepy
    https://coverage.readthedocs.io/en/6.1.2/
    
    en el environment:
        pip install coverage
        
    
    Uso:
    
    En el root del repo:
        coverage run -m pytest
        
    Esto correra todos los tests.
    
    Generar el reporte
        coverage report
        
    Generar un mejor reporte...
    
        coverage html
    
    El html estara dentro de la carpeta htmlcov
    
    
    OJO: La metrica porcentual de coverage es solo un indicador, tambien toca preguntarse que tan ATOMICAS fueron las pruebas.
    
    

- Continuous Integration/Deployment mediante Github Actions

La idea del CI CD pipeline es automatizar lo mas posible todo el proceso de desarrollo.

En nuestro caso vamos a automatizar el testeo y el code coverage. Pero esto tiene mas alcance.

Actions
    set up workflow yourself --> creara un archivo en repo/.github/workflows/main.yml
    start commit
    
    La idea es que cada vez que haya un cambio en la rama principal, se ejecute el workflow automaticamente.
    
    Mostrar aqui la corrida del workflow por defecto.
    
    un workflow es un archivo YML (markup language simple de leer por humanos), es como un json mas bonito.
    
    Este archivo YML configura el workflow.
    
    Tiene name, on, y jobs
    
    name, es el nombre duh...
    
    on configura cuando se activa el workflow
    
    y jobs configura lo que se hace en si, esta subdivido en trabajos cada uno con su nombre.
    
    cada job consta de una maquina donde corre y la serie de pasos que debe ejecutar.
    
    
    CI TEST
    Primero correremos solo los tests:
    
    
    # This is a basic workflow to help you get started with Actions

name: CI

# Controls when the workflow will run
on:
  # Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
 testing:

    runs-on: ubuntu-latest
    strategy:
      fail-fast: false
      matrix:
        python-version: [3.8]
    steps:
    - uses: actions/checkout@v2
    - name: Set up Python ${{ matrix.python-version }}
      uses: actions/setup-python@v2
      with:
        python-version: ${{ matrix.python-version }}
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        python -m pip install pytest
        pip install .
    - name: Test with pytest
      run: |
        pytest
        
        
Ejercicio, cada uno trata de correr este Github Actions en su fork, y luego tratan de hacer que el test falle. (cambiando el nombre a tu funcion lo haria fallar por error de importacion).
Verificar los logs de CI

Noten que se pueden llamar partes del yaml en otras , como pasa con la version de python en este yaml.

    CI Coverage
    
    Utilizaremos la pagina https://about.codecov.io/for/open-source/ para hostear los reportes de coverage.
    
    Para esto es necesario registrarnos en esa pagina (gratis para open-source).
    
    Register Now
        Sign In with github
            Continue to Github
                Authorize Code Coverage
                    resyncing si no aparece el repo tuyo
                        view repos for setup
                            seleccionar repo actual
                                setup repo (ala derecha)

En el workflow, por facilidad solo copiar esto


# This is a basic workflow to help you get started with Actions

name: CI

# Controls when the workflow will run
on:
  # Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
 testing:

    runs-on: ubuntu-latest
    strategy:
      fail-fast: false
      matrix:
        python-version: [3.8]
    steps:
    - uses: actions/checkout@v2
    - name: Set up Python ${{ matrix.python-version }}
      uses: actions/setup-python@v2
      with:
        python-version: ${{ matrix.python-version }}
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        python -m pip install pytest
        python -m pip install pytest-cov
        pip install .
    - name: Test with pytest
      run: |
        pytest tests/ --cov=examplepy/ --cov-report=xml --verbose -s
    - name : Coverage
      uses: codecov/codecov-action@v1
      with:
        fail_ci_if_error: true
        #token: ${{ secrets.CODECOV_TOKEN }} # not required for public repos
        

Ademas necesitamos agregar un __init__.py para que se puedan reconocer bien los test:
https://stackoverflow.com/questions/47287721/coverage-py-warning-no-data-was-collected-no-data-collected

repo
    paquete
    tests
        __init__.py
        
        
    Es posible agregar un badge de coverage al readme (mostrar el de algun paquete famoso para que tengan una referencia).
    
    settings, badge, copiar codigo de markdown en el readme.
    
    Mencionar que se pueden obtener mas badges pero con ese basta para ilustrar.
    



- Documentación automatizada con sphinx y read the docs

Sphinx es una herramienta para crear paginas de documentacion automatica.

https://www.sphinx-doc.org/en/master/

Puede resultar algo magica y no tan intuitiva de usar. Lo que yo les voy a dar es una receta para facilitar su uso.

Mostrar paginas que usan sphinx
    https://numpy.org/doc/stable/
    https://scikit-learn.org/stable/modules/classes.html , https://github.com/scikit-learn/scikit-learn/blob/main/doc/conf.py 
    https://mne.tools/stable/python_reference.html

Lo primero es instalar los paquetes necesarios, como son varios vamos a crear un archivo de requisitos.

Este archivo se usa para facilitar la instalacion para otros desarrolladores y usuarios. Se puede crear un archivo para cada uno.

Crearemos entonces un txt con estos requisitos:


paquete
    requirements-dev.txt
        pytest
        pytest-cov
        sphinx>3
        furo
        sphinx_gallery
        sphinx-copybutton
        sphinxcontrib-mermaid
        sphinx-autoapi
        myst-parser
        matplotlib


y modificaremos nos CI de forma acorde:


# This is a basic workflow to help you get started with Actions

name: CI

# Controls when the workflow will run
on:
  # Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
 testing:

    runs-on: ubuntu-latest
    strategy:
      fail-fast: false
      matrix:
        python-version: [3.8]
    steps:
    - uses: actions/checkout@v2
    - name: Set up Python ${{ matrix.python-version }}
      uses: actions/setup-python@v2
      with:
        python-version: ${{ matrix.python-version }}
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        if [ -f requirements-dev.txt ]; then pip install -r requirements-dev.txt; fi
        pip install .
    - name: Test with pytest
      run: |
        pytest tests/ --cov=examplepy/ --cov-report=xml --verbose -s
    - name : Coverage
      uses: codecov/codecov-action@v1
      with:
        fail_ci_if_error: true
        #token: ${{ secrets.CODECOV_TOKEN }} # not required for public repos


Revisar que a todos le correa bien el test. En este caso simplemente instalamos usando el archivo nuevo con la estructura if fi.




INICIALIZACION DE SPHINX


Vamos a crear una subcarpeta llamada docsrc que va a contener el codigo generatriz de la documentacion

repo
    paquete
    docsrc
    
vamos a colocar la terminal de nuestro environment en ese directorio

cd docsrc

sphinx-quickstart --ext-autodoc

Nos va a realizar preguntas:

Separar build y src : Si

Nombre Proyecto
Autores
Release Vacio
Languagfes en ingles por ahora


En el archivo conf.py creado copiar esto https://github.com/SemilleroNeuroCo/examplepy/blob/main/docs/source/conf.py


repo
    docsrc
        source
            conf.py
            

Explicar mas o menos que hace cada cosa.

Se debe cambiar todo lo que diga examplepy y bueno el autor.

ademas comentar por ahora todo lo de sphinx gallery:

extensions = [
    'sphinx.ext.autodoc',
    'sphinx.ext.napoleon',
#    "sphinx_gallery.gen_gallery",
]

#sphinx_gallery_conf = {
#    "doc_module": "examplepy",
#    "reference_url": {
#        "examplepy": None,
#    },
#    "examples_dirs": "../../examples",
#    "gallery_dirs": "auto_examples",
#    "filename_pattern": "^((?!sgskip).)*$",
#    "backreferences_dir": "generated",
#    'run_stale_examples': False, #Force (or not) re running examples
#}


MODIFICAR    el archivo index.rst que es el que tiene el esqueleto de la documentacion.

los rst son archivos en el lenguaje restructured text que es un lenguaje de marcado como html, latex, markdown etc. Tiene capacidades poderosas pero es feo a la vista.

Este archivo debe quedar con: https://raw.githubusercontent.com/SemilleroNeuroCo/examplepy/main/docs/source/index.rst

.. toctree::
   :maxdepth: 2
   :caption: Contents:

   autoapi/index.rst



con la terminal en docsrc



make clean --> Limpiar builds previos
make html --> generar html static


static pages.https://en.wikipedia.org/wiki/Static_web_page



En sphinx tambien se puede generar una galeria de ejemplos de uso que se pueden visualizar como notebooks de python mediante la extension sphinx-gallery

crear una carpeta examples para estos ejemplos


repo
    paquete
    tests
    examples
        README.rst --> texto introductorio de los ejemplos
        ejemplo.py --> Ejemplo que quedara como notebook.
        
        
Referencia: https://github.com/SemilleroNeuroCo/examplepy/tree/main/examples


Index rst se le debe agregar
.. toctree::
   :maxdepth: 2
   :caption: Contents:

   autoapi/index.rst
   auto_examples/index.rst

Y se debe descomentar lo de sphinx gallery de conf.py

Regenerar documentacion y visualizar

Ejercicio: CAda quien haga un ejemplo de su funcion, simplemente reemplazar el titulo del apartado y llamar a la funcion.

Las particularidades del lenguaje rst no nos interesa ahorita.


Alojamiento de documentacion en internet:

2 vias:
    READ THE DOCS: Un poco mas complicada pero es la via habitual del software libre.
    Github Pages la que haremos en este tutorial.

1. Generar la documentacion tal como queremos que quede.


crear una nueva rama llamada gh-pages, u otro nombre

en esa nueva rama.

Crear una nueva carpeta llamada docs

repo
    docs

en esa carpeta copiar el contenido de docsrc/build/html, es decir, debe quedar

paquete
    docs
        index.html
        .nojekyll --> necesario
        
push de la rama al remoto

ir a nuestro repositorio en github

settings
    pages
        branch:gh-pages
        folder:docs
            Save

Deberia dentro de un rato estar la documentacion disponible

Si a alguien le interesa como hacerlo con readthedocs (se hace de forma automatica al actualizar docsrc me puede decir, aunque esto igual se puede imitar con Github Actions).
----------------------------------------------------------

Para el taller necesitan:

- LLEVAR UNA LAPTOP
- CREARSE UNA CUENTA DE GITHUB
- Instalar miniconda, Visual Studio Code y Git for Windows.

En el siguiente video pueden ver el proceso de instalacion https://youtu.be/6SR34FBkIBE .

El video esta sin audio y no es particularmente rapido (por eso dura 20 min). Ponganlo mas rapido o mas lento segun la parte donde tengan dudas.

Los pasos mostrados en el video son los siguientes:

- Descargar miniconda segun su equipo (de 64 o 32 bits)
- Escoger una carpeta de instalacion para conda, yo prefiero una diferente a la por defecto.
- Por facilidad usar la opcion de "Register Miniconda3 as my default Python", NO usar la primera opcion de agregarlo al PATH.

- Descargar visual studio code segun su equipo (de 64 o 32 bits)
- Instalar visual studio code (VSC)

- Para asegurar la correcta integracion de VSC con anaconda lo mejor es abrir VSC desde conda
- Para esto abrir VSC desde el Anaconda Prompt
    - Inicio -> Buscar -> Anaconda Prompt y abrirlo, debería abrirse un terminal
    - Escribir "code" y dar Enter
- Deberia de abrirse VSC


- Probar la integracion de VSC con conda
- Para esto abrir un terminal y escribir "python" y dar enter para ver si abre el interprete de python.

- Abrir un proyecto en una nueva carpeta (yo le puse helloWorld) para seguir probando la integracion VSC-python
- Instalar "Python Extension for Visual Studio Code". Yo tuve que reiniciar VSC para que la extension se mostrara como instalada aunque esto no debería pasar.
- Crear un script cualquiera de python.
- Probar la ejecucion con >Click Derecho en el script >Run python file in terminal
- Probar la ejecucion de una sola linea en el interprete con la opcion de >Run Selection/Line in Python Terminal
- Probar el modo debug
    - Colocar un punto de debug en cualquier parte del codigo
    - >Menu Superior >Run >Start Debugging >Python File
    - Tarda un poquito pero saben que entro si se muestra la linea seleccionada como debug en amarillo
    - Probar la consola de debug yendose a la parte inferior >Debug Console y escribir cualquier sentencia de python
    - Por ejemplo si se crea una variable, esta debe aparecer luego en el menu a la izquierda en el apartado de variables.

- Descargar Git For Windows
- Instalarlo
    - Pueden usar las opciones por defecto, aunque yo modifico un par:
        - Nombre default de la rama principal lo cambio a "main" en vez de "master"
        - Editor por defecto, donde uso Notepad++
    - Sin embargo se pueden quedar con todas las opciones por defecto.
    
- Probar la terminal
    - Click derecho en cualquier directorio
    - >Git Bash Here
    - Probar algun comando de BASH, por ejemplo ls
    - Por el momento esta terminal no va a estar integrada con conda, esto lo pueden verificar escribiendo "conda" y notaran que no identifica el comando.
    - En el taller vamos a ver como solventar esto.






