
============================
Tryton: Capacitación técnica
============================

:Autores: Mario Puntin, Adrián Bernardi <contacto@silix.com.ar>
:Versión: 0.2
:Fecha: Mayo de 2015

.. footer::
   *Silix - Soluciones Informáticas Libres* | *###Title###*

Temario
=======

.. class:: temario-n1

1\. Presentación


.. class:: temario-n2

1.1 Características generales de Tryton 

.. class:: temario-n2

1.2 Herramientas de uso e instalación 



.. class:: temario-n1

2\. Un módulo básico


.. class:: temario-n2

2.1 Crear un modelo

.. class:: temario-n2

2.2 Agregar campos a un modelo

.. class:: temario-n2

2.3 Los campos del modelo: su representación gráfica y en base de datos

.. class:: temario-n2

2.4 La presentación gráfica de los datos

.. class:: temario-n2

2.5 Responder a las acciones del usuario: *on_change*



.. class:: temario-n1

3\. Características avanzadas


.. class:: temario-n2

3.1 Workflows

.. class:: temario-n2

3.2 Mejorando las vistas

.. class:: temario-n2

3.3 Los campos *function*

.. class:: temario-n2

3.4 Wizards (asistentes)

.. class:: temario-n2

3.5 Cómo extender objetos preexistentes



.. class:: temario-n1

4\. Temas adicionales


.. class:: temario-n2

4.1 Reportes

.. class:: temario-n2

4.2 Permisos y reglas de acceso

.. class:: temario-n2

4.3 *proteus*



.. class:: temario-n1

5\. Referencias y fuentes




1. Presentación
===============

1.1. Características generales de Tryton
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tryton es una plataforma para aplicaciones de propósito general. Puede utilizarse para desarrollar sistemas con diferentes objetivos: ERP para empresas, software para establecimientos de salud (como GNU Health) o para universidades, tiendas virtuales para ventas on-line, etc.

Características
---------------

**. Escrito en Python**

**. Modular**

**. Arquitectura de tres capas**

- Cliente de escritorio en GTK (tryton) y cliente web en javascript (sao, en desarrollo)
- Servidor (trytond)
- Gestor de base de datos (DBMS): PostgreSQL (también SQLite y MySQL)



1.2. Herramientas de uso e instalación 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Es recomendable utilizar algunas herramientas que facilitan la instalación y gestión de Tryton

**pip**
  Herramienta para instalar y gestionar paquetes de Python

**virtualenv**
  Herramienta para crear entornos controlados de Python.
  Permite tener diferentes versiones de algunas librerías y controlar las dependencias instaladas para cada entorno

**virtualenvwrapper**
  Conjunto de extensiones hechas sobre *virtualenv* para simplificar su uso.

**Sistemas de Control de Versiones**
  Hay que mencionar además la gran utilidad que tienen sistemas
  como **Mercurial** o **Git**, que permiten llevar registro
  de las distintas modificaciones hechas al código.


Instalación de *pip* y *virtualenvwrapper*
------------------------------------------

En primer lugar podemos instalar el paquete *pip* que trae el sistema operativo.
Luego podemos usar *pip* para instalar *virtualenvwrapper*

::

  $ sudo apt-get install python-pip

  $ pip install --user virtualenvwrapper


.. sidebar:: Uso de pip
    :subtitle: La opción **--user**

    La opción **--user** de *pip* hace que instale dentro
    de la carpeta *.local/* del *home* del usuario.
    De esa manera no es necesario utilizar carpetas del sistema
    o recurrir al superusuario para instalar mediante *pip*

.. sidebar:: El repositorio de pip: *Python Package Index*

    El comando *pip* funciona por medio de un repositorio público localizado en https://pypi.python.org
    cuyo propósito es ser un catálogo exhaustivo de todos los paquetes de Python escritos en código abierto


Configuración de *virtualenvwrapper*
-------------------------------------

Hay que indicarle al sistema cómo trabajar con *virtualenvwrapper*. Podemos crear una carpeta llamada *.virtualenvs/*, en el *home*, y usarla para contener los entornos creados.

Agregar en el archivo **/home/usuario/.bashrc** las siguientes líneas:

::

  export WORKON_HOME=$HOME/.virtualenvs
  source $HOME/.local/bin/virtualenvwrapper.sh

De esta manera, en el *home* tendremos dos carpetas:

- *$HOME/.local/*:
    todo lo que se instale con *pip* con la opción *--user*

- *$HOME/.virtualenvs/*:
    los entornos virtuales creados con *virtualenv[wrapper]*

Creación del entorno e instalación de Tryton
--------------------------------------------

Se crea el entorno virtual, al que llamamos, por ejemplo, *tryton-3.4*:

::

  $ mkvirtualenv tryton-3.4
  (tryton-3.4)$ pip install trytond==3.4.3
  
Al crear el entorno virtual el comando *mkvirtualenv* también activa este entorno: el prompt de la consola indica **(tryton-3.4)$**, es decir que antepone el nombre del entorno en el que nos encontramos.

.. topic:: *pip* dentro de un entorno virtual

    Al ejecutar *pip* **dentro** del entorno no hace falta indicarle *--user*,
    porque directamente instala dentro del entorno virtual,
    que se encuentra en *$HOME/.virtualenvs/*

.. sidebar:: Dependencias de Tryton

    Es importante chequear cuáles son las dependencias para ejecutar Tryton
    en determinadas condiciones. Por ejemplo, para ejecutarlo en combinación
    con el gestor PostgreSQL es necesario instalar el paquete *psycopg2*
    
    Para una referencia completa, dentro de la carpeta del servidor Tryton leer
    las indicaciones del archivo *INSTALL*
    


Instalación de módulos
----------------------

Pueden instalarse módulos de Tryton, por ejemplo:

::

  (tryton-3.4)$ pip install trytond_account==3.4.2

Esto instala el módulo *account* en su versión 3.4.2, junto con sus dependencias: *company, currency, country, party*, dentro de la carpeta *modules* del servidor *trytond*, en el entorno virtual. Es decir que en este caso instalamos cinco módulos.

Para comenzar a trabajar en un entorno de python y dejar de trabajar en él utilizamos los comandos *workon* y *deactivate*

::

  $ workon tryton-3.4
  (tryton-3.4)$ ...
  (tryton-3.4)$ deactivate
  $

El paquete *virtualenvwrapper* ofrece varios comandos útiles, uno de los cuales es *cdsitepackages*, que permite posicionarse fácilmente en la carpeta donde se instalan los paquetes y módulos de Tryton:

::

  (tryton-3.4)$ cdsitepackages
  (tryton-3.4)~/.virtualenvs/tryton-3.4/lib/python2.7/site-packages$

El comando *pip list* también permite ver los paquetes instalados

::

  (tryton-3.4)$ pip list
  Genshi (0.7)
  lxml (3.4.4)
  pip (6.1.1)
  polib (1.0.6)
  psycopg2 (2.6)
  python-dateutil (2.4.2)
  python-sql (0.6)
  pytz (2015.2)
  relatorio (0.6.1)
  setuptools (15.0)
  six (1.9.0)
  trytond (3.4.3)
  trytond-company (3.4.1)
  trytond-country (3.4.1)
  trytond-currency (3.4.1)
  [...]

También es posible eliminar todo el entorno:

::

  $ rmvirtualenv tryton-3.4


El archivo *trytond.conf*
-------------------------

Tryton podría funcionar sin un archivo *trytond.conf*. Pero normalmente querremos tenerlo.
Podemos ubicarlo en cualquier lugar del sistema de archivos, y no debemos olvidar indicarle al servidor dónde encontrarlo, con la opción **-c**

::

  [jsonrpc]
  listen=*:8000
  data=/var/www/localhost/tryton

  [database]
  uri=postgresql://usuario:password@localhost:5432
  path=/var/lib/tryton/data # directorio donde se guardaran los adjuntos
  
  [session]
  timeout=3600
  super_pwd=V6imlhDMI0fiY


La contraseña de super usuario
------------------------------

En el archivo de configuración la contraseña debe estar encriptada.

Para encriptar una contraseña podemos ejecutar el siguiente comando en una terminal. El resultado que se obtiene es el que hay que agregar en el archivo de configuración, como valor de *super_pwd*.

::

  $ python -c 'import getpass,crypt,random,string;
    print crypt.crypt(getpass.getpass(),
    "".join(random.sample(string.ascii_letters + string.digits, 8)))'


2. Un módulo básico
===================

Un módulo mínimo de Tryton consiste de dos archivos:

**__init__.py**

  Archivo estándar de todos los módulos de Python

**tryton.cfg**
  Permite establecer cuáles son las dependencias del módulo y los archivos XML adicionales que deben ser utilizados

Ejemplo de *tryton.cfg*

::

    [tryton]
    version=3.4.2
    depends:
        company
    xml:
        account.xml


2.1. Crear un modelo
~~~~~~~~~~~~~~~~~~~~

En Tryton un *modelo* es una clase normal de Python, que hereda de la clase *Model*. Pero para que el modelo persista en la base de datos hay que heredar de *ModelSQL*

Para nuestro ejemplo vamos a crear un archivo llamado *opportunity.py*, en el que ingresaremos el siguiente código:

En **opportunity.py**:

.. code-block:: python

    from trytond.model import ModelSQL

    __all__ = ['Opportunity']
     
    class Opportunity(ModelSQL):
    'Opportunity'
    __name__ = 'training.opportunity'
    
Para que Tryton tome nota de la existencia de este modelo es necesario registrarlo en el *Pool* de modelos

En **__init__.py**:

.. code-block:: python

    from trytond.pool import Pool
    from .opportunity import *
    
    
    def register():
        Pool.register(
            Opportunity,
            module='training', type_='model')

2.2. Agregar campos a un modelo
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Volvemos a **opportunity.py**:

.. code-block:: python

    from trytond.model import ModelSQL, ModelView, fields
    
    __all__ = ['Opportunity']
    
    
    class Opportunity(ModelSQL, ModelView):
        'Opportunity'
        __name__ = 'training.opportunity'
        _rec_name = 'description'
        description = fields.Char('Description', required=True)
        start_date = fields.Date('Start Date', required=True)
        end_date = fields.Date('End Date')
        party = fields.Many2One('party.party', 'Party', required=True)
        comment = fields.Text('Comment')

Para definir los atributos (campos) de la clase se utiliza *fields*

Existen distintos tipos de campos, por ejemplo *Char*, *Integer*, *Boolean*, *Date*, entre otros.

Cada uno de ellos tiene atributos que establecen su comportamiento:

**string**
  Nombre o etiqueta para el campo

**required**
  Si se le asigna *True*, el campo es requerido

**readonly**
  Si se le asigna *True*, no se permite editar el campo desde la interfaz de usuario

**domain**
  Una lista que define un dominio o subconjunto de registros válidos

**states**
  Es un diccionario de Python con al menos alguna de las siguientes claves:
    *required*, *readonly* e *invisible*

  Nótese que las dos primeras coinciden con atributos ya mencionados.
  
  Los valores posibles para estas claves son expresiones **pyson**
  que se evalúan con valores de cada registro.
  De esta manera es posible cambiar dinámicamente los atributos del campo.
  Por ejemplo, que determinado campo no sea de solo lectura (*readonly*) siempre,
  sino en determinada circunstancia o estado del registro.


2.3. Los campos del modelo: su representación gráfica y en base de datos
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Al desarrollar una aplicación utilizando la plataforma Tryton tenemos la ventaja de que fácilmente podemos ver representados nuestros campos en una base de datos (capa de persistencia de datos) y también de manera gráfica (capa de presentación).

En cierta medida estamos hablando del *mapeo objeto-relacional* (conocido por su nombre en inglés, Object-Relational mapping, o sus siglas *ORM*).

Veamos algunos ejemplos:

------------

**fields.Char**:

En un módulo Tryton:

.. code-block:: python

        name = fields.Char('Nombre', required=True)

En la interfaz gráfica:

.. figure:: images/img_char_ejemplo.png

En la base de datos (SQL):

.. code-block:: sql

    name VARCHAR NOT NULL

-------------

**fields.Date**:

En un módulo Tryton:

.. code-block:: python

        fecha_factura = fields.Date('Fecha factura')

En la interfaz gráfica:

.. figure:: images/img_fecha_ejemplo.png

En la base de datos (SQL):

.. code-block:: sql

    fecha_factura DATE

------------

**fields.Many2One**:

En un módulo Tryton:

.. code-block:: python

        party = fields.Many2One('party.party', 'Entidad', required=True)

En la interfaz gráfica:

.. figure:: images/img_m2o_ejemplo.png

En la base de datos (SQL):

.. code-block:: sql

    party INTEGER NOT NULL
    FOREIGN KEY(party) REFERENCES party_party(id)


2.4. La presentación gráfica de los datos
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Para poder usar la capa de presentación, el modelo debe heredar *ModelView*

.. code-block:: python

    class Opportunity(ModelSQL, ModelView):

La representación gráfica se determina por medio de archivos XML.

Hay que indicarle a Tryton de dónde tomar la definición XML. Y para ello hay que crear un archivo llamado *opportunity.xml*

En el archivo *tryton.cfg*:

::

    xml:
        opportunity.xml

Una vista (*View*) es un objeto más de Tryton; se almacena en base de datos y guarda información que toma el servidor para construir la representación gráfica.

Hay dos tipos principales de vista:

    - **Tree**: es una lista de registros
    - **Form**: es una vista de formulario, que permite crear y editar un registro

Vista Tree
----------

En la definición se hace referencia al objeto View (*ir.ui.view*) que va a contener la vista.

En los campos de este objeto se define el modelo que está asociado a la vista (*training.opportunity*), el tipo (*tree*) y el nombre del archivo que contiene la definición: *opportunity_list*

.. code-block:: xml

    <record model="ir.ui.view" id="opportunity_view_list">
        <field name="model">training.opportunity</field>
        <field name="type">tree</field>
        <field name="name">opportunity_list</field>
    </record>

El nombre de archivo al que se alude está alojado por defecto en una subcarpeta del módulo: *view/opportunity_list.xml*

.. code-block:: xml

    <tree string="Opportunities">
        <field name="party"/>
        <field name="description"/>
        <field name="start_date"/>
        <field name="end_date"/>
    </tree>


Vista Form
----------

También en este caso tenemos la referencia al objeto View (*ir.ui.view*).

La diferencia es que el tipo es *form*, y el nombre del archivo que contiene la definición es *opportunity_form*

.. code-block:: xml

    <record model="ir.ui.view" id="opportunity_view_form">
        <field name="model">training.opportunity</field>
        <field name="type">form</field>
        <field name="name">opportunity_form</field>
    </record>

Definición de *view/opportunity_form.xml*:

.. code-block:: xml

    <form string="Opportunity">
        <label name="party"/>
        <field name="party"/>
        <label name="description"/>
        <field name="description"/>
        <label name="start_date"/>
        <field name="start_date"/>
        <label name="end_date"/>
        <field name="end_date"/>
        <separator name="comment" colspan="4"/>
        <field name="comment" colspan="4"/>
    </form>
    

Armando las piezas
------------------

Definidas las vistas, sólo falta *armarlas* o *pegarlas*, para que actúen de manera coordinada.

Para ello se utiliza el objeto *ActionActWindow*, que define un tipo particular de acción, en este caso, abrir una ventana.

En **opportunity.xml**:

.. code-block:: xml

    <record model="ir.action.act_window" id="act_opportunity_open">
        <field name="name">Opportunities</field>
        <field name="res_model">training.opportunity</field>
    </record>

Y vinculadas a esta nueva acción, dos *acciones/vistas*

.. code-block:: xml

    <record model="ir.action.act_window.view" id="act_opportunity_open_view1">
        <field name="sequence" eval="10"/>
        <field name="view" ref="opportunity_view_list"/>
        <field name="act_window" ref="act_opportunity_open"/>
    </record>
    <record model="ir.action.act_window.view" id="act_opportunity_open_view2">
        <field name="sequence" eval="20"/>
        <field name="view" ref="opportunity_view_form"/>
        <field name="act_window" ref="act_opportunity_open"/>
    </record>

Como se puede ver, el campo *act_window* enlaza la **acción** de abrir una ventana con las **vistas** a las que se alude por medio del campo *view*.

Agregar entradas al menú
------------------------

Por último, esta acción es disparada por el usuario por medio de una entrada del menú de Tryton, que se puede crear de la siguiente manera:

.. code-block:: xml

    <menuitem name="Training" id="menu_training"/>

    <menuitem parent="menu_training" action="act_opportunity_open"
        id="menu_opportunity_form"/>


2.5. Responder a las acciones del usuario: *on_change*
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tryton provee un mecanismo para responder a acciones del usuario, de modo que si cambia algún valor otros campos resulten modificados.

Este mecanismo es el de *on_change*

Se puede aplicar de dos maneras:

**on_change_<nombre campo>**
  Cuando se modifica un campo, se envía al servidor una lista de valores. En base a ellos, el servidor devuelve nuevos valores para los campos.

**on_change_with_<nombre campo>**
  El valor de un campo se calcula cuando cualquier campo de una lista de campos es modificada. El cálculo lo realiza el servidor.

En ambos casos, la lista de campos que se envía al servidor se especifica por medio de un *decorador* de Python **@fields.depends**.

**Ejemplo de on_change**

.. code-block:: python

    @fields.depends('party')
    def on_change_party(self):
        cuit = None
        if self.party:
            cuit = self.party.cuit

        return {
            'cuit': cuit,
        }

**Ejemplo de on_change_with**: *end_date* toma el valor de *start_date* pero con siete días más

.. code-block:: python

    @fields.depends('start_date')
    def on_change_with_end_date(self):
        if self.start_date:
            return self.start_date + datetime.timedelta(days=7)
        return None


3. Características avanzadas
============================


3.1. Workflows
~~~~~~~~~~~~~~

Los *workflows* o flujos de trabajo permiten establecer estados para determinadas tareas, en este caso relacionadas con alguna clase de Tryton.

Para que una clase pueda manejar flujos de trabajo debe heredar la clase *Workflow*

.. code-block:: python

    class Opportunity(Workflow, ModelSQL, ModelView):

También debe tener un campo *state*.

.. code-block:: python

    state = fields.Selection([
            ('opportunity', 'Opportunity'),
            ('converted', 'Converted'),
            ('lost', 'Lost'),
            ], 'State', required=True, readonly=True, sort=False)

El flujo además requiere definir las posibles *transiciones* entre un estado y otro. Esto se hace en la función *__setup__()* por medio de *tuplas*:

.. code-block:: python

    @classmethod
    def __setup__(cls):
        super(Opportunity, cls).__setup__()
        cls._transitions |= set((
                ('opportunity', 'converted'),
                ('opportunity', 'lost'),
                ))

Finalmente, cada transición debe estar relacionada con un método de clase:

.. code-block:: python

    @classmethod
    @ModelView.button
    @Workflow.transition('converted')
    def convert(cls, opportunities):
        pool = Pool()
        Date = pool.get('ir.date')
        cls.write(opportunities, {
                'end_date': Date.today(),
                })

Agregar botones en la vista
---------------------------

La transición de un estado a otro es disparada normalmente por el usuario. Esto se puede hacer agregando un botón en la vista del formulario definido en XML:

.. code-block:: xml

    <button name="convert" string="Convert" icon="tryton-go-next"/>

Primero, en *__setup__()* se declara la existencia del botón. Luego se *decora* el método con *@ModelView.button* para que el método pueda ser invocado por medio del botón.

.. code-block:: python

    @classmethod
    def __setup__(cls):
        [...]
        cls._buttons.update({
                'convert': {
                    'invisible': ~Eval('state').in_(['opportunity']),
                    },
                })

    @classmethod
    @ModelView.button
    @Workflow.transition('converted')
    def convert(cls, opportunities):
        [...]

Los botones pueden estar activos o visibles de acuerdo con el estado actual del objeto, que define el flujo posible a seguir. Para eso se utiliza el atributo *invisible* de los botones.

Hay que tener presente que como el método está vinculado con la transición del *workflow*, al ejecutarse cambia de forma automática el estado de los objetos afectados por la transición. En otros palabras, no es necesario modificar manualmente el valor del campo *state*.


3.2. Mejorando las vistas
~~~~~~~~~~~~~~~~~~~~~~~~~

En el caso de los *workflows*, es importante mostrar el estado y los botones disponibles.

Es posible agrupar los elementos a mostrar, como una forma de controlar mejor la forma en que se muestran:

.. code-block:: xml

    <group col="2" colspan="2" id="state">
        <label name="state"/>
        <field name="state"/>
    </group>
    <group col="2" colspan="2" id="buttons">
        <button name="lost" string="Lost" icon="tryton-cancel"/>
        <button name="convert" string="Convert" icon="tryton-go-next"/>
    </group>


Formularios dinámicos
---------------------

Es frecuente que se quiera que campos o botones estén visibles o no, o sean de solo lectura u obligatorios, de acuerdo con determinadas condiciones variables. Estas condiciones se evalúan utilizando el lenguaje *Pyson*, que se verá a continuación.

Ya se habló del atributo *states*, que define un conjunto de valores posibles para **readonly**, **required**, **invisible**

.. code-block:: python

    start_date = fields.Date('Start Date', required=True, states={
            'readonly': Eval('state') != 'opportunity',
            }, depends=['state'])
    end_date = fields.Date('End Date', readonly=True, states={
            'required': Eval('state').in_(['converted', 'lost']),
            }, depends=['state'])

Pyson
-----

Pyson es una forma de representar una declaración que puede ser evaluada, es decir que de ella siempre se obtiene un resultado.

Es necesario importar aquellos tipos de declaración que se van a utilizar.

.. code-block:: python

    from trytond.pyson import Eval, Equal, Not

*Eval* evalúa el valor de un campo y lo devuelve, en este caso para realizar una comparación:

.. code-block:: python

    'readonly': Eval('state') != 'opportunity'


Las declaraciones Pyson se pueden combinar y anidar, agregando como en este caso *Equal* y *Not*

.. code-block:: python

    'readonly': Not(Equal(Eval('state'), 'opportunity'))

En los dos casos citados, el campo al que se le aplique esta definición será de solo lectura (*'readonly'*: True) cuando el valor del campo *state* sea distinto de 'opportunity'. Caso contrario, *readonly* tomará el valor *falso*: (*'readonly'*: False)


3.3. Los campos *function*
~~~~~~~~~~~~~~~~~~~~~~~~~~

Un campo de tipo *function* es un campo que puede emular otro tipo cualquiera de campo, y es calculado de forma dinámica. Su valor **no** es almacenado en la base de datos.

.. code-block:: python

    duration = fields.Function(fields.Integer('Duration'), 'get_duration')
    
    def get_duration(self, name=None):
        if not self.start_date or not self.end_date:
            return None
        return (self.end_date - self.start_date).days

El primer parámetro a definir es el tipo del campo (*Integer* en el ejemplo). Cualquier tipo de campo puede ser usado, siempre que se provea un mecanismo para calcularlo (un método *getter*, que en el ejemplo es *get_duration*).

.. sidebar:: El *getter* como *on_change_with*

    Hay que notar que el método *getter* que se define es semejante en su estructura al *on_change_with*:
    en virtud de ciertos valores o condiciones, se obtiene un valor para el campo.
    
    Por este motivo, no es extraño encontrar que la misma función es usada con ese fin:
    en lugar de algo como *'get_duration'*, se la escribe como *'on_change_with_duration'*

Setter y searcher
-----------------

Cuando estos campos *function* operan en base a cálculos hechos sobre otros campos relacionados, es posible también modificar valores por medio de un método *setter*. Asimismo es posible definir un *searcher*, para que se puedan realizar búsquedas por el campo *function*

Campos *function* que operan por lotes
--------------------------------------

El cálculo del campo *function* como lo hemos visto hasta ahora se ejecuta una vez por cada registro que se muestra.

No obstante, es posible calcular los valores de manera masiva, por lotes. Para ello el método *getter* debe ser un método de clase y debe retornar un diccionario que mapee el valor devuelto con su respectivo *id* de registro.

.. code-block:: python

    description_length = fields.Function(fields.Integer('Description Length'),
        'get_description_length')

    @classmethod
    def get_description_length(cls, opportunities, name):
        cursor = Transaction.cursor()
        
        opportunity = cls.__table__()
        query = opportunity.select(
            opportunity.id, CharLength(opportunity.description))
        cursor.execute(∗query)
        
        return dict(cursor.fetchall())



3.4. Wizards (asistentes)
~~~~~~~~~~~~~~~~~~~~~~~~~

Agregar acciones a un modelo
----------------------------

En ocasiones se puede requerir alguna funcionalidad o acción de cierta complejidad, que requiere una intervención adicional del usuario. Para estas situaciones la solución es crear un *wizard* o asistente.

Un *wizard* se compone de dos elementos:

  - Vistas o formularios que permiten al usuario ingresar ciertos valores o tomar una decisión.
  - Una *máquina de estados* que permite determinar lo que se debe o se puede hacer.


Vistas de wizard
----------------

Las vistas de un wizard son *ModelView* como los que ya se han visto. En este caso, no se hace persistir la información en base de datos, por lo cual no es necesario heredar de *ModelSQL*

.. code-block:: python

    class ConvertOpportunitiesStart(ModelView):
        'Convert Opportunities'
        __name__ = 'training.opportunity.convert.start'

Por lo demás, es posible establecer valores por defecto o utilizar las funcionalidades de tipo *on_change*, como con cualquier otro modelo.


Una máquina de estados
----------------------

Las clases que constituyen el wizard heredan, precisamente, de *Wizard*, y en ellas se pueden definir diferentes estados

.. code-block:: python

    from trytond.wizard import Wizard, StateView, StateTransition, Button

    [...]

    class ConvertOpportunities(Wizard):
        'Convert Opportunities'
        __name__ = 'training.opportunity.convert'
    
        start = StateView('training.opportunity.convert.start',
            'training.opportunity_convert_start_view_form', [
                Button('Cancel', 'end', 'tryton-cancel'),
                Button('Convert', 'convert', 'tryton-ok', default=True),
                ])
        convert = StateTransition()
    
        def transition_convert(self):
            pool = Pool()
            Opportunity = pool.get('training.opportunity')
            opportunities = Opportunity.browse(Transaction().context['active_ids'])
            Opportunity.convert(opportunities)
            return 'end'

.. sidebar:: El estado final

    Por defecto, todo wizard tiene un estado final: *end*. No es necesario definirlo.


Activación del wizard
----------------------

Para activar el wizard es necesario definirlo en el archivo XML:

.. code-block:: xml

    <record model="ir.action.wizard" id="act_convert_opportunities">
        <field name="name">Convert Opportunities</field>
        <field name="wiz_name">training.opportunity.convert</field>
        <field name="model">training.opportunity</field>
    </record>
    <record model="ir.action.keyword" id="act_convert_opportunities_keyword">
        <field name="keyword">form_action</field>
        <field name="model">training.opportunity,-1</field>
        <field name="action" ref="act_convert_opportunities"/>
    </record>

En este caso, con *ir.action.keyword* se indica que el wizard puede dispararse desde el botón de acciones (*form_action*) del modelo *training.opportunity*. Es posible seleccionar uno o más registros y lanzar el wizard vinculado con esos registros.

Sin embargo, también podría lanzarse el wizard asociándolo a un botón en un formulario. Para eso se crea el botón y en el método que tiene asociado se utiliza el decorador *@ModelView.button_action*.

.. code-block:: python

    @classmethod
    @ModelView.button_action('training.act_convert_opportunities')
    def convert_opportunities(cls, opportunities):
        pass

Finalmente, es necesario registrar el modelo (el wizard) en el archivo *__init__.py*, en este caso indicando su tipo.

.. code-block:: python

    def register():
        [...]
        Pool.register(
            ConvertOpportunities,
            module='training', type_='wizard')



3.5. Cómo extender objetos preexistentes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

La metaclase *PoolMeta*
-----------------------

Algunas veces lo que se desea no es crear modelos u objetos nuevos, sino simplemente agregar información.

Existe una clase llamada *PoolMeta*, que es una *metaclase*. Una *metaclase* es una clase que facilita la creación de otras clases. En este caso, estamos hablando de clases ya existentes en el Pool de modelos de Tryton.

.. code-block:: python

    from trytond.model import fields
    from trytond.pool import PoolMeta
    
    __all__ = ['Party']
    __metaclass__ = PoolMeta
    
    
    class Party:
        __name__ = 'party.party'
        opportunities = fields.One2Many('training.opportunity',
            'party', 'Opportunities')

Al especificar el atributo *__metaclass__ = PoolMeta* ya no hace falta indicar de qué clases hereda la clase *Party*, es decir, no hace falta que especifiquemos: *class Party(ModelSQL, ModelView)*

La clase *Party*, identificada por el atributo *__name__* = 'party.party', ya fue reconocida por Tryton, cuando se cargó, previamente, el módulo *party*.

Tryton se da cuenta de que se está trabajando con el mismo modelo y por lo tanto se produce todo el mecanismo de herencia, y finalmente se agrega el atributo deseado, *opportunities*.


Extender las vistas
-------------------

Para extender o modificar las vistas que ya existen hay que agregar un registro en un archivo XML.

En el registro se indica con el atributo *inherit* cuál es la vista que se va a modificar. En el valor de *ref* hay que indicar *<módulo>.<id_vista>*

.. code-block:: xml

    <record model="ir.ui.view" id="party_view_form">
        <field name="model">party.party</field>
        <field name="inherit" ref="party.party_view_form"/>
        <field name="name">party_form</field>
    </record>


La definición de aquello que se va a modificar se realiza por medio de *XPATH*, que permite identificar el elemento a modificar o la ubicación de referencia para agregar algo.

.. code-block:: xml

    <xpath expr="/form/notebook/page[@id='accounting']"
        position="after">
        <page name="opportunities" col="1">
            <separator name="opportunities"/>
            <field name="opportunities"/>
        </page>
    </xpath>



4. Temas adicionales
====================

4.1. Reportes
~~~~~~~~~~~~~

Para crear reportes se utilizan archivos de tipo *.odt* (Open Document) a modo de plantilla. Se los puede generar con herramientas como LibreOffice, aunque también es posible tomar como base algún reporte ya existente.

Para procesar los reportes se utilizan las librerías de Python *relatorio* y *Genshi*.

Se debe definir una clase que herede *Report*. Para personalizar el reporte se puede *sobrecargar* o *extender* el método *get_context()*, que se encuentra en *trytond/report/report.py*. De esa manera se pueden realizar cálculos adicionales para obtener datos que se utilizarán en el reporte.

.. code-block:: python

    from trytond.report import Report


    class ReporteConsultas(Report):
        __name__ = 'servicio.reporte.consultas'
    
        @classmethod
        def get_context(cls, records, data):
            report_context = super(ReporteConsultas, cls).get_context(records, data)
            # Con 'super' se invoca el método 'get_context'
            # de la clase que se hereda (Report)
            # 'report_context' es entonces un diccionario
            # que trae ya por defecto un conjunto de valores
            # que pueden ser utilizados en el reporte

            # En este lugar se pueden realizar operaciones o invocar
            # otros métodos para obtener valores adicionales
            # que se utilizarán en el reporte que se va a generar

            # Finalmente, los nuevos valores calculados u obtenidos
            # se agregan en el diccionario 'report_context'
            report_context['consultas'] = consultas
            report_context['hoy'] = Date.today()
            return report_context

Además hay que registrar este nuevo objeto en el Pool de Tryton, en el archivo *__init__.py*. El módulo de este ejemplo se llama *servicio*

.. code-block:: python

    def register():
        Pool.register(
            ReporteConsultas,
            module='servicio', type_='report')


Por otra parte, para poder lanzar el reporte debemos crear un objeto de tipo *ActionReport*. El modelo asociado a este reporte se llama *servicio.consulta* y es un modelo que contiene, en nuestro ejemplo hipotético, un listado de consultas recibidas.

También hay que indicar desde dónde se lanzará esta acción: se define un *ActionKeyword* de tipo *form_print*, con lo cual se asocia la acción al botón de *Imprimir informe* que se muestra en la barra de acciones de la interfaz gráfica.

.. code-block:: xml

    <record model="ir.action.report" id="act_servicio_reporte_consultas">
        <field name="name">Reporte de consultas</field>
        <field name="model">servicio.consulta</field>
        <field name="report_name">servicio.reporte.consultas</field>
        <field name="report">servicio/report/reporte_consultas.odt</field>
    </record>
    <record model="ir.action.keyword" id="servicio_reporte_consultas_keyword">
        <field name="keyword">form_print</field>
        <field name="model">servicio.consulta,-1</field>
        <field name="action" ref="act_servicio_reporte_consultas"/>
    </record>


En la definición del *ActionReport* se indica dónde se encuentra la plantilla (el archivo .odt), dentro de la carpeta del módulo.

Esta plantilla podría tener un formato como el siguiente:

.. figure:: images/img_reporte_ejemplo.png

Se utilizan los valores *hoy* y *consultas*, definidos en el diccionario *report_context*.

*consultas* contiene una lista de elementos (las consultas) sobre los cuales se itera, para que se muestren una debajo de la otra. Esta iteración se realiza con el comando *<for each>* ... *</for>*

Esta incorporación de datos de forma dinámica se realiza por medio de funciones especiales en la plantilla. En el archivo .odt (LibreOffice) hay que ir a *Insertar > Campos > Otros* y luego en la pestaña *Funciones > Marcador de posición > Texto*

La edición de estos campos se realiza apretando Botón derecho sobre ellos y eligiendo *Campos...*


4.2. Permisos y reglas de acceso
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

En Tryton es posible definir grupos de usuarios, y luego establecer un conjunto de permisos para cada grupo.

Los permisos se pueden determinar a nivel de modelo, de campo, de botón o de registro.

En el caso de los permisos para modelos y campos, es posible desactivar el chequeo si para determinada transacción se da al atributo *check_access* el valor *False*.

.. code-block:: python

    with Transaction().set_context(_check_access=False):
        [...]
        # Aquí se realiza la acción que afecta al modelo o campo en cuestión

En el caso de botones y registros, las reglas de acceso siempre se imponen.


Definición de reglas de acceso
------------------------------

Para establecer reglas de acceso a modelos se utilizan registros de tipo *ir.model.access*, en los cuales se define, para cada par *modelo/grupo*, los permisos de lectura, escritura, creación y eliminación. Si el usuario en cuestión pertenece a un grupo con permisos, entonces puede realizar la operación. En caso contrario, no se permite.

En el caso de accesos a un campo, el mecanismo es el mismo, pero se utilizan registros de tipo *ir.model.field.access*.

Para los botones, en el registro *ir.model.button* se define la lista de grupos de usuarios habilitados para ejecutarlo.


Grupos de usuarios
------------------

Para asignar permisos a un grupo de usuarios primero se debe crear ese grupo y, eventualmente, asociarlo a uno o más usuarios.

Por ejemplo, se puede crear un grupo *Administrador de Cuentas*, y además asociar ese grupo al usuario *admin* que tiene por defecto el sistema

.. code-block:: xml

        <record model="res.group" id="group_account_admin">
            <field name="name">Grupo Administrador de Cuentas</field>
        </record>

        <record model="res.user-res.group" id="user_admin_group_account_admin">
            <field name="user" ref="res.user_admin"/>
            <field name="group" ref="group_account_admin"/>
        </record>


Una vez hecho esto, se crean dos registros en *ir.model.access*: en el primero no se define ningún grupo, de modo que es genérico y se aplica a todos los usuarios. Se niegan todos los permisos, salvo el de lectura (*perm_read*).

En el segundo registro se asocia al grupo *Administrador de Cuentas* (*group_account_admin*), y se le otorgan permisos para todo.

De esta manera, nadie que no pertenezca al grupo *Administrador de Cuentas* podrá modificar el modelo *account.account*

.. code-block:: xml

        <record model="ir.model.access" id="access_account_general">
            <field name="model" search="[('model', '=', 'account.account')]"/>
            <field name="perm_read" eval="True"/>
            <field name="perm_write" eval="False"/>
            <field name="perm_create" eval="False"/>
            <field name="perm_delete" eval="False"/>
        </record>

        <record model="ir.model.access" id="access_account_admin">
            <field name="model" search="[('model', '=', 'account.account')]"/>
            <field name="group" ref="group_account_admin"/>
            <field name="perm_read" eval="True"/>
            <field name="perm_write" eval="True"/>
            <field name="perm_create" eval="True"/>
            <field name="perm_delete" eval="True"/>
        </record>


Toda esta información se guarda en un archivo que puede llamarse *access_rights.xml*, dentro de una carpeta denominada *security*.

Y como ya se ha visto en otros casos, no hay que olvidar indicar a Tryton que procese este archivo. En *tryton.cfg*, en el apartado *xml* hay que agregar una línea como la siguiente:

::

    xml:
        security/access_rights.xml



4.3. *proteus*
~~~~~~~~~~~~~~

*proteus* es una librería que permite acceder a los modelos de Tryton como si fuera una aplicación cliente. Sin embargo, no es necesario que el servidor Tryton esté ejecutándose para poder utilizarlo: el servidor Tryton es utilizado como un módulo más.

Se puede usar *proteus* para instalar módulos, crear entidades (*Party*) o cualquier otro modelo, e incluso ejecutar *wizards*, todo sin intervención directa de un usuario.

Es necesario configurar una conexión con la base de datos:

.. code-block:: python

    config.set_trytond(password='admin', database_name='training')


En el siguiente ejemplo se toma una archivo con datos de tipo *CSV* (valores separados por coma) y se lo procesa.

El objetivo es que nuevas oportunidades (*Opportunity*) se carguen en la base de datos y se asocien a una entidad (Party). Si esta entidad no existiera, se la crea primero.

.. code-block:: python

    import csv
    import datetime
    import sys
    from proteus import config, Model


    def main(args):
        Party = Model.get('party.party')
        Opportunity = Model.get('training.opportunity')
        csv_file = csv.DictReader(open(args[1], 'r'))
        for line in csv_file:
            parties = Party.find([('name', '=' , line['Party'])])
            if not parties:
                # no existe la Entidad: se la crea
                party = Party(name=line['Party'])
                party.save()
            else:
                # la Entidad existe ya
                party = parties[0]
            line_date = datetime.datetime.strptime(line['Date'], '%d/%m/%y').date()
            new_opportunity = Opportunity(party=party,
                    description=line['Description'], start_date=line_date)
            new_opportunity.save()
            
    if __name__ == '__main__':
        config.set_trytond(password='admin', database_name='training')
        main(sys.argv)


Si suponemos que este código Python se almacena en un archivo llamado *load_opportunities.py*, para ejecutarlo habría que escribir:

::

  $ python load_opportunities.py archivo_con_datos.csv

Se asume además que se utiliza una base de datos llamada *training*, y que el password del *admin* es 'admin'



5. Referencias y fuentes
========================

. La inspiración principal de este documento corresponde a una presentación de Nicolas Évrard: http://downloads.tryton.org/TUL2014/crash-course.pdf

. El módulo *training* utilizado en los ejemplos se puede encontrar en forma de parches (*patches* de *Mercurial*) en http://hg.tryton.org/

. Documentación de Tryton: http://doc.tryton.org/

. Tryton es español: http://www.tryton-erp.es/

