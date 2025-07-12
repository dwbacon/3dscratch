# Project Variables and Custom Blocks

This document lists variables defined in the project and the custom blocks implemented in the `renderer` sprite.

## Stage Variables
- CamSpeed: controls how fast the camera moves when the user presses the movement keys
- ModelTris: stores how many triangles were imported from the OBJ model
- ModelVerts: stores the total number of vertices in the model
- RotSpeed: sets the rotation rate used for camera turning
- a: temporary scratch variable used in calculations
- b: another temporary value used for short expressions
- c: third scratch variable for intermediate results
- ch: holds the current character while parsing OBJ text
- cmd: numeric index of the current command being processed
- current: loop index pointing to the currently processed item
- cx: x coordinate of the camera in the 3D world
- cy: y coordinate of the camera in the 3D world
- cz: z coordinate of the camera in the 3D world
- d: generic distance value for distance calculations
- draggingVert: set to true while a vertex is being dragged with the mouse
- far: distance to the far clipping plane
- floor y: vertical position where the floor grid is drawn
- gridSize: spacing between grid lines in the floor display
- i: loop counter i for general use
- idxtext: text of the index currently being read or displayed
- isDragging: flag indicating the mouse is being dragged
- j: secondary loop counter j
- k: tertiary loop counter k
- line: contents of the line currently parsed from OBJ
- max: generic maximum value used for clamping
- maxLine: highest line number found during import
- min: generic minimum value
- minLine: lowest line number encountered
- mode: indicates which rendering mode or tool is active
- mouseStartX: mouse x position when drag started
- mouseStartY: mouse y position when drag started
- moveDX: x translation amount to move the camera
- moveDY: y translation amount to move the camera
- moveDZ: z translation amount to move the camera
- my variable: placeholder variable not currently used
- near: distance to the near clipping plane
- objlines: count of OBJ file lines read from disk
- p: general purpose parameter for computations
- pitch: camera pitch angle in degrees
- px: projected x position on the screen
- px2: secondary projected x value
- pxA: screen x of triangle vertex A
- pxB: screen x of triangle vertex B
- py: projected y position on the screen
- py2: secondary projected y value
- pyA: screen y of triangle vertex A
- pyB: screen y of triangle vertex B
- roll: camera roll angle in degrees
- sb2b: helper value for Scratch to ScratchB blocks
- screenCenterX: x coordinate of the screen centre
- screenCenterY: y coordinate of the screen centre
- selectedVert: index of the currently selected vertex
- sx: x scale factor applied when transforming
- sxa: projected x value for vertex A
- sxb: projected x value for vertex B
- sy: y scale factor used in transforms
- sya: projected y value for vertex A
- syb: projected y value for vertex B
- sz: z scale factor for the model
- sz2: secondary z scale value
- sz2a: second z value for vertex A
- sz2b: second z value for vertex B
- sza: z coordinate of vertex A in world space
- szb: z coordinate of vertex B in world space
- szb2: alternate z value for vertex B
- t: current time or frame counter
- tokens: list of tokens parsed from OBJ text
- tri: index of the triangle being processed
- vx: x coordinate of a temporary vertex
- vxa: x coordinate of vertex A
- vxb: x coordinate of vertex B
- vy: y coordinate of a temporary vertex
- vya: y coordinate of vertex A
- vyb: y coordinate of vertex B
- vz: z coordinate of a temporary vertex
- vza: z coordinate of vertex A
- vzb: z coordinate of vertex B
- x: width of the view or generic x value
- xa: temporary x value a
- xb: temporary x value b
- ya: temporary y value a
- yaw: camera yaw angle in degrees
- yb: temporary y value b
- z: height of the view or generic z value
- za: temporary z value a
- zb: temporary z value b

## Stage Lists
The stage defines several lists used by the renderer to keep model data and
intermediate results.
- VerticesX / VerticesY / VerticesZ: store X, Y and Z coordinates for each imported vertex
- UVsU / UVsV: hold the U and V texture coordinates in the same order as the vertices
- TrianglesA / TrianglesB / TrianglesC: vertex indices composing each triangle
- TrianglesUVA / TrianglesUVB / TrianglesUVC: UV index for each corner of a triangle
- ProjectedX / ProjectedY / ProjectedZ: transformed coordinates written during projection
- ProjX / ProjY / ProjZ: temporary screen positions for the active triangle
- SelVerts: indices of vertices currently selected by the editor
- HandleID: numeric identifiers for the editing handles
- ShapesStart / ShapesLen / ShapesType: properties describing each shape in the scene
- vx / vy / vz: per-vertex workspace variables used while editing
- tokens: text tokens parsed from OBJ strings
- OBJlist: individual lines loaded from the OBJ file

## Custom Blocks in `renderer`
- Draw3dLine (advanced) %s %s %s %s %s %s: render an antialiased 3D line
- DrawFloorGrid: draw the floor grid
- DrawModelEdges: draw all edges of the model
- DrawTriangle: render a triangle
- ImportOBJ: load an OBJ format model
- MoveCamera: update the camera position
- Render3D: main 3D rendering loop
- SetCamera %s %s %s %s: set camera position and rotation
- TransformVertices: transform model vertices for rendering
- first slash %s: get text before first slash

## Searching `project.json`
After unzipping `Project.sb3` you will find `project.json`. Once the file is
pretty-printed, these commands help you quickly list data relevant to the
`renderer` sprite:

- **Stage variable names**
  ```bash
  jq -r '.targets[] | select(.isStage) | .variables | to_entries | .[].value[0]' project.json
  ```
- **Stage list names**
  ```bash
  jq -r '.targets[] | select(.isStage) | .lists | to_entries | .[].value[0]' project.json
  ```
- **Custom block names in `renderer`**
  ```bash
  jq -r '.targets[] | select(.name=="renderer") | .blocks | to_entries | map(select(.value.opcode=="procedures_prototype")) | .[].value.mutation.proccode' project.json
  ```

These snippets let you jump straight to the data you need without manually
scanning the entire file. Use `grep -n <name> project.json` to locate a specific
variable or procedure quickly.
