<script setup>
import * as THREE from 'three'
import {FontLoader} from 'three/examples/jsm/loaders/FontLoader';
import {TextGeometry} from 'three/examples/jsm/geometries/TextGeometry.js'
import { OrbitControls } from 'three-orbitcontrols-ts'
// const scene = new THREE.Scene();
// 			const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );

// 			const renderer = new THREE.WebGLRenderer();
// 			renderer.setSize( window.innerWidth, window.innerHeight );
// 			document.body.appendChild( renderer.domElement );

// 			const geometry = new THREE.BoxGeometry( 1, 1, 1 );
// 			const material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
// 			const cube = new THREE.Mesh( geometry, material );
// 			scene.add( cube );

// 			camera.position.z = 5;

// 			function animate() {
// 				requestAnimationFrame( animate );

// 				cube.rotation.x += 0.01;
// 				cube.rotation.y += 0.01;

// 				renderer.render( scene, camera );
// 			};

// 			animate();
 const scene = new THREE.Scene();
//  const axesHelper = new THREE.AxesHelper( 10000 );
//   scene.add( axesHelper );
 const camera = new THREE.OrthographicCamera( 
   window.innerWidth /-2,
   window.innerWidth / 2,
   window.innerHeight/2,
   window.innerHeight/-2);
   camera.position.set(50,100,800);
   camera.lookAt(0,0,0);
 const renderer = new THREE.WebGLRenderer();
 	renderer.setSize( window.innerWidth, window.innerHeight );
   document.body.appendChild( renderer.domElement );

const controls=new OrbitControls(camera,renderer.domElement);
controls.autoRotate=true;
controls.addEventListener('change',function(){
  renderer.render(scene,camera);
})

const loader = new FontLoader();

loader.load( './Times_New_Roman_Bold.json', function ( font ) {
  let myhours,mymins,mysec;
  let cube;
  setInterval(
   () =>{
    myhours=new Date().getHours();
   mymins=new Date().getMinutes();
   mysec=new Date().getSeconds();
   
   if(cube){
      scene.remove(cube)

   }
	const geometry = new TextGeometry( `${myhours}:${mymins}:${mysec}`, {
		font: font,
		size: window.innerHeight * 0.4,
		height: 5,
		curveSegments: 12,
		bevelEnabled: true,
		bevelThickness: 10,
		bevelSize: 8,
		bevelOffset: 0,
		bevelSegments: 5
	} );

  geometry.center()
  const material = new THREE.MeshMatcapMaterial( { color: 0xffffff } );
  		cube = new THREE.Mesh( geometry, material );
			scene.add( cube );
      renderer.render( scene, camera );
      },1000
  );
} );
</script>

<template>
  
</template>

<style>
*{
  margin:0;
  padding:0;
}
</style>
