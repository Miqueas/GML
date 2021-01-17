# GML (WIP)

GTK Mockup Metalanguage (GML for simplicity) is an attempt to replace the XML used in GTK templates.

__Note: GML is a WIP, some things can drastically change.__

### *"Why?"*

Honestly, I think it's a pain in the \*ss to create GTK templates with XML. Also, the current syntax for templates has poor readability, so it's easy to get lost if you create the templates by hand.

### *"How does it work?*

You write your templates in GML and then compile them into the usual XML used by GTK.

### Example

This simple template:

```css
GtkWindow {
  id: "Window";
  default-width: 400;
  default-height: 400;

  children {
    GtkLabel {
      visible: true;
      // Function _() makes text translatable
      label: _("Hello, world!");
    }
  }
}
```

Compiles to something like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<interface>

<object class="GtkWindow" id="Window">
  <property name="default-width">400</property>
  <property name="default-height">400</property>
  <child>
    <object class="GtkLabel">
      <property name="visible">True</property>
      <property name="label">Hello, world!</property>
    </object>
  </child>
</object>

</interface>
```

Templates for subclasses can look like this:

```css
MyWindow : GtkWindow {
  default-width: 400;
  default-height: 400;

  children {
    GtkLabel {
      visible: true;
      // Function _() makes text translatable
      label: _("Hello, world!");
    }
  }
}
```

And compiles to this:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<interface>

<template class="MyWindow" parent="GtkWindow">
  <property name="default-width">400</property>
  <property name="default-height">400</property>
  <child>
    <object class="GtkLabel">
      <property name="visible">True</property>
      <property name="label">Hello, world!</property>
    </object>
  </child>
</template>

</interface>
```