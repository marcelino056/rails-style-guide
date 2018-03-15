# Preludio

> Los modelos de roles son importantes. <br/>
> - Oficial Alex J. Murphy / RoboCop

El objetivo de esta guía es presentar un conjunto de mejores prácticas y estilo recomendados para el desarrollo de Ruby on Rails 4. Es un guía complementa a la ya existente impulsada por la comunidad [Ruby coding style guide](https://github.com/bbatsov/ruby-style-guide).

Algunos de los consejos aquí son aplicables solo a Rails 4.0+.

Puede generar un PDF o una copia HTML de esta guía usando
[Pandoc] (http://pandoc.org/).


Las traducciones de la guía están disponibles en los siguientes idiomas:

* [Ingles](https://github.com/bbatsov/rails-style-guide/blob/master/README.md)
* [Chino Simplificado](https://github.com/JuanitoFatas/rails-style-guide/blob/master/README-zhCN.md)
* [Chino tradicional](https://github.com/JuanitoFatas/rails-style-guide/blob/master/README-zhTW.md)
* [Japonés](https://github.com/satour/rails-style-guide/blob/master/README-jaJA.md)
* [Ruso](https://github.com/arbox/rails-style-guide/blob/master/README-ruRU.md)
* [Turco](https://github.com/tolgaavci/rails-style-guide/blob/master/README-trTR.md)
* [Coreano](https://github.com/pureugong/rails-style-guide/blob/master/README-koKR.md)
* [Vietnamita](https://github.com/CQBinh/rails-style-guide/blob/master/README-viVN.md)

# La guía de estilos de ruby on rails

Esta guía de estilo de Rails recomienda las mejores prácticas para que los rails del mundo real los programadores pueden escribir código que pueda ser mantenido por otros programadores de rails del mundo real. Se usa una guía de estilo que refleja el uso del mundo real y una guía de estilo que se aferra a un ideal que ha sido rechazado por la gente se supone que ayuda a que los riesgos no se usen para nada & ndash; no importa que tan bueno es.

La guía está separada en varias secciones de reglas relacionadas. He intentado agregar la razón de ser de las reglas (si se omite, supongo que es bonita obvio).

No presenté todas las reglas de la nada, se basan principalmente en mi extensa carrera como ingeniero de software profesional, comentarios y sugerencias
de los miembros de la comunidad de Rails y de varios prestigiosos recursos de rails.

## Tabla de contenido

* [Configuración](#configuración)
* [Enrutamiento](#enrutamiento)
* [Controladores](#controladores)
   * [Representación](#representación)
* [Modelos](#modelos)
   * [ActiveRecord](#activerecord)
   * [Consultas ActiveRecord](#activerecord-consultas)
* [Migraciones](#migraciones)
* [Vistas](#vistas)
* [Internacionalización](#internacionalización)
* [Activos](#activos)
* [Anuncios publicitarios](#anuncios publicitarios)
* [Extensiones principales de soporte activo](#active-support-core-extensions)
* [Tiempo tiempo)
* [Bundler](#bundler)
* [Gestión de procesos](#procesos de gestión)

## Configuración

* <a name="config-initializers"> </a>
  Coloque el código de inicialización personalizado en `config / initializers`. El código en
  los inicializadores se ejecutan al inicio de la aplicación.
<sup> [[link] (# config-initializers)] </ sup>

* <a name="gem-initializers"> </a>
  Mantenga el código de inicialización para cada gema en un archivo separado con el mismo nombre
  como la gema, por ejemplo `carrierwave.rb`,` active_admin.rb`, etc.
<sup> [[link] (# gem-initializers)] </ sup>

* <a name="dev-test-prod-configs"> </a>
  Ajuste en consecuencia las configuraciones para desarrollo, prueba y producción
  entorno (en los archivos correspondientes en `config / environments /`)
<sup> [[link] (# dev-test-prod-configs)] </ sup>

  * Marque activos adicionales para precompilación (si corresponde):

    `` `ruby
    # config / environments / production.rb
    # Precompilar activos adicionales (application.js, application.css,
    # y todos los que no son JS / CSS ya están agregados)
    config.assets.precompile + =% w (rails_admin / rails_admin.css rails_admin / rails_admin.js)
    `` `

* <a name="app-config"> </a>
  Mantenga la configuración que se aplica a todos los entornos en el
  archivo `config / application.rb`.
<sup> [[link] (# app-config)] </ sup>

* <a name="staging-like-prod"> </a>
  Cree un entorno `de ensayo 'adicional que se parezca mucho al
  `producción` uno.
<sup> [[link] (# staging-like-prod)] </ sup>

* <a name="yaml-config"> </a>
  Mantenga cualquier configuración adicional en archivos YAML en el directorio `config /`.
<sup> [[link] (# yaml-config)] </ sup>

  Dado que los archivos de configuración Rails 4.2 YAML se pueden cargar fácilmente con el nuevo método `config_for`:

  ```ruby
  Rails::Application.config_for(:yaml_file)
  ```
## Cotroladores

* <a name="skinny-controllers"></a>
  manten los controles flacos - solo deberían recuperar datos para la vista
   capa y no debe contener ninguna lógica de negocios (toda la lógica de negocios
   debería residir naturalmente en el modelo).
<sup>[[link](#skinny-controllers)]</sup>

* <a name="one-method"></a>
 
Cada accion de controlador deberia (idealmente) invocar solo un metodo invocar solo un método que no sea un
   descubrimiento inicial o nuevo.	
<sup>[[link](#one-method)]</sup>

* <a name="shared-instance-variables"></a>

	Comparte no mas de dos variables de instancia entre un controlador y una vista.
<sup>[[link](#shared-instance-variables)]</sup>

