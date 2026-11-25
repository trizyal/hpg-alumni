<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";

const props = defineProps({
  sceneType: { type: String, default: "hero" },
  initialMode: { type: String, default: "shaded" },
});

const container = ref(null);
const mode = ref(props.initialMode);
const camPreset = ref("default");

let renderer, scene, camera, controls, rootGroup, frameId, resizeObserver;
const meshes = [];
const wireMeshes = [];
const animatedObjects = [];

const targetCamPos = new THREE.Vector3(0.6, 0.4, 4.3);
let isTransitioning = false;

const setCameraPreset = (preset) => {
  camPreset.value = preset;
  isTransitioning = true;
  if (preset === "macro") {
    targetCamPos.set(1.2, 0.6, 2.1);
  } else if (preset === "wide") {
    targetCamPos.set(-1.5, 2.2, 5.4);
  } else {
    targetCamPos.set(0.6, 0.4, 4.3);
  }
};

const setMode = (newMode) => {
  mode.value = newMode;
  meshes.forEach((m) => {
    m.visible = newMode !== "wireframe";
    if (newMode === "normals") {
      m.material = new THREE.MeshNormalMaterial();
    } else if (m.userData.origMat) {
      m.material = m.userData.origMat;
    }
  });
  wireMeshes.forEach((w) => {
    w.visible = newMode === "wireframe" || w.userData.alwaysShow;
  });
};

const registerMesh = (
  geo,
  mat,
  parent,
  pos = [0, 0, 0],
  alwaysWire = false,
  wireColor = 0xff2a85,
) => {
  const m = new THREE.Mesh(geo, mat);
  m.position.set(...pos);
  m.userData.origMat = mat;
  parent.add(m);
  meshes.push(m);

  const wGeo = new THREE.WireframeGeometry(geo);
  const wMat = new THREE.LineBasicMaterial({
    color: wireColor,
    transparent: true,
    opacity: 0.65,
  });
  const w = new THREE.LineSegments(wGeo, wMat);
  w.position.copy(m.position);
  w.userData.alwaysShow = alwaysWire;
  parent.add(w);
  wireMeshes.push(w);
  return { mesh: m, wire: w };
};

onMounted(() => {
  const el = container.value;
  const w = el.clientWidth || 400;
  const h = el.clientHeight || 320;

  scene = new THREE.Scene();
  camera = new THREE.PerspectiveCamera(46, w / h, 0.1, 100);
  camera.position.copy(targetCamPos);

  renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
  renderer.setSize(w, h);
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
  el.appendChild(renderer.domElement);

  resizeObserver = new ResizeObserver(() => {
    if (!el || !renderer || !camera) return;
    const nw = el.clientWidth;
    const nh = el.clientHeight;
    if (nw > 0 && nh > 0) {
      camera.aspect = nw / nh;
      camera.updateProjectionMatrix();
      renderer.setSize(nw, nh);
    }
  });
  resizeObserver.observe(el);

  controls = new OrbitControls(camera, renderer.domElement);
  controls.enableDamping = true;
  controls.dampingFactor = 0.06;
  controls.addEventListener("start", () => {
    isTransitioning = false;
  });

  // Cyber-Holographic 3-Point Lighting (Electric Cyan + Neon Magenta + Violet)
  const key = new THREE.DirectionalLight(0x00f0ff, 3.6);
  key.position.set(4, 5, 5);
  const rimMagenta = new THREE.DirectionalLight(0xff2a85, 3.2);
  rimMagenta.position.set(-4, -2, 3);
  const rimViolet = new THREE.PointLight(0x9d4edd, 4.0, 12);
  rimViolet.position.set(0, 3, -3);
  scene.add(key, rimMagenta, rimViolet, new THREE.AmbientLight(0x1e1b4b, 1.8));

  rootGroup = new THREE.Group();
  scene.add(rootGroup);

  // Holographic Iridescent PBR Materials
  const holoCyanMat = new THREE.MeshPhysicalMaterial({
    color: 0x00f0ff,
    metalness: 0.65,
    roughness: 0.15,
    iridescence: 1.0,
    iridescenceIOR: 1.6,
    clearcoat: 1.0,
  });
  const neonMagentaMat = new THREE.MeshPhysicalMaterial({
    color: 0xff2a85,
    metalness: 0.6,
    roughness: 0.2,
    iridescence: 0.85,
    clearcoat: 0.8,
  });
  const cyberVioletMat = new THREE.MeshPhysicalMaterial({
    color: 0x9d4edd,
    metalness: 0.65,
    roughness: 0.18,
    iridescence: 1.0,
  });
  const mintMat = new THREE.MeshStandardMaterial({
    color: 0x2ec4b6,
    metalness: 0.5,
    roughness: 0.25,
  });

  if (props.sceneType === "pipeline") {
    const stages = [
      { pos: [-1.8, 0.4, 0], mat: holoCyanMat, wire: 0x00f0ff },
      { pos: [-0.6, -0.2, 0.3], mat: neonMagentaMat, wire: 0xff2a85 },
      { pos: [0.6, 0.3, -0.2], mat: cyberVioletMat, wire: 0x9d4edd },
      { pos: [1.8, -0.3, 0.2], mat: mintMat, wire: 0x2ec4b6 },
    ];
    stages.forEach((s, idx) => {
      const box = registerMesh(
        new THREE.BoxGeometry(0.7, 1.1, 0.25),
        s.mat,
        rootGroup,
        s.pos,
        false,
        s.wire,
      );
      animatedObjects.push({
        obj: box.mesh,
        wire: box.wire,
        phase: idx * 1.4,
        bob: true,
      });
    });
    registerMesh(
      new THREE.CylinderGeometry(0.03, 0.03, 4.2, 12),
      cyberVioletMat,
      rootGroup,
      [0, 0, 0],
    ).mesh.rotation.z = Math.PI / 2;
  } else if (props.sceneType === "raytrace") {
    const sphere = registerMesh(
      new THREE.IcosahedronGeometry(0.75, 3),
      holoCyanMat,
      rootGroup,
      [0.4, -0.1, 0],
      false,
      0x00f0ff,
    );
    animatedObjects.push({ obj: sphere.mesh, wire: sphere.wire, spin: 0.008 });
    registerMesh(
      new THREE.BoxGeometry(1.75, 1.75, 1.75),
      cyberVioletMat,
      rootGroup,
      [0.4, -0.1, 0],
      true,
      0xff2a85,
    );

    const ray1 = registerMesh(
      new THREE.CylinderGeometry(0.025, 0.025, 2.2, 8),
      neonMagentaMat,
      rootGroup,
      [-1.1, 0.7, 0.2],
    );
    ray1.mesh.rotation.z = -0.95;
    ray1.wire.rotation.z = -0.95;

    const ray2 = registerMesh(
      new THREE.CylinderGeometry(0.02, 0.02, 2.0, 8),
      mintMat,
      rootGroup,
      [0.8, 1.0, -0.3],
    );
    ray2.mesh.rotation.z = 0.55;
    ray2.wire.rotation.z = 0.55;
  } else if (props.sceneType === "game") {
    registerMesh(
      new THREE.CylinderGeometry(1.4, 0.9, 0.45, 7),
      cyberVioletMat,
      rootGroup,
      [0, -0.6, 0],
      false,
      0x9d4edd,
    );
    registerMesh(
      new THREE.ConeGeometry(0.45, 1.1, 6),
      mintMat,
      rootGroup,
      [-0.45, 0.1, -0.2],
      false,
      0x2ec4b6,
    );
    registerMesh(
      new THREE.ConeGeometry(0.35, 0.85, 6),
      holoCyanMat,
      rootGroup,
      [0.1, -0.05, -0.4],
      false,
      0x00f0ff,
    );
    const gem = registerMesh(
      new THREE.OctahedronGeometry(0.34, 0),
      neonMagentaMat,
      rootGroup,
      [0.55, 0.45, 0.35],
      false,
      0xff2a85,
    );
    animatedObjects.push({
      obj: gem.mesh,
      wire: gem.wire,
      spin: 0.03,
      bob: true,
      phase: 0,
    });
  } else if (props.sceneType === "career") {
    for (let i = 0; i < 8; i++) {
      const t = (i / 7) * Math.PI * 1.6;
      const x = Math.cos(t) * 1.1;
      const z = Math.sin(t) * 1.1;
      const y = (i - 3.5) * 0.38;
      const mat = i === 7 ? neonMagentaMat : i > 4 ? mintMat : holoCyanMat;
      const node = registerMesh(
        new THREE.OctahedronGeometry(i === 7 ? 0.32 : 0.2, 1),
        mat,
        rootGroup,
        [x, y, z],
        false,
        i === 7 ? 0xff2a85 : 0x00f0ff,
      );
      animatedObjects.push({ obj: node.mesh, wire: node.wire, spin: 0.02 });
    }
  } else {
    const hero = registerMesh(
      new THREE.TorusKnotGeometry(1.05, 0.35, 180, 36),
      holoCyanMat,
      rootGroup,
      [0, 0, 0],
      false,
      0xff2a85,
    );
    animatedObjects.push({ obj: hero.mesh, wire: hero.wire, spin: 0.007 });
  }

  setMode(props.initialMode);

  let clock = 0;
  const animate = () => {
    frameId = requestAnimationFrame(animate);
    clock += 0.03;
    rootGroup.rotation.y += 0.0045;
    animatedObjects.forEach((item) => {
      if (item.spin) {
        item.obj.rotation.y += item.spin;
        item.obj.rotation.x += item.spin * 0.5;
        item.wire.rotation.copy(item.obj.rotation);
      }
      if (item.bob) {
        item.obj.position.y += Math.sin(clock + item.phase) * 0.003;
        item.wire.position.copy(item.obj.position);
      }
    });

    if (isTransitioning) {
      camera.position.lerp(targetCamPos, 0.06);
      if (camera.position.distanceTo(targetCamPos) < 0.02) isTransitioning = false;
    }

    controls.update();
    renderer.render(scene, camera);
  };
  animate();
});

onUnmounted(() => {
  cancelAnimationFrame(frameId);
  resizeObserver?.disconnect();
  controls?.dispose();
  renderer?.dispose();
});
</script>

<template>
  <div
    class="relative w-full h-full rounded-xl overflow-hidden border border-fuchsia-500/40 bg-[#07070D]/90 backdrop-blur shadow-[0_0_30px_rgba(255,42,133,0.12)]"
  >
    <!-- Cyber grid + subtle corner HUD brackets -->
    <div
      class="pointer-events-none absolute inset-0 bg-[radial-gradient(#38bdf8_1px,transparent_1px)] [background-size:18px_18px] opacity-20"
    />
    <div
      class="pointer-events-none absolute top-0 left-0 w-3 h-3 border-t-2 border-l-2 border-cyan-400 z-20"
    />
    <div
      class="pointer-events-none absolute top-0 right-0 w-3 h-3 border-t-2 border-r-2 border-fuchsia-500 z-20"
    />
    <div
      class="pointer-events-none absolute bottom-0 left-0 w-3 h-3 border-b-2 border-l-2 border-fuchsia-500 z-20"
    />
    <div
      class="pointer-events-none absolute bottom-0 right-0 w-3 h-3 border-b-2 border-r-2 border-cyan-400 z-20"
    />

    <div ref="container" class="w-full h-full cursor-grab active:cursor-grabbing relative z-10" />

    <div
      class="absolute top-2.5 left-3 z-20 font-mono text-[10px] px-2 py-0.5 rounded bg-black/80 border border-cyan-400/50 text-cyan-300 uppercase tracking-wider"
    >
      ✦ SYS // {{ sceneType }}
    </div>

    <div
      class="absolute top-2.5 right-3 z-20 flex gap-1 bg-black/80 p-1 rounded border border-fuchsia-500/40 font-mono text-[10px]"
    >
      <button
        v-for="c in ['default', 'macro', 'wide']"
        :key="c"
        @click="setCameraPreset(c)"
        :class="
          camPreset === c
            ? 'bg-fuchsia-500 text-white font-bold shadow-[0_0_10px_#ff2a85]'
            : 'text-slate-400 hover:text-cyan-300'
        "
        class="px-1.5 py-0.5 rounded uppercase transition cursor-pointer"
      >
        {{ c }}
      </button>
    </div>

    <div
      class="absolute bottom-2.5 left-3 z-20 flex gap-1 bg-black/80 p-1 rounded border border-cyan-500/40 font-mono text-[10px]"
    >
      <button
        v-for="m in ['shaded', 'normals', 'wireframe']"
        :key="m"
        @click="setMode(m)"
        :class="
          mode === m
            ? 'bg-cyan-400 text-slate-950 font-bold shadow-[0_0_10px_#00f0ff]'
            : 'text-slate-400 hover:text-fuchsia-300'
        "
        class="px-2 py-0.5 rounded uppercase transition cursor-pointer"
      >
        {{ m }}
      </button>
    </div>
  </div>
</template>
