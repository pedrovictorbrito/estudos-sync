@@0001

- Where to import QApplication from?
- What to pass to the constructor of QApplication?
- How to set window title and resize?
- What to pass to the constructor of QPushButton?
- How to make a button checkable (togglable)?
- How to connect to the toggled signal and what to receive from the lambda?
- How to show the window and execute the app?
- How to create a layout, add widgets and attach it to a container?
- 

import sys
from PySide6.QtWidgets import QApplication, QMainWindow, QPushButton

# 1. Create the application instance
app = QApplication(sys.argv)

# 2. Create the main window
window = QMainWindow()
window.setWindowTitle("My First App")
window.resize(400, 300)

# 3. Add a widget
button = QPushButton("Click Me", window)
button.setCheckable(True)
window.setCentralWidget(button)

button = QPushButton("Mute")
button.setCheckable(True)

# Connect to the 'toggled' signal
button.toggled.connect(lambda checked: print("Muted" if checked else "Unmuted"))

# 4. Show the window and start the event loop
window.show()
sys.exit(app.exec())

def button_was_clicked():
    print("The button was pressed!")

button = QPushButton("Click Me")

# Connect the signal (clicked) to the slot (the function)
button.clicked.connect(button_was_clicked)

from PySide6.QtWidgets import QVBoxLayout, QWidget, QLabel

layout = QVBoxLayout()

layout.addWidget(QLabel("Top Label"))
layout.addWidget(QPushButton("Bottom Button"))

container = QWidget()
container.setLayout(layout)
window.setCentralWidget(container)

class MyWindow(QMainWindow):
    def __init__(self):
        super().__init__()

        self.setWindowTitle("Class-based App")
        
        self.button = QPushButton("Press me")
        self.button.clicked.connect(self.handle_click)
        
        self.setCentralWidget(self.button)

    def handle_click(self):
        self.button.setText("You clicked it!")

app = QApplication(sys.argv)
window = MyWindow()
window.show()
app.exec()

from PySide6.QtWidgets import QMainWindow, QWidget, QVBoxLayout, QPushButton, QTextEdit

class MyWindow(QMainWindow):
    def __init__(self):
        super().__init__()

        # 1. Create a container widget
        self.container = QWidget()
        
        # 2. Create a layout and add your UI elements to it
        layout = QVBoxLayout()
        layout.addWidget(QTextEdit())
        layout.addWidget(QPushButton("Submit"))
        
        # 3. Apply the layout to the container
        self.container.setLayout(layout)

        # 4. Tell the QMainWindow to use this container as the "living room"
        self.setCentralWidget(self.container)
 
