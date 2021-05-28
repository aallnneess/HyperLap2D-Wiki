Before runtime can render [Talos VFX](https://talosvfx.com/) a custom extension needs to be loaded into `SceneLoader`

First add dependencies
```groovy
dependencies {
    api "com.talosvfx:talos-libgdx:$talosVersion"
    api "games.rednblack.hyperlap2d:libgdx-talos-extension:$h2dTalosExtension"
}
```

Use [compatibility table](https://github.com/rednblackgames/h2d-libgdx-talos-extension) to choose right version for each dependence.

Then inject newly loaded code into `SceneLoader`

```Java
mSceneLoader.injectExternalItemType(new TalosItemType());
```

Congratulations! Now runtime is able to render `TalosVO` objects.

### Additional Components

You can access to additional `TalosComponent` to work with Talos data.

```Java
TalosComponent talosComponent = ComponentRetriever.get(portal, TalosComponent.class);
talosComponent.effect.restart();
```