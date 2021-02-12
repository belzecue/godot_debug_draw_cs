# Debug drawing utility

This is a debug drawing script, which you can setup as an autoload singleton. Written in C#, so only Godot Mono supported.

Inspired by Zilann's addon for the GDScript https://github.com/Zylann/godot_debug_draw

## Features

Primitives:

* Box
* Sphere
* Cylinder
* Line
* Line with Arrow
* Line Path
* Camera Frustum
* Billboard opaque square
* Position 3D (3 crossing axis)

Overlay:

* Text (with grouping and coloring)
* FPS Graph

No need to warry about removing or disabling functionality of this addon in export builds. Everything in this addon will be disabled automatically.

## Usage

1. Copy `addons/debug_draw_cs` to your `addon` folder, create it if the folder doesn't exist.
1. Rebuild project.
1. Add `addons/debug_draw_cs/DebugDraw.cs` to your project as autoload singleton.
1. (Optionally) Enable the `Debug Draw For Editor` plugin to enable debug drawing support inside the editor.

Example (information about all public static functions and properties is present inside the script):

```csharp
public override void _Process(float delta)
{
    var time = OS.GetTicksMsec() / 1000f;
    var box_pos = new Vector3(0, Mathf.Sin(time * 4f), 0);
    var line_begin = new Vector3(-1, Mathf.Sin(time * 4f), 0);
    var line_end = new Vector3(1, Mathf.Cos(time * 4f), 0);

    DebugDraw.DrawBox(box_pos, new Vector3(1, 2, 1), new Color(0, 1, 0), 0, false);
    DebugDraw.DrawLine3D(line_begin, line_end, new Color(1, 1, 0));
    DebugDraw.SetText("Time", time);
    DebugDraw.SetText("Frames drawn", Engine.GetFramesDrawn());
    DebugDraw.SetText("FPS", Engine.GetFramesPerSecond());
    DebugDraw.SetText("delta", delta);
}
```

![image](screenshot_3.png)

## More screenshots

`DebugDrawDemoScene.tscn` in editor
![image](screenshot_1.png)

`DebugDrawDemoScene.tscn` in play mode
![image](screenshot_2.png)