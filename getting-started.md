---
layout: default
title: Getting started

components:
#- toolkit-ui/elements/g-panels.html
#- toolkit-ui/elements/g-tabs.html
#- samples/components/basic-element.html
#- samples/components/tk-element.html
#- samples/components/tk-element-databinding-color.html
#- samples/components/tk-element-databinding.html
#- samples/components/tk-element-property.html
#- samples/components/tk-element-ready.html
#- samples/components/tk-element-property-public.html
#- samples/components/tk-element-property-public-publish.html
#- samples/components/tk-element-event-binding.html
#- samples/components/tk-element-public-access.html
#- samples/components/tk-node-finding.html
##- samples/components/tk-twoway-binding.html
#- samples/components/tk-binding-to-elements.html
---

<script src="/polymer/polymer.min.js?{{'now' | date: "%Y%m%d"}}"></script>

{% comment %}
{% include outofdate.html %}
{% endcomment %}

## Basics

The basics of using {{site.project_title}} are simple:

1. Load **platform.js** to polyfill missing platform features, such as [Shadow DOM](/platform/shadow-dom.html)
and [HTML Imports](/platform/html-imports.html).
2. Load components with `<link rel="import" href="/path/to/component-file.html">`
3. Use the custom element in your page.

Here's a bare bones example:

    <!DOCTYPE html>
    <html>
      <head>
        <!-- 1. Shim missing platform features -->
        <script src="polymer/platform/platform.js"></script>
        <!-- 2. Load a component -->
        <link rel="import" href="toolkit-ui/elements/g-menu-item.html">
      </head>
      <body>
        <!-- 3. Instantiate the component with its tag. -->
        <g-menu-item src="images/email.svg">Email Link</g-menu-item>
      </body>
    </html>

<p class="alert"><b>Note</b>: You must always run your app from a web server. This
  is for the <a href="/platform/html-imports.html">HTML Imports</a> polyfill
  will work properly. This requirement will go away when the API is available 
natively in browsers.</p>

## Components

[Custom Elements](/platform/custom-elements.html) are the core building blocks of
{{site.project_title}}-based applications. You create applications by assembling custom elements
together, either ones provided by {{site.project_title}} or that you create yourself.

### Creating a basic component

The platform polyfills provided by {{site.project_title}} let you load and display
custom elements. Just by loading `platform.js` you get support for these
new technologies.

{% include samples/basic-element.html %}

### Creating a {{site.project_title}} element

{{site.project_title}} provides extra goodies for creating custom elements. We call these souped-up
custom elements "{{site.project_title}} elements". To create one, follow these steps:

1. Load [{{site.project_title}} core](/polymer.html) (`polymer/polymer.js` or `polymer/polymer.min.js`).

    **Note:** `polymer.js` loads `platform.js` under the hood.
You only need to include `polymer.js` when writing a {{site.project_title}} element.
    {: .alert }

1. In your custom element, add a `<script>` element that calls the `{{site.project_title}}.register()`. This endows the custom element with {{site.project_title}} features, such as data binding and event mapping.

In the following sample we convert our basic custom element into a {{site.project_title}} element named `tk-element`.

{% include samples/tk-element.html %}

`{{site.project_title}}.register()` takes the element it needs to register as its first argument.
In the context of `<element>`, `this` refers to the element.

{% comment %}
### Add properties to our component

The `{{site.project_title}}.register()` takes an object as a parameter whose members define the properties and methods that belong to our component.

{% include samples/tk-element-property.html %}

Now that we've added a private variable, let's add data binding to display its value in the DOM.
{% endcomment %}

## Declarative data binding

You can bind properties in your component using declarative data binding and the "double-mustache" syntax (`{%raw%}{{}}{%endraw%}`) from [Model Driven Views](/platform/mdv.html). The `{%raw%}{{}}{%endraw%}` is replaced by the value of the property referenced between the brackets.

{% include samples/tk-element-databinding.html %}

### Binding to markup

You can use binding expressions in most HTML markup, except for tag names themselves. In the following example, we create a new property on our component named `color` whose value is bound to the value of the `color` style applied to the custom element.

{% include samples/tk-element-databinding-color.html %}

### Binding between components and native elements ####

The following example demonstrates binding component properties to attributes of native input elements.

{% include samples/tk-binding-to-elements.html %}

### Adding a ready() lifecycle method ###

When a component has finished initializing itself, it calls its `ready` method, if it exists.

{% include samples/tk-element-ready.html %}

## Publishing properties ###

By default, properties you declare are not accessible via attribute. You can _publish_ a property by listing it in the `attributes` attribute on the `<element>` tag. Published properties can be initialized using attributes on the node, and can be data-bound using attributes on the node.

A property declared in the `attributes` attribute is initially set to `null`. You can provide a more appropriate default value by also including the property directly in your prototype, as usual.

#### Using the "attributes" attribute

The following example defines an `attributes` attribute on the custom element whose value is the string `"owner color"`. 

{% include samples/tk-element-property-public.html %}


{% comment %}
#### Using a publish object (advanced)

There is another way to publish a property (but you probably will never need it): the `publish` object. Properties included in an object named `publish` are published just like properties named in `attributes`.

{% include samples/tk-element-property-public-publish.html %}

### Change watching

### Accessing public properties on an element

A element's published properties can be set using attributes on its custom element, as shown in `index.html` below.

{% include samples/tk-element-public-access.html %}  
{% endcomment %}


### Automatic node finding

Shadow DOM is a self-contained document-like subtree; id's in that subtree do not interact with id's in other trees. Each {{site.project_title}} element generates a map of id's to node references in the element's template. This map is accessible as `$` on the element. 

{% include samples/tk-node-finding.html %}
