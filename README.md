
<html lang="pt-BR" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SROS + SAMS | Pontes e Elevadores Espaciais Dinâmicos</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        sci: {
                            950: '#020617',
                            900: '#090d16',
                            800: '#111827',
                            700: '#1f2937',
                            cyan: '#06b6d4',
                            emerald: '#10b981',
                            amber: '#f59e0b',
                            rose: '#f43f5e',
                            purple: '#8b5cf6'
                        }
                    }
                }
            }
        }
    </script>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
        .font-mono { font-family: 'JetBrains Mono', monospace; }
        .glass-panel {
            background: rgba(15, 23, 42, 0.75);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(6, 182, 212, 0.2);
        }
        .glow-cyan {
            box-shadow: 0 0 25px rgba(6, 182, 212, 0.25);
        }
        .glow-purple {
            box-shadow: 0 0 25px rgba(139, 92, 246, 0.25);
        }
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #020617;
        }
        ::-webkit-scrollbar-thumb {
            background: #1e293b;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #06b6d4;
        }
    </style>
</head>
<body class="bg-sci-950 text-slate-100 min-h-screen flex flex-col overflow-x-hidden">

    <!-- Header / Navbar -->
    <header class="glass-panel border-b border-cyan-500/20 px-6 py-4 flex flex-wrap items-center justify-between gap-4 sticky top-0 z-50">
        <div class="flex items-center space-x-3">
            <div class="relative flex items-center justify-center w-10 h-10 rounded-xl bg-cyan-950 border border-cyan-500/50 glow-cyan">
                <svg class="w-6 h-6 text-cyan-400 animate-pulse" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/>
                </svg>
            </div>
            <div>
                <h1 class="text-lg font-bold tracking-wider text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-purple-400">SROS + SAMS SPACE ELEVATOR</h1>
                <p class="text-xs text-slate-400 font-mono">Túnel de Lasers Full Duplex & Amortecimento Atmosférico</p>
            </div>
        </div>

        <!-- System Status Pills -->
        <div class="flex items-center gap-3 text-xs font-mono flex-wrap">
            <div class="flex items-center gap-2 px-3 py-1.5 rounded-full bg-slate-900 border border-slate-700">
                <span id="sros-status-dot" class="w-2.5 h-2.5 rounded-full bg-cyan-500 animate-ping"></span>
                <span>SROS Alinhamento: <strong id="sros-status-text" class="text-cyan-400">99.999% (Gimbals OK)</strong></span>
            </div>
            <div class="flex items-center gap-2 px-3 py-1.5 rounded-full bg-slate-900 border border-slate-700">
                <span class="w-2.5 h-2.5 rounded-full bg-purple-500"></span>
                <span>SAMS Cabine: <strong id="sams-status-text" class="text-purple-400">BLINDADO (0.0g tremor)</strong></span>
            </div>
            <div class="flex items-center gap-2 px-3 py-1.5 rounded-full bg-slate-900 border border-slate-700">
                <span class="w-2 h-2 rounded-full bg-emerald-500"></span>
                <span>Feixe Full Duplex: <strong class="text-emerald-400">ATIVO (48 THz)</strong></span>
            </div>
        </div>
    </header>

    <!-- Main Workspace -->
    <main class="flex-1 grid grid-cols-1 lg:grid-cols-12 gap-6 p-6 max-w-[1700px] mx-auto w-full">
        
        <!-- Left Sidebar: Controls & Scenarios -->
        <section class="lg:col-span-3 flex flex-col gap-6">
            
            <!-- Scenario Selection -->
            <div class="glass-panel rounded-2xl p-5 shadow-xl">
                <h2 class="text-sm font-semibold tracking-wide text-cyan-400 uppercase mb-4 flex items-center gap-2">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3.055 11H5a2 2 0 012 2v1a2 2 0 002 2 2 2 0 012 2v2.945M8 3.935V5.5A2.5 2.5 0 0010.5 8h.5a2 2 0 012 2 2 2 0 104 0 2 2 0 012-2h1.064M15 20.488V18a2 2 0 012-2h3.064M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>
                    Condições Atmosféricas & Orbitais
                </h2>
                <div class="space-y-3">
                    <button onclick="setScenario('normal')" id="scen-normal" class="w-full text-left p-3 rounded-xl border border-cyan-500/40 bg-cyan-500/10 transition-all hover:bg-cyan-500/20 flex items-center justify-between group">
                        <div>
                            <div class="font-semibold text-sm text-cyan-300">Ascensão Padrão Estável</div>
                            <div class="text-xs text-slate-400">Atmosfera calma / Alinhamento perfeito</div>
                        </div>
                        <span class="w-2 h-2 rounded-full bg-cyan-400"></span>
                    </button>
                    <button onclick="setScenario('storm')" id="scen-storm" class="w-full text-left p-3 rounded-xl border border-slate-700 bg-slate-900/60 transition-all hover:border-amber-500/40 flex items-center justify-between group">
                        <div>
                            <div class="font-semibold text-sm text-slate-200 group-hover:text-amber-300">Tempestade de Vento Estratosférico</div>
                            <div class="text-xs text-slate-400">Rajadas de 250 km/h e turbulência ionosférica</div>
                        </div>
                        <span class="w-2 h-2 rounded-full bg-slate-600" id="dot-storm"></span>
                    </button>
                    <button onclick="setScenario('debris')" id="scen-debris" class="w-full text-left p-3 rounded-xl border border-slate-700 bg-slate-900/60 transition-all hover:border-rose-500/40 flex items-center justify-between group">
                        <div>
                            <div class="font-semibold text-sm text-slate-200 group-hover:text-rose-300">Desvio de Detrito Espacial</div>
                            <div class="text-xs text-slate-400">Ajuste dinâmico de Gimbals SROS</div>
                        </div>
                        <span class="w-2 h-2 rounded-full bg-slate-600" id="dot-debris"></span>
                    </button>
                </div>
            </div>

            <!-- SROS + SAMS Control Unit -->
            <div class="glass-panel rounded-2xl p-5 shadow-xl border-cyan-500/30">
                <div class="flex items-center justify-between mb-4">
                    <h2 class="text-sm font-semibold tracking-wide text-cyan-400 uppercase flex items-center gap-2">
                        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4"/></svg>
                        Parâmetros de Controle
                    </h2>
                    <span id="sys-badge" class="px-2.5 py-0.5 rounded text-xs font-mono font-bold bg-cyan-500/20 text-cyan-300 border border-cyan-500/40">ATIVO</span>
                </div>
                
                <div class="space-y-4">
                    <div class="flex items-center justify-between bg-slate-900/80 p-3 rounded-xl border border-slate-800">
                        <div>
                            <div class="text-xs font-medium text-slate-300">SAMS Amortecimento de Cabine</div>
                            <div class="text-[10px] text-slate-400 font-mono">Anulação de oscilação eólica</div>
                        </div>
                        <label class="relative inline-flex items-center cursor-pointer">
                            <input type="checkbox" id="samsToggle" checked onchange="toggleSAMS()" class="sr-only peer">
                            <div class="w-11 h-6 bg-slate-700 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-purple-500"></div>
                        </label>
                    </div>

                    <div>
                        <div class="flex justify-between text-xs mb-1 font-mono">
                            <span class="text-slate-400">Potência do Túnel Laser Full Duplex</span>
                            <span id="laser-val" class="text-emerald-400">92%</span>
                        </div>
                        <input type="range" id="laserPower" min="30" max="100" value="92" oninput="updateLaser(this.value)" class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer accent-emerald-400">
                    </div>

                    <div>
                        <div class="flex justify-between text-xs mb-1 font-mono">
                            <span class="text-slate-400">Velocidade da Cabine (Mach)</span>
                            <span class="text-cyan-400">Mach 12.5</span>
                        </div>
                        <input type="range" min="2" max="25" value="12" class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer accent-cyan-400">
                    </div>
                </div>
            </div>

            <!-- Action Triggers -->
            <div class="glass-panel rounded-2xl p-5 shadow-xl flex flex-col gap-3">
                <h2 class="text-sm font-semibold tracking-wide text-cyan-400 uppercase mb-1">Comandos SROS</h2>
                <button onclick="triggerLaserPulse()" class="w-full py-3 px-4 rounded-xl bg-gradient-to-r from-cyan-600 to-purple-600 hover:from-cyan-500 hover:to-purple-500 text-white font-semibold text-sm shadow-lg shadow-cyan-900/30 transition-all flex items-center justify-center gap-2">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/></svg>
                    Disparar Sincronização Óptica SROS
                </button>
                <button onclick="recalculateGimbals()" class="w-full py-2.5 px-4 rounded-xl bg-slate-900 hover:bg-slate-800 border border-slate-700 text-slate-300 font-medium text-xs transition-all flex items-center justify-center gap-2">
                    <svg class="w-4 h-4 text-cyan-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"/></svg>
                    Realinhar Gimbals Magnéticos
                </button>
            </div>

        </section>

        <!-- Center: Canvas 2D Simulation Viewport -->
        <section class="lg:col-span-6 flex flex-col gap-6">
            <div class="glass-panel rounded-2xl p-4 shadow-2xl relative flex flex-col overflow-hidden border-cyan-500/30">
                
                <!-- Viewport Header HUD -->
                <div class="flex items-center justify-between pb-3 mb-3 border-b border-slate-800 text-xs font-mono">
                    <div class="flex items-center gap-2">
                        <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
                        <span class="text-slate-300">ELEVADOR ESPACIAL - TÚNEL DE LASERS FULL DUPLEX</span>
                    </div>
                    <div class="flex items-center gap-4 text-slate-400">
                        <span>Altitude: <strong id="hud-alt" class="text-cyan-400">18,450 km</strong></span>
                        <span>Cabine: <strong id="hud-status" class="text-emerald-400">EM ASCENSÃO</strong></span>
                    </div>
                </div>

                <!-- Canvas Container -->
                <div class="relative w-full aspect-[4/3] bg-slate-950 rounded-xl overflow-hidden border border-slate-800 shadow-inner">
                    <canvas id="simCanvas" class="w-full h-full block"></canvas>
                    
                    <!-- HUD Instructions / Legend -->
                    <div class="absolute bottom-4 left-4 pointer-events-none bg-slate-900/80 backdrop-blur-md px-3 py-2 rounded-lg border border-cyan-500/30 text-[11px] font-mono text-cyan-300 space-y-1">
                        <div>🌐 Estação Orbital (Topo) &bull; Terra (Base)</div>
                        <div>⚡ Túnel de Laser Full Duplex sem cabo físico</div>
                    </div>

                    <!-- Storm Warning Banner -->
                    <div id="storm-banner" class="absolute top-4 inset-x-4 pointer-events-none hidden transition-all duration-300">
                        <div class="bg-amber-950/90 border border-amber-500 text-amber-200 px-4 py-2 rounded-xl text-xs font-mono font-bold flex items-center justify-center gap-2 animate-bounce">
                            <svg class="w-4 h-4 text-amber-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z"/></svg>
                            TURBULÊNCIA EÓLICA ESTRATOSFÉRICA! SAMS MANTÉM CABINE ESTÁVEL SEM TREMORES!
                        </div>
                    </div>
                </div>

                <!-- Quick Metrics Bar -->
                <div class="grid grid-cols-3 gap-3 mt-4 text-center font-mono">
                    <div class="bg-slate-900/60 p-2.5 rounded-xl border border-slate-800">
                        <div class="text-[10px] text-slate-400">Precisão do Laser SROS</div>
                        <div id="metric-precision" class="text-sm font-bold text-cyan-400">99.999%</div>
                    </div>
                    <div class="bg-slate-900/60 p-2.5 rounded-xl border border-slate-800">
                        <div class="text-[10px] text-slate-400">Amortecimento SAMS</div>
                        <div id="metric-damp" class="text-sm font-bold text-purple-400">100% Blindado</div>
                    </div>
                    <div class="bg-slate-900/60 p-2.5 rounded-xl border border-slate-800">
                        <div class="text-[10px] text-slate-400">Resistência a Detritos</div>
                        <div id="metric-debris" class="text-sm font-bold text-emerald-400">Desvio Dinâmico OK</div>
                    </div>
                </div>

            </div>
        </section>

        <!-- Right Sidebar: Telemetry & SROS AI Console -->
        <section class="lg:col-span-3 flex flex-col gap-6">
            
            <!-- Orbital Station Telemetry -->
            <div class="glass-panel rounded-2xl p-5 shadow-xl">
                <h2 class="text-sm font-semibold tracking-wide text-cyan-400 uppercase mb-4 flex items-center gap-2">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10"/></svg>
                    Telemetria da Estação Orbital
                </h2>
                <div class="space-y-3 font-mono text-xs">
                    <div class="flex justify-between items-center bg-slate-900/80 p-2.5 rounded-xl border border-slate-800">
                        <span class="text-slate-400">Altitude Orbital</span>
                        <span class="text-cyan-400 font-bold">35,786 km (GEO)</span>
                    </div>
                    <div class="flex justify-between items-center bg-slate-900/80 p-2.5 rounded-xl border border-slate-800">
                        <span class="text-slate-400">Gimbals Magnéticos</span>
                        <span class="text-emerald-400 font-bold">12 Ativos</span>
                    </div>
                    <div class="flex justify-between items-center bg-slate-900/80 p-2.5 rounded-xl border border-slate-800">
                        <span class="text-slate-400">Eficiência Full Duplex</span>
                        <span class="text-purple-400 font-bold">99.8%</span>
                    </div>
                    <div class="flex justify-between items-center bg-slate-900/80 p-2.5 rounded-xl border border-slate-800">
                        <span class="text-slate-400">Passageiros / Carga</span>
                        <span class="text-amber-400 font-bold">14 Toneladas</span>
                    </div>
                </div>
            </div>

            <!-- SROS AI Console -->
            <div class="glass-panel rounded-2xl p-5 shadow-xl flex flex-col flex-1 min-h-[260px]">
                <h2 class="text-sm font-semibold tracking-wide text-cyan-400 uppercase mb-3 flex items-center gap-2">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 9l3 3-3 3m5 0h3M5 20h14a2 2 0 002-2V6a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"/></svg>
                    Console SROS AI Telemetry
                </h2>
                <div id="ai-console" class="flex-1 bg-slate-950/80 rounded-xl p-3 border border-slate-900 font-mono text-[11px] text-slate-300 space-y-1.5 overflow-y-auto max-h-[220px]">
                    <div class="text-slate-500">[00:00:01] SROS AutoNav & Gimbals magnéticos inicializados.</div>
                    <div class="text-cyan-400">[00:00:03] Túnel de lasers Full Duplex estabelecido com a Terra.</div>
                    <div class="text-purple-400">[00:00:05] SAMS ativado na cabine de ascensão automática.</div>
                </div>
            </div>

        </section>

    </main>

    <!-- Footer -->
    <footer class="text-center py-4 text-xs text-slate-500 border-t border-slate-900 font-mono">
        SROS (Spatial Robotic Optical System) & SAMS (Smart Active Micro-Vibration Suppression) &bull; Elevadores Espaciais v3.1
    </footer>

    <!-- JavaScript Simulation Engine -->
    <script>
        // --- Simulation State ---
        let state = {
            scenario: 'normal', // 'normal', 'storm', 'debris'
            samsActive: true,
            laserPower: 92,
            cabinProgress: 0.35, // 0.0 (Earth) to 1.0 (Orbit)
            time: 0,
            stormActive: false
        };

        // DOM Elements
        const canvas = document.getElementById('simCanvas');
        const ctx = canvas.getContext('2d');
        const samsToggleEl = document.getElementById('samsToggle');
        const sysBadgeEl = document.getElementById('sys-badge');
        const stormBannerEl = document.getElementById('storm-banner');
        const hudAltEl = document.getElementById('hud-alt');
        const hudStatusEl = document.getElementById('hud-status');
        const metricPrecisionEl = document.getElementById('metric-precision');
        const metricDampEl = document.getElementById('metric-damp');
        const aiConsole = document.getElementById('ai-console');

        // Audio Helper
        let audioCtx = null;
        function initAudio() {
            if (!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        }

        function playBeep(freq = 440, type = 'sine', duration = 0.1) {
            try {
                initAudio();
                if (!audioCtx) return;
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = type;
                osc.frequency.value = freq;
                gain.gain.setValueAtTime(0.04, audioCtx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.0001, audioCtx.currentTime + duration);
                osc.connect(gain);
                gain.connect(audioCtx.destination);
                osc.start();
                osc.stop(audioCtx.currentTime + duration);
            } catch (e) {}
        }

        // Resize Canvas
        function resizeCanvas() {
            const rect = canvas.getBoundingClientRect();
            canvas.width = rect.width * window.devicePixelRatio;
            canvas.height = rect.height * window.devicePixelRatio;
            ctx.setTransform(window.devicePixelRatio, 0, 0, window.devicePixelRatio, 0, 0);
        }

        window.addEventListener('resize', resizeCanvas);

        // Control Handlers
        function setScenario(scen) {
            state.scenario = scen;
            ['normal', 'storm', 'debris'].forEach(s => {
                const btn = document.getElementById(`scen-${s}`);
                if (s === scen) {
                    btn.className = "w-full text-left p-3 rounded-xl border border-cyan-500/40 bg-cyan-500/10 transition-all flex items-center justify-between group";
                } else {
                    btn.className = "w-full text-left p-3 rounded-xl border border-slate-700 bg-slate-900/60 transition-all hover:border-slate-500 flex items-center justify-between group";
                }
            });

            if (scen === 'storm') {
                state.stormActive = true;
                stormBannerEl.classList.remove('hidden');
                logAI("⚠️ Tempestade eólica estratosférica detectada! Gimbals SROS compensando desalinhamento.");
                playBeep(450, 'sawtooth', 0.2);
            } else if (scen === 'debris') {
                state.stormActive = false;
                stormBannerEl.classList.add('hidden');
                logAI("☄️ Detrito espacial na rota orbital! SROS AutoNav desviou o túnel laser Full Duplex em 12 metros.");
                playBeep(650, 'triangle', 0.2);
            } else {
                state.stormActive = false;
                stormBannerEl.classList.add('hidden');
                logAI("Cenário de Ascensão Padrão Estável ativado.");
                playBeep(440, 'sine', 0.1);
            }
        }

        function toggleSAMS() {
            state.samsActive = samsToggleEl.checked;
            if (state.samsActive) {
                sysBadgeEl.textContent = "ATIVO";
                sysBadgeEl.className = "px-2.5 py-0.5 rounded text-xs font-mono font-bold bg-cyan-500/20 text-cyan-300 border border-cyan-500/40";
                logAI("SAMS reativado na cabine: 100% de anulação de tremores e oscilações.");
                playBeep(880, 'sine', 0.2);
            } else {
                sysBadgeEl.textContent = "VULNERÁVEL";
                sysBadgeEl.className = "px-2.5 py-0.5 rounded text-xs font-mono font-bold bg-rose-500/20 text-rose-300 border border-rose-500/40";
                logAI("ALERTA: SAMS desativado! Cabine sujeita a oscilações severas por rajadas de vento.");
                playBeep(180, 'sawtooth', 0.3);
            }
        }

        function updateLaser(val) {
            state.laserPower = parseInt(val);
            document.getElementById('laser-val').textContent = val + '%';
        }

        function triggerLaserPulse() {
            logAI("⚡ Pulso Full Duplex de alta coerência disparado. Sincronização quântica de feixe concluída.");
            playBeep(1200, 'square', 0.25);
        }

        function recalibrateGimbals() {
            logAI("🔄 Gimbals magnéticos realinhados com sucesso. Precisão sub-micrométrica restaurada.");
            playBeep(750, 'sine', 0.2);
        }

        function logAI(message) {
            const timeStr = new Date().toTimeString().split(' ')[0];
            const div = document.createElement('div');
            div.className = "text-slate-300";
            div.innerHTML = `<span class="text-slate-500">[${timeStr}]</span> ${message}`;
            aiConsole.appendChild(div);
            aiConsole.scrollTop = aiConsole.scrollHeight;
        }

        // --- Main Animation & Simulation Loop ---
        function updateSimulation() {
            state.time += 0.03;
            state.cabinProgress += 0.0025;
            if (state.cabinProgress > 1.0) state.cabinProgress = 0.0; // Loop cabin ascent

            drawCanvas();
            requestAnimationFrame(updateSimulation);
        }

        function drawCanvas() {
            const width = canvas.clientWidth;
            const height = canvas.clientHeight;
            
            ctx.clearRect(0, 0, width, height);

            // Draw space background (top) and Earth (bottom)
            // Space Gradient
            const bgGrad = ctx.createLinearGradient(0, 0, 0, height);
            bgGrad.addColorStop(0, '#020617'); // deep space
            bgGrad.addColorStop(0.3, '#090d16');
            bgGrad.addColorStop(0.7, '#0e1b2a'); // stratosphere / atmosphere
            bgGrad.addColorStop(1, '#06283d'); // Earth surface
            ctx.fillStyle = bgGrad;
            ctx.fillRect(0, 0, width, height);

            // Draw stars in space
            ctx.fillStyle = '#ffffff';
            for (let i = 0; i < 40; i++) {
                const sx = (Math.sin(i * 123.45) * 10000) % width;
                const sy = (Math.cos(i * 67.89) * 10000) % (height * 0.4);
                ctx.fillRect(Math.abs(sx), Math.abs(sy), 1.5, 1.5);
            }

            // Coordinates for Space Elevator Line (Vertical center)
            const elevatorX = width / 2;
            const earthSurfaceY = height - 60;
            const orbitalStationY = 70;

            // Draw Earth Curve at bottom
            ctx.fillStyle = '#06b6d4';
            ctx.beginPath();
            ctx.arc(elevatorX, earthSurfaceY + 800, 800, 0, Math.PI * 2);
            ctx.fill();

            // Earth Base Station
            ctx.fillStyle = '#0f172a';
            ctx.strokeStyle = '#06b6d4';
            ctx.lineWidth = 2;
            ctx.fillRect(elevatorX - 40, earthSurfaceY - 30, 80, 30);
            ctx.strokeRect(elevatorX - 40, earthSurfaceY - 30, 80, 30);

            // Orbital Station (Top)
            ctx.fillStyle = '#0f172a';
            ctx.strokeStyle = '#8b5cf6';
            ctx.lineWidth = 3;
            ctx.fillRect(elevatorX - 60, orbitalStationY - 15, 120, 30);
            ctx.strokeRect(elevatorX - 60, orbitalStationY - 15, 120, 30);

            // Draw Full Duplex Laser Tunnel (Two glowing parallel beams)
            const laserWidth = 18;
            ctx.save();
            ctx.shadowColor = '#10b981';
            ctx.shadowBlur = 15;

            // Left Laser Beam (Upward transmission)
            ctx.strokeStyle = 'rgba(16, 185, 129, 0.8)';
            ctx.lineWidth = 3;
            ctx.beginPath();
            ctx.moveTo(elevatorX - laserWidth, earthSurfaceY - 30);
            ctx.lineTo(elevatorX - laserWidth + (state.stormActive ? Math.sin(state.time * 15) * 12 : 0), orbitalStationY + 15);
            ctx.stroke();

            // Right Laser Beam (Downward synchronization return)
            ctx.strokeStyle = 'rgba(6, 182, 212, 0.8)';
            ctx.lineWidth = 3;
            ctx.beginPath();
            ctx.moveTo(elevatorX + laserWidth, earthSurfaceY - 30);
            ctx.lineTo(elevatorX + laserWidth + (state.stormActive ? Math.sin(state.time * 15) * 12 : 0), orbitalStationY + 15);
            ctx.stroke();

            ctx.restore();

            // Draw magnetic gimbal rings along the laser corridor
            for (let y = 150; y < earthSurfaceY - 50; y += 120) {
                const gimbalShift = state.stormActive ? Math.sin(state.time * 10 + y) * 8 : 0;
                ctx.strokeStyle = 'rgba(139, 92, 246, 0.5)';
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.arc(elevatorX + gimbalShift, y, 22, 0, Math.PI * 2);
                ctx.stroke();
            }

            // Calculate Cabin position along the laser tunnel
            const cabinY = earthSurfaceY - 30 - (state.cabinProgress * (earthSurfaceY - 30 - orbitalStationY - 15));
            const currentWindShake = state.stormActive ? Math.sin(state.time * 30) * (state.samsActive ? 0.5 : 18) : 0;
            const cabinX = elevatorX + currentWindShake;

            // Draw Automated Cabin
            ctx.fillStyle = '#0f172a';
            ctx.strokeStyle = state.samsActive ? '#8b5cf6' : '#f43f5e';
            ctx.lineWidth = 3;
            ctx.fillRect(cabinX - 16, cabinY - 22, 32, 44);
            ctx.strokeRect(cabinX - 16, cabinY - 22, 32, 44);

            // Cabin Windows
            ctx.fillStyle = '#06b6d4';
            ctx.fillRect(cabinX - 8, cabinY - 12, 16, 8);
            ctx.fillRect(cabinX - 8, cabinY + 4, 16, 8);

            // SAMS dampening forcefield ripple around cabin if active
            if (state.samsActive) {
                ctx.strokeStyle = 'rgba(139, 92, 246, 0.6)';
                ctx.lineWidth = 1.5;
                ctx.beginPath();
                ctx.arc(cabinX, cabinY, 28 + Math.sin(state.time * 8) * 4, 0, Math.PI * 2);
                ctx.stroke();
            }

            // Update HUD values dynamically
            const currentAltitudeKm = Math.round(state.cabinProgress * 35786);
            hudAltEl.textContent = currentAltitudeKm.toLocaleString() + " km";

            if (state.stormActive && !state.samsActive) {
                hudStatusEl.textContent = "TURBULÊNCIA CRÍTICA!";
                hudStatusEl.className = "text-rose-400 font-bold";
                metricDampEl.textContent = "DESLIGADO (Vulnerável)";
                metricDampEl.className = "text-sm font-bold text-rose-400";
            } else if (state.stormActive && state.samsActive) {
                hudStatusEl.textContent = "EM ASCENSÃO (SAMS ATIVO)";
                hudStatusEl.className = "text-amber-400 font-bold";
                metricDampEl.textContent = "100% Amortecido";
                metricDampEl.className = "text-sm font-bold text-purple-400";
            } else {
                hudStatusEl.textContent = "EM ASCENSÃO ESTÁVEL";
                hudStatusEl.className = "text-emerald-400 font-bold";
                metricDampEl.textContent = "100% Blindado";
                metricDampEl.className = "text-sm font-bold text-purple-400";
            }
        }

        // Initialize on load
        window.onload = function() {
            resizeCanvas();
            updateSimulation();
        };
    </script>
</body>
</html>
