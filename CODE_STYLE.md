# Code Style and Formatting

Over the years I've been programming in Java, I've developed a style that, _for me_, appears organized, is easily comprehensible, and makes my code cohesive and simple to understand. While I understand that my coding style and formatting may not be what people may be used to, if your considering contributing to my open source projects, I ask that you to follow and replicate my style to the best of your ability. 

## Why?

Having a cohesive coding style and format is important to me. The reason why I have one is to make my code more professional and organized. When a bunch of different styles are being used, the code looks messy and disorganized. I simply request that when contributing code to my projects, that you try your best to maintain the style I've established (even if you don't necessarily agree with it). When you don't follow this style, I typically tell you to change your code so it matches, or I change it myself. And this process just takes time away from the both of us to make cool things. I'm not expecting perfection but I am expecting your honest effort when it comes to keeping the style and format consistent. You can think of this document as a sort of loose agreement between you (the contributor) and me, and perhaps more of a guideline.

## Style

### Curly Brackets For Blocks

When writing an IF, WHILE, FOR, SWITCH, or any code block, I expect the opening curly brace ``{`` to appear on the **next line**, AKA the line directly following the statement:

```java
if (!nextValues.isEmpty())
{ // <--- curly brace is on the next line after the "if" statement
  ConfigCategory nextCategory = list.makeCategory(path, category);
  buildConfigList(modid, type, list, nextValues, path, Optional.of(nextCategory));
}
```

Please do not keep them on the same line:

```java
if (!nextValues.isEmpty()) { // <--- please dont do this
  ConfigCategory nextCategory = list.makeCategory(path, category);
  buildConfigList(modid, type, list, nextValues, path, Optional.of(nextCategory));
}
```

This applies to following ELSE and ELSE IF statements attached to the IF in this example. This format also applies to WHILE, FOR, SWITCH, etc. statements, including methods/functions and classes, interfaces, records, or any other code block.

In some cases, I remove the curly brackets entirely. This is only if the content inside of a code block is a single line, and the brackets can be removed (and in other cases outlined below)

```java
if (renderable instanceof Widget3D widget) //brackets removed
  widget.renderAs3D(stack.pose(), bufferSource, pMouseX, pMouseY, this.minecraft.getPartialTick());
```

Please do not keep them, like this:

```java
if (renderable instanceof Widget3D widget)
{ // <---- please remove the brackets
  widget.renderAs3D(stack.pose(), bufferSource, pMouseX, pMouseY, this.minecraft.getPartialTick());
}
```

This does not apply to methods/functions, try-catch blocks, classes, interfaces, records, and other objects.

### Accessing Fields and Methods

When accessing a field or method from an instance of a class, interface, record, etc., please include a ``this.`` before accessing the field or method:

```java
protected boolean canZoom() 
{ 
  return this.moveFor <= 0.0F;
}
```

In the example above, the field ``moveFor`` includes a ``this.``, indicating that this is an instance field. This also applies to accessing methods/functions:

```java
@Override
protected void addTranslations()
{
  ...
  this.add("config.crackerslib.preset.note", "NOTE: Changing the preset may override other values, make backups!");
  ...
}
```

In this example, the method ``add`` includes the ``this.`` before it. This helps avoid possible ambiguity between parameters and wobject/static fields and method variables.

``this.`` is not included for static fields or methods (your IDE should complain at you for doing that anyways)

### Naming

Fields and methods all follow the camel case convention. When naming something, try your best to keep it short yet concise. Long names are no fun, but names that are so short they make no sense aren't fun either. Short names may be allowed if the context they are in clearly describes them. For example, take a class such as ``Vector3`` which contains fields ``x``, ``y``, and ``z``. It's obvious that those three fields are three dimensional positional data because they're contained in the class ``Vector3``.

Classes, interfaces, records, etc. follow pascal case. This is typical Java convention and your IDE may complain at you if you don't capitalize the first letter.

### Where to Put New Classes, Interfaces, Records, Packages, and Objects.

Before creating a new class, interface, record, etc., please take a look through the code to see if there's an already existing package that would work for it. For example, if you're making a class that contains data for a registry, try to include it with other classes that contain the same kind of content. If you're working on one of my mods, a package named similiar to ``dev.nonamecrackers2.mod.common.init`` would be where you would put something called ``ModEntities``. Please try your best to find a suitable spot for something, if you can't find one that would work well then make a new package that would make sense.

### Local Fields

When creating a new local field in a method, include the type, then the name of the local field and its optional assignment (if it's assigned at declaration). While using ``var`` instead of the type can be handy (I do it too if I'm lazy enough), try to include the type of the field if possible, unless if its super long because of generics (such as with ``Map<SomeSuperLongClassName, Pair<String, AnotherLongClassName>> map = ...``, which in this case can be replaced with ``var map = ...``, if possible).

### Method Parameters

If you're working on one of my mods, and you're attempting to override a method implemented by Minecraft, please try to rename the parameters to something sensible, if you roughly know what it is.

```java
@Override
protected void addPassenger(Entity p_20349_)
{
  super.addPassenger(p_20349_);
}
```

In the above example, what the method does is clearly described, and therefore so is the parameter. The function adds the given ``Entity`` as a passenger. In this case, ``p_20349_`` can be renamed to ``passenger``. If this was a case where you're not entirely sure what the parameter is used for, just name the parameter its given type. In this case ``p_20349_`` could also be called ``entity``, since the parameter is an ``Entity``.

Some of my newer mods may contain ParchmentMC which has names for most of these obscure parameters. If it does not, then please try to follow these rules to rename parameters.

### Nested (or Inner) Classes

When accessing a nested (or inner) class, please include the parent class it is inside of, then the name of the inner class, when referencing it. 

```java
protected ConfigHelper(ForgeConfigSpec.Builder builder, String modid)
{
  this.builder = builder;
  this.modid = modid;
}
```

Here, the parameter ``builder`` with the nested inner class type ``Builder`` includes the name of the parent class it is inside of, ``ForgeConfigSpec``. Try not to do this:

```java
protected ConfigHelper(Builder builder /* <--- it's not clear that this is a nested inner class */, String modid)
{
  this.builder = builder;
  this.modid = modid;
}
```

## Conclusion

This document is incomplete and will most likely expand in the future.

Thank you for taking time to read this! Keeping the code in my projects organized, concise, and comprehensible is important to me, hence this document. Please try to keep this stuff in mind when writing code for my projects.

Thanks, nonamecrackers2
