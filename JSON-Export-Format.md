**[Current Export format : 0.1.1]**

HyperLap2D export data into JSON format. This makes easily to render your compositions to any engine!

Exported data are saved into `.dt` format that contains a single JSON object, file is minimized so default values are omitted. The main file is `project.dt` and contains all basic information about your HyperLap2D project. It is organized as follow:
- `pixelToWorld` : how many pixels should be 1 World Unit
- `originalResolution` : resolution of the original assets
    * `name` : name of the resolution
    * `width` : width in pixels
    * `height` : height in pixels
    * `base` : size used to calculate automatic texture scaling, 0 for width, 1 for height
- `resolutions` : array of supported resolution in the same format of `originalResolution`
- `scenes` : array of object that contains only `sceneName`
- `libraryItems` : array of composites, for library items that can be placed on the scene at runtime with code
- `libraryActions` : array of actions, to create actions at runtime from node graph representation with a single line of code

Example of `project.dt` file
```JSON
{
  "pixelToWorld": 3,
  "originalResolution": {
    "name": "orig",
    "width": 1920,
    "height": 1080
  },
  "scenes": [
    {
      "sceneName": "MainScene"
    },
    {
      "sceneName": "scene2"
    }
  ],
  "libraryItems": {
    "item1": {
      ...
    },
    "item2": {
      ...
    }
  },
  "libraryActions": {
    "action1": {
      ...
    },
    "action2": {
      ...
    }
  }
}
```

## Scenes

Each scene is exported in its own `.dt` file placed in `/scenes` directory. This file contains some basic information as well as of all placed objects with their position:

- `sceneName` : name of the scene
- `lightsPropertiesVO` : describe ambient light
    * `enable` : boolean, true if scene use lights
    * `ambientColor` : array of 4 float value (in the range 0-1) for RGBA values
    * `lightType` : with type of light should be applied, supported `BRIGHT`, `DIFFUSE`, `DIRECTIONAL`
    * `directionalRays` : rays number for directional light
    * `directionalDegree` : degree of directional light
    * `directionalColor` : array of 4 float value (in the range 0-1) for RGBA values
- `physicsPropertiesVO` : describe ambient physic system
    * `enabled` : boolean, true if scene use physic
    * `gravityX` : x component of gravity force
    * `gravityY` : y component of gravity force
- `verticalGuides` : array of float values that indicate X coordinate of a vertical debug guideline
- `horizontalGuides` : array of float values that indicate X coordinate of a horizontal debug guideline
- `composite` : description of root scene and nested composites

Example of `<scene name>.dt` file
```JSON
{
  "sceneName": "MainScene",
  "composite": {
    ...
  },
  "physicsPropertiesVO": {
      "enabled": true,
      "gravityX":-1,
      "gravityY":-9
  },
  "lightsPropertiesVO": {
    "enabled": true,
    "ambientColor": [
      0.050980393,
      0.050980393,
      0.050980393,
      0.25882354
    ],
    "lightType": "DIRECTIONAL",
    "directionalRays": 300,
    "directionalDegree": -45,
    "directionalColor": [
      0.47843137,
      0.3137255,
      0.3137255,
      1
    ]
  },
  "verticalGuides": [
    358.5,
    0
  ],
  "horizontalGuides": [
    639.56464,
    0
  ]
}
```

### Composite object

It's the main container for any kind of objects that can be attached to the scene, it has a hierarchical recursive structure as follow:

- `sImages` : array of all images
- `sImage9patchs` : array of all 9-patches
- `sLabels` : array of all labels
- `sComposites` : array of composite info objects, each element has:
    * `width` : width in world unit
    * `height` : height in world unit
    * `automaticResize` : true if size should be dynamically calculated
    * `scissorsEnabled` : true if scissor should be applied to this composite
    * `composite` : ... recursive of the main composite object
- `sParticleEffects` : array of all particle effects
- `sLights` : array of all lights
- `sSpineAnimations` : array of all Spine animation
- `sSpriteAnimations` : array of all Sprite animations
- `layers` : array of all layers, each element has:
    * `layerName` : name of the layer
    * `isLocked` : if layer is locked or not
    * `isVisible` : if layer is visible or not

```JSON
{
    "sImages": [
      ...
    ],
    "sImage9patchs": [
      ...
    ],
    "sLabels": [
      ...
    ],
    "sComposites": [
      ...
    ],
    "sParticleEffects": [
      ...
    ],
    "sLights": [
      ...
    ],
    "sSpineAnimations": [
      ...
    ],
    "sSpriteAnimations": [
      ...
    ],
    "layers": [
      {
        "layerName": "Default",
        "isLocked": true,
        "isVisible": true
      },
      {
        "layerName": "Levels",
        "isVisible": true
      }
    ]
}
```  

### Main Item

Any object has different properties based on its type; however, every object has a common base that describe core information:
- `uniqueId` : unique number that identifies the entity
- `itemIdentifier` : unique string defined by the user identifies the entity
- `tags` : strings array of custom defined tags
- `customVars` : strings array of custom defined variables in the format `key:value`
- `x` and `y` : item coordinates
- `originX` and `originY` : local coordinates of origin position
- `rotation` : item rotation in degree
- `zIndex` : integer that indicate z-index in the layer
- `layerName` : name of the layer item belong
- `tint` : array of 4 float value (in the range 0-1) for RGBA values for the color used to multiply the texture to tint the item
- `shaderName` : string of the name of the custom shader
- `shaderUniforms` : object of objects that contains user defined uniforms
  * `uniformName`
    * `type` : type of the uniform, only allowed: `int`, `float`, `vec2`, `vec3`, `vec4`
    * `intValue` : value if uniform type is `int`
    * `floatValue` : value if uniform type is `float`
    * `floatValue2`, `floatValue3`, `floatValue4` : additional floats for `vec2`, `vec3` and `vec4`
- `shape` : describe the polygon shape of the item it contains:
  * `polygon` : array of array each contains a point of the polygon
- `physics` : describe the physic object

### sImages

Images has following additional fields:
- `imageName` : name of the texture
- `isRepeat` : true if the image has to be repeat when container is bigger than texture size
- `isPolygon` : true if texture should be rendered into polygon shape

### sImage9patchs

9-patch has following additional fields:
- `imageName` : name of the texture
- `width` and `height` : size of the item

### sLabels

Label has following additional fields:
- `text` : string of the user defined text
- `style` : name of the font
- `size` : font size
- `align` : integer that define align in [libGDX format](https://libgdx.badlogicgames.com/ci/nightlies/docs/api/com/badlogic/gdx/utils/Align.html)
- `width` and `height` : size of the container box
- `wrap` : create new line when text exceeds container width
- `isTyping` : if typing effect should be applied

### sParticleEffects

Particle Effect has following additional fields:
- `particleName` : string of the particle effect

### sLights

Light has following additional fields:
- `type` : type of the light `POINT` or `CONE`
- `rays` : number of light rays
- `distance` : light distance in world unit
- `directionDegree` : rotation for cone light
- `coneDegree` : cone section size in degree
- `softnessLength` : soft outer area
- `isStatic` : light position should not change
- `isXRay` : light should pass or not through physics bodies
- `isSoft` : enable softness
- `isActive` : enable or disable light

### sSpineAnimations

Spine (see [Esoteric Software](http://esotericsoftware.com/)) has following additional fields:
- `animationName` : name of the asset spine animation
- `currentAnimationName` : name of Spine current playing animation

### sSpriteAnimations

Sprite Animation has following additional fields:
- `animationName` : name of the sprite texture atlas
- `fps` : frame per seconds value
- `frameRangeMap` : each sprite texture atlas can be divided into multiple animation by defining their range, array of:
  * `name` : name of the animation
  * `startFrame` and `endFrame` : index of sprite atlas that define animation range
- `currentAnimation` : name of the current sub-animation defined as above
- `playMode` : how the animation should be played (0 = `Normal`, 1 = `Reversed`, 2 = `LOOP`, 3 = `Reversed Loop`, 4 = `PingPong Loop`, 5 = `Random Loop`)

### Actions

A single action is described as a graph structure **Current version is 1**: 
- `version` : indicate format version
- `nodes` : array of all nodes contained in the graph:
  * `id` : unique identifier for the node
  * `type` : type of the node, it describe what this action should be
  * `x` and `y` : used for graphical representation
- `connections` : array of all connections contained in the graph:
  * `fromNode` : unique id of the source node
  * `fromField` : name of the source field
  * `toNode` : unique id of the destination node
  * `toField` : name of destination field
- `groups` : array of groups used only in graphical representation:
  * `name` : name of the group
  * `nodes` : array of unique ids