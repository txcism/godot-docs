.. _doc_scenes_and_nodes:

Scenes and nodes
================

场景和节点
==========

Introduction
------------

介绍
----

.. image:: /img/chef.png

Imagine for a second that you are not a game developer anymore. Instead,
You are a chef! Change your hipster outfit for a toque and a double
breasted jacket. Now, instead of making games, you create new and
delicious recipes for your guests.

想象一下你不是一个游戏开发者，而是一个厨师！你时髦的衣服换成了无边帽和双排扣夹克。
现在你正在为你的顾客创造一份美味的菜谱，而不是制作游戏。

So, how does a chef create a recipe? Recipes are divided in two
sections, the first is the ingredients and the second is the
instructions to prepare it. This way, anyone can follow the recipe and
savor your magnificent creation.

所以，一个厨师是怎样制作一份菜谱的？菜谱通常由两部分构成，一是食材，二是制作步骤。
这样子，任何人只要遵从菜谱上指南就都能品尝到你高超的厨艺。

Making games in Godot feels pretty much the same way. Using the engine
feels like being in a kitchen. In this kitchen, *nodes* are like a
refrigerator full of fresh ingredients to cook with.

在Godot中制作游戏的感觉和这一样。使用引擎的感觉就像身处厨房。在这个厨房里，*节点*
就像塞满新鲜食材的冰箱。

There are many types of nodes, some show images, others play sound,
other nodes display 3D models, etc. There's dozens of them.

节点有很多类型，一些显示图片，一些播放声音，另一些则展示3D模型，等等。总之，有一大把。

Nodes
-----

节点
-----

But let's go to the basics. A node is a basic element for creating a
game, it has the following characteristics:

让我们从最基本的开始。一个节点是制作游戏的基本的元素，它有下列特征：

-  Has a name.
-  有一个名字
-  Has editable properties.
-  有可编辑的属性
-  Can receive a callback to process every frame.
-  能够接收回调
-  Can be extended (to have more functions).
-  能够被扩展
-  Can be added to other nodes as children.
-  能够作为子节点添加到其它节点

.. image:: /img/tree.png

The last one is very important. Nodes can have other nodes as
children. When arranged in this way, the nodes become a **tree**.

最后一点很重要。节点能包含其它作为子节点的节点。节点以这样的方式组成一棵**节点树**。

In Godot, the ability to arrange nodes in this way creates a powerful
tool for organizing the projects. Since different nodes have different
functions, combining them allows to create more complex functions.

在Godot引擎里面，这种组织节点的方式成为一个组织工程的强有力工具。
不同的节点可以拥有不同的函数，将节点合并起来就可以生成更加复杂的函数。

This is probably not clear yet and it makes little sense, but everything
will click a few sections ahead. The most important fact to remember for
now is that nodes exist and can be arranged this way.

要你现在明白这一点似乎为时过早。不过，最重要的是记住节点是以这样存在和被组织起来的。

Scenes
------

场景
----

.. image:: /img/scene_tree_example.png

Now that the existence of nodes has been defined, the next logical
step is to explain what a Scene is.

节点已经说的差不多了，下一步解释一下啥叫场景。

A scene is composed of a group of nodes organized hierarchically (in
tree fashion). It has the following properties:

一个场景由一组节点构成，其中这些节点以层次的方式组织起来（像一棵树那样）。
场景有下列属性：

-  A scene always has only one root node.
-  一个场景有且只有一个根节点
-  Scenes can be saved to disk and loaded back.
-  场景能被保存到磁盘，或从磁盘中导出来
-  Scenes can be *instanced* (more on that later).
-  场景能被 *实列化* （待会儿详解）
-  Running a game means running a scene.
-  运行一个游戏也就是意味着运行一个场景
-  There can be several scenes in a project, but for it to start, one of
   them must selected to be loaded first.
-  一个工程里面可以存在多个场景，但要开始，其中一个场景必须被先加载进来

Basically, the Godot editor is a **scene editor**. It has plenty of
tools for editing 2D and 3D scenes as well as user interfaces, but all
the editor revolves around the concept of editing a scene and the nodes
that compose it.

可以说，Godot编辑器就是一个 **场景编辑器** 。编辑器包含很多工具用来编辑2D或3D场景以及
用户界面。所有的编辑器都为编辑场景而生。

Creating a new project
----------------------

创建一个新的项目
----------------

Theory is boring, so let's change subject and go practical. Following a
long tradition in tutorials, the first project will be a hello world.
For this, the editor will be used.

理论是枯燥的，就让我们动手大干一场，实践出真知吧。按照国际惯例，第一个项目
必须是 hello world 。我们将用到刚刚讲到的编辑器。

When godot executable is run outside a project, the Project Manager
appears. This helps developers manage their projects.

.. image:: /img/project_manager.png

To create a new project, the "New Project" option must be used. Choose
and create a path for the project and specify the project name:

.. image:: /img/create_new_project.png

Editor
------

Once the "New Project" is created, the next step is opening it. This
will open the Godot editor. Here is how the editor looks when freshly
opened:

.. image:: /img/empty_editor.png

As mentioned before, making games in Godot feels like being in a
kitchen, so let's open the refrigerator and add some fresh nodes to the
project. We'll begin with a Hello World! To do this, the "New Node"
button must be pressed:

.. image:: /img/newnode_button.png

This will open the Create Node dialog, showing the long list of nodes
that can be created:

.. image:: /img/node_classes.png

From there, select the "Label" node first. Searching for it is probably
the quickest way:

.. image:: /img/node_search_label.png

And finally, create the Label! A lot happens when Create is pressed:

.. image:: /img/editor_with_label.png

First of all, the scene is changed to the 2D editor (because Label is
a 2D Node type), and the Label appears, selected, at the top left
corner of the viewport.

The node appears in the scene tree editor (box in the top left
corner), and the label properties appear in the Inspector (box on the
right side).

The next step will be to change the "Text" Property of the label, let's
change it to "Hello, World!":

.. image:: /img/hw.png

Ok, everything's ready to run the scene! Press the PLAY SCENE Button on
the top bar (or hit F6):

.. image:: /img/playscene.png

Aaaand... Oops.

.. image:: /img/neversaved.png

Scenes need to be saved to be run, so save the scene to something like
hello.scn in Scene -> Save:

.. image:: /img/save_scene.png

And here's when something funny happens. The file dialog is a special
file dialog, and only allows to save inside the project. The project
root is "res://" which means "resource path. This means that files can
only be saved inside the project. For the future, when doing file
operations in Godot, remember that "res://" is the resource path, and no
matter the platform or install location, it is the way to locate where
resource files are from inside the game.

After saving the scene and pressing run scene again, the "Hello, World!"
demo should finally execute:

.. image:: /img/helloworld.png

Success!

.. _doc_scenes_and_nodes-configuring_the_project:

Configuring the project
-----------------------

Ok, It's time to do some configuration to the project. Right now, the
only way to run something is to execute the current scene. Projects,
however, have several scenes so one of them must be set as the main
scene. This scene is the one that will be loaded at the time the project
is run.

These settings are all stored in the engine.cfg file, which is a
plaintext file in win.ini format, for easy editing. There are dozens of
settings that can be set in that file to alter how a project executes,
so to make matters simpler, a project setting dialog exists, which is
sort of a frontend to editing engine.cfg

To access that dialog, simply go to Scene -> Project Settings.

Once the window opens, the task will be to select a main scene. This can
be done easily by changing the application/main_scene property and
selecting 'hello.scn'.

.. image:: /img/main_scene.png

With this change, pressing the regular Play button (or F5) will run the
project, no matter which scene is being edited.

Going back to the project settings dialog. This dialog provides a lot
of options that can be added to engine.cfg and show their default
values. If the default value is ok, then there isn't any need to
change it.

When a value is changed, a tick is marked to the left of the name.
This means that the property will be saved to the engine.cfg file and
remembered.

As a side note, for future reference and a little out of context (this
is the first tutorial after all!), it is also possible to add custom
configuration options and read them in run-time using the
:ref:`Globals <class_Globals>` singleton.

To be continued...
------------------

This tutorial talks about "scenes and nodes", but so far there has been
only *one* scene and *one* node! Don't worry, the next tutorial will
deal with that...
