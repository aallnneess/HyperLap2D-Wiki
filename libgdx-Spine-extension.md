Before runtime can render [Spine Animations](http://en.esotericsoftware.com/) a custom extension needs to be loaded into `SceneLoader`

First add dependencies
```groovy
dependencies {
    api "com.esotericsoftware.spine:spine-libgdx:$spineVersion"
    api "games.rednblack.hyperlap2d:libgdx-spine-extension:$h2dSpineExtension"
}
```

Use [compatibility table](https://github.com/rednblackgames/h2d-libgdx-spine-extension) to choose right version for each dependence.

Then inject newly loaded code into `SceneLoader`

```Java
mSceneLoader.injectExternalItemType(new SpineItemType());
```

Congratulations! Now runtime is able to render `SpineVO` objects.

### Additional Components

You can access to additional `SpineObjectComponent` to work with Spine data.

```Java
SpineObjectComponent spineObjectComponent = ComponentRetriever.get(sheepAnimation, SpineObjectComponent.class);
spineObjectComponent.state.setAnimation(0, "death", false);
```