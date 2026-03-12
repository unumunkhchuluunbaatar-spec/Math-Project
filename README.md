# Math-Project
<!DOCTYPE html>
<html>
<head>
    <title>Math Project: 3D Cone</title>
    <style>
        body { margin: 0; overflow: hidden; font-family: sans-serif; }
        #info {
            position: absolute; top: 20px; left: 20px;
            background: rgba(255, 255, 255, 0.8);
            padding: 15px; border-radius: 8px; pointer-events: none;
        }
    </style>
</head>
<body>
    <div id="info">
        <h2>The Geometry of a Cone</h2>
        <p><b>Volume:</b> V = 1/3 * π * r² * h</p>
        <p><b>Surface Area:</b> A = π * r * (r + √(h² + r²))</p>
    </div>

    <script type="importmap">
        { "imports": { "three": "https://unpkg.com/three@0.160.0/build/three.module.js" } }
    </script>

    <script type="module">
        import * as THREE from 'three';

        // 1. Setup Scene
        const scene = new THREE.Scene();
        scene.background = new THREE.Color(0xf0f0f0);
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        document.body.appendChild(renderer.domElement);

        // 2. Create Cone (Radius 5, Height 10)
        const geometry = new THREE.ConeGeometry(5, 10, 32);
        const material = new THREE.MeshPhongMaterial({ color: 0x3498db, flatShading: false });
        const cone = new THREE.Mesh(geometry, material);
        scene.add(cone);

        // 3. Add Lights
        const light = new THREE.DirectionalLight(0xffffff, 1);
        light.position.set(5, 5, 5);
        scene.add(light);
        scene.add(new THREE.AmbientLight(0x404040));

        camera.position.z = 20;

        // 4. Animation Loop
        function animate() {
            requestAnimationFrame(animate);
            cone.rotation.y += 0.01; // Spins the cone
            renderer.render(scene, camera);
        }
        animate();

        // Handle window resizing
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
    </script>
</body>
</html>
