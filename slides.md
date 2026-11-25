---
theme: default
title: From University Engines to Shipping Pixels
transition: view-transition
class: bg-[#06060B] text-slate-100 overflow-hidden
fonts:
  sans: "Space Grotesk"
  mono: "JetBrains Mono"
---

<!-- SLIDE 1: WHO AM I? -->
<div class="grid grid-cols-12 gap-8 h-full items-center relative">
  <div v-motion :initial="{ scale: 0.65, opacity: 0 }" :enter="{ scale: 1, opacity: 1, transition: { duration: 650, type: 'spring' } }" class="col-span-7">
    <div style="view-transition-name: section-tag" class="inline-flex items-center gap-2 font-mono text-xs tracking-widest text-fuchsia-400 uppercase mb-3 px-2.5 py-1 rounded border border-fuchsia-500/40 bg-fuchsia-500/10">
      <span>✦ 01 // ALUMNI TALK</span>
      <span class="text-cyan-400">• MSc GRAPHICS & GAMES</span>
    </div>
    <h1 class="text-5xl font-bold tracking-tight leading-tight mb-4">
      From Uni Engines to
      <span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 via-fuchsia-400 to-purple-400">
        Shipping Pixels.
      </span>
    </h1>
    <p class="text-slate-300 text-base mb-5">
      Hi, I'm <strong class="text-white">[Your Name]</strong> — alumni of this exact course, now a Graphics Programmer at <strong class="text-cyan-300">[Studio Name]</strong>.
    </p>
    <!-- Cyber pixel wave accent strip -->
    <div class="flex items-center gap-1 mb-5 opacity-80">
      <span class="h-1.5 w-8 bg-cyan-400 rounded-sm" />
      <span class="h-1.5 w-4 bg-fuchsia-500 rounded-sm" />
      <span class="h-1.5 w-12 bg-purple-500 rounded-sm" />
      <span class="h-1.5 w-3 bg-teal-400 rounded-sm" />
      <span class="text-fuchsia-400 text-xs font-mono ml-2">✦ RENDER_ONLINE</span>
    </div>
    <div class="flex gap-2.5 font-mono text-xs">
      <span class="px-3 py-1.5 rounded bg-cyan-950/60 border border-cyan-400/50 text-cyan-300">C++ / HLSL / GLSL</span>
      <span class="px-3 py-1.5 rounded bg-fuchsia-950/60 border border-fuchsia-400/50 text-fuchsia-300">DX12 / Vulkan</span>
      <span class="px-3 py-1.5 rounded bg-purple-950/60 border border-purple-400/50 text-purple-300">Real-Time Raytracing</span>
    </div>
  </div>
  <div v-motion :initial="{ scale: 1.45, opacity: 0 }" :enter="{ scale: 1, opacity: 1, transition: { duration: 750 } }" class="col-span-5 h-80">
    <ShaderViewport sceneType="hero" initialMode="shaded" />
  </div>
</div>

---

<!-- SLIDE 2: WHAT DO I DO? -->
<div class="grid grid-cols-12 gap-6 h-full items-center">
  <div class="col-span-7">
    <div style="view-transition-name: section-tag" class="font-mono text-xs text-cyan-400 mb-1">✦ 02 // SYSTEM_ROLE</div>
    <h2 v-motion :initial="{ scale: 1.35, opacity: 0 }" :enter="{ scale: 1, opacity: 1, transition: { duration: 500 } }" class="text-3xl font-bold mb-4">
      What Does a <span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-fuchsia-400">Graphics Programmer</span> Do?
    </h2>
    <div class="space-y-3">
      <div v-click v-motion :initial="{ scale: 0.7, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-3.5 rounded-xl bg-slate-950/90 border-l-4 border-cyan-400 border-y border-r border-slate-800">
        <div class="font-mono text-cyan-400 text-xs font-bold">01 // RENDER FEATURES & SHADERS</div>
        <p class="text-xs text-slate-300 mt-1">Lighting passes, PBR materials, shadows, and post-FX that define the game's visual identity.</p>
      </div>
      <div v-click v-motion :initial="{ scale: 0.7, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-3.5 rounded-xl bg-slate-950/90 border-l-4 border-fuchsia-500 border-y border-r border-slate-800">
        <div class="font-mono text-fuchsia-400 text-xs font-bold">02 // FRAME BUDGET OPTIMIZATION</div>
        <p class="text-xs text-slate-300 mt-1">Profiling GPU bottlenecks in RenderDoc/PIX to hit a locked <strong class="text-cyan-300">16.6ms (60fps)</strong> or <strong class="text-fuchsia-300">8.3ms (120fps)</strong>.</p>
      </div>
      <div v-click v-motion :initial="{ scale: 0.7, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-3.5 rounded-xl bg-slate-950/90 border-l-4 border-purple-400 border-y border-r border-slate-800">
        <div class="font-mono text-purple-400 text-xs font-bold">03 // TECH ART & ENGINE PIPELINES</div>
        <p class="text-xs text-slate-300 mt-1">Building tools so artists can push visual fidelity without melting console memory or GPU budgets.</p>
      </div>
    </div>
  </div>
  <div v-motion :initial="{ scale: 0.5, opacity: 0 }" :enter="{ scale: 1, opacity: 1, transition: { duration: 700 } }" class="col-span-5 h-80">
    <ShaderViewport sceneType="pipeline" initialMode="shaded" />
  </div>
</div>

---

<!-- SLIDE 3: EXPERIENCE IN 3RD & 4TH YEARS -->
<div style="view-transition-name: section-tag" class="font-mono text-xs text-fuchsia-400 mb-1">✦ 03 // SKILL_TREE_UNLOCKED</div>
<h2 v-motion :initial="{ scale: 0.6, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="text-3xl font-bold mb-4">
  3rd & 4th Year: <span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 via-purple-400 to-fuchsia-400">Where Everything Clicked</span>
</h2>
<div v-motion :initial="{ scaleX: 0.3, opacity: 0 }" :enter="{ scaleX: 1, opacity: 1, transition: { duration: 600 } }" class="mb-5 p-3 rounded-xl bg-black/80 border border-purple-500/30 flex items-center justify-between font-mono text-xs">
  <span class="px-2.5 py-1 rounded bg-cyan-500/20 text-cyan-300 border border-cyan-400/50">LOCAL SPACE</span>
  <span class="text-fuchsia-400">──[ Model ]──▶</span>
  <span class="px-2.5 py-1 rounded bg-purple-500/20 text-purple-300 border border-purple-400/50">WORLD SPACE</span>
  <span class="text-cyan-400">──[ View ]──▶</span>
  <span class="px-2.5 py-1 rounded bg-fuchsia-500/20 text-fuchsia-300 border border-fuchsia-400/50">CLIP SPACE</span>
  <span class="text-teal-400">──[ Raster ]──▶</span>
  <span class="px-2.5 py-1 rounded bg-teal-500/20 text-teal-300 border border-teal-400/50">SCREEN PIXELS</span>
</div>
<div class="grid grid-cols-2 gap-5">
  <div v-click v-motion :initial="{ scale: 1.3, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-5 rounded-xl bg-gradient-to-br from-cyan-950/40 to-slate-950 border border-cyan-500/40">
    <span class="font-mono text-xs text-cyan-400">LEVEL 03 • FOUNDATIONS</span>
    <h3 class="font-bold text-lg mt-1 mb-2 text-white">OpenGL, Linear Algebra & C++ Memory</h3>
    <p class="text-xs text-slate-300 leading-relaxed">Going from "how do I draw a triangle?" to mastering MVP matrices, manual memory management, and cache-friendly data layouts.</p>
  </div>
  <div v-click v-motion :initial="{ scale: 1.3, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-5 rounded-xl bg-gradient-to-br from-fuchsia-950/40 to-slate-950 border border-fuchsia-500/40">
    <span class="font-mono text-xs text-fuchsia-400">LEVEL 04 (MSc) • HIGH PERFORMANCE</span>
    <h3 class="font-bold text-lg mt-1 mb-2 text-white">Modern APIs, Parallelism & Profiling</h3>
    <p class="text-xs text-slate-300 leading-relaxed">Multithreading, Vulkan/DX12 command buffers, RenderDoc frame captures, and engineering engines under strict 60fps constraints.</p>
  </div>
</div>

---

<!-- SLIDE 4: RENDERING - RAYTRACING - FYP -->
<div class="grid grid-cols-12 gap-6 h-full items-center">
  <div v-motion :initial="{ scale: 0.55, opacity: 0 }" :enter="{ scale: 1, opacity: 1, transition: { duration: 600 } }" class="col-span-6">
    <div style="view-transition-name: section-tag" class="font-mono text-xs text-fuchsia-400 mb-1">✦ 04 // FINAL_YEAR_PROJECT</div>
    <h2 class="text-3xl font-bold mb-3">
      Rendering & <span class="text-transparent bg-clip-text bg-gradient-to-r from-fuchsia-400 to-cyan-400">Raytracing FYP</span>
    </h2>
    <p class="text-xs text-slate-300 mb-4">
      Building a raytracer from scratch taught me more about light transport and GPU architecture than any textbook.
    </p>
    <ul class="space-y-2 text-xs text-slate-200 font-mono">
      <li v-click class="p-2.5 rounded bg-cyan-950/40 border border-cyan-500/40"><span class="text-cyan-400">✦</span> BVH Acceleration Structures (O(log N) traversal)</li>
      <li v-click class="p-2.5 rounded bg-fuchsia-950/40 border border-fuchsia-500/40"><span class="text-fuchsia-400">✦</span> Path Tracing, Reflections & Soft Shadows</li>
      <li v-click class="p-2.5 rounded bg-purple-950/40 border border-purple-500/40"><span class="text-purple-400">✦</span> Optimizing ray-triangle intersection & cache locality</li>
    </ul>
  </div>
  <div v-motion :initial="{ scale: 1.5, opacity: 0 }" :enter="{ scale: 1, opacity: 1, transition: { duration: 750 } }" class="col-span-6 h-80">
    <ShaderViewport sceneType="raytrace" initialMode="shaded" />
  </div>
</div>

---

<!-- SLIDE 5: THE JOY OF MAKING A GAME -->
<div class="grid grid-cols-12 gap-6 h-full items-center">
  <div v-motion :initial="{ scale: 0.5, opacity: 0 }" :enter="{ scale: 1, opacity: 1, transition: { duration: 700 } }" class="col-span-5 h-80">
    <ShaderViewport sceneType="game" initialMode="shaded" />
  </div>
  <div class="col-span-7">
    <div style="view-transition-name: section-tag" class="font-mono text-xs text-teal-400 mb-1">✦ 05 // WHY_WE_BUILD</div>
    <h2 class="text-3xl font-bold mb-4">
      The Joy of <span class="text-transparent bg-clip-text bg-gradient-to-r from-teal-300 via-cyan-400 to-fuchsia-400">Making a Game</span>
    </h2>
    <div class="space-y-4">
      <div v-click v-motion :initial="{ scale: 1.25, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-4 rounded-xl bg-gradient-to-r from-cyan-950/50 via-slate-950 to-slate-950 border border-cyan-500/40">
        <h3 class="text-base font-bold text-cyan-300 mb-1">✦ Instant Visual Feedback</h3>
        <p class="text-xs text-slate-300 leading-relaxed">
          Unlike backend systems where success is a green log line, in graphics programming a math equation turns into water caustics, volumetric fog, or holographic reflections right on screen.
        </p>
      </div>
      <div v-click v-motion :initial="{ scale: 1.25, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-4 rounded-xl bg-gradient-to-r from-fuchsia-950/50 via-slate-950 to-slate-950 border border-fuchsia-500/40">
        <h3 class="text-base font-bold text-fuchsia-300 mb-1">✦ The "2 AM Breakthrough"</h3>
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
    <div style="view-transition-name: section-tag" class="font-mono text-xs text-cyan-400 mb-1">✦ 06 // ACCESS_GRANTED</div>
    <h2 class="text-3xl font-bold mb-4">
      Turning This Course Into a <span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-purple-400">Studio Offer</span>
    </h2>
    <div class="space-y-2.5 text-xs">
      <div v-click v-motion :initial="{ scale: 0.75, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-3.5 rounded-lg bg-slate-950/90 border-l-4 border-cyan-400 border-y border-r border-slate-800">
        <strong class="text-cyan-300">1. Your FYP & Custom C++ Demos Are Your Golden Ticket:</strong> Studios care way more about a small custom renderer with clean GitHub code than a drag-and-drop template game.
      </div>
      <div v-click v-motion :initial="{ scale: 0.75, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-3.5 rounded-lg bg-slate-950/90 border-l-4 border-teal-400 border-y border-r border-slate-800">
        <strong class="text-teal-300">2. Show Frame-Time Telemetry:</strong> Include a README with RenderDoc captures and before/after GPU timings (<span class="font-mono text-fuchsia-400">24.2ms → 8.1ms</span>).
      </div>
      <div v-click v-motion :initial="{ scale: 0.75, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-3.5 rounded-lg bg-slate-950/90 border-l-4 border-fuchsia-500 border-y border-r border-slate-800">
        <strong class="text-fuchsia-300">3. Nail C++ & 3D Math Basics:</strong> Dot/cross products, coordinate spaces, and memory ownership come up in almost every interview.
      </div>
    </div>
  </div>
  <div v-motion :initial="{ scale: 1.4, opacity: 0 }" :enter="{ scale: 1, opacity: 1, transition: { duration: 700 } }" class="col-span-5 h-80">
    <ShaderViewport sceneType="career" initialMode="shaded" />
  </div>
</div>

---

<!-- SLIDE 7: HOW FUN THE JOB IS -->
<div style="view-transition-name: section-tag" class="font-mono text-xs text-fuchsia-400 mb-1">✦ 07 // STUDIO_LIFE</div>
<h2 v-motion :initial="{ scale: 1.3, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="text-3xl font-bold mb-4">
  How Fun Is the <span class="text-transparent bg-clip-text bg-gradient-to-r from-fuchsia-400 via-purple-400 to-cyan-400">Industry Actually?</span>
</h2>
<div v-motion :initial="{ scale: 0.8, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="mb-5 p-3 rounded-xl bg-black/90 border border-fuchsia-500/30 font-mono text-[10px]">
  <div class="flex justify-between text-slate-400 mb-1.5">
    <span class="text-cyan-400">FRAME 4092 // STUDIO_BUILD_DEBUG</span>
    <span class="text-fuchsia-400">11.4 ms (87 FPS)</span>
  </div>
  <div class="flex gap-1 h-4 rounded overflow-hidden">
    <div class="w-1/5 bg-cyan-400 flex items-center justify-center text-slate-950 font-bold">SHADOWS</div>
    <div class="w-2/5 bg-purple-500 flex items-center justify-center text-white font-bold">G-BUFFER + PBR</div>
    <div class="w-1/5 bg-fuchsia-500 flex items-center justify-center text-white font-bold">VOLUMETRICS</div>
    <div class="w-1/5 bg-teal-400 flex items-center justify-center text-slate-950 font-bold">POST-FX</div>
  </div>
</div>
<div class="grid grid-cols-3 gap-4 text-center">
  <div v-click v-motion :initial="{ scale: 0.6, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-4 rounded-xl bg-slate-950 border border-cyan-500/40">
    <div class="text-2xl mb-1.5">🎮</div>
    <h3 class="font-bold text-sm text-cyan-300 mb-1">Playtests Are Work</h3>
    <p class="text-xs text-slate-400">Debugging lighting bugs while playing unreleased builds with your team.</p>
  </div>
  <div v-click v-motion :initial="{ scale: 0.6, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-4 rounded-xl bg-slate-950 border border-purple-500/40">
    <div class="text-2xl mb-1.5">🧠</div>
    <h3 class="font-bold text-sm text-purple-300 mb-1">Surrounded by Nerds</h3>
    <p class="text-xs text-slate-400">Daily chats about SIGGRAPH papers, GPU hardware quirks, and shader tricks.</p>
  </div>
  <div v-click v-motion :initial="{ scale: 0.6, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-4 rounded-xl bg-slate-950 border border-fuchsia-500/40">
    <div class="text-2xl mb-1.5">🚀</div>
    <h3 class="font-bold text-sm text-fuchsia-300 mb-1">Seeing Credits Roll</h3>
    <p class="text-xs text-slate-400">Watching players react online to visual effects you personally engineered.</p>
  </div>
</div>

---

<!-- SLIDE 8: FAQs -->
<div class="grid grid-cols-12 gap-6 h-full items-center">
  <div class="col-span-8">
    <div style="view-transition-name: section-tag" class="font-mono text-xs text-cyan-400 mb-1">✦ 08 // DATA_STREAM</div>
    <h2 class="text-3xl font-bold mb-4">Questions You're Probably Thinking</h2>
    <div class="space-y-2.5 text-xs">
      <div v-click v-motion :initial="{ scale: 1.2, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-3 rounded-lg bg-slate-950/90 border border-cyan-500/30">
        <div class="font-mono text-cyan-400 font-bold">Q: Do I need to be a math genius?</div>
        <div class="text-slate-300 mt-0.5">No—you need strong intuition for vectors, matrices, and trig, plus knowing how to visualize spaces.</div>
      </div>
      <div v-click v-motion :initial="{ scale: 1.2, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-3 rounded-lg bg-slate-950/90 border border-purple-500/30">
        <div class="font-mono text-purple-400 font-bold">Q: Unreal/Unity vs. Custom C++ Engine for portfolio?</div>
        <div class="text-slate-300 mt-0.5">Custom C++ (OpenGL/DX12/Vulkan) proves you understand the metal; custom shaders in UE5 are a great bonus.</div>
      </div>
      <div v-click v-motion :initial="{ scale: 1.2, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="p-3 rounded-lg bg-slate-950/90 border border-fuchsia-500/30">
        <div class="font-mono text-fuchsia-400 font-bold">Q: Is crunch still everywhere?</div>
        <div class="text-slate-300 mt-0.5">The industry has improved hugely—ask studios directly about work-life balance during interviews!</div>
      </div>
    </div>
  </div>
  <div v-motion :initial="{ scale: 0.5, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }" class="col-span-4 h-72">
    <ShaderViewport sceneType="hero" initialMode="wireframe" />
  </div>
</div>

---

<!-- SLIDE 9: CONTACT ME -->
<div v-motion :initial="{ scale: 0.45, opacity: 0 }" :enter="{ scale: 1, opacity: 1, transition: { duration: 700, type: 'spring' } }" class="flex flex-col items-center justify-center h-full text-center relative">
  <!-- Decorative Holographic Glow Orb -->
  <div class="pointer-events-none absolute w-72 h-72 rounded-full bg-gradient-to-tr from-cyan-500/15 via-fuchsia-500/15 to-purple-500/15 blur-3xl" />

  <div style="view-transition-name: section-tag" class="font-mono text-xs tracking-widest text-fuchsia-400 uppercase mb-3">✦ 09 // TARGET_LOCKED • Q&A</div>
  <h2 class="text-5xl font-bold mb-4 text-transparent bg-clip-text bg-gradient-to-r from-cyan-300 via-white to-fuchsia-300">
    Ask Me Anything!
  </h2>
  <p class="text-slate-300 max-w-md mb-8 text-sm">
    Happy to review CVs, look at your FYP shaders, or chat about applying to studio roles.
  </p>
  <div class="flex gap-4 font-mono text-sm relative z-10">
    <div class="px-5 py-3 rounded-xl bg-black/80 border border-cyan-400/50 hover:shadow-[0_0_20px_rgba(0,240,255,0.3)] transition">
      GitHub: <span class="text-cyan-400">github.com/yourhandle</span>
    </div>
    <div class="px-5 py-3 rounded-xl bg-black/80 border border-fuchsia-400/50 hover:shadow-[0_0_20px_rgba(255,42,133,0.3)] transition">
      LinkedIn: <span class="text-fuchsia-400">/in/yourname</span>
    </div>
  </div>
</div>
