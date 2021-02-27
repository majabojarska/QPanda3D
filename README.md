# QPanda3D

A PyQt5 wrapper for Panda3D scenes. Allows embedding a Panda3D world within a PyQt5 GUI.

**This package is still a work in progress.**

What works:

- Embedding a Panda3D world inside a QWidget, that can be placed within a PyQt5 GUI.
- Full access to Panda3D nodes.
- Hardware support:
    - Key press and release events. This includes `Ctrl`, `Shift`, `Alt` modifier keys and mouse buttons.
    - Mouse movement and scroll wheel events.

What doesn't work yet:

- Timed keyboard interactions.

## Installation

```bash
pip install QPanda3D
```

## Usage

### 1. Subclass Panda3DWorld to implement a custom world.

```python
from QPanda3D.Panda3DWorld import Panda3DWorld

class MyWorld(Panda3DWorld):
    def __init__(self):
        Panda3DWorld.__init__(self, width=1024, height=768)
        # from this point, act as if you are defining a classic Panda3D environment.
        self.cam.setPos(0, -28, 6)
        self.testModel = self.loader.loadModel('panda')
        self.testModel.reparentTo(self.render)
```

### 2. Embed a Panda3DWorld instance within a PyQt5 GUI

```python
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
```

## Special thanks

I want to thank all the contributors to this little open source project. In chronological order:

- Thanks to [fraca7](https://github.com/fraca7) for his commit (Change film size according to widget resize)
- Many thanks to [nmevenkamp](https://github.com/nmevenkamp) for the valuable updates and bugfixes he contributed to this project.

If other people want to contribute to this project, they're welcome.
