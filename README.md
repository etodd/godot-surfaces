# Surfaces

A Godot 4 plugin that detects the kind of surface a player is standing on by
inspecting mesh materials.

## Instructions

1. Install and enable the plugin.
2. Re-import your environment meshes. The plugin will split up any mesh that has
   multiple materials and a static
   [`ConcavePolygonShape3D`](https://docs.godotengine.org/en/stable/classes/class_concavepolygonshape3d.html#class-concavepolygonshape3d)
   into separate collision meshes so that each material corresponds to a
   separate collision mesh.
3. Set up a
   [`RayCast3D`](https://docs.godotengine.org/en/stable/classes/class_raycast3d.html)
   node on your player object.
4. Use this code in your `_physics_process` function to get the name of the
   material the player is standing on:
```
if raycast.get_collider() is CollisionObject3D:
    var material_name: String = Surfaces.detect(raycast.get_collider())
```

## Tips

- If you're using Blender, simply add `-col` to the name of your mesh object to
  give it a static `ConcavePolygonShape3D`.
- Add `-convcol` to make it a `ConvexPolygonShape3D` instead. The plugin
  does not split up convex meshes, so `Surfaces.detect` will instead return the
  name of the first material on the mesh.
- To create a custom collision mesh that's different than the visible mesh, add
  a new mesh as a child of the visible mesh and add `-colonly` or
  `-convcolonly` to the name. `Surfaces.detect` will search through the parents
  of the collision mesh until it finds a visible mesh and use that to determine
  the material.
