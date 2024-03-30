# Godot

## From the documentation

- Enable low-processor mode when creating non-game applications ([See docs](https://docs.godotengine.org/en/stable/classes/class_projectsettings.html#class-projectsettings-property-application-run-low-processor-mode))
- The Godot licensing should be put in the credits ([See docs](https://docs.godotengine.org/en/stable/about/complying_with_licenses.html))
- The default font for `Control` nodes is small and doesn't scale well ([See docs](https://docs.godotengine.org/en/4.0/tutorials/ui/gui_using_fonts.html))
- If directional shadows look too blurry after switching to an orthogonal camera, decrease the camera's `Far` property to a lower value such as `100` ([See docs](https://docs.godotengine.org/en/4.0/tutorials/3d/lights_and_shadows.html))
- Masks control the layers that a body will listen to and detect ([See docs](https://docs.godotengine.org/en/4.0/tutorials/physics/physics_introduction.html#collision-layers-and-masks))- You can use the autoload feature to have Godot load a node or a scene automatically at the start of the game, outside the current scene ([See docs](https://docs.godotengine.org/en/stable/tutorials/scripting/singletons_autoload.html#doc-singletons-autoload))
- Directly animating the `Player` node would prevent movement through code. Use a `Pivot` ([See docs](https://docs.godotengine.org/en/stable/getting_started/first_3d_game/09.adding_animations.html#the-float-animation))


### GDScript

- `$` is shorthand for `get_node()` ([See docs](https://docs.godotengine.org/en/4.0/tutorials/scripting/scene_unique_nodes.html#creation-and-usage))
- Clamping a value means restricting it to a given range ([See docs](https://docs.godotengine.org/en/4.0/contributing/development/core_and_modules/common_engine_methods_and_macros.html#clamp-a-value))
- The `delta` parameter in the `_process()` function refers to the frame length ([See docs](https://docs.godotengine.org/en/4.0/tutorials/scripting/scene_unique_nodes.html#creation-and-usage))
- Using `set_deferred()` tells Godot to wait to do something until it's safe to do so ([See docs](https://docs.godotengine.org/en/4.0/classes/class_object.html#class-object-method-set-deferred))
- When you need to pause for a brief time, an alternative to using a `Timer` node is to use the `SceneTree`'s `create_timer()` function ([See docs](https://docs.godotengine.org/en/4.0/classes/class_timer.html))
- Unused parameters can be prefixed with an `_` to avoid the editor warning ([See docs](https://github.com/godotengine/godot/issues/26056#issuecomment-465151648))


### 3D

- In 3D, the XZ plane is the ground plane ([See docs](https://docs.godotengine.org/en/4.0/tutorials/3d/introduction_to_3d.html#coordinate-system))
- `CharacterBody3D.move_and_slide()` allows you to move a character smoothly ([See docs](https://docs.godotengine.org/en/4.0/tutorials/physics/physics_introduction.html#move-and-slide))
- In 3D, the Y axis is positive upwards. In 2D, the Y axis is positive downwards ([See docs](https://docs.godotengine.org/en/4.0/getting_started/first_3d_game/06.jump_and_squash.html#jumping))


## Practical considerations

### 1. Add units to export variables

```py
@export var fall_acceleration : int = 75 # in meter/second^2
var jump_impulse : int = 20 # in meters/second
```