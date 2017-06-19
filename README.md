PyDark
======

PyDark is a 2D and Online Multiplayer video game framework written on-top of Python and PyGame. 

Our goal with PyDark was to make it easy to learn and integrate into existing pygame applications. PyDark is designed to be fully customizable and scalable, allowing developers to inherit base classes and make new sub-classes.

**Prerequisites:** Python 2.7.x, PyGame, Twisted


Overview
========
PyDark runs on top of PyDark.engine.Scene objects. A scene is a collection of objects that are displayed within' the scene. Think of it like a movie scene, where a series of scenes define a movie.

In a nutshell, you have a collection of modules avaialble to you, them being:
1. PyDark.engine (core functionality, i.e.: Scenes, Sprites, etc).
2. PyDark.ui (base UI elements for your game, integrate them into your games or build entirely new UI elements).
3. PyDark.net (twisted networking TCP and UDP client/server networking classes)
4. PyDark.io (series of functions and classes for file-access, SpriteSheet loading, encryption, map generation and much more)
5. PyDark.constants (classes that define PyDark event types)
6. PyDark.icon (static module containing base64 encoded string of base window icon)
7. PyDark.vector2d (contains base vector2d class for 2D vector math functionality) 

Examples
========
**Main menu**
> A simple example showcasing PyDarks UI module that displays a main menu scene. Keep in mind you'll be needing to manually provide the following files: (input.png, input_selected.png, click.wav, button.png, button_hover.png).
```
import PyDark.engine
import PyDark.ui
import PyDark.vector2d


def login_button_pressed(event):
    global game
    game.currentScene = "game_scene"
    print event, event.fired_by
    print username.text
    print password.text
    

game = PyDark.engine.Game(
    title="FrowCraft",
    window_size=(800, 650),
    center_window=True,
    FPS=30,
    online=True,
    server_ip="localhost",
    server_port=8000
)

login_scene = PyDark.engine.Scene(surface=game, name="login_scene")
game_scene = PyDark.engine.Scene(surface=game, name="game_scene")

login_overlay = PyDark.ui.Overlay(
    parent=login_scene,
    size=(login_scene.window_size()[0], 330),
    image="login_overlay_bg.jpg",
    position=(0,0),
)


login_header = PyDark.ui.Label(
    name="login_header",
    text="FrowCraft",
    size=30,
    font="Arial",
    color=PyDark.engine.Color(255, 255, 255, 1),
    position=(100, 10),
    aa=True,
    center=True
)

username_label = PyDark.ui.Label(
    name="username_label",
    text="Username:",
    size=14,
    font="Arial",
    color=PyDark.engine.Color(0, 0, 0, 1),
    position=(0, 60),
    center=True
)

username = PyDark.ui.TextBox(
    name="username",
    position=(100, 80),
    center=True,
    default_image="input.png",
    image_selected="input_selected.png"
)

password_label = PyDark.ui.Label(
    name="password_label",
    text="Password:",
    size=14,
    font="Arial",
    color=PyDark.engine.Color(0, 0, 0, 1),
    position=(0, 150),
    center=True
)

password = PyDark.ui.TextBox(
    name="password",
    position=(0, 170),
    center=True,
    default_image="input.png",
    image_selected="input_selected.png"
)

login_button = PyDark.ui.Button(
    name="login_button",
    position=(100, 260),
    on_press=login_button_pressed,
    center=True,
    sound="click.wav",
    default_image="button.png",
    image_hover="button_hover.png",
    image_selected="button_hover.png"
)

login_overlay.add_object(login_header)
login_overlay.add_object(username_label)
login_overlay.add_object(username)
login_overlay.add_object(password_label)
login_overlay.add_object(password)
login_overlay.add_object(login_button)

login_scene.add_object(login_overlay)

game.add_scene(login_scene)
game.add_scene(game_scene)

game.currentScene = "login_scene"
game.start()
```
