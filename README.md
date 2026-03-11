<!DOCTYPE html>
<html>
<head>
<title>3D Car Game</title>
<style>
body { margin:0; overflow:hidden; }
</style>
</head>
<body>

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

<script>
let scene = new THREE.Scene();
let camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);

let renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

// yol
let roadGeometry = new THREE.PlaneGeometry(20,200);
let roadMaterial = new THREE.MeshBasicMaterial({color:0x333333});
let road = new THREE.Mesh(roadGeometry, roadMaterial);
road.rotation.x = -Math.PI/2;
scene.add(road);

// maşın
let carGeometry = new THREE.BoxGeometry(2,1,4);
let carMaterial = new THREE.MeshBasicMaterial({color:0xff0000});
let car = new THREE.Mesh(carGeometry, carMaterial);
car.position.y = 0.5;
scene.add(car);

camera.position.z = 10;
camera.position.y = 5;
camera.rotation.x = -0.3;

let speed = 0.2;

document.addEventListener("keydown", function(e){
    if(e.key=="ArrowLeft") car.position.x -= 0.5;
    if(e.key=="ArrowRight") car.position.x += 0.5;
});

function animate(){
requestAnimationFrame(animate);

road.position.z += speed;
if(road.position.z > 50) road.position.z = 0;

renderer.render(scene, camera);
}

animate();
</script>

</body>
</html>
