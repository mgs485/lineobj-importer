# lineobj-importer
### Problem
Whenever Unity imports a mesh, it will only recognize primitives which are connected to a face. Any floating vertices or edges will not be imported. For example, this `.obj` has no faces, so when it is imported into Unity, no `Mesh` object will be created for it:
```
o Plane
v -1.000000 0.000000 1.000000
v 1.000000 0.000000 1.000000
v -1.000000 0.000000 -1.000000
v 1.000000 0.000000 -1.000000
l 3 1
l 1 2
l 2 4
l 4 3
```
`lineobj-importer` is a custom parser to fix this problem. The parser detects when `.lineobj` files are imported via an experimental Unity feature available from version `2017.1` called [Scripted Importers](https://docs.unity3d.com/Manual/ScriptedImporters.html).

### Results
Before (in Blender):

![Before](/examples/readme/before.gif?raw=true "Before")

After (in Unity):

![Final](/examples/readme/final.gif?raw=true "Final")

![Prefab](/examples/readme/final-prefab.jpg?raw=true "Prefab")

### Usage
1. Place [LineobjImporter.cs](examples/basic-usage/Assets/LineobjImporter.cs) anywhere in your Unity project.
2. Export model as `.obj` from Blender with these settings:

    ![Blender export settings](/examples/readme/blender-export-settings.jpg?raw=true "Blender export settings")

    The most important thing is to check `Triangulate Faces`. The importer will not work if you don't triangulate the faces. Other settings like `Include UVs`, `Write Materials`, or `Write Normals` can be turned on, but this importer will ignore these settings.

3. Rename the file extension from `.obj` to `.lineobj`

4. When you open Unity, the model should automatically be imported. All Blender objects should have been flattened and merged into a single `Mesh`.

### Known to work with versions:
* Blender: 2.78
* Unity: 2017.1

### Supported OBJ features
* Vertices
* Edges
* Faces

### Unsupported OBJ features
* Vertex Normals
* Vertex Colors
* Texture coordinates
* Free-form geometry (like NURBS)
* Negative indices
* Materials
* Smooth shading
* Groups
* Object Names

### Contribution
* The current implementation is good enough for my purposes. I might add Blender plugin that enables importing `.lineobj` in order to speed up the development process, and I might add vertex normals, but beyond that, I don't foresee myself adding any more features to this for the time being. But if you would like to contribute, go ahead and submit a PR and add your name and github email to [`contributors.txt`](contributors.txt).
* Thanks to [Tim R.](https://gamedev.stackexchange.com/users/9002/tim-r) for pointing me in the right direction.
