.. _doc_scripting:

Scripting
=========
脚本
====

Introduction
------------
介绍
----

Much has been said about tools that allow users to create video games
without programming. It's been a dream for many independent developers
to create games without learning how to code. This need has been around
for a long time, even inside companies, where game designers wish to
have more control of the game flow.

很多工具都宣称它们的使用者不需要编程就能制作电子游戏。制做游戏而不需要
学会怎么编程对很多独立游戏开发者来说是一个梦想。这种愿景由来已久，在游
戏公司内部，游戏设计师都想对游戏流程多一些控制。

Many products have been shipped promising a no-programming environment,
but the result is often incomplete, too complex or inefficient compared
to traditional code. As a result, programming is here to stay for a long
time. In fact, the general direction in game engines has been to add
tools that try to reduce the amount of code that needs to be written for
specific tasks, to speed up development.

很多产品都承诺一个无需编程的环境，但结果往往是要么不完整，或者太复杂，或者
与传统编程的方式比起来缺乏效率。因此，编程一直存在。实际上，？？？

In that sense, Godot has taken some useful design decisions towards that
goal. The first and most important is the scene system. The aim of it is
not obvious at first, but works well later on. That is, to relieve
programmers from the responsibility of architecting code.

在这种意义下，为了实现了个目标，Godot采用了一些有用的设计决策。第一个也是
最重要一个的设计就是场景系统。

When designing games using the scene system, the whole project is
fragmented into *complementary* scenes (not individual ones). Scenes
complement each other, instead of being separate. There will be plenty
of examples about this later on, but it's very important to remember it.

For those with a good amount of programming expertise, this means a
different design pattern to MVC. Godot promises efficiency at the
expense of dropping the MVC habits, which are replaced by the *scenes as
a complement* pattern.

Godot also uses the `extend <http://c2.com/cgi/wiki?EmbedVsExtend>`__
pattern for scripting, meaning that scripts extend from all the
available engine classes.

GDScript
--------

:ref:`doc_gdscript` is a dynamically typed scripting language to fit
inside Godot. It was designed with the following goals:

-  First and most importantly, making it simple, familiar and as easy to
   learn as possible.
-  Making the code readable and error safe. The syntax is mostly
   borrowed from Python.

Programmers generally take a few days to learn it, and within two weeks
feel comfortable with it.

As with most dynamically typed languages though, the higher productivity
(code is easier to learn, faster to write, no compilation, etc) is
balanced with a performance penalty, but most critical code is written
in C++ already in the engine (vector ops, physics, math, indexing, etc),
making the resulting performance more than enough for most types of
games.

In any case, if more performance is required, critical sections can be
rewritten in C++ and exposed transparently to the script. This allows
for replacing a GDScript class with a C++ class without altering the
rest of the game.

Scripting a scene
-----------------

Before continuing, please make sure to read the :ref:`doc_gdscript` reference.
It's a simple language and the reference is short, should not take more
than a few minutes to glance.

Scene setup
~~~~~~~~~~~

This tutorial will begin by scripting a simple GUI scene. Use the add
node dialog to create the following hierarchy, with the following nodes:

- Panel

  * Label
  * Button

It should look like this in the scene tree:

.. image:: /img/scriptscene.png

And try to make it look like this in the 2D editor, so it makes sense:

.. image:: /img/scriptsceneimg.png

Finally, save the scene, a fitting name could be "sayhello.scn"

.. _doc_scripting-adding_a_script:

Adding a script
~~~~~~~~~~~~~~~

Select the Panel node, then press the "Add Script" Icon as follows:

.. image:: /img/addscript.png

The script creation dialog will pop up. This dialog allows to select
the language, class name, etc. GDScript does not use class names in
script files, so that field is not editable. The script should inherit
from "Panel" (as it is meant to extend the node, which is of Panel type,
this is automatically filled anyway).

Select the filename for the script (if you saved the scene previously,
one will be automatically generated as sayhello.gd) and push "Create":

.. image:: /img/scriptcreate.png

Once this is done, the script will be created and added to the node. You
can see this both as an extra icon in the node, as well as in the script
property:

.. image:: /img/scriptadded.png

To edit the script, pushing the icon above should do it (although, the
UI will take you directly to the Script editor screen). So, here's the
template script:

.. image:: /img/script_template.png

There is not much in there. The "_ready()" function is called when the
node (and all it's children) entered the active scene. (Remember, It's
not a constructor, the constructor is "_init()" ).

The role of the script
~~~~~~~~~~~~~~~~~~~~~~

A script basically adds a behavior to a node. It is used to control the
node functions as well as other nodes (children, parent, siblings, etc).
The local scope of the script is the node (just like in regular
inheritance) and the virtual functions of the node are captured by the
script.

.. image:: /img/brainslug.jpg

Handling a signal
~~~~~~~~~~~~~~~~~

Signals are used mostly in GUI nodes, (although other nodes have them
too). Signals are "emitted" when some specific kind of action happens,
and can be connected to any function of any script instance. In this
step, the "pressed" signal from the button will be connected to a custom
function.

There is a GUI for connecting signals, just select the node and press
the "Signals" button:

.. image:: /img/signals.png

Which will show the list of signals a Button can emit.

.. image:: /img/button_connections.png

But this example will not use it. We don't want to make things *too*
easy. So please close that screen!

In any case, at this point it is clear that that we are interested in
the "pressed" signal, so instead of doing it with the visual
interface, the connection will be done using code.

For this, there is a function that is probably the one that Godot
programmers will use the most, this is
:ref:`Node.get_node() <class_Node_get_node>`.
This function uses paths to fetch nodes in the current tree or anywhere
in the scene, relative to the node holding the script.

To fetch the button, the following must be used:

::

    get_node("Button")

So, next, a callback will be added for when a button is pressed, that
will change the label's text:

::

    func _on_button_pressed():  
        get_node("Label").set_text("HELLO!")

Finally, the button "pressed" signal will be connected to that callback
in _ready(), by using :ref:`Object.connect() <class_Object_connect>`.

::

    func _ready():
        get_node("Button").connect("pressed",self,"_on_button_pressed")

The final script should look like this:

::

    extends Panel

    # member variables here, example:

    # var a=2
    # var b="textvar"

    func _on_button_pressed():
        get_node("Label").set_text("HELLO!")

    func _ready():
        get_node("Button").connect("pressed",self,"_on_button_pressed")

Running the scene should have the expected result when pressing the
button:

.. image:: /img/scripthello.png

**Note:** As it is a common mistake in this tutorial, let's clarify
again that get_node(path) works by returning the immediate children to
the node controlled by the script (in this case, *Panel*), so *Button*
must be a child of *Panel* for the above code to work. To give this
clarification more context, if *Button* was a child of *Label*, the code
to obtain it would be:

::

    # not for this case
    # but just in case
    get_node("Label/Button") 

And, also, try to remember that nodes are referenced by name, not by
type.
