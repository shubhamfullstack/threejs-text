# threejs-text
Text geometry using orbit controls

```
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );

const renderer = new THREE.WebGLRenderer({
  canvas: document.getElementById("threejs-canvas")
});

renderer.setPixelRatio(Math.max(window.devicePixelRatio),2)

const controls = new OrbitControls( camera, renderer.domElement );
renderer.setSize( window.innerWidth, window.innerHeight );

const matCapTexture = new THREE.TextureLoader().load('assets/matcaps/matcap1.png')
const fontLoader = new FontLoader();

fontLoader.load( 'assets/fonts/helvetiker_regular.typeface.json', function ( font ) {

	const geometry = new TextGeometry( 'Shubham Aggarwal', {
		font: font,
		size: 0.5,
		height: 0.2,
		curveSegments: 12,
		bevelEnabled: true,
		bevelThickness: 0.03,
		bevelSize: 0.02,
		bevelOffset: 0,
		bevelSegments: 5
	} );
  geometry.center()
  const material = new THREE.MeshMatcapMaterial( { matcap: matCapTexture } );
  const cube = new THREE.Mesh( geometry, material );
  scene.add( cube );

  let torusCount = 100;
  const torusGeometry = new THREE.TorusGeometry( 0.3, 0.2, 20, 45 );
  for (let index = 0; index < torusCount; index++) {
    const torus = new THREE.Mesh( torusGeometry, material );
    scene.add( torus );

    torus.position.set((Math.random() - 0.5)*10, (Math.random() - 0.5)*10,(Math.random() - 0.5)*10);
    let random = Math.random();
    torus.scale.set(random, random, random);
    torus.rotation.x = Math.random() * Math.PI;
    torus.rotation.y = Math.random() * Math.PI;
  }

} );

camera.position.z = 5;
controls.update()
function animate() {
	requestAnimationFrame( animate );
  controls.update()
	renderer.render( scene, camera );
}
animate();
```
