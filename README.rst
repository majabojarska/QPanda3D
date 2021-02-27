QPanda3D
========

A PyQt5 wrapper for Panda3D scenes. Allows embedding a Panda3D world within a PyQt5 GUI.

.. warning::

    This package is still a work in progress.

What works:

- Embedding a Panda3D world inside a QWidget, that can be placed within a PyQt5 GUI.
- Full access to Panda3D nodes.
- Hardware support:

  - Key press and release events. This includes `Ctrl`, `Shift`, `Alt` modifier keys and mouse buttons.
  - Mouse movement and scroll wheel events.

What is known to **not** work:

- Timed keyboard interactions.

Installation
------------

Install the latest version of `QPanda3D` from `PyPI` via `pip`.

.. code-block:: bash

    pip install -U QPanda3D

Usage
-----

1. Subclass Panda3DWorld.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Implement a custom world by subclassing `Panda3DWorld`.

.. code-block:: python

    from QPanda3D.Panda3DWorld import Panda3DWorld


    class MyWorld(Panda3DWorld):
        def __init__(self):
            Panda3DWorld.__init__(self, width=1024, height=768)
            # from this point, act as if you are defining a classic Panda3D environment.
            self.cam.setPos(0, -28, 6)
            self.testModel = self.loader.loadModel('panda')
            self.testModel.reparentTo(self.render)

2. Embed Panda3DWorld within a PyQt5 GUI.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

    import sys

    from PyQt5.QtWidgets import QApplication, QMainWindow
    from QPanda3D.QPanda3DWidget import QPanda3DWidget


    if __name__ == "__main__":
        world = MyWorld()

        app = QApplication(sys.argv)
        appw = QMainWindow()
        appw.setGeometry(50, 50, 800, 600)

        pandaWidget = QPanda3DWidget(world)
        appw.setCentralWidget(pandaWidget)
        appw.show()

        sys.exit(app.exec_())
