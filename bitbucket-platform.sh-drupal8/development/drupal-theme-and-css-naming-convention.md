<!-- @format -->

# Drupal theme and CSS naming convention

The Drupal naming convention consist in the core and the theme that are
operating in the site. For this project, the Drupal 8 core and Bootstrap 3 are
the components that defines the structure and classes in the site.



## Menu



### Drupal Core



The navigation section is a block in a region in the site, the twig template
[block--system-menu-block.html.twig](#Core:block--system-menu-block.html.twig) is the file that defines such structure:



```
{% set heading_id = attributes.id ~ '-menu'|clean_id %}

<nav role="navigation" aria-labelledby="{{ heading_id }}"{{ attributes|without('role', 'aria-labelledby') }}>

  {# Label. If not displayed, we still provide it for screen readers. #}

  {% if not configuration.label_display %}

    {% set title_attributes = title_attributes.addClass('visually-hidden') %}

  {% endif %}

  {{ title_prefix }}

  <h2{{ title_attributes.setAttribute('id', heading_id) }}>{{ configuration.label }}</h2>

  {{ title_suffix }}

  {# Menu. #}

  {% block content %}

    {{ content }}

  {% endblock %}

</nav>
```



Where:

```
* - attributes: HTML attributes for the containing element.
 *   - id: A valid HTML ID and guaranteed unique.
* - children: Optional additional rendered elements.
```



Then, inside the _{{content}}_ is the _menu_ template with the following structure, the file [menu.html.twig](#Core:menu.html.twig) :

```
{{ menus.menu_links(items, attributes, 0) }}

{% macro menu_links(items, attributes, menu_level) %}

  {% import _self as menus %}

  {% if items %}

    {% if menu_level == 0 %}

      <ul{{ attributes }}>

    {% else %}

      <ul>

    {% endif %}

    {% for item in items %}

      <li{{ item.attributes }}>

        {{ link(item.title, item.url) }}

        {% if item.below %}

          {{ menus.menu_links(item.below, attributes, menu_level + 1) }}

        {% endif %}

      </li>

    {% endfor %}

    </ul>

  {% endif %}

{% endmacro %}
```



In other words, there’s a `<li>` nested in `<ul>` tag, the classes are in the attributes variable.



### Menu Bootstrap Theme



Bootstrap as theme, modifies the core structure and adds its own classes, at first there’s the  [block--system-menu-block--main.html.twig](#Bootstrap:block--system-menu-block--main.html.twig).

```
{% set heading_id = attributes.id ~ '-menu'|clean_id %}

<nav role="navigation" aria-labelledby="{{ heading_id }}"{{ attributes.removeClass('clearfix')|without('role', 'aria-labelledby') }}>

  {# Label. If not displayed, we still provide it for screen readers. #}

  {% if not configuration.label_display %}

    {% set title_attributes = title_attributes.addClass('sr-only') %}

  {% endif %}

  <h2{{ title_attributes.setAttribute('id', heading_id) }}>{{ configuration.label }}</h2>

  {% block content %}

    {{ content }}

  {% endblock %}

</nav>
```



Where just the “contextual-region” class left in the nav tag.



Then, in the variable _{{content}}_ is the _menu_ template [menu.html.twig](#Bootstrap:menu.html.twig) shown
above:



```
{% macro menu_links(items, attributes, menu_level, classes, dropdown_classes) %}

  {% if items %}

    <ul{{ attributes.addClass(menu_level == 0 ? classes : dropdown_classes) }}>

    {% for item in items %}

      {%

        set item_classes = item.url.getOption('container_attributes').class | split(" ")

      %}

      {%

        set item_classes = [

          item.is_expanded and item.below ? 'expanded dropdown',

          item.in_active_trail ? 'active active-trail',

          loop.first ? 'first',

          loop.last ? 'last',

        ]

      %}

      <li{{ item.attributes.addClass(item_classes) }}>

        {% set link_title = item.title %}

        {% set link_attributes = item.link_attributes %}

        {% if menu_level == 0 and item.is_expanded and item.below %}

          {% set link_title %}{{ link_title }} <span class="caret"></span>{% endset %}

          {% set link_attributes = link_attributes.addClass('dropdown-toggle').setAttribute('data-toggle', 'dropdown') %}

        {% endif %}

        {# Must use link() here so it triggers hook_link_alter(). #}

        {{ link(link_title, item.url, link_attributes.addClass(item.in_active_trail ? 'active-trail')) }}

        {% if item.below %}

          {{ _self.menu_links(item.below, attributes.removeClass(classes), menu_level + 1, classes, dropdown_classes) }}

        {% endif %}

      </li>

    {% endfor %}

    </ul>

  {% endif %}

{% endmacro %}

{{ _self.menu_links(items, attributes, 0, classes ?: ['menu', 'menu--' ~ menu_name|clean_class, 'nav'], dropdown_classes ?: ['dropdown-menu']) }}
```





The menu classes are added in the `<ul>` tag by the template
[menu--main.html.twig](#Bootstrap:menu--main.html.twig):

```
{% extends "menu.html.twig" %}

{%

  set classes = [

    'menu',

    'menu--' ~ menu_name|clean_class,

    'nav',

    'navbar-nav',

  ]

%}
```



**Note. When a link is active the class ‘is active’ is added to the `<a>` tag.**



At the end, when page is rendered and show in the site, we can see an example of
the structure, ids and classes taken.





## Forms



### Drupal Core



The essential structure of all the forms is declared in the [form.html.twig](#Core:form.html.twig):



```
<form{{ attributes }}>

  {{ children }}

</form>
```



Then, depending of the form type the next structure in the _{{children}}_ variable is taken. The code below shows the [form-element.html.twig](#Core:form-element.html.twig):



```
{%

  set classes = [

    'js-form-item',

    'form-item',

    'js-form-type-' ~ type|clean_class,

    'form-item-' ~ name|clean_class,

    'js-form-item-' ~ name|clean_class,

    title_display not in ['after', 'before'] ? 'form-no-label',

    disabled == 'disabled' ? 'form-disabled',

    errors ? 'form-item--error',

  ]

%}

{%

  set description_classes = [

    'description',

    description_display == 'invisible' ? 'visually-hidden',

  ]

%}

<div{{ attributes.addClass(classes) }}>

  {% if label_display in ['before', 'invisible'] %}

    {{ label }}

  {% endif %}

  {% if prefix is not empty %}

    <span class="field-prefix">{{ prefix }}</span>

  {% endif %}

  {% if description_display == 'before' and description.content %}

    <div{{ description.attributes }}>

      {{ description.content }}

    </div>

  {% endif %}

  {{ children }}

  {% if suffix is not empty %}

    <span class="field-suffix">{{ suffix }}</span>

  {% endif %}

  {% if label_display == 'after' %}

    {{ label }}

  {% endif %}

  {% if errors %}

    <div class="form-item--error-message">

      {{ errors }}

    </div>

  {% endif %}

  {% if description_display in ['after', 'invisible'] and description.content %}

    <div{{ description.attributes.addClass(description_classes) }}>

      {{ description.content }}

    </div>

  {% endif %}

</div>
```



If there’s any input required, the [input.html.twig](#Core:input.html.twig) defines the structure:

```
<input{{ attributes }} />{{ children }}
```





### Bootstrap – form



To bootstrap, just add the class ‘input-group’ to the `<div>` that will nest the
input fields as shown in the [input.html.twig](#Bootstrap:input.html.twig) template below.



```
{% spaceless %}

  {% if input_group %}

    <div class="input-group">

  {% endif %}

  {% if prefix %}

    {{ prefix }}

  {% endif %}

  {% block input %}

    <input{{ attributes }} />

  {% endblock %}

  {% if suffix %}

    {{ suffix }}

  {% endif %}

  {% if input_group %}

    </div>

  {% endif %}

  {{ children }}

{% endspaceless %}
```



Then, in the {{children}} variable add the [input--form-control.html.twig](#Bootrstap:input--form-control.html.twig) file
and just add to the input a class called ‘form-control’:



```
{% spaceless %}

  {%

    set classes = [

      'form-control',

    ]

  %}

  {% block input %}

    <input{{ attributes.addClass(classes) }} />

  {% endblock %}

{% endspaceless %}
```





If a button is added, the next structure of the [input--button.html.twig](#Bootstrap:input--button.html.twig) is
added at the `<input>` level:



```
{% spaceless %}

  {%

    set classes = [

      'btn',

      type == 'submit' ? 'js-form-submit',

      icon and icon_position and not icon_only ? 'icon-' ~ icon_position,

    ]

  %}

  {% block input %}

    {% if icon and icon_only %}

      <button{{ attributes.addClass(classes, 'icon-only') }}>

        <span class="sr-only">{{ label }}</span>

        {{ icon }}

      </button>

    {% else %}

      {% if icon_position == 'after' %}

        <button{{ attributes.addClass(classes) }}>{{ label }}{{ icon }}</button>{{ children }}

      {% else %}

        <button{{ attributes.addClass(classes) }}>{{ icon }}{{ label }}</button>{{ children }}

      {% endif %}

    {% endif %}

    {{ children }}

  {% endblock %}

{% endspaceless %}
```







As example, the html code is shown below:



```
<form action="/search/node" method="get" id="search-block-form" accept-charset="UTF-8" data-drupal-form-fields="edit-keys">

  <div class="form-item js-form-item form-type-search js-form-type-search form-item-keys js-form-item-keys form-no-label form-group">

      <label for="edit-keys" class="control-label sr-only">Search</label>

    <div class="input-group">

      <input title="" data-drupal-selector="edit-keys" class="form-search form-control" placeholder="Search" type="search" id="edit-keys" name="keys" value="" size="15" maxlength="128" data-toggle="tooltip" data-original-title="Enter the terms you wish to search for.">

      <span class="input-group-btn">

        <button type="submit" value="Search" class="button js-form-submit form-submit btn-primary btn icon-only" name="">

        <span class="sr-only">Search</span>

        <span class="icon glyphicon glyphicon-search" aria-hidden="true"></span>

        </button>

    </span>

    </div>

  </div>

<div class="form-actions form-group js-form-wrapper form-wrapper" data-drupal-selector="edit-actions" id="edit-actions"></div>

</form>
```



Therefore, the naming convention is taken for the previous files.

## Node

### Drupal Core

The default node template is the [node.html.twig](#Core:node.html.twig:) and it comes inside of an article tag, and is shown below:

```
 <article{{ attributes }}>

  {{ title_prefix }}
  {% if label and not page %}
    <h2{{ title_attributes }}>
      <a href="{{ url }}" rel="bookmark">{{ label }}</a>
    </h2>
  {% endif %}
  {{ title_suffix }}

  {% if display_submitted %}
    <footer>
      {{ author_picture }}
      <div{{ author_attributes }}>
        {% trans %}Submitted by {{ author_name }} on {{ date }}{% endtrans %}
        {{ metadata }}
      </div>
    </footer>
  {% endif %}

  <div{{ content_attributes }}>
    {{ content }}
  </div>

</article>
```

### Bootstrap - Node

The Bootstrap Node template has the same name [node.html.twig](#Bootstrap:node.html.twig:) and has a similar structure. The differences are in the classes that Bootstrap uses.

```
{%
  set classes = [
    node.bundle|clean_class,
    node.isPromoted() ? 'is-promoted',
    node.isSticky() ? 'is-sticky',
    not node.isPublished() ? 'is-unpublished',
    view_mode ? view_mode|clean_class,
    'clearfix',
  ]
%}
<article{{ attributes.addClass(classes) }}>

  {{ title_prefix }}
  {% if label and not page %}
    <h2{{ title_attributes }}>
      <a href="{{ url }}" rel="bookmark">{{ label }}</a>
    </h2>
  {% endif %}
  {{ title_suffix }}

  {% if display_submitted %}
    <footer>
      {{ author_picture }}
      <div{{ author_attributes.addClass('author') }}>
        {% trans %}Submitted by {{ author_name }} on {{ date }}{% endtrans %}
        {{ metadata }}
      </div>
    </footer>
  {% endif %}

  <div{{ content_attributes.addClass('content') }}>
    {{ content }}
  </div>

</article>
```

## Paragraphs

Paragraphs is not a core module but you can [download](https://www.drupal.org/project/paragraphs) it from the [Drupal](https://www.drupal.org) site, then you can enable like any other module.

The original paragraphs template is [paragraphs.html.twig](#Module:paragraphs.html.twig:) and is this one:

```
{%
  set classes = [
    'paragraph',
    'paragraph--type--' ~ paragraph.bundle|clean_class,
    view_mode ? 'paragraph--view-mode--' ~ view_mode|clean_class,
    not paragraph.isPublished() ? 'paragraph--unpublished'
  ]
%}
{% block paragraph %}
  <div{{ attributes.addClass(classes) }}>
    {% block content %}
      {{ content }}
    {% endblock %}
  </div>
{% endblock paragraph %}
```

You can edit in your templates folder inside your custom theme folder location, and if you have enabled bootstrap you can add the classes that you want to build it.

## Drupal Practices

Class names should reflect design semantics instead of content semantics, “they should reflect the intent and purpose of the design element they represent”.



A good practice is to find an existing theme and insert a design-derived class
name, actually it can be from the core. For this case, if there´s a new item
without default design, the class name should be based on how the content is
built.



Abbreviations must be avoided, rather, try to use full words.



## Extra information



For more information about Drupal CSS architecture and Naming components using
design semantics

<https://www.drupal.org/docs/develop/standards/css/css-architecture-for-drupal-8>

For more information about Bootstrap 3 documentation:

<https://drupal-bootstrap.org/api/bootstrap>

Bootstrap theme installed, more general information:

<https://getbootstrap.com/docs/3.3/>

More information about Paragraphs you can visit the next link:

<https://www.drupal.org/docs/8/modules/paragraphs/how-to-start-with-paragraphs-for-drupal-8>

## Files Path & External links

#### Core:block--system-menu-block.html.twig:

[{docroot}/web/core/modules/system/templates/block--system-menu-block.html.twig](https://api.drupal.org/api/drupal/core%21modules%21system%21templates%21block--system-menu-block.html.twig/8.2.x)

#### Core:menu.html.twig:

[{docroot}/web/core/modules/system/templates/menu.html.twig](https://api.drupal.org/api/drupal/core%21modules%21system%21templates%21menu.html.twig/8.2.x)

#### Bootstrap:block--system-menu-block--main.html.twig:

[{docroot}/web/themes/contrib/Bootstrap/templates/block/block--system-menu-block--main.html.twig](https://drupal-bootstrap.org/api/bootstrap/templates%21block%21block--system-menu-block--main.html.twig/8.x-3.x)

#### Bootstrap:menu.html.twig:

[{docroot}/web/themes/contrib/Bootstrap/templates/menu/menu.html.twig](https://drupal-bootstrap.org/api/bootstrap/templates%21menu%21menu.html.twig/8.x-3.x)

#### Bootstrap:menu--main.html.twig: 

[{docroot}/web/themes/contrib/Bootstrap/templates/menu/menu--main.html.twig](https://drupal-bootstrap.org/api/bootstrap/templates%21menu%21menu--main.html.twig/8.x-3.x)

#### Core:form.html.twig:

[{docroot}/web/core/modules/system/templates/form.html.twig](https://api.drupal.org/api/drupal/core%21modules%21system%21templates%21form.html.twig/8.2.x)

#### Core:form-element.html.twig:

[{docroot}/web/core/modules/system/templates/form-element.html.twig](https://api.drupal.org/api/drupal/core%21modules%21system%21templates%21form-element.html.twig/8.2.x)

#### Core:input.html.twig:

[{docroot}/web/core/modules/system/templates/input.html.twig](https://api.drupal.org/api/drupal/core%21modules%21system%21templates%21input.html.twig/8.2.x)

#### #Bootstrap:input.html.twig:

[{docroot}/web/themes/contrib/Bootstrap/templates/input/input.html.twig](https://drupal-bootstrap.org/api/bootstrap/templates%21input%21input.html.twig/8.x-3.x)

#### Bootrstap:input--form-control.html.twig:

[{docroot}/web/themes/contrib/Bootstrap/templates/input/input--form-control.html.twig](https://drupal-bootstrap.org/api/bootstrap/templates%21input%21input--form-control.html.twig/8.x-3.x)

#### Bootstrap:input--button.html.twig:

[{docroot}/web/themes/contrib/Bootstrap/templates/input/input--button.html.twig](https://drupal-bootstrap.org/api/bootstrap/templates%21input%21input--button.html.twig/8.x-3.x)

#### Core:node.html.twig:

[{docroot}/web/core/modules/node/templates/node.html.twig](https://api.drupal.org/api/drupal/core%21modules%21node%21templates%21node.html.twig/8.2.x)

#### Bootstrap:node.html.twig:

[{docroot}/web/themes/contrib/Bootstrap/templates/node/node.html.twig](https://drupal-bootstrap.org/api/bootstrap/templates%21node%21node.html.twig/8.x-3.x)

#### Module:paragraphs.html.twig:

[{docroot}/web/modules/contrib/paragraphs/templates/paragraphs.html.twig](https://www.drupal.org/docs/8/modules/paragraphs/theming-in-paragraphs-for-drupal-8)

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
