<script>
    import * as THREE from 'three';
    import { AudioAnalyser } from 'audio-analyser';

    //crée la scene
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);

    // Créer un rendu WebGL
    const renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

    // Créer une sphère pour visualiser l'audio
    const sphereGeometry = new THREE.SphereGeometry(1, 32, 32);
    const sphereMaterial = new THREE.MeshBasicMaterial({ color: 0xffffff, wireframe: true });
    const sphere = new THREE.Mesh(sphereGeometry, sphereMaterial);
    scene.add(sphere);

    // Créer un analyseur audio
    const audio = new Audio();
    audio.src = 'path/to/audio/file.mp3';
    audio.crossOrigin = 'anonymous';
    const audioContext = new AudioContext();
    const source = audioContext.createMediaElementSource(audio);
    const analyser = new AudioAnalyser(source, 128);
    analyser.analyser.fftSize = 256;

    // Mettre à jour la sphère en fonction de l'analyse audio
    function animate() {
    requestAnimationFrame(animate);

    const data = analyser.getFrequencyData();
    const average = data.reduce((a, b) => a + b) / data.length;
    sphere.scale.set(1 + average / 256, 1 + average / 256, 1 + average / 256);

    renderer.render(scene, camera);
    }

    // Commencer la lecture de l'audio et l'animation
    audio.play();
    animate();

</script>