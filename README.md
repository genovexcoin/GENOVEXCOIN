<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GENOVEX | Professional Web3 Explorer</title>
    
    <!-- External Libraries -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=JetBrains+Mono&display=swap" rel="stylesheet">

    <style>
        :root {
            --primary: #f97316;
            --primary-dark: #ea580c;
            --bg: #050508;
            --card: rgba(15, 15, 25, 0.8);
            --border: rgba(249, 115, 22, 0.2);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Plus Jakarta Sans', sans-serif;
            cursor: default;
        }

        body {
            background-color: var(--bg);
            color: white;
            overflow-x: hidden;
            min-height: 100vh;
        }

        /* Osiris Particle Engine Background */
        #osiris-bg {
            position: fixed;
            top: 0;
            left: 0;
            z-index: -1;
            width: 100%;
            height: 100%;
        }

        .glass {
            background: var(--card);
            backdrop-filter: blur(15px);
            border: 1px solid var(--border);
            border-radius: 20px;
            transition: all 0.3s ease;
        }

        .glass:hover {
            border-color: var(--primary);
            box-shadow: 0 0 20px rgba(249, 115, 22, 0.1);
        }

        .nav-link {
            transition: all 0.3s ease;
            position: relative;
            color: #a0a0a0;
            cursor: pointer;
        }

        .nav-link:hover, .nav-link.active {
            color: var(--primary);
        }

        .btn-primary {
            background: var(--primary);
            color: black;
            font-weight: 800;
            padding: 10px 24px;
            border-radius: 12px;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            cursor: pointer;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 0 25px rgba(249, 115, 22, 0.5);
        }

        section {
            display: none;
            animation: slideUp 0.6s cubic-bezier(0.23, 1, 0.32, 1) forwards;
        }

        section.active {
            display: block;
        }

        @keyframes slideUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .mono { font-family: 'JetBrains Mono', monospace; }

        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: #050508; }
        ::-webkit-scrollbar-thumb { background: #333; border-radius: 10px; }
        ::-webkit-scrollbar-thumb:hover { background: var(--primary); }

        .brand-text {
            background: linear-gradient(to right, #ffffff, #f97316);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            font-weight: 800;
            letter-spacing: -1px;
        }
    </style>
</head>
<body>

    <!-- Three.js Background -->
    <canvas id="osiris-bg"></canvas>

    <!-- Navigation -->
    <nav class="fixed top-0 w-full z-50 px-6 py-6">
        <div class="max-w-7xl mx-auto glass px-8 py-4 flex justify-between items-center">
            <div class="flex items-center gap-4 cursor-pointer" onclick="showSection('home')">
                <div class="w-10 h-10 bg-orange-500 rounded-lg flex items-center justify-center shadow-lg shadow-orange-500/20">
                    <i class="fa-solid fa-bolt-lightning text-black text-xl"></i>
                </div>
                <span class="text-3xl brand-text">GENOVEX</span>
            </div>
            
            <div class="hidden md:flex gap-10 font-bold text-xs uppercase tracking-widest">
                <a onclick="showSection('home')" class="nav-link active" id="btn-home">Home</a>
                <a onclick="showSection('dashboard')" class="nav-link" id="btn-dashboard">Dashboard</a>
                <a onclick="showSection('explorer')" class="nav-link" id="btn-explorer">Osiris Map</a>
            </div>

            <div class="flex gap-4 items-center">
                <button onclick="connectWallet()" id="wallet-status" class="btn-primary text-[10px] tracking-tighter">
                    <i class="fa-solid fa-wallet"></i> CONNECT WALLET
                </button>
            </div>
        </div>
    </nav>

    <!-- MAIN APP CONTENT -->
    <main class="pt-32 pb-20 px-6 max-w-7xl mx-auto relative z-10">

        <!-- SECTION: HOME -->
        <section id="home" class="active">
            <div class="grid lg:grid-cols-2 gap-16 items-center min-h-[60vh]">
                <div>
                    <div class="inline-block px-4 py-1 border border-orange-500/30 rounded-full mb-6 bg-orange-500/10">
                        <p class="text-orange-500 text-[10px] font-bold tracking-widest uppercase">NovaChain protocols active</p>
                    </div>
                    <h1 class="text-6xl md:text-8xl font-extrabold leading-[0.9] mb-8">
                        NAVIGATE THE <br><span class="text-orange-500">DIGITAL PULSE</span>
                    </h1>
                    <p class="text-gray-400 text-lg mb-10 max-w-lg leading-relaxed">
                        GENOVEX is the next-generation explorer for the NovaChain ecosystem. Real-time data visualization through the Osiris 3D Engine.
                    </p>
                    
                    <div class="flex flex-wrap gap-6 mb-12">
                        <button onclick="showSection('dashboard')" class="btn-primary px-10 py-5">
                            ENTER TERMINAL <i class="fa-solid fa-arrow-right"></i>
                        </button>
                        <a href="https://t.me/GENOVEXCOIN" target="_blank" class="glass px-10 py-5 font-bold flex items-center gap-3 hover:bg-white/5">
                            <i class="fa-brands fa-telegram text-xl"></i> COMMUNITY
                        </a>
                    </div>

                    <div class="glass p-6 border-orange-500/20">
                        <div class="flex items-center justify-between mb-4">
                            <p class="text-[10px] text-gray-500 font-bold uppercase tracking-widest">Live Token Link</p>
                            <span class="w-2 h-2 rounded-full bg-green-500 animate-pulse"></span>
                        </div>
                        <a href="https://pump.fun/coin/EdyKUwxsR8MXwonFemDEuwSPxpjMMLtvoJNNRcubpump" target="_blank" class="mono text-orange-500 text-sm break-all font-bold hover:underline">
                            pump.fun/coin/EdyKUwxsR8MXwonFem...cubpump
                        </a>
                    </div>
                </div>

                <div class="relative hidden lg:block">
                    <div class="absolute -inset-20 bg-orange-500/10 rounded-full blur-[120px]"></div>
                    <div class="glass aspect-square flex items-center justify-center p-12 relative overflow-hidden">
                        <div class="absolute inset-0 bg-gradient-to-tr from-orange-500/10 to-transparent"></div>
                        <i class="fa-solid fa-cube text-[250px] text-orange-500/20"></i>
                        <div class="absolute flex flex-col items-center">
                            <div class="text-center">
                                <h3 class="text-5xl font-black mb-2 tracking-tighter">NVC</h3>
                                <p class="mono text-orange-500 text-xs animate-pulse tracking-widest">OSIRIS CORE ACTIVE</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- SECTION: DASHBOARD -->
        <section id="dashboard">
            <div class="flex flex-col md:flex-row justify-between items-end gap-6 mb-10">
                <div>
                    <h2 class="text-4xl font-extrabold mb-2 uppercase tracking-tighter">Market <span class="text-orange-500">Analytics</span></h2>
                    <p class="text-gray-500 mono text-xs">Contract: EdyKUwxsR8MXwonFemDEuwSPxpjMMLtvoJNNRcubpump</p>
                </div>
                <div class="flex gap-4">
                    <div class="glass px-6 py-3 text-center">
                        <p class="text-[10px] text-gray-500 font-bold uppercase mb-1">NVC Price</p>
                        <p class="text-xl font-bold text-orange-500">$1.42</p>
                    </div>
                    <div class="glass px-6 py-3 text-center">
                        <p class="text-[10px] text-gray-500 font-bold uppercase mb-1">24h Vol</p>
                        <p class="text-xl font-bold">$642.8K</p>
                    </div>
                </div>
            </div>

            <div class="grid lg:grid-cols-3 gap-8">
                <!-- Trading Chart -->
                <div class="lg:col-span-2 glass p-8 h-[500px] flex flex-col">
                    <div class="flex justify-between items-center mb-8">
                        <h3 class="font-bold flex items-center gap-2">
                            <i class="fa-solid fa-chart-area text-orange-500"></i> NVC / SOL PRICE PERFORMANCE
                        </h3>
                        <div class="flex gap-2">
                            <span class="px-3 py-1 bg-orange-500 text-black rounded text-[10px] font-bold">LIVE</span>
                        </div>
                    </div>
                    <div class="flex-grow relative">
                        <canvas id="nvc-chart"></canvas>
                    </div>
                </div>

                <!-- Wallet Panel -->
                <div class="space-y-8">
                    <div class="glass p-8 border-orange-500/40 bg-gradient-to-b from-orange-500/5 to-transparent">
                        <h3 class="text-sm font-bold mb-6 uppercase tracking-widest text-gray-400">Assets Portfolio</h3>
                        <div class="space-y-6">
                            <div>
                                <p class="text-[10px] text-gray-500 font-bold mb-1">STAKED BALANCE</p>
                                <div class="flex justify-between items-end">
                                    <h4 class="text-4xl font-extrabold" id="bal-nvc">0.00</h4>
                                    <p class="text-orange-500 font-bold pb-1">NVC</p>
                                </div>
                            </div>
                            <div class="pt-6 border-t border-white/5">
                                <p class="text-[10px] text-gray-500 font-bold mb-1">ESTIMATED VALUE</p>
                                <h4 class="text-2xl font-bold text-gray-300" id="bal-usd">$0.00 USD</h4>
                            </div>
                        </div>
                        <button onclick="connectWallet()" class="w-full mt-8 btn-primary justify-center py-4">MANAGE ASSETS</button>
                    </div>

                    <div class="glass p-8">
                        <h3 class="text-sm font-bold mb-6 uppercase tracking-widest text-gray-400">Recent Blocks</h3>
                        <div class="space-y-4" id="block-list">
                            <!-- Injected by JS -->
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- SECTION: EXPLORER -->
        <section id="explorer">
            <div class="mb-10 text-center">
                <h2 class="text-4xl font-extrabold mb-2 uppercase">Osiris <span class="text-orange-500">Map</span></h2>
                <p class="text-gray-400 max-w-xl mx-auto">Visualizing NovaChain node density and validator health across the global mesh network.</p>
            </div>
            
            <div class="w-full h-[600px] glass overflow-hidden relative" id="map-container">
                <div class="absolute inset-0 bg-gradient-to-b from-transparent to-black/60 pointer-events-none"></div>
                <!-- Node Stats -->
                <div class="absolute top-8 left-8 z-10 glass p-6 max-w-[280px]">
                    <h4 class="font-bold text-orange-500 mb-4 uppercase text-xs tracking-widest">Network Telemetry</h4>
                    <div class="space-y-4">
                        <div class="flex justify-between items-center">
                            <span class="text-[10px] text-gray-500 font-bold uppercase">Validators</span>
                            <span class="mono text-sm">1,204</span>
                        </div>
                        <div class="flex justify-between items-center">
                            <span class="text-[10px] text-gray-500 font-bold uppercase">Net Load</span>
                            <span class="mono text-sm text-green-500">Normal</span>
                        </div>
                        <div class="flex justify-between items-center">
                            <span class="text-[10px] text-gray-500 font-bold uppercase">TPS Avg</span>
                            <span class="mono text-sm">4,821</span>
                        </div>
                    </div>
                    <hr class="my-4 border-white/5">
                    <button class="w-full py-2 bg-white/5 hover:bg-white/10 rounded font-bold text-[10px] transition cursor-pointer">PING GLOBAL NODES</button>
                </div>

                <div class="absolute bottom-8 right-8 z-10">
                    <div class="glass p-4 px-6 flex items-center gap-6">
                        <div class="flex items-center gap-2">
                            <div class="w-2 h-2 bg-green-500 rounded-full"></div>
                            <span class="text-[10px] font-bold text-gray-400 uppercase">System Optimal</span>
                        </div>
                        <div class="flex items-center gap-2">
                            <div class="w-2 h-2 bg-orange-500 rounded-full"></div>
                            <span class="text-[10px] font-bold text-gray-400 uppercase">V1.0.4 Osiris</span>
                        </div>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- FOOTER COMMUNITY -->
    <footer class="fixed bottom-0 w-full px-6 py-6 z-50 pointer-events-none">
        <div class="max-w-7xl mx-auto flex justify-between items-center pointer-events-auto">
            <div class="glass px-6 py-3 flex gap-8 text-orange-500">
                <a href="https://t.me/GENOVEXCOIN" target="_blank" class="hover:scale-125 transition-transform"><i class="fa-brands fa-telegram"></i></a>
                <a href="https://pump.fun/coin/EdyKUwxsR8MXwonFemDEuwSPxpjMMLtvoJNNRcubpump" target="_blank" class="hover:scale-125 transition-transform"><i class="fa-solid fa-rocket"></i></a>
                <a href="#" class="hover:scale-125 transition-transform"><i class="fa-brands fa-x-twitter"></i></a>
            </div>
            <div class="glass px-6 py-3 text-[10px] font-black text-gray-500 tracking-[0.4em] uppercase">
                Term v1.0 • NovaChain Secured
            </div>
        </div>
    </footer>

    <!-- APP SCRIPTS -->
    <script>
        // 1. SPA Navigation Logic
        function showSection(id) {
            document.querySelectorAll('section').forEach(s => s.classList.remove('active'));
            document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
            
            document.getElementById(id).classList.add('active');
            document.getElementById('btn-' + id).classList.add('active');
            
            if(id === 'dashboard') loadChart();
            if(id === 'explorer') loadExplorer();
        }

        // 2. Osiris Particle Background (Three.js)
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ canvas: document.getElementById('osiris-bg'), antialias: true, alpha: true });
        
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(window.devicePixelRatio);

        const particlesGeometry = new THREE.BufferGeometry();
        const posArray = new Float32Array(2000 * 3);

        for(let i=0; i < 2000 * 3; i++) {
            posArray[i] = (Math.random() - 0.5) * 100;
        }

        particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));
        const particlesMaterial = new THREE.PointsMaterial({
            size: 0.05,
            color: '#f97316',
            transparent: true,
            opacity: 0.4,
            blending: THREE.AdditiveBlending
        });

        const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
        scene.add(particlesMesh);

        camera.position.z = 30;

        function animateBg() {
            requestAnimationFrame(animateBg);
            particlesMesh.rotation.y += 0.0008;
            particlesMesh.rotation.x += 0.0003;
            renderer.render(scene, camera);
        }
        animateBg();

        // 3. Simulated Wallet Connection
        let connected = false;
        function connectWallet() {
            const btn = document.getElementById('wallet-status');
            if(!connected) {
                const addr = "0x" + Math.random().toString(16).slice(2, 10).toUpperCase() + "...pump";
                document.getElementById('bal-nvc').innerText = "12,500.00";
                document.getElementById('bal-usd').innerText = "$17,750.00 USD";
                btn.innerHTML = `<i class="fa-solid fa-circle-check"></i> 0x${addr.slice(2,6)}...`;
                btn.style.background = "#22c55e";
                connected = true;
            }
        }

        // 4. Performance Chart (Chart.js)
        let chart;
        function loadChart() {
            const ctx = document.getElementById('nvc-chart').getContext('2d');
            if(chart) chart.destroy();
            
            const gradient = ctx.createLinearGradient(0, 0, 0, 400);
            gradient.addColorStop(0, 'rgba(249, 115, 22, 0.4)');
            gradient.addColorStop(1, 'rgba(249, 115, 22, 0)');

            chart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['12 AM', '04 AM', '08 AM', '12 PM', '04 PM', '08 PM', 'Now'],
                    datasets: [{
                        label: 'NVC Price',
                        data: [0.85, 0.92, 0.88, 1.15, 1.25, 1.40, 1.42],
                        borderColor: '#f97316',
                        borderWidth: 4,
                        fill: true,
                        backgroundColor: gradient,
                        tension: 0.4,
                        pointRadius: 0
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } },
                    scales: {
                        y: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: '#666', font: { family: 'JetBrains Mono' } } },
                        x: { grid: { display: false }, ticks: { color: '#666', font: { family: 'JetBrains Mono' } } }
                    }
                }
            });
        }

        // 5. Explorer 3D Map (Mini Renderer)
        function loadExplorer() {
            const container = document.getElementById('map-container');
            if(container.querySelector('canvas')) return;

            const mapRenderer = new THREE.WebGLRenderer({ antialias: true });
            mapRenderer.setSize(container.offsetWidth, container.offsetHeight);
            container.appendChild(mapRenderer.domElement);

            const mapScene = new THREE.Scene();
            const mapCamera = new THREE.PerspectiveCamera(75, container.offsetWidth / container.offsetHeight, 0.1, 1000);
            mapCamera.position.z = 25;

            const group = new THREE.Group();
            
            // Sphere mesh
            const geo = new THREE.SphereGeometry(12, 40, 40);
            const mat = new THREE.MeshBasicMaterial({ color: '#f97316', wireframe: true, transparent: true, opacity: 0.1 });
            const sphere = new THREE.Mesh(geo, mat);
            group.add(sphere);

            // Nodos
            for(let i=0; i<60; i++) {
                const nodeGeo = new THREE.SphereGeometry(0.2, 10, 10);
                const nodeMat = new THREE.MeshBasicMaterial({ color: '#f97316' });
                const node = new THREE.Mesh(nodeGeo, nodeMat);
                
                const phi = Math.acos(-1 + (2 * i) / 60);
                const theta = Math.sqrt(60 * Math.PI) * phi;
                
                node.position.set(
                    12 * Math.cos(theta) * Math.sin(phi),
                    12 * Math.sin(theta) * Math.sin(phi),
                    12 * Math.cos(phi)
                );
                group.add(node);
            }

            mapScene.add(group);

            function animateMap() {
                requestAnimationFrame(animateMap);
                group.rotation.y += 0.003;
                mapRenderer.render(mapScene, mapCamera);
            }
            animateMap();
        }

        // 6. Block Injections
        function updateBlocks() {
            const list = document.getElementById('block-list');
            const blocks = [
                { id: '842,912', time: '12s ago', status: 'Finalized' },
                { id: '842,911', time: '24s ago', status: 'Finalized' },
                { id: '842,910', time: '36s ago', status: 'Finalized' }
            ];
            list.innerHTML = blocks.map(b => `
                <div class="flex justify-between items-center p-3 border border-white/5 rounded-lg bg-white/5">
                    <div>
                        <p class="mono text-[10px] text-orange-500 font-bold">#${b.id}</p>
                        <p class="text-[8px] text-gray-500 uppercase">${b.time}</p>
                    </div>
                    <span class="text-[8px] font-bold bg-green-500/10 text-green-500 px-2 py-1 rounded uppercase tracking-tighter">${b.status}</span>
                </div>
            `).join('');
        }
        updateBlocks();

        // Mouse interaction for background
        window.addEventListener('mousemove', (e) => {
            const x = (e.clientX / window.innerWidth) - 0.5;
            const y = (e.clientY / window.innerHeight) - 0.5;
            particlesMesh.rotation.y = x * 0.1;
            particlesMesh.rotation.x = y * 0.1;
        });

        // Resize handler
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });

    </script>
</body>
</html>
