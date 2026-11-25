---
theme: default
title: From University Engines to Shipping Pixels
transition: view-transition
class: bg-[#090A0F] text-slate-100 overflow-hidden
fonts:
  sans: "Space Grotesk"
  mono: "JetBrains Mono"
---

<!-- SLIDE 1: WHO AM I? -->
<div class="grid grid-cols-12 gap-8 h-full items-center">
  <div v-motion :initial="{ scale: 0.65, rotate: -4, opacity: 0 }" :enter="{ scale: 1, rotate: 0, opacity: 1, transition: { duration: 650, type: 'spring' } }" class="col-span-7">
    <div style="view-transition-name: section-tag" class="font-mono text-xs tracking-widest text-sky-400 uppercase mb-3">
      01 // ALUMNI TALK • MSc HIGH PERFORMANCE GRAPHICS & GAMES
    </div>
    <h1 class="text-5xl font-bold tracking-tight leading-tight mb-4">
      From Uni Engines to <span class="text-sky-400">Shipping Pixels.</span>
    </h1>
    <p class="text-slate-400 text-base mb-6">
      Hi, I'm <strong class="text-white">[Your Name]</strong> — alumni of this exact course, now a Graphics Programmer at <strong class="text-sky-400">[Studio Name]</strong>.
    </p>
    <div class="flex gap-2.5 font-mono text-xs text-slate-300">
      <span class="px-3 py-1.5 rounded bg-slate-900 border border-slate-700 -rotate-1">C++ / HLSL / GLSL</span>
      <span class="px-3 py-1.5 rounded bg-slate-900 border border-slate-700 rotate-1">DX12 / Vulkan</span>
      <span class="px-3 py-1.5 rounded bg-slate-900 border border-slate-700 -rotate-1">Real-Time Rendering</span>
    </div>
  </div>
  <div v-motion :initial="{ scale: 1.45, rotate: 6, opacity: 0 }" :enter="{ scale: 1, rotate: -2, opacity: 1, transition: { duration: 750 } }" class="col-span-5 h-80">
    <ShaderViewport sceneType="hero" initialMode="shaded" />
  </div>
</div>

---

<!-- SLIDE 2: WHAT DO I DO? -->
<div class="grid grid-cols-12 gap-6 h-full items-center">
  <div class="col-span-7">
    <div style="view-transition-name: section-tag" class="font-mono text-xs text-sky-400 mb-1">02 // DAY_TO_DAY</div>
    <h2 v-motion :initial="{ scale: 1.35, opacity: 0 }" :enter="{ scale: 1, opacity: 1, transition: { duration: 500 } }" class="text-3xl font-bold mb-4">
      What Does a Graphics Programmer Do?
    </h2>
    <div class="space-y-3">
      <div v-click v-motion :initial="{ scale: 0.7, rotate: -3, opacity: 0 }" :enter="{ scale: 1, rotate: -1, opacity: 1 }" class="p-3.5 rounded-xl bg-slate-900/90 border border-slate-800">
        <div class="font-mono text-sky-400 text-xs font-bold">01. RENDER FEATURES & SHADERS</div>
        <p class="text-xs text-slate-300 mt-1">Lighting passes, PBR materials, shadows, and post-FX that define the game's visual identity.</p>
      </div>
      <div v-click v-motion :initial="{ scale: 0.7, rotate: 3, opacity: 0 }" :enter="{ scale: 1, rotate: 1, opacity: 1 }" class="p-3.5 rounded-xl bg-slate-900/90 border border-slate-800">
        <div class="font-mono text-amber-400 text-xs font-bold">02. FRAME BUDGET OPTIMIZATION</div>
        <p class="text-xs text-slate-300 mt-1">Profiling GPU bottlenecks in RenderDoc/PIX to hit a locked <strong>16.6ms (60fps)</strong> or <strong>8.3ms (120fps)</strong>.</p>
      </div>
      <div v-click v-motion :initial="{ scale: 0.7, rotate: -2, opacity: 0 }" :enter="{ scale: 1, rotate: -0.5, opacity: 1 }" class="p-3.5 rounded-xl bg-slate-900/90 border border-slate-800">
        <div class="font-mono text-emerald-400 text-xs font-bold">03. TECH ART & ENGINE PIPELINES</div>
        <p class="text-xs text-slate-300 mt-1">Building tools so artists can push visual fidelity without melting console memory or GPU budgets.</p>
      </div>
    </div>
  </div>
  <div v-motion :initial="{ scale: 0.5, rotate: -8, opacity: 0 }" :enter="{ scale: 1, rotate: 2, opacity: 1, transition: { duration: 700 } }" class="col-span-5 h-80">
    <ShaderViewport sceneType="pipeline" initialMode="shaded" />
  </div>
</div>

---

<!-- SLIDE 3: EXPERIENCE IN 3RD & 4TH YEARS -->
<div style="view-transition-name: section-tag" class="font-mono text-xs text-sky-400 mb-1">03 // THE_DEGREE</div>
<h2 v-motion :initial="{ scale: 0.6, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="text-3xl font-bold mb-4">
  3rd & 4th Year: Where Everything Clicked
</h2>
<div v-motion :initial="{ scaleX: 0.3, opacity: 0 }" :enter="{ scaleX: 1, opacity: 1, transition: { duration: 600 } }" class="mb-5 p-3 rounded-xl bg-slate-900/80 border border-slate-800 flex items-center justify-between font-mono text-xs">
  <span class="px-2.5 py-1 rounded bg-sky-500/20 text-sky-300 border border-sky-500/40">LOCAL SPACE</span>
  <span class="text-slate-500">──[ Model ]──▶</span>
  <span class="px-2.5 py-1 rounded bg-indigo-500/20 text-indigo-300 border border-indigo-500/40">WORLD SPACE</span>
  <span class="text-slate-500">──[ View ]──▶</span>
  <span class="px-2.5 py-1 rounded bg-amber-500/20 text-amber-300 border border-amber-500/40">CLIP SPACE</span>
  <span class="text-slate-500">──[ Raster ]──▶</span>
  <span class="px-2.5 py-1 rounded bg-emerald-500/20 text-emerald-300 border border-emerald-500/40">SCREEN PIXELS</span>
</div>
<div class="grid grid-cols-2 gap-5">
  <div v-click v-motion :initial="{ scale: 1.3, rotate: -4, opacity: 0 }" :enter="{ scale: 1, rotate: -1.5, opacity: 1 }" class="p-5 rounded-xl bg-slate-900/90 border border-slate-800">
    <span class="font-mono text-xs text-sky-400">YEAR 3 • FOUNDATIONS</span>
    <h3 class="font-bold text-lg mt-1 mb-2">OpenGL, Linear Algebra & C++ Memory</h3>
    <p class="text-xs text-slate-300 leading-relaxed">Going from "how do I draw a triangle?" to mastering MVP matrices, manual memory management, and cache-friendly data layouts.</p>
  </div>
  <div v-click v-motion :initial="{ scale: 1.3, rotate: 4, opacity: 0 }" :enter="{ scale: 1, rotate: 1.5, opacity: 1 }" class="p-5 rounded-xl bg-slate-900/90 border border-sky-500/40">
    <span class="font-mono text-xs text-amber-400">YEAR 4 (MSc) • HIGH PERFORMANCE</span>
    <h3 class="font-bold text-lg mt-1 mb-2">Modern APIs, Parallelism & Profiling</h3>
    <p class="text-xs text-slate-300 leading-relaxed">Multithreading, Vulkan/DX12 command buffers, RenderDoc frame captures, and engineering engines under strict 60fps constraints.</p>
  </div>
</div>

---

<!-- SLIDE 4: RENDERING - RAYTRACING - FYP -->
<div class="grid grid-cols-12 gap-6 h-full items-center">
  <div v-motion :initial="{ scale: 0.55, rotate: -3, opacity: 0 }" :enter="{ scale: 1, rotate: 0, opacity: 1, transition: { duration: 600 } }" class="col-span-6">
    <div style="view-transition-name: section-tag" class="font-mono text-xs text-amber-400 mb-1">04 // FINAL YEAR PROJECT</div>
    <h2 class="text-3xl font-bold mb-3">Rendering & Raytracing FYP</h2>
    <p class="text-xs text-slate-300 mb-4">
      Building a raytracer from scratch taught me more about light transport and GPU architecture than any textbook.
    </p>
    <ul class="space-y-2 text-xs text-slate-300 font-mono">
      <li v-click class="p-2 rounded bg-slate-900/90 border border-slate-800">▸ BVH Acceleration Structures (O(log N) traversal)</li>
      <li v-click class="p-2 rounded bg-slate-900/90 border border-slate-800">▸ Path Tracing, Reflections & Soft Shadows</li>
      <li v-click class="p-2 rounded bg-slate-900/90 border border-slate-800">▸ Optimizing ray-triangle intersection & cache locality</li>
    </ul>
  </div>
  <div v-motion :initial="{ scale: 1.5, rotate: -6, opacity: 0 }" :enter="{ scale: 1, rotate: 2, opacity: 1, transition: { duration: 750 } }" class="col-span-6 h-80">
    <ShaderViewport sceneType="raytrace" initialMode="shaded" />
  </div>
</div>

---

<!-- SLIDE 5: THE JOY OF MAKING A GAME -->
<div class="grid grid-cols-12 gap-6 h-full items-center">
  <div v-motion :initial="{ scale: 0.5, rotate: 6, opacity: 0 }" :enter="{ scale: 1, rotate: -2, opacity: 1, transition: { duration: 700 } }" class="col-span-5 h-80">
    <ShaderViewport sceneType="game" initialMode="shaded" />
  </div>
  <div class="col-span-7">
    <div style="view-transition-name: section-tag" class="font-mono text-xs text-sky-400 mb-1">05 // WHY_WE_BUILD</div>
    <h2 class="text-3xl font-bold mb-4">The Joy of Making a Game</h2>
    <div class="space-y-4">
      <div v-click v-motion :initial="{ scale: 1.25, rotate: 2, opacity: 0 }" :enter="{ scale: 1, rotate: 1, opacity: 1 }" class="p-4 rounded-xl bg-gradient-to-br from-slate-900 to-slate-900/40 border border-slate-800">
        <h3 class="text-base font-bold text-sky-400 mb-1">Instant Visual Feedback</h3>
        <p class="text-xs text-slate-300 leading-relaxed">
          Unlike backend systems where success is a green log line, in graphics programming a math equation turns into water caustics, volumetric fog, or metallic reflections right on screen.
        </p>
      </div>
      <div v-click v-motion :initial="{ scale: 1.25, rotate: -2, opacity: 0 }" :enter="{ scale: 1, rotate: -1, opacity: 1 }" class="p-4 rounded-xl bg-gradient-to-br from-slate-900 to-slate-900/40 border border-slate-800">
        <h3 class="text-base font-bold text-amber-400 mb-1">The "2 AM Breakthrough"</h3>
        <p class="text-xs text-slate-300 leading-relaxed">
          Fixing a single inverted normal or broken UV coordinate and suddenly watching an entire scene come alive is an unbeatable feeling.
        </p>
      </div>
    </div>
  </div>
</div>

---

<!-- SLIDE 6: GETTING A JOB FROM IT -->
<div class="grid grid-cols-12 gap-6 h-full items-center">
  <div class="col-span-7">
    <div style="view-transition-name: section-tag" class="font-mono text-xs text-sky-400 mb-1">06 // BREAKING_IN</div>
    <h2 class="text-3xl font-bold mb-4">Turning This Course Into a Studio Offer</h2>
    <div class="space-y-2.5 text-xs">
      <div v-click v-motion :initial="{ scale: 0.75, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-3.5 rounded-lg bg-slate-900/90 border-l-4 border-sky-400">
        <strong class="text-white">1. Your FYP & Custom C++ Demos Are Your Golden Ticket:</strong> Studios care way more about a small custom renderer with clean GitHub code than a drag-and-drop template game.
      </div>
      <div v-click v-motion :initial="{ scale: 0.75, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-3.5 rounded-lg bg-slate-900/90 border-l-4 border-emerald-400">
        <strong class="text-white">2. Show Frame-Time Telemetry:</strong> Include a README with RenderDoc captures and before/after GPU timings (<span class="font-mono text-emerald-400">24.2ms → 8.1ms</span>).
      </div>
      <div v-click v-motion :initial="{ scale: 0.75, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-3.5 rounded-lg bg-slate-900/90 border-l-4 border-amber-400">
        <strong class="text-white">3. Nail C++ & 3D Math Basics:</strong> Dot/cross products, coordinate spaces, and memory ownership come up in almost every interview.
      </div>
    </div>
  </div>
  <div v-motion :initial="{ scale: 1.4, rotate: 5, opacity: 0 }" :enter="{ scale: 1, rotate: -2, opacity: 1, transition: { duration: 700 } }" class="col-span-5 h-80">
    <ShaderViewport sceneType="career" initialMode="shaded" />
  </div>
</div>

---

<!-- SLIDE 7: HOW FUN THE JOB IS -->
<div style="view-transition-name: section-tag" class="font-mono text-xs text-sky-400 mb-1">07 // STUDIO_LIFE</div>
<h2 v-motion :initial="{ scale: 1.3, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="text-3xl font-bold mb-4">
  How Fun Is the Industry Actually?
</h2>
<div v-motion :initial="{ scale: 0.8, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="mb-5 p-3 rounded-xl bg-slate-900/90 border border-slate-800 font-mono text-[10px]">
  <div class="flex justify-between text-slate-400 mb-1.5">
    <span>FRAME 4092 // STUDIO_BUILD_DEBUG</span>
    <span class="text-emerald-400">11.4 ms (87 FPS)</span>
  </div>
  <div class="flex gap-1 h-4 rounded overflow-hidden">
    <div class="w-1/5 bg-sky-500 flex items-center justify-center text-slate-950 font-bold">SHADOWS</div>
    <div class="w-2/5 bg-indigo-500 flex items-center justify-center text-white font-bold">G-BUFFER + PBR</div>
    <div class="w-1/5 bg-amber-400 flex items-center justify-center text-slate-950 font-bold">VOLUMETRICS</div>
    <div class="w-1/5 bg-emerald-400 flex items-center justify-center text-slate-950 font-bold">POST-FX</div>
  </div>
</div>
<div class="grid grid-cols-3 gap-4 text-center">
  <div v-click v-motion :initial="{ scale: 0.6, rotate: -5, opacity: 0 }" :enter="{ scale: 1, rotate: -2, opacity: 1 }" class="p-4 rounded-xl bg-slate-900 border border-slate-800">
    <div class="text-2xl mb-1.5">🎮</div>
    <h3 class="font-bold text-sm mb-1">Playtests Are Work</h3>
    <p class="text-xs text-slate-400">Debugging lighting bugs while playing unreleased builds with your team.</p>
  </div>
  <div v-click v-motion :initial="{ scale: 0.6, rotate: 0, opacity: 0 }" :enter="{ scale: 1, rotate: 0, opacity: 1 }" class="p-4 rounded-xl bg-slate-900 border border-slate-800">
    <div class="text-2xl mb-1.5">🧠</div>
    <h3 class="font-bold text-sm mb-1">Surrounded by Nerds</h3>
    <p class="text-xs text-slate-400">Daily chats about SIGGRAPH papers, GPU hardware quirks, and shader tricks.</p>
  </div>
  <div v-click v-motion :initial="{ scale: 0.6, rotate: 5, opacity: 0 }" :enter="{ scale: 1, rotate: 2, opacity: 1 }" class="p-4 rounded-xl bg-slate-900 border border-slate-800">
    <div class="text-2xl mb-1.5">🚀</div>
    <h3 class="font-bold text-sm mb-1">Seeing Credits Roll</h3>
    <p class="text-xs text-slate-400">Watching players react online to visual effects you personally engineered.</p>
  </div>
</div>

---

<!-- SLIDE 8: FAQs -->
<div class="grid grid-cols-12 gap-6 h-full items-center">
  <div class="col-span-8">
    <div style="view-transition-name: section-tag" class="font-mono text-xs text-sky-400 mb-1">08 // RAPID_FIRE</div>
    <h2 class="text-3xl font-bold mb-4">Questions You're Probably Thinking</h2>
    <div class="space-y-2.5 text-xs">
      <div v-click v-motion :initial="{ scale: 1.2, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-3 rounded-lg bg-slate-900/90 border border-slate-800">
        <div class="font-mono text-sky-400 font-bold">Q: Do I need to be a math genius?</div>
        <div class="text-slate-300 mt-0.5">No—you need strong intuition for vectors, matrices, and trig, plus knowing how to visualize spaces.</div>
      </div>
      <div v-click v-motion :initial="{ scale: 1.2, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-3 rounded-lg bg-slate-900/90 border border-slate-800">
        <div class="font-mono text-sky-400 font-bold">Q: Unreal/Unity vs. Custom C++ Engine for portfolio?</div>
        <div class="text-slate-300 mt-0.5">Custom C++ (OpenGL/DX12/Vulkan) proves you understand the metal; custom shaders in UE5 are a great bonus.</div>
      </div>
      <div v-click v-motion :initial="{ scale: 1.2, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-3 rounded-lg bg-slate-900/90 border border-slate-800">
        <div class="font-mono text-sky-400 font-bold">Q: Is crunch still everywhere?</div>
        <div class="text-slate-300 mt-0.5">The industry has improved hugely—ask studios directly about work-life balance during interviews!</div>
      </div>
    </div>
  </div>
  <div v-motion :initial="{ scale: 0.5, rotate: -6, opacity: 0 }" :enter="{ scale: 1, rotate: 2, opacity: 1 }" class="col-span-4 h-72">
    <ShaderViewport sceneType="hero" initialMode="wireframe" />
  </div>
</div>

---

<!-- SLIDE 9: CONTACT ME -->
<div v-motion :initial="{ scale: 0.45, rotate: -4, opacity: 0 }" :enter="{ scale: 1, rotate: 0, opacity: 1, transition: { duration: 700, type: 'spring' } }" class="flex flex-col items-center justify-center h-full text-center relative">
  <div style="view-transition-name: section-tag" class="font-mono text-xs tracking-widest text-sky-400 uppercase mb-3">09 // Q&A + CONNECT</div>
  <h2 class="text-5xl font-bold mb-4">Ask Me Anything!</h2>
  <p class="text-slate-400 max-w-md mb-8 text-sm">
    Happy to review CVs, look at your FYP shaders, or chat about applying to studio roles.
  </p>
  <div class="flex gap-4 font-mono text-sm">
    <div class="px-5 py-3 rounded-xl bg-slate-900 border border-slate-700 -rotate-2 hover:rotate-0 hover:border-sky-400 transition">
      GitHub: <span class="text-sky-400">github.com/yourhandle</span>
    </div>
    <div class="px-5 py-3 rounded-xl bg-slate-900 border border-slate-700 rotate-2 hover:rotate-0 hover:border-amber-400 transition">
      LinkedIn: <span class="text-amber-400">/in/yourname</span>
    </div>
  </div>
</div>
