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
const camPreset = ref("dutch");

let renderer, scene, camera, controls, rootGroup, frameId, resizeObserver;
const meshes = [];
const wireMeshes = [];
const animatedObjects = [];

const targetCamPos = new THREE.Vector3(0.8, 0.5, 4.4);
const targetCamRotZ = ref(-0.14);
let isTransitioning = false;

const setCameraPreset = (preset) => {
  camPreset.value = preset;
  isTransitioning = true;
  if (preset === "macro") {
    targetCamPos.set(1.2, 0.6, 2.1);
    targetCamRotZ.value = 0.16;
  } else if (preset === "wide") {
    targetCamPos.set(-1.5, 2.2, 5.4);
    targetCamRotZ.value = -0.18;
  } else {
    targetCamPos.set(0.6, 0.4, 4.3);
    targetCamRotZ.value = -0.1;
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
) => {
  const m = new THREE.Mesh(geo, mat);
  m.position.set(...pos);
  m.userData.origMat = mat;
  parent.add(m);
  meshes.push(m);

  const wGeo = new THREE.WireframeGeometry(geo);
  const wMat = new THREE.LineBasicMaterial({
    color: 0x38bdf8,
    transparent: true,
    opacity: 0.6,
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

  // ResizeObserver ensures off-screen slides resize properly once visible
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

  const key = new THREE.DirectionalLight(0x38bdf8, 3.2);
  key.position.set(4, 5, 5);
  const rim = new THREE.DirectionalLight(0xf59e0b, 2.2);
  rim.position.set(-4, -3, -2);
  scene.add(key, rim, new THREE.AmbientLight(0x1e293b, 1.5));

  rootGroup = new THREE.Group();
  rootGroup.rotation.z = -0.14;
  scene.add(rootGroup);

  const cyanMat = new THREE.MeshStandardMaterial({
    color: 0x38bdf8,
    metalness: 0.75,
    roughness: 0.2,
  });
  const amberMat = new THREE.MeshStandardMaterial({
    color: 0xf59e0b,
    metalness: 0.7,
    roughness: 0.25,
  });
  const emeraldMat = new THREE.MeshStandardMaterial({
    color: 0x10b981,
    metalness: 0.65,
    roughness: 0.25,
  });
  const slateMat = new THREE.MeshStandardMaterial({
    color: 0x334155,
    metalness: 0.5,
    roughness: 0.4,
  });

  if (props.sceneType === "pipeline") {
    const stages = [
      { pos: [-1.8, 0.4, 0], mat: cyanMat },
      { pos: [-0.6, -0.2, 0.3], mat: amberMat },
      { pos: [0.6, 0.3, -0.2], mat: emeraldMat },
      { pos: [1.8, -0.3, 0.2], mat: cyanMat },
    ];
    stages.forEach((s, idx) => {
      const box = registerMesh(
        new THREE.BoxGeometry(0.7, 1.1, 0.25),
        s.mat,
        rootGroup,
        s.pos,
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
      slateMat,
      rootGroup,
      [0, 0, 0],
    ).mesh.rotation.z = Math.PI / 2;
  } else if (props.sceneType === "raytrace") {
    const sphere = registerMesh(
      new THREE.IcosahedronGeometry(0.75, 3),
      cyanMat,
      rootGroup,
      [0.4, -0.1, 0],
    );
    animatedObjects.push({ obj: sphere.mesh, wire: sphere.wire, spin: 0.008 });
    registerMesh(
      new THREE.BoxGeometry(1.75, 1.75, 1.75),
      slateMat,
      rootGroup,
      [0.4, -0.1, 0],
      true,
    );

    const ray1 = registerMesh(
      new THREE.CylinderGeometry(0.025, 0.025, 2.2, 8),
      amberMat,
      rootGroup,
      [-1.1, 0.7, 0.2],
    );
    ray1.mesh.rotation.z = -0.95;
    ray1.wire.rotation.z = -0.95;

    const ray2 = registerMesh(
      new THREE.CylinderGeometry(0.02, 0.02, 2.0, 8),
      emeraldMat,
      rootGroup,
      [0.8, 1.0, -0.3],
    );
    ray2.mesh.rotation.z = 0.55;
    ray2.wire.rotation.z = 0.55;
  } else if (props.sceneType === "game") {
    registerMesh(
      new THREE.CylinderGeometry(1.4, 0.9, 0.45, 7),
      slateMat,
      rootGroup,
      [0, -0.6, 0],
    );
    registerMesh(
      new THREE.ConeGeometry(0.45, 1.1, 6),
      emeraldMat,
      rootGroup,
      [-0.45, 0.1, -0.2],
    );
    registerMesh(
      new THREE.ConeGeometry(0.35, 0.85, 6),
      emeraldMat,
      rootGroup,
      [0.1, -0.05, -0.4],
    );
    const gem = registerMesh(
      new THREE.OctahedronGeometry(0.32, 0),
      amberMat,
      rootGroup,
      [0.55, 0.45, 0.35],
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
      const mat = i === 7 ? amberMat : i > 4 ? emeraldMat : cyanMat;
      const node = registerMesh(
        new THREE.OctahedronGeometry(i === 7 ? 0.32 : 0.2, 1),
        mat,
        rootGroup,
        [x, y, z],
      );
      animatedObjects.push({ obj: node.mesh, wire: node.wire, spin: 0.02 });
    }
  } else {
    const hero = registerMesh(
      new THREE.TorusKnotGeometry(1.05, 0.35, 180, 36),
      cyanMat,
      rootGroup,
      [0, 0, 0],
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
      rootGroup.rotation.z = THREE.MathUtils.lerp(
        rootGroup.rotation.z,
        targetCamRotZ.value,
        0.06,
      );
      if (camera.position.distanceTo(targetCamPos) < 0.02)
        isTransitioning = false;
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
    class="relative w-full h-full rounded-xl overflow-hidden border border-slate-700/80 bg-slate-950/80 backdrop-blur shadow-2xl shadow-sky-950/30"
  >
    <div
      class="pointer-events-none absolute inset-0 bg-[radial-gradient(#1e293b_1px,transparent_1px)] [background-size:16px_16px] opacity-35"
    />
    <div
      ref="container"
      class="w-full h-full cursor-grab active:cursor-grabbing relative z-10"
    />
    <div
      class="absolute top-2.5 left-2.5 z-20 font-mono text-[10px] px-2 py-0.5 rounded bg-slate-900/90 border border-slate-700/80 text-sky-400 uppercase"
    >
      VIEWPORT // {{ sceneType }}
    </div>
    <div
      class="absolute top-2.5 right-2.5 z-20 flex gap-1 bg-slate-900/90 p-1 rounded-lg border border-slate-700/80 font-mono text-[10px]"
    >
      <button
        v-for="c in ['dutch', 'macro', 'wide']"
        :key="c"
        @click="setCameraPreset(c)"
        :class="
          camPreset === c
            ? 'bg-amber-400 text-slate-950 font-bold'
            : 'text-slate-400 hover:text-white'
        "
        class="px-1.5 py-0.5 rounded uppercase transition cursor-pointer"
      >
        {{ c }}
      </button>
    </div>
    <div
      class="absolute bottom-2.5 left-2.5 z-20 flex gap-1 bg-slate-900/90 p-1 rounded-lg border border-slate-700/80 font-mono text-[10px]"
    >
      <button
        v-for="m in ['shaded', 'normals', 'wireframe']"
        :key="m"
        @click="setMode(m)"
        :class="
          mode === m
            ? 'bg-sky-500 text-slate-950 font-bold'
            : 'text-slate-400 hover:text-white'
        "
        class="px-2 py-0.5 rounded uppercase transition cursor-pointer"
      >
        {{ m }}
      </button>
    </div>
  </div>
</template>
