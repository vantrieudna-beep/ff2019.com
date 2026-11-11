<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FF CyberHack - Trình Chỉnh Độ Nhạy Free Fire Hacker Edition</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Orbitron & Fira Code -->
    <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;600;700&family=Orbitron:wght@500;700;900&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        cyber: {
                            black: '#08080a',
                            card: '#121218',
                            border: '#ff003c',
                            red: '#ff003c',
                            redglow: '#ff1744',
                            darkred: '#80001c',
                            neon: '#ff3366',
                            text: '#e0e0e0'
                        }
                    },
                    fontFamily: {
                        orbitron: ['Orbitron', 'sans-serif'],
                        mono: ['Fira Code', 'monospace']
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #08080a;
            color: #e0e0e0;
            font-family: 'Fira Code', monospace;
            overflow-x: hidden;
        }

        /* Glitch & Neon Glow Effects */
        .neon-text-red {
            text-shadow: 0 0 5px #ff003c, 0 0 15px #ff003c, 0 0 30px #ff003c;
        }

        .neon-border-red {
            box-shadow: 0 0 10px rgba(255, 0, 60, 0.4), inset 0 0 10px rgba(255, 0, 60, 0.2);
            border: 1px solid #ff003c;
        }

        .cyber-card {
            background: rgba(18, 18, 24, 0.85);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 0, 60, 0.3);
            position: relative;
            clip-path: polygon(0 0, calc(100% - 15px) 0, 100% 15px, 100% 100%, 15px 100%, 0 calc(100% - 15px));
        }

        .cyber-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 2px;
            background: linear-gradient(90deg, transparent, #ff003c, transparent);
        }

        /* Custom Range Slider */
        input[type=range] {
            -webkit-appearance: none;
            width: 100%;
            background: #1a1a24;
            height: 8px;
            border-radius: 4px;
            outline: none;
            border: 1px solid rgba(255, 0, 60, 0.3);
        }

        input[type=range]::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 20px;
            height: 20px;
            border-radius: 4px;
            background: #ff003c;
            cursor: pointer;
            box-shadow: 0 0 10px #ff003c, 0 0 20px #ff003c;
            border: 2px solid #ffffff;
            transition: transform 0.1s;
        }

        input[type=range]::-webkit-slider-thumb:hover {
            transform: scale(1.2);
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #08080a;
        }
        ::-webkit-scrollbar-thumb {
            background: #ff003c;
            border-radius: 3px;
        }

        /* Tech Checkbox Toggle */
        .cyber-switch input:checked + .cyber-slider {
            background-color: #ff003c;
            box-shadow: 0 0 10px #ff003c;
        }
        .cyber-switch input:checked + .cyber-slider:before {
            transform: translateX(20px);
            background-color: #ffffff;
        }

        /* Matrix / Scanline overlay */
        .scanline {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%);
            background-size: 100% 4px;
            z-index: 5;
            pointer-events: none;
            opacity: 0.6;
        }

        /* Cyber Button Effect */
        .cyber-btn {
            position: relative;
            background: rgba(255, 0, 60, 0.15);
            border: 1px solid #ff003c;
            transition: all 0.2s ease;
            text-transform: uppercase;
            letter-spacing: 1px;
            overflow: hidden;
        }
        .cyber-btn:hover {
            background: #ff003c;
            color: #000;
            box-shadow: 0 0 15px #ff003c;
            font-weight: bold;
        }
    </style>
</head>
<body class="min-h-screen relative pb-12 select-none">

    <!-- Scanline Overlay -->
    <div class="scanline"></div>

    <!-- Canvas Hạt Nền Cyberpunk -->
    <canvas id="cyber-canvas" class="fixed top-0 left-0 w-full h-full z-0 pointer-events-none opacity-40"></canvas>

    <!-- Main Container -->
    <div class="relative z-10 max-w-6xl mx-auto px-4 pt-6">

        <!-- Header -->
        <header class="flex flex-col md:flex-row items-center justify-between border-b border-cyber-red/40 pb-4 mb-8">
            <div class="flex items-center space-x-3 mb-4 md:mb-0">
                <div class="w-12 h-12 rounded bg-cyber-red/20 border border-cyber-red flex items-center justify-center text-cyber-red neon-border-red">
                    <i class="fa-solid fa-crosshairs text-2xl animate-pulse"></i>
                </div>
                <div>
                    <h1 class="font-orbitron text-2xl md:text-3xl font-black tracking-wider text-white flex items-center gap-2">
                        FF <span class="text-cyber-red neon-text-red">CYBERHACK</span> v3.0
                    </h1>
                    <p class="text-xs text-gray-400 tracking-widest font-mono">[ SYSTEM: SENSITIVITY ENGINE & AIM ASSIST ]</p>
                </div>
            </div>

            <!-- Audio Toggle & System Status -->
            <div class="flex items-center gap-4">
                <button id="sound-toggle" onclick="toggleSound()" class="cyber-btn px-3 py-1.5 rounded text-xs text-cyber-red flex items-center gap-2">
                    <i id="sound-icon" class="fa-solid fa-volume-high"></i>
                    <span id="sound-status">AUDIO: ON</span>
                </button>
                <div class="hidden sm:flex items-center gap-2 px-3 py-1.5 rounded bg-black/60 border border-cyber-red/30 text-xs">
                    <span class="w-2 h-2 rounded-full bg-green-500 animate-ping"></span>
                    <span class="text-gray-300">STATUS: ACTIVE</span>
                </div>
            </div>
        </header>

        <!-- Presets Quick Bar -->
        <section class="mb-8">
            <h2 class="text-xs font-orbitron uppercase text-gray-400 mb-3 tracking-wider flex items-center gap-2">
                <i class="fa-solid fa-bolt text-cyber-red"></i> Quick Preset Injection (Cấu Hình Mẫu Nhanh)
            </h2>
            <div class="grid grid-cols-2 sm:grid-cols-4 gap-3">
                <button onclick="applyPreset('headshot')" class="cyber-btn p-3 rounded text-left group">
                    <div class="text-xs text-gray-400 group-hover:text-black">100% RED HEADSHOT</div>
                    <div class="font-orbitron font-bold text-sm text-cyber-red group-hover:text-black flex items-center justify-between">
                        Kéo Tâm Siêu Nhạy <i class="fa-solid fa-fire text-xs"></i>
                    </div>
                </button>
                <button onclick="applyPreset('antirecoil')" class="cyber-btn p-3 rounded text-left group">
                    <div class="text-xs text-gray-400 group-hover:text-black">STABLE SPRAY</div>
                    <div class="font-orbitron font-bold text-sm text-cyber-red group-hover:text-black flex items-center justify-between">
                        Ổn Định Chống Rung <i class="fa-solid fa-shield-halved text-xs"></i>
                    </div>
                </button>
                <button onclick="applyPreset('lowend')" class="cyber-btn p-3 rounded text-left group">
                    <div class="text-xs text-gray-400 group-hover:text-black">LOW-END DEVICE</div>
                    <div class="font-orbitron font-bold text-sm text-cyber-red group-hover:text-black flex items-center justify-between">
                        Máy Yếu (Max Sens) <i class="fa-solid fa-mobile-screen text-xs"></i>
                    </div>
                </button>
                <button onclick="applyPreset('highend')" class="cyber-btn p-3 rounded text-left group">
                    <div class="text-xs text-gray-400 group-hover:text-black">HIGH-END DEVICE</div>
                    <div class="font-orbitron font-bold text-sm text-cyber-red group-hover:text-black flex items-center justify-between">
                        Máy Mượt / iPad <i class="fa-solid fa-gamepad text-xs"></i>
                    </div>
                </button>
            </div>
        </section>

        <!-- Main Layout: Sliders & Drag-Aim Config -->
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8 mb-8">

            <!-- Left 2 Columns: Sensitivity Sliders (0 - 200) -->
            <div class="lg:col-span-2 space-y-6">
                <div class="cyber-card p-6">
                    <div class="flex items-center justify-between border-b border-cyber-red/30 pb-3 mb-6">
                        <h3 class="font-orbitron font-bold text-lg text-white flex items-center gap-2">
                            <i class="fa-solid fa-sliders text-cyber-red"></i> ĐỘ NHẠY SÚNG (0 - 200)
                        </h3>
                        <span class="text-xs font-mono text-cyber-red bg-cyber-red/10 px-2 py-1 rounded border border-cyber-red/30">FF-RANGE CONTROL</span>
                    </div>

                    <div id="sliders-container" class="space-y-5">
                        <!-- Sliders generated dynamically via JavaScript -->
                    </div>
                </div>
            </div>

            <!-- Right Column: Drag Aim & Hardware Config -->
            <div class="space-y-6">
                <!-- Aim & Fire Button Config -->
                <div class="cyber-card p-6">
                    <div class="border-b border-cyber-red/30 pb-3 mb-5">
                        <h3 class="font-orbitron font-bold text-lg text-white flex items-center gap-2">
                            <i class="fa-solid fa-bullseye text-cyber-red"></i> CẤU HÌNH KÉO TÂM
                        </h3>
                    </div>

                    <div class="space-y-5">
                        <!-- Fire Button Size -->
                        <div>
                            <div class="flex justify-between items-center mb-1 text-sm">
                                <span class="text-gray-300 font-semibold flex items-center gap-2">
                                    <i class="fa-solid fa-circle-dot text-cyber-red text-xs"></i> Nút Bắn (Fire Button):
                                </span>
                                <span id="val-firebutton" class="text-cyber-red font-mono font-bold">52%</span>
                            </div>
                            <input type="range" id="firebutton" min="30" max="80" value="52" oninput="updateConfig('firebutton', this.value)">
                            <div class="flex justify-between text-[10px] text-gray-500 mt-1">
                                <span>Nhỏ (30%)</span>
                                <span>Khuyên dùng (45-55%)</span>
                                <span>Lớn (80%)</span>
                            </div>
                        </div>

                        <!-- DPI / Pointer Speed -->
                        <div>
                            <div class="flex justify-between items-center mb-1 text-sm">
                                <span class="text-gray-300 font-semibold flex items-center gap-2">
                                    <i class="fa-solid fa-microchip text-cyber-red text-xs"></i> DPI / Tốc Độ Con Trỏ:
                                </span>
                                <span id="val-dpi" class="text-cyber-red font-mono font-bold">480 DPI</span>
                            </div>
                            <input type="range" id="dpi" min="320" max="960" step="10" value="480" oninput="updateConfig('dpi', this.value)">
                        </div>

                        <!-- Drag Tech Type -->
                        <div>
                            <label class="block text-sm text-gray-300 font-semibold mb-2 flex items-center gap-2">
                                <i class="fa-solid fa-arrow-trend-up text-cyber-red text-xs"></i> Kĩ Thuật Kéo Tâm:
                            </label>
                            <select id="drag-tech" onchange="playSound('click'); saveState()" class="w-full bg-black/80 border border-cyber-red/50 text-white rounded p-2.5 text-sm focus:outline-none focus:border-cyber-red font-mono">
                                <option value="Kéo Thẳng Đứng (Straight Drag)">Kéo Thẳng Đứng (Cận Chiến / SMG)</option>
                                <option value="Kéo Chữ U (U-Shape Drag)">Kéo Chữ U (Tầm Trung / Shotgun)</option>
                                <option value="Kéo Vuốt Nhẹ (Soft Flick)">Kéo Vuốt Nhẹ (Sniper / AR Long)</option>
                                <option value="Kéo Xoay Tròn (Circle Drag)">Kéo Xoay Tròn (Đảo Tâm Headshot)</option>
                            </select>
                        </div>

                        <!-- Anti-shake / Lock Assist Toggles -->
                        <div class="pt-3 border-t border-cyber-red/20 space-y-3">
                            <div class="flex items-center justify-between">
                                <span class="text-xs text-gray-300 flex items-center gap-2">
                                    <i class="fa-solid fa-lock text-cyber-red"></i> Gắn Khóa Tâm (Aim Lock Helper)
                                </span>
                                <label class="relative inline-flex items-center cursor-pointer cyber-switch">
                                    <input type="checkbox" id="toggle-aimlock" checked onchange="playSound('click'); saveState()" class="sr-only">
                                    <div class="w-10 h-5 bg-gray-800 rounded-full border border-cyber-red/40 cyber-slider transition-all duration-300 before:content-[''] before:absolute before:top-[2px] before:left-[2px] before:bg-cyber-red before:w-4 before:h-4 before:rounded-full before:transition-all"></div>
                                </label>
                            </div>

                            <div class="flex items-center justify-between">
                                <span class="text-xs text-gray-300 flex items-center gap-2">
                                    <i class="fa-solid fa-wave-square text-cyber-red"></i> Ổn Định Chống Rung Tâm
                                </span>
                                <label class="relative inline-flex items-center cursor-pointer cyber-switch">
                                    <input type="checkbox" id="toggle-antishake" checked onchange="playSound('click'); saveState()" class="sr-only">
                                    <div class="w-10 h-5 bg-gray-800 rounded-full border border-cyber-red/40 cyber-slider transition-all duration-300 before:content-[''] before:absolute before:top-[2px] before:left-[2px] before:bg-cyber-red before:w-4 before:h-4 before:rounded-full before:transition-all"></div>
                                </label>
                            </div>
                        </div>

                    </div>
                </div>

                <!-- Action Controls (Copy & Reset) -->
                <div class="cyber-card p-6 flex flex-col gap-3">
                    <button onclick="copyConfiguration()" class="cyber-btn py-3 px-4 rounded text-white font-orbitron font-bold text-sm flex items-center justify-center gap-2 bg-cyber-red/30">
                        <i class="fa-solid fa-copy text-base"></i> SAO CHÉP THÔNG SỐ (COPY)
                    </button>
                    <button onclick="resetConfiguration()" class="cyber-btn py-2.5 px-4 rounded text-gray-300 hover:text-black font-orbitron text-xs flex items-center justify-center gap-2 border-gray-600">
                        <i class="fa-solid fa-rotate-left"></i> ĐẶT LẠI CẤU HÌNH (RESET)
                    </button>
                </div>
            </div>

        </div>

        <!-- System Preview Box (Generated Output Code) -->
        <div class="cyber-card p-6 mb-8">
            <div class="flex items-center justify-between mb-3">
                <span class="text-xs font-orbitron text-cyber-red uppercase tracking-wider flex items-center gap-2">
                    <i class="fa-solid fa-terminal"></i> Config Export Output (Xem Trước)
                </span>
                <span class="text-[10px] text-gray-500 font-mono">READY TO SHARE</span>
            </div>
            <textarea id="config-output" readonly class="w-full h-32 bg-black/90 text-cyber-red border border-cyber-red/30 rounded p-3 font-mono text-xs focus:outline-none resize-none select-all"></textarea>
        </div>

        <!-- Footer -->
        <footer class="text-center text-xs text-gray-500 font-mono py-4 border-t border-cyber-red/20">
            <p>FF CYBERHACK SENSITIVITY GENERATOR &copy; 2026 | DESIGNED FOR FREE FIRE OPERATORS</p>
            <p class="text-[10px] text-gray-600 mt-1">Disclaimer: Công cụ hỗ trợ tối ưu hóa cài đặt độ nhạy & thông số kỹ năng trong game.</p>
        </footer>

    </div>

    <!-- Notification Toast -->
    <div id="toast" class="fixed bottom-6 right-6 z-50 transform translate-y-20 opacity-0 transition-all duration-300 pointer-events-none">
        <div class="cyber-card px-5 py-3 flex items-center gap-3 border-cyber-red text-white shadow-2xl">
            <i id="toast-icon" class="fa-solid fa-circle-check text-cyber-red text-lg"></i>
            <div>
                <h4 id="toast-title" class="font-orbitron font-bold text-xs text-white">SUCCESS</h4>
                <p id="toast-msg" class="text-xs text-gray-300 font-mono">Thông số đã được chép vào Clipboard!</p>
            </div>
        </div>
    </div>

    <!-- Script Application Logic -->
    <script>
        // Configuration Schema
        const SENS_ITEMS = [
            { id: 'general', name: 'Nhìn Xung Quanh (General)', icon: 'fa-eye', default: 175 },
            { id: 'reddot', name: 'Red Dot Sight', icon: 'fa-circle-dot', default: 150 },
            { id: 'scope2x', name: 'Ống Ngắm 2X (Scope 2X)', icon: 'fa-crosshairs', default: 145 },
            { id: 'scope4x', name: 'Ống Ngắm 4X (Scope 4X)', icon: 'fa-expand', default: 125 },
            { id: 'awm', name: 'Ống Ngắm AWM / Sniper', icon: 'fa-bullseye', default: 90 },
            { id: 'freelook', name: 'Nhìn Tự Do (Free Look)', icon: 'fa-compass', default: 100 }
        ];

        // Global Audio State
        let soundEnabled = true;
        let audioCtx = null;

        // Sound Generator using Web Audio API
        function playSound(type) {
            if (!soundEnabled) return;
            try {
                if (!audioCtx) {
                    audioCtx = new (window.AudioContext || window.webkitAudioContext)();
                }
                if (audioCtx.state === 'suspended') {
                    audioCtx.resume();
                }

                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.connect(gain);
                gain.connect(audioCtx.destination);

                if (type === 'slider') {
                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(400, audioCtx.currentTime);
                    gain.gain.setValueAtTime(0.03, audioCtx.currentTime);
                    gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 0.05);
                    osc.start();
                    osc.stop(audioCtx.currentTime + 0.05);
                } else if (type === 'click') {
                    osc.type = 'triangle';
                    osc.frequency.setValueAtTime(800, audioCtx.currentTime);
                    gain.gain.setValueAtTime(0.08, audioCtx.currentTime);
                    gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 0.08);
                    osc.start();
                    osc.stop(audioCtx.currentTime + 0.08);
                } else if (type === 'copy') {
                    osc.type = 'square';
                    osc.frequency.setValueAtTime(520, audioCtx.currentTime);
                    osc.frequency.exponentialRampToValueAtTime(1040, audioCtx.currentTime + 0.15);
                    gain.gain.setValueAtTime(0.1, audioCtx.currentTime);
                    gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 0.15);
                    osc.start();
                    osc.stop(audioCtx.currentTime + 0.15);
                }
            } catch (e) {
                console.error("Audio playback error", e);
            }
        }

        function toggleSound() {
            soundEnabled = !soundEnabled;
            const statusText = document.getElementById('sound-status');
            const icon = document.getElementById('sound-icon');
            if (soundEnabled) {
                statusText.innerText = "AUDIO: ON";
                icon.className = "fa-solid fa-volume-high";
                playSound('click');
            } else {
                statusText.innerText = "AUDIO: OFF";
                icon.className = "fa-solid fa-volume-xmark";
            }
        }

        // Initialize Sliders HTML Dynamic Generation
        function initSliders() {
            const container = document.getElementById('sliders-container');
            container.innerHTML = '';

            SENS_ITEMS.forEach(item => {
                const itemEl = document.createElement('div');
                itemEl.className = 'space-y-1 bg-black/40 p-3 rounded border border-cyber-red/10 hover:border-cyber-red/40 transition-all';
                itemEl.innerHTML = `
                    <div class="flex justify-between items-center mb-1">
                        <label for="${item.id}" class="text-sm font-semibold text-gray-200 flex items-center gap-2">
                            <i class="fa-solid ${item.icon} text-cyber-red text-xs"></i> ${item.name}
                        </label>
                        <div class="flex items-center gap-2">
                            <input type="number" id="num-${item.id}" min="0" max="200" value="${item.default}" 
                                onchange="onNumberInput('${item.id}', this.value)"
                                class="w-16 bg-black border border-cyber-red/40 text-cyber-red text-right px-2 py-0.5 text-sm font-mono rounded focus:outline-none focus:border-cyber-red">
                            <span class="text-xs text-gray-500 font-mono">/ 200</span>
                        </div>
                    </div>
                    <input type="range" id="range-${item.id}" min="0" max="200" value="${item.default}" 
                        oninput="onRangeInput('${item.id}', this.value)">
                `;
                container.appendChild(itemEl);
            });
        }

        // Handle Slider & Number Sync
        function onRangeInput(id, val) {
            val = Math.min(200, Math.max(0, parseInt(val) || 0));
            document.getElementById(`num-${id}`).value = val;
            playSound('slider');
            updateOutputText();
        }

        function onNumberInput(id, val) {
            val = Math.min(200, Math.max(0, parseInt(val) || 0));
            document.getElementById(`range-${id}`).value = val;
            document.getElementById(`num-${id}`).value = val;
            playSound('click');
            updateOutputText();
        }

        function updateConfig(id, val) {
            if (id === 'firebutton') {
                document.getElementById('val-firebutton').innerText = val + '%';
            } else if (id === 'dpi') {
                document.getElementById('val-dpi').innerText = val + ' DPI';
            }
            playSound('slider');
            updateOutputText();
        }

        // Apply Preset Configurations
        function applyPreset(presetType) {
            playSound('click');
            let configs = {};

            switch(presetType) {
                case 'headshot':
                    configs = { general: 195, reddot: 185, scope2x: 170, scope4x: 160, awm: 110, freelook: 120, firebutton: 48, dpi: 560 };
                    break;
                case 'antirecoil':
                    configs = { general: 140, reddot: 130, scope2x: 125, scope4x: 110, awm: 80, freelook: 100, firebutton: 58, dpi: 420 };
                    break;
                case 'lowend':
                    configs = { general: 200, reddot: 200, scope2x: 190, scope4x: 180, awm: 130, freelook: 150, firebutton: 45, dpi: 600 };
                    break;
                case 'highend':
                    configs = { general: 155, reddot: 145, scope2x: 135, scope4x: 120, awm: 85, freelook: 90, firebutton: 54, dpi: 450 };
                    break;
            }

            // Update UI elements
            SENS_ITEMS.forEach(item => {
                if (configs[item.id] !== undefined) {
                    document.getElementById(`range-${item.id}`).value = configs[item.id];
                    document.getElementById(`num-${item.id}`).value = configs[item.id];
                }
            });

            if (configs.firebutton) {
                document.getElementById('firebutton').value = configs.firebutton;
                document.getElementById('val-firebutton').innerText = configs.firebutton + '%';
            }
            if (configs.dpi) {
                document.getElementById('dpi').value = configs.dpi;
                document.getElementById('val-dpi').innerText = configs.dpi + ' DPI';
            }

            showToast("PRESET APPLIED", `Đã tải cấu hình: ${presetType.toUpperCase()}`);
            updateOutputText();
        }

        // Generate Formatted Text Configuration for Sharing
        function generateExportString() {
            let text = "🎮 === CẤU HÌNH ĐỘ NHẠY FREE FIRE [CYBERHACK V3.0] === 🎮\n\n";
            text += "🎯 [ĐỘ NHẠY SÚNG / SENSITIVITY]:\n";

            SENS_ITEMS.forEach(item => {
                const val = document.getElementById(`num-${item.id}`).value;
                text += `  • ${item.name}: ${val}\n`;
            });

            const fireBtn = document.getElementById('firebutton').value;
            const dpiVal = document.getElementById('dpi').value;
            const dragTech = document.getElementById('drag-tech').value;
            const aimlock = document.getElementById('toggle-aimlock').checked ? "BẬT (ON)" : "TẮT (OFF)";
            const antishake = document.getElementById('toggle-antishake').checked ? "BẬT (ON)" : "TẮT (OFF)";

            text += "\n⚙️ [CẤU HÌNH KÉO TÂM & NÚT BẮN]:\n";
            text += `  • Nút Bắn (Fire Button): ${fireBtn}%\n`;
            text += `  • Khuyên Dùng DPI: ${dpiVal} DPI\n`;
            text += `  • Kĩ Thuật Kéo: ${dragTech}\n`;
            text += `  • Khóa Tâm Hỗ Trợ: ${aimlock}\n`;
            text += `  • Ổn Định Chống Rung: ${antishake}\n\n`;
            text += "⚡ Tạo tại: FF CyberHack Sensitivity Engine";

            return text;
        }

        function updateOutputText() {
            document.getElementById('config-output').value = generateExportString();
        }

        // Copy configuration to Clipboard
        function copyConfiguration() {
            const configText = generateExportString();

            // Native ExecCommand / Clipboard Fallback
            const tempInput = document.createElement("textarea");
            tempInput.value = configText;
            document.body.appendChild(tempInput);
            tempInput.select();
            document.execCommand("copy");
            document.body.removeChild(tempInput);

            playSound('copy');
            showToast("ĐÃ SAO CHÉP", "Thông số cấu hình đã lưu vào bộ nhớ tạm!");
        }

        // Reset configuration to default
        function resetConfiguration() {
            playSound('click');
            SENS_ITEMS.forEach(item => {
                document.getElementById(`range-${item.id}`).value = item.default;
                document.getElementById(`num-${item.id}`).value = item.default;
            });
            document.getElementById('firebutton').value = 52;
            document.getElementById('val-firebutton').innerText = '52%';
            document.getElementById('dpi').value = 480;
            document.getElementById('val-dpi').innerText = '480 DPI';
            document.getElementById('drag-tech').selectedIndex = 0;
            document.getElementById('toggle-aimlock').checked = true;
            document.getElementById('toggle-antishake').checked = true;

            showToast("ĐÃ ĐẶT LẠI", "Cấu hình đã khôi phục về mặc định!");
            updateOutputText();
        }

        // Notification Toast Helper
        function showToast(title, message) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-title').innerText = title;
            document.getElementById('toast-msg').innerText = message;

            toast.classList.remove('translate-y-20', 'opacity-0');
            toast.classList.add('translate-y-0', 'opacity-100');

            setTimeout(() => {
                toast.classList.remove('translate-y-0', 'opacity-100');
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }

        // Background Cyber Particles Canvas Simulation
        function initCyberCanvas() {
            const canvas = document.getElementById('cyber-canvas');
            const ctx = canvas.getContext('2d');
            let width = canvas.width = window.innerWidth;
            let height = canvas.height = window.innerHeight;

            window.addEventListener('resize', () => {
                width = canvas.width = window.innerWidth;
                height = canvas.height = window.innerHeight;
            });

            const particles = [];
            const particleCount = Math.floor(width < 768 ? 40 : 80);

            for (let i = 0; i < particleCount; i++) {
                particles.push({
                    x: Math.random() * width,
                    y: Math.random() * height,
                    vx: (Math.random() - 0.5) * 0.8,
                    vy: (Math.random() - 0.5) * 0.8,
                    size: Math.random() * 2 + 1,
                    alpha: Math.random() * 0.5 + 0.2
                });
            }

            function render() {
                ctx.clearRect(0, 0, width, height);

                // Draw Cyber Grid Lines
                ctx.strokeStyle = 'rgba(255, 0, 60, 0.03)';
                ctx.lineWidth = 1;
                const gridSize = 40;
                for (let x = 0; x < width; x += gridSize) {
                    ctx.beginPath();
                    ctx.moveTo(x, 0);
                    ctx.lineTo(x, height);
                    ctx.stroke();
                }
                for (let y = 0; y < height; y += gridSize) {
                    ctx.beginPath();
                    ctx.moveTo(0, y);
                    ctx.lineTo(width, y);
                    ctx.stroke();
                }

                // Render & Connect Particles
                for (let i = 0; i < particles.length; i++) {
                    let p = particles[i];
                    p.x += p.vx;
                    p.y += p.vy;

                    if (p.x < 0) p.x = width;
                    if (p.x > width) p.x = 0;
                    if (p.y < 0) p.y = height;
                    if (p.y > height) p.y = 0;

                    ctx.fillStyle = `rgba(255, 0, 60, ${p.alpha})`;
                    ctx.beginPath();
                    ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
                    ctx.fill();

                    // Connect close particles with red cyber beam
                    for (let j = i + 1; j < particles.length; j++) {
                        let p2 = particles[j];
                        let dist = Math.hypot(p.x - p2.x, p.y - p2.y);
                        if (dist < 100) {
                            ctx.strokeStyle = `rgba(255, 0, 60, ${0.15 * (1 - dist / 100)})`;
                            ctx.beginPath();
                            ctx.moveTo(p.x, p.y);
                            ctx.lineTo(p2.x, p2.y);
                            ctx.stroke();
                        }
                    }
                }

                requestAnimationFrame(render);
            }

            render();
        }

        // On Page Load Init
        window.onload = function() {
            initSliders();
            updateOutputText();
            initCyberCanvas();
        };
    </script>
</body>
</html>
