# Godot

## From the documentation

- Enable low-processor mode when creating non-game applications ([See docs](https://docs.godotengine.org/en/stable/classes/class_projectsettings.html#class-projectsettings-property-application-run-low-processor-mode))
- The Godot licensing should be put in the credits ([See docs](https://docs.godotengine.org/en/stable/about/complying_with_licenses.html))
- `$` is shorthand for `get_node()`
- Clamping a value means restricting it to a given range
- The `delta` parameter in the `_process()` function refers to the frame length
- Using `set_deferred()` tells Godot to wait to do something until it's safe to do so
- The default font for `Control` nodes is small and doesn't scale well
- When you need to pause for a brief time, an alternative to using a `Timer` node is to use the `SceneTree`'s `create_timer()` function
- The `.glb` files contain 3D scene data based on the open source GLTF 2.0 specification
- In 3D, the XZ plane is the ground plane
- `CharacterBody3D.move_and_slide()` allows you to move a character smoothly
- If directional shadows look too blurry after switching to an orthogonal camera, decrease the camera's Far property to a lower value such as 100
- Masks control the layers that a body will listen to and detect
- Layers define on which physics layer(s) an object is
- In 3D, the Y axis is positive upwards. In 2D, the Y axis is positive downwards

## Practical considerations

### 1. Add units to export variables

```py
@export var fall_acceleration = 75 # in meter/second^2
@export var jump_impulse = 20 # in meters/second
```