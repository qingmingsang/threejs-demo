
# getting started
## 场景（Scene）
场景允许你在什么地方、摆放什么东西来交给three.js来渲染，这是你放置物体、灯光和摄像机的地方。

`Scene()`
创建一个新的场景对象。

```
var scene = new THREE.Scene();

var geometry = new THREE.BoxGeometry(1, 1, 1);

var material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });

var cube = new THREE.Mesh(geometry, material);
scene.add(cube);
```

## 摄像机（Camera）
摄像机的抽象基类。在构建新摄像机时，应始终继承此类。

构造函数
`Camera()`
创建一个新的Camera（摄像机）。注意：这个类并不是被直接调用的；你所想要的或许是一个 `PerspectiveCamera（透视摄像机）`或者 `OrthographicCamera（正交摄像机）`。


## 透视相机（PerspectiveCamera）

这一摄像机使用[perspective projection（透视投影）](https://en.wikipedia.org/wiki/Perspective_(graphical))来进行投影。

这一投影模式被用来模拟人眼所看到的景象，它是3D场景的渲染中使用得最普遍的投影模式。

`PerspectiveCamera( fov : Number, aspect : Number, near : Number, far : Number )`
* fov — 摄像机视锥体垂直视野角度
* aspect — 摄像机视锥体长宽比
* near — 摄像机视锥体近端面
* far — 摄像机视锥体远端面

```
var camera = new THREE.PerspectiveCamera( 45, width / height, 1, 1000 );

scene.add( camera );
```

## WebGLRenderer
WebGL Render 用WebGL渲染出你制作的场景。

```
var renderer = new THREE.WebGLRenderer();

renderer.setSize( window.innerWidth, window.innerHeight );

document.body.appendChild( renderer.domElement );
```

## 立方几何体（BoxGeometry）
BoxGeometry是四边形的原始几何类，它通常使用构造函数所提供的“width”、“height”、“depth”参数来创建立方体或者不规则四边形。

`BoxGeometry(width : Float, height : Float, depth : Float, widthSegments : Integer, heightSegments : Integer, depthSegments : Integer)`
* width — X轴上面的宽度，默认值为1。
* height — Y轴上面的高度，默认值为1。
* depth — Z轴上面的深度，默认值为1。
* widthSegments — （可选）宽度的分段数，默认值是1。
* heightSegments — （可选）宽度的分段数，默认值是1。
* depthSegments — （可选）宽度的分段数，默认值是1。

```
var geometry = new THREE.BoxGeometry( 1, 1, 1 );

var material = new THREE.MeshBasicMaterial( {color: 0x00ff00} );

var cube = new THREE.Mesh( geometry, material );
scene.add( cube );
```



## Geometry
Geometry 是一个便于用户使用的 BufferGeometry 的替代品。Geometry 利用 Vector3 或 Color 存储了几何体的相关 attributes（如顶点位置，面信息，颜色等）比起 BufferGeometry 更容易读写，但是运行效率不如有类型的队列。

对于大型工程或正式工程，推荐采用 BufferGeometry。

构造函数
`Geometry()`
构造函数没有任何参数。

```
var geometry = new THREE.Geometry();

geometry.vertices.push(
	new THREE.Vector3( -10,  10, 0 ),
	new THREE.Vector3( -10, -10, 0 ),
	new THREE.Vector3(  10, -10, 0 )
);

geometry.faces.push( new THREE.Face3( 0, 1, 2 ) );

geometry.computeBoundingSphere();
```

## 文本几何体（TextGeometry）
一个用于将文本生成为单一的几何体的类。 它是由一串给定的文本，以及由加载的Font（字体）和该几何体ExtrudeGeometry父类中的设置所组成的参数来构造的。 请参阅Font、FontLoader和Creating_Text页面来查看更多详细信息。

`TextGeometry(text : String, parameters : Object)`

```
var loader = new THREE.FontLoader();

loader.load( 'fonts/helvetiker_regular.typeface.json', function ( font ) {

	var geometry = new THREE.TextGeometry( 'Hello three.js!', {
		font: font,
		size: 80,
		height: 5,
		curveSegments: 12,
		bevelEnabled: true,
		bevelThickness: 10,
		bevelSize: 8,
		bevelSegments: 5
	} );
} );
```

## 基础网格材质(MeshBasicMaterial)
一个以简单着色（平面或线框）方式来绘制几何体的材质。

这种材质不受光照的影响。

`MeshBasicMaterial( parameters : Object )`


```
var geometry = new THREE.BoxGeometry( 1, 1, 1 );

var material = new THREE.MeshBasicMaterial( {color: 0x00ff00} );

var cube = new THREE.Mesh( geometry, material );
scene.add( cube );
```


## 基础线条材质（LineBasicMaterial）
一种用于绘制线框样式几何体的材质。

`LineBasicMaterial( parameters : Object )`

```
var material = new THREE.LineBasicMaterial( {
	color: 0xffffff,
	linewidth: 1,
	linecap: 'round', //ignored by WebGLRenderer
	linejoin:  'round' //ignored by WebGLRenderer
} );
```



## 网格（Mesh）
表示基于以三角形为polygon mesh（多边形网格）的物体的类。 同时也作为其他类的基类，例如SkinnedMesh。

`Mesh( geometry : Geometry, material : Material )`

```
var geometry = new THREE.BoxBufferGeometry( 1, 1, 1 );

var material = new THREE.MeshBasicMaterial( { color: 0xffff00 } );

var mesh = new THREE.Mesh( geometry, material );

scene.add( mesh );
```

## 线（Line）
一条连续的线。

它几乎和LineSegments是一样的，唯一的区别是它在渲染时使用的是gl.LINE_STRIP， 而不是gl.LINES。

构造器
`Line( geometry : Geometry, material : Material )`
geometry —— 表示线段的顶点，默认值是一个新的BufferGeometry。
material —— 线的材质，默认值是一个新的具有随机颜色的LineBasicMaterial。
如果没有指定材质，一个随机颜色的线的材质将会被创建，并应用到该物体上。

```
var material = new THREE.LineBasicMaterial({
	color: 0x0000ff
});

var geometry = new THREE.Geometry();
geometry.vertices.push(
	new THREE.Vector3( -10, 0, 0 ),
	new THREE.Vector3( 0, 10, 0 ),
	new THREE.Vector3( 10, 0, 0 )
);

var line = new THREE.Line( geometry, material );
scene.add( line );
```

## 三维向量（Vector3）
该类表示的是一个三维向量（3D vector）。 一个三维向量表示的是一个有顺序的、三个为一组的数字组合（标记为x、y和z）， 可被用来表示很多事物，例如：
* 一个位于三维空间中的点。
* 一个在三维空间中的方向与长度的定义。在three.js中，长度总是从(0, 0, 0)到(x, y, z)的 Euclidean distance（欧几里德距离，即直线距离）， 方向也是从(0, 0, 0)到(x, y, z)的方向。
* 任意的、有顺序的、三个为一组的数字组合。


其他的一些事物也可以使用二维向量进行表示，比如说动量矢量等等； 但以上这些是它在three.js中的常用用途。

构造函数
`Vector3( x : Float, y : Float, z : Float )`
* x - 向量的x值，默认为0。
* y - 向量的y值，默认为0。
* z - 向量的z值，默认为0。

创建一个新的Vector3。

```
var a = new THREE.Vector3( 0, 1, 0 );

//no arguments; will be initialised to (0, 0, 0)
var b = new THREE.Vector3( );

var d = a.distanceTo( b );
```

