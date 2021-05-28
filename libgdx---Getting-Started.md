## Quick Start?

[Working example](https://github.com/rednblackgames/hyperlap2d-getting-started)

# Basic Integration

Runtime needs to be included into your `core` project.
```groovy
dependencies {
    //HyperLap2D Runtime
    api "games.rednblack.hyperlap2d:runtime-libgdx:$h2dVersion"

    //Mandatory
    api "com.badlogicgames.gdx:gdx:$gdxVersion"
    api "com.badlogicgames.gdx:gdx-box2d:$gdxVersion"
    api "com.badlogicgames.gdx:gdx-freetype:$gdxVersion"
    api "com.badlogicgames.ashley:ashley:$ashleyVersion"

    //Optional - typing labels
    api "com.rafaskoberg.gdx:typing-label:$typingLabelVersion"
}
```

Use [compatibility table](https://github.com/rednblackgames/hyperlap2d-runtime-libgdx#support) to choose right version for each dependence.

### Architecture
HyperLap2D's libGDX runtime is based on Entity Component System (ECS) architecture using [Ashley](https://github.com/libgdx/ashley) library. If you are not familiar with this kind of design pattern, please consider to [learn more](https://en.wikipedia.org/wiki/Entity_component_system) before continue reading.

### SceneLoader

A `SceneLoader`is the object that helps you to setup minimal working configuration for HyperLap to work. It parse `JSON` format to build ECS Engine, Entities and all required Components to render your scenes and assets.

**NOTE:** This runtime uses `PooledEngine`.

```Java
mCamera = new OrthographicCamera();
mViewport = new ExtendViewport(360, 640, 0, 0, mCamera);

//Initialize HyperLap2D's SceneLoader, all assets will be loaded here
mSceneLoader = new SceneLoader();
//Load the desired scene with custom viewport
mSceneLoader.loadScene("MainScene", mViewport);
```

By default `SceneLoader` create a `ScreenViewPort`, in many cases this is not what you want, especially if you target Pixel per World Unit  other than 1. You can measure the size of your world using [guidelines](https://github.com/rednblackgames/HyperLap2D/wiki/Editor-UI#guidelines) in order to choose the best ViewPort for your scene.

### Rendering scene

Runtime Engine already have all necessary Systems for rendering and basic entities manipulation. `SceneLoader` is a wrapper for all these features. This will make rendering very easy, just update ECS Engine.

```Java
@Override
public void render() {
    mCamera.update(); //Update camera

    //Clear screen
    Gdx.gl.glClearColor(0, 0, 0, 1);
    Gdx.gl.glClear(GL20.GL_COLOR_BUFFER_BIT);

    //Apply ViewPort and update SceneLoader's ECS engine
    mViewport.apply();
    mSceneLoader.getEngine().update(Gdx.graphics.getDeltaTime());
}
```

### Retrieve Entities and navigate through composites 

Ashley's Entities are basically empty objects, they can't contains methods or fields while any definition is provided by their Components. To help you navigate and manipulate elements you can use the `ItemWrapper` class that expose some useful methods.
By default all objects are placed in a single root `Composite`.

```Java
ItemWrapper root = new ItemWrapper(mSceneLoader.getRoot());
```

You can navigate inside nested composites with `ItemWrapper#getChild` using object's [unique identifier](https://github.com/rednblackgames/HyperLap2D/wiki/Basic-Tools#basic-properties):
```Java
ItemWrapper foo = root.getChild("foo")
```

### Default Components

There are several default components created for each Entity.

* `MainItemComponent` : This is present almost in any object and contains core information like entity type, identifier, unique Id, custom variables etc.
* `TransformComponent`, `DimensionComponent` `TintComponent` `ZIndexComponent` : These are present in almost any object too and contains information like position, dimension, origin point, rotation, z-index, color etc.
* `NodeComponent` : Is present in any `Composite Item`, it stores children references as `Entity` objects.
* `ViewportComponent` : Can be present only on a single Entity. It's the point where rendering pipeline starts from. Usually `root` composite has this component.

Specific components are created based on entity's type, for example `TextureRegionComponent`, `LabelComponent`, `ActionComponent` ,`LightObjectComponent`, `ParticleComponent`, `SpriteAnimationComponent`, `PhysicsBodyComponent` and much more. [Full list](https://github.com/rednblackgames/hyperlap2d-runtime-libgdx/tree/master/src/main/java/games/rednblack/editor/renderer/components)

### Actions System

HyperLap2D uses an Actions System similar to [libGDX's Scene2D actions](https://github.com/libgdx/libgdx/wiki/Scene2d#actions) but for ECS pattern. You can manually create actions in Java, or use [Node Graph Editor](https://github.com/rednblackgames/HyperLap2D/wiki/Actions).

```Java
ActionData rotation = Actions.sequence(
            Actions.delay(2),
            Actions.parallel(
                    Actions.moveBy(-30, -30, 5, Interpolation.pow2),
                    Actions.rotateBy(180, 2, Interpolation.exp5))
    );
ActionData repeatData = Actions.forever(rotation);

Actions.addAction(mSceneLoader.getEngine(),  entity, repeatData);
```

Load Actions from library:
```Java
ActionData actionData = mSceneLoader.loadActionFromLibrary("testAction");

Actions.addAction(mSceneLoader.getEngine(),  entity, actionData);

//Load actions with params and event listener
ObjectMap<String, Object> params = new ObjectMap<>();
params.put("delay", 2f);

ActionData actionData = mSceneLoader.getActionFactory().loadFromLibrary("test", params, new ActionEventListener() {
    @Override
    public void onActionEvent(String s) {
        System.out.println("Triggered event: " + s);
    }
});

Actions.addAction(mSceneLoader.getEngine(),  entity, actionData);
```

### Create entities at runtime with `EntityFactory`

`EntityFactory` helps you create runtime objects ready to be used with this runtime. Before creating the real entity, you have to describe it using a `VO` class. Common `VO`s are: `SimpleImageVO`, `Image9patchVO`, `LabelVO`, `CompositeItemVO`, `ParticleEffectVO`, `LightVO`, `SpriteAnimationVO`, `ColorPrimitiveVO`, `TalosVO`, `SpineVO`. [Full list](https://github.com/rednblackgames/hyperlap2d-runtime-libgdx/tree/master/src/main/java/games/rednblack/editor/renderer/data)

```Java
LabelVO labelVO = new LabelVO();
labelVO.itemIdentifier = "unique_id_name";
labelVO.text = "This is a runtime label";
labelVO.style = "Lato";
labelVO.size = 26;
labelVO.layerName = "Default";
labelVO.x = 10;
labelVO.y = 10;
labelVO.width = 100;
labelVO.height = 100;

Entity label = mSceneLoader.getEntityFactory().createEntity(root, labelVO);
mSceneLoader.getEngine().addEntity(label);
```
**Load Composite Item from HyperLap2D's Library**
```Java
CompositeItemVO sheepData = mSceneLoader.loadVoFromLibrary("sheep");
sheepData.layerName = "Default";
sheepData.x = 100;
sheepData.y = 100;

Entity sheep = mSceneLoader.getEntityFactory().createEntity(root, sheepData);
mSceneLoader.getEntityFactory().initAllChildren(mSceneLoader.getEngine(), sheep, sheepData.composite);
mSceneLoader.getEngine().addEntity(sheep);
```

### Resource Management

Each asset (image, font, etc.) needs to be loaded and unloaded according to game needs. This can be done using `IResourceRetriever` interface and pass it to `SceneLoader` constructor.

Methods in `IResourceRetriever` are invoked whenever `EntityFactory` needs an asset. You are free to implement this part according to needs of your game. You can use the default [`ResourceManager`](https://github.com/rednblackgames/hyperlap2d-runtime-libgdx/blob/master/src/main/java/games/rednblack/editor/renderer/resources/ResourceManager.java).