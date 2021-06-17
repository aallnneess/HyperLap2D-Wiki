<b>Getting started with Html 5 with Hyperlap2D runtime</b>



If you want to be able to use your Hyperlap project in the browser using Html / Gwt, there is a lot to do.<br>
As of now, this is implemented as follows:<p>

<b>GdxDefinition.gwt.xml</b><p>
![image](https://user-images.githubusercontent.com/73443724/122401820-3d39ec80-cf7d-11eb-8401-c4650e36bc42.png)
  <p>
    
First we have to add some `extend-configuration-property`<br>
    They have to be placed inside the modules, and they are needed for Hyperlap2D per se:<p>
      
```
<extend-configuration-property name="gdx.reflect.include" value="java.util.HashSet" />

<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.environment.AmbientCubemap" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.environment.DirectionalLight" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.environment.DirectionalShadowLight" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.environment.SpotLight" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.environment.PointLight" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.environment.SphericalHarmonics" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.environment.ShadowMap" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.environment.BaseLight" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.loader.ObjLoader" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.loader.G3dModelLoader" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.ModelInstance" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.MeshPartBuilder" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.RenderContext" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.FirstPersonCameraController" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.shapebuilders.CylinderShapeBuilder" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.shapebuilders.SphereShapeBuilder" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.shapebuilders.ArrowShapeBuilder" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.shapebuilders.BaseShapeBuilder" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.shapebuilders.FrustumShapeBuilder" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.shapebuilders.PatchShapeBuilder" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.shapebuilders.BoxShapeBuilder" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.shapebuilders.EllipseShapeBuilder" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.shapebuilders.ConeShapeBuilder" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.shapebuilders.CapsuleShapeBuilder" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.shapebuilders.RenderableShapeBuilder" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.ShaderProvider" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.DefaultTextureBinder" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.TextureBinder" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.BaseAnimationController" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.TextureProvider" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.AnimationController" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.DefaultRenderableSorter" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.CameraInputController" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.TextureDescriptor" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.DepthShaderProvider" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.DefaultShaderProvider" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.MeshBuilder" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.RenderableSorter" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.BaseShaderProvider" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.ShapeCache" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.utils.ModelBuilder" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.emitters.Emitter" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.emitters.RegularEmitter" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.ParticleShader" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.ParticleEffect" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.renderers.PointSpriteControllerRenderData" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.renderers.ModelInstanceRenderer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.renderers.BillboardRenderer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.renderers.ModelInstanceControllerRenderData" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.renderers.ParticleControllerControllerRenderer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.renderers.PointSpriteRenderer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.renderers.ParticleControllerRenderData" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.renderers.ParticleControllerRenderer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.renderers.BillboardControllerRenderData" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.ParticleController" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.influencers.ModelInfluencer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.influencers.ColorInfluencer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.influencers.RegionInfluencer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.influencers.DynamicsInfluencer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.influencers.DynamicsModifier" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.influencers.ScaleInfluencer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.influencers.Influencer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.influencers.ParticleControllerFinalizerInfluencer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.influencers.ParticleControllerInfluencer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.influencers.SpawnInfluencer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.influencers.SimpleInfluencer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.ParticleChannels" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.ResourceData" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.ParticleControllerComponent" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.ParticleSystem" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.ParticleEffectLoader" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.ParticleSorter" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.values.CylinderSpawnShapeValue" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.values.ScaledNumericValue" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.values.PrimitiveSpawnShapeValue" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.values.WeightMeshSpawnShapeValue" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.values.PointSpawnShapeValue" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.values.RectangleSpawnShapeValue" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.values.EllipseSpawnShapeValue" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.values.SpawnShapeValue" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.values.UnweightedMeshSpawnShapeValue" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.values.ParticleValue" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.values.MeshSpawnShapeValue" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.values.NumericValue" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.values.RangedNumericValue" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.values.GradientColorValue" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.values.LineSpawnShapeValue" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.batches.ModelInstanceParticleBatch" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.batches.PointSpriteParticleBatch" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.batches.ParticleBatch" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.batches.BillboardParticleBatch" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.batches.BufferedParticleBatch" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.particles.ParallelArray" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.shaders.DepthShader" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.shaders.BaseShader" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.shaders.DefaultShader" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.decals.CameraGroupStrategy" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.decals.GroupPlug" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.decals.DecalBatch" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.decals.Decal" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.decals.GroupStrategy" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.decals.PluggableGroupStrategy" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.decals.DecalMaterial" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.decals.SimpleOrthoGroupStrategy" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.attributes.CubemapAttribute" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.attributes.DirectionalLightsAttribute" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.attributes.DepthTestAttribute" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.attributes.PointLightsAttribute" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.attributes.IntAttribute" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.attributes.ColorAttribute" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.attributes.FloatAttribute" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.attributes.SpotLightsAttribute" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.attributes.TextureAttribute" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.attributes.BlendingAttribute" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.Attributes" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.Shader" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.Model" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.RenderableProvider" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.model.NodePart" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.model.NodeAnimation" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.model.data.ModelTexture" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.model.data.ModelMesh" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.model.data.ModelNode" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.model.data.ModelMeshPart" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.model.data.ModelData" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.model.data.ModelNodeKeyframe" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.model.data.ModelNodeAnimation" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.model.data.ModelAnimation" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.model.data.ModelNodePart" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.model.data.ModelMaterial" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.model.MeshPart" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.model.NodeKeyframe" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.model.Node" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.model.Animation" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.ModelBatch" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.ModelCache" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.Environment" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.Renderable" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.Attribute" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.graphics.g3d.Material" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.MapGroupLayer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.ImageResolver" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.MapProperties" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.MapObject" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.Map" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.MapLayers" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.objects.PolylineMapObject" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.objects.CircleMapObject" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.objects.PolygonMapObject" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.objects.TextureMapObject" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.objects.RectangleMapObject" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.objects.EllipseMapObject" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.MapLayer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.TiledMap" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.TiledMapTileSets" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.TiledMapTileSet" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.TideMapLoader" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.TmxMapLoader" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.renderers.OrthoCachedTiledMapRenderer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.renderers.BatchTiledMapRenderer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.renderers.HexagonalTiledMapRenderer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.renderers.OrthogonalTiledMapRenderer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.renderers.IsometricStaggeredTiledMapRenderer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.renderers.IsometricTiledMapRenderer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.tiles.StaticTiledMapTile" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.tiles.AnimatedTiledMapTile" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.BaseTmxMapLoader" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.AtlasTmxMapLoader" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.TiledMapTile" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.objects.TiledMapTileMapObject" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.TiledMapRenderer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.TiledMapImageLayer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.tiled.TiledMapTileLayer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.MapRenderer" />
<extend-configuration-property name="gdx.reflect.exclude" value="com.badlogic.gdx.maps.MapObjects" />
```      
      
<p>
  
If you add `components` during runtime with reflection, this must also be noted:<p>
  
```
<extend-configuration-property name="gdx.reflect.include" value="com.your.game.components.ExampleComponent" />
```
  




