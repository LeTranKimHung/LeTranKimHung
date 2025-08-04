
# 🌍 Interactive 3D Globe (Three.js)

![Glowing universe](https://github.githubassets.com/images/modules/site/home/hero-glow.svg)

```html
<div id="globeCanvas"></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>

<script>
// Three.js Globe Code
const container = document.getElementById('globeCanvas');
const scene = new THREE.Scene();
const renderer = new THREE.WebGLRenderer({ alpha: true });
renderer.setClearColor(0x000000, 0);
renderer.setSize(container.offsetHeight, container.offsetHeight);
scene.background = null;
container.appendChild(renderer.domElement);

const light1 = new THREE.PointLight(0x5a54ff, 0.75);
light1.position.set(-150, 150, -50);
const light2 = new THREE.PointLight(0x4158f6, 0.75);
light2.position.set(-400, 200, 150);
const light3 = new THREE.PointLight(0x803bff, 0.7);
light3.position.set(100, 250, -100);
scene.add(light1, light2, light3);

// Atmosphere Shader
const atmosphereShader = {
  'atmosphere': {
    uniforms: {},
    vertexShader: \`
      varying vec3 vNormal;
      void main() {
        vNormal = normalize( normalMatrix * normal );
        gl_Position = projectionMatrix * modelViewMatrix * vec4( position, 1.0 );
      }\`,
    fragmentShader: \`
      varying vec3 vNormal;
      void main() {
        float intensity = pow( 0.99 - dot( vNormal, vec3( 0, 0, 1.0 ) ), 6.0 );
        gl_FragColor = vec4( .28, .48, 1.0, 1.0 ) * intensity;
      }\`
  }
};

const atmosphereGeometry = new THREE.SphereGeometry(2, 64, 64);
const atmosphereMaterial = new THREE.ShaderMaterial({
  uniforms: THREE.UniformsUtils.clone(atmosphereShader['atmosphere'].uniforms),
  vertexShader: atmosphereShader['atmosphere'].vertexShader,
  fragmentShader: atmosphereShader['atmosphere'].fragmentShader,
  side: THREE.BackSide,
  blending: THREE.AdditiveBlending,
  transparent: true
});
const atm = new THREE.Mesh(atmosphereGeometry, atmosphereMaterial);
atm.scale.set(1.05, 1.05, 1.05);
scene.add(atm);
atm.position.set(-.1, .1, 0);

const sphereGeometry = new THREE.SphereGeometry(2, 64, 64);
const sphereMaterial = new THREE.MeshLambertMaterial({ color: 0xeeeeee });
const sphere = new THREE.Mesh(sphereGeometry, sphereMaterial);
scene.add(sphere);

const loader = new THREE.TextureLoader();
const overlayMaterial = new THREE.MeshBasicMaterial({
  map: loader.load('https://i.imgur.com/JLFp6Ws.png'),
  transparent: true
});
const overlaySphereGeometry = new THREE.SphereGeometry(2.003, 64, 64);
const overlaySphere = new THREE.Mesh(overlaySphereGeometry, overlayMaterial);
sphere.add(overlaySphere);

// Camera Setup
const camera = new THREE.PerspectiveCamera(75, 900 / 900, 0.1, 1000);
camera.position.z = 6;

// Animation Loop
const animate = function() {
  requestAnimationFrame(animate);
  sphere.rotation.y += 0.0005;
  renderer.render(scene, camera);
};
animate();
</script>
```

## 🔥 GitHub Stats 🔥
<div align="center">
  <a href="https://github.com/LeTranKimHung">
    <img width="350" src="https://github-readme-stats.vercel.app/api/top-langs/?username=LeTranKimHung&hide=c%23,powershell,Mathematica,Ruby,Objective-C,Objective-C%2b%2b,Cuda&title_color=61dafb&text_color=ffffff&icon_color=61dafb&bg_color=20232a&langs_count=8&layout=compact&border_color=61dafb&hide_border=true" />
  </a>
  <a href="https://github.com/LeTranKimHung">
    <img width="450" src="https://github-readme-stats.vercel.app/api?username=LeTranKimHung&show_icons=true&theme=react&border_color=61dafb&hide_border=true&rank_icon=github&include_all_commits=true" />
  </a>
</div>

## 👽 Where to find me 👽
<div align="center">
  <a href="https://www.facebook.com/hung.letrankim.16" target="_blank">
    <img src="https://img.icons8.com/bubbles/100/000000/facebook-new.png" alt="Facebook" />
  </a>
  <a href="https://www.linkedin.com/in/hungltk" target="_blank">
    <img src="https://img.icons8.com/bubbles/100/000000/linkedin.png" alt="LinkedIn" />
  </a>
  <a href="mailto:hungltk2004@gmail.com" target="_blank">
    <img src="https://img.icons8.com/bubbles/100/000000/apple-mail.png" alt="Email" />
  </a>
</div>
