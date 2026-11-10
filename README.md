# SNCLO-SHOPPING-<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HomeNest - Luxury Real Estate Platform</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif; }
        body { background-color: #080808; color: #f5f5f5; overflow: hidden; height: 100vh; display: flex; flex-direction: column; }
        
        /* Yuqori Header paneli */
        header { height: 75px; background: rgba(12, 12, 12, 0.98); border-bottom: 1px solid #222; display: flex; align-items: center; justify-content: space-between; padding: 0 35px; z-index: 10; }
        .logo { font-size: 24px; font-weight: 700; color: #d4af37; letter-spacing: 3px; }
        .nav-tabs { display: flex; gap: 15px; }
        .tab-btn { background: #161616; border: 1px solid #333; color: #aaa; padding: 9px 20px; border-radius: 6px; cursor: pointer; transition: 0.3s; font-size: 14px; }
        .tab-btn.active, .tab-btn:hover { background: #d4af37; color: #000; border-color: #d4af37; font-weight: 600; }
        .actions { display: flex; gap: 12px; }
        .action-btn { background: transparent; border: 1px solid #d4af37; color: #d4af37; padding: 9px 18px; border-radius: 6px; cursor: pointer; transition: 0.3s; font-size: 13px; font-weight: 600; }
        .action-btn:hover { background: #d4af37; color: #000; }

        /* Asosiy ishchi maydon */
        .workspace { flex: 1; display: flex; position: relative; }
        #canvas-container { flex: 1; height: 100%; background: radial-gradient(circle, #181818 0%, #050505 100%); position: relative; }

        /* O'ng tomon ma'lumotlar paneli */
        .sidebar { width: 400px; background: rgba(15, 15, 15, 0.98); border-left: 1px solid #222; padding: 30px; display: flex; flex-direction: column; gap: 20px; z-index: 10; box-shadow: -5px 0 25px rgba(0,0,0,0.5); }
        .sidebar h2 { color: #d4af37; font-size: 24px; font-weight: 600; }
        .price { font-size: 32px; font-weight: 700; color: #fff; margin-bottom: 5px; }
        .specs { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 10px; }
        .spec-card { background: #121212; border: 1px solid #262626; padding: 14px; border-radius: 8px; text-align: center; }
        .spec-card span { display: block; font-size: 12px; color: #888; margin-bottom: 4px; }
        .spec-card strong { font-size: 16px; color: #fff; }
        
        .section-title { font-size: 12px; color: #aaa; text-transform: uppercase; letter-spacing: 1.5px; margin-bottom: 4px; }
        .color-options { display: flex; gap: 14px; }
        .color-btn { width: 36px; height: 36px; border-radius: 50%; border: 2px solid #444; cursor: pointer; transition: 0.2s; }
        .color-btn:hover { transform: scale(1.1); border-color: #d4af37; }
        .material-options { display: flex; gap: 10px; }
        .mat-btn { background: #1a1a1a; border: 1px solid #333; color: #fff; padding: 10px; border-radius: 6px; font-size: 13px; cursor: pointer; flex: 1; transition: 0.3s; }
        .mat-btn:hover { border-color: #d4af37; color: #d4af37; background: #222; }

        .book-btn { margin-top: auto; background: #d4af37; color: #000; border: none; padding: 16px; border-radius: 8px; font-weight: 700; font-size: 15px; cursor: pointer; transition: 0.3s; text-transform: uppercase; letter-spacing: 1.5px; }
        .book-btn:hover { background: #e6c555; box-shadow: 0 0 20px rgba(212, 175, 55, 0.4); }

        .controls-hint { position: absolute; bottom: 25px; left: 25px; background: rgba(0,0,0,0.8); padding: 12px 20px; border-radius: 25px; border: 1px solid #333; font-size: 13px; color: #bbb; pointer-events: none; backdrop-filter: blur(5px); }
    </style>
</head>
<body>

    <header>
        <div class="logo">HOMENEST</div>
        <div class="nav-tabs">
            <button class="tab-btn active" onclick="switchLevel('residence', this)">The Residence</button>
            <button class="tab-btn" onclick="switchLevel('penthouse', this)">The Penthouse</button>
            <button class="tab-btn" onclick="switchLevel('sky', this)">The Sky Club</button>
        </div>
        <div class="actions">
            <button class="action-btn" onclick="toggleLighting()">☀️ / 🌙 Kun / Tun</button>
            <button class="action-btn" onclick="openCalculator()">📊 Kalkulyator</button>
        </div>
    </header>

    <div class="workspace">
        <div id="canvas-container">
            <div class="controls-hint">💡 360° aylantirish uchun sichqoncha yoki barmoqdan foydalaning</div>
        </div>
        
        <div class="sidebar">
            <h2 id="res-title">Maison Aurelle Villa</h2>
            <div class="price" id="res-price">$2,450,000</div>
            
            <div class="specs">
                <div class="spec-card"><span>Maydoni</span><strong id="res-area">340 m²</strong></div>
                <div class="spec-card"><span>Xonalar</span><strong id="res-rooms">4 xona</strong></div>
            </div>

            <div>
                <div class="section-title">Mebel Rangi (Customizer)</div>
                <div class="color-options">
                    <div class="color-btn" style="background: #d4af37;" onclick="changeColor('#d4af37')" title="Oltin"></div>
                    <div class="color-btn" style="background: #222222;" onclick="changeColor('#222222')" title="Qora"></div>
                    <div class="color-btn" style="background: #2e5a44;" onclick="changeColor('#2e5a44')" title="Yashil"></div>
                    <div class="color-btn" style="background: #8b0000;" onclick="changeColor('#8b0000')" title="Qizil"></div>
                </div>
            </div>

            <div>
                <div class="section-title">Pol Qoplamasi</div>
                <div class="material-options">
                    <button class="mat-btn" onclick="changeFloor('wood')">Yog'och</button>
                    <button class="mat-btn" onclick="changeFloor('marble')">Marmar</button>
                    <button class="mat-btn" onclick="changeFloor('concrete')">Beton</button>
                </div>
            </div>

            <button class="book-btn" onclick="alert('Muvaffaqiyatli! Konsultatsiya zayavkasi qabul qilindi.')">Eksklyuziv Band Qilish</button>
        </div>
    </div>

    <!-- Three.js va TWEEN kutubxonalari -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/controls/OrbitControls.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/tween.js/18.6.4/tween.umd.js"></script>
    
    <script>
        let scene, camera, renderer, controls, houseGroup, sofaMat, floorMesh;
        let isNight = false;

        function init() {
            const container = document.getElementById('canvas-container');
            
            scene = new THREE.Scene();
            scene.background = new THREE.Color(0x080808);

            camera = new THREE.PerspectiveCamera(45, container.clientWidth / container.clientHeight, 0.1, 1000);
            camera.position.set(15, 12, 18);

            renderer = new THREE.WebGLRenderer({ antialias: true });
            renderer.setSize(container.clientWidth, container.clientHeight);
            renderer.shadowMap.enabled = true;
            container.appendChild(renderer.domElement);

            controls = new THREE.OrbitControls(camera, renderer.domElement);
            controls.enableDamping = true;
            controls.dampingFactor = 0.05;

            // Yoritish tizimi
            const ambientLight = new THREE.AmbientLight(0xffffff, 0.8);
            scene.add(ambientLight);

            const dirLight = new THREE.DirectionalLight(0xffeedd, 1.3);
            dirLight.position.set(20, 30, 20);
            dirLight.castShadow = true;
            scene.add(dirLight);

            // Bino 3D Gruppasi
            houseGroup = new THREE.Group();

            // Asosiy qavat / Pol
            const floorGeo = new THREE.BoxGeometry(10, 0.4, 8);
            const floorMatGeo = new THREE.MeshStandardMaterial({ color: 0x444444, roughness: 0.4 });
            floorMesh = new THREE.Mesh(floorGeo, floorMatGeo);
            houseGroup.add(floorMesh);

            // Devorlar
            const wallMat = new THREE.MeshStandardMaterial({ color: 0xf2f2f2, roughness: 0.2 });
            
            const wallBack = new THREE.Mesh(new THREE.BoxGeometry(9.6, 2.5, 0.3), wallMat);
            wallBack.position.set(0, 1.25, -3.85);
            houseGroup.add(wallBack);

            const wallLeft = new THREE.Mesh(new THREE.BoxGeometry(0.3, 2.5, 7.7), wallMat);
            wallLeft.position.set(-4.85, 1.25, 0);
            houseGroup.add(wallLeft);

            // Mehmonxona divani
            const sofaGeo = new THREE.BoxGeometry(3.5, 0.7, 1.5);
            sofaMat = new THREE.MeshStandardMaterial({ color: 0xd4af37, roughness: 0.3 });
            const sofa = new THREE.Mesh(sofaGeo, sofaMat);
            sofa.position.set(-1.8, 0.55, 1);
            houseGroup.add(sofa);

            // Kofe stoli
            const tableGeo = new THREE.BoxGeometry(1.8, 0.4, 1.0);
            const tableMat = new THREE.MeshStandardMaterial({ color: 0x111111, roughness: 0.1 });
            const table = new THREE.Mesh(tableGeo, tableMat);
            table.position.set(-1.8, 0.4, -0.8);
            houseGroup.add(table);

            scene.add(houseGroup);

            window.addEventListener('resize', onWindowResize);
            animate();
        }

        function animate(time) {
            requestAnimationFrame(animate);
            TWEEN.update(time);
            controls.update();
            renderer.render(scene, camera);
        }

        function onWindowResize() {
            const container = document.getElementById('canvas-container');
            camera.aspect = container.clientWidth / container.clientHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(container.clientWidth, container.clientHeight);
        }

        function switchLevel(level, btnElement) {
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
            btnElement.classList.add('active');

            let targetY = 0;
            let title = "Maison Aurelle Villa";
            let price = "$2,450,000";
            let area = "340 m²";
            let rooms = "4 xona";

            if(level === 'penthouse') {
                targetY = 4;
                title = "The Penthouse Residence";
                price = "$4,800,000";
                area = "520 m²";
                rooms = "6 xona + Terassa";
            } else if(level === 'sky') {
                targetY = 8;
                title = "The Sky Club & Rooftop";
                price = "$7,200,000";
                area = "680 m²";
                rooms = "VIP Lounge & Pool";
            }

            document.getElementById('res-title').innerText = title;
            document.getElementById('res-price').innerText = price;
            document.getElementById('res-area').innerText = area;
            document.getElementById('res-rooms').innerText = rooms;

            new TWEEN.Tween(houseGroup.position)
                .to({ y: targetY }, 1200)
                .easing(TWEEN.Easing.Cubic.Out)
                .start();
        }

        function changeColor(hex) {
            if(sofaMat) sofaMat.color.set(hex);
        }

        function changeFloor(type) {
            if(!floorMesh) return;
            if(type === 'wood') floorMesh.material.color.set(0x8b5a2b);
            if(type === 'marble') floorMesh.material.color.set(0xe8e8e8);
            if(type === 'concrete') floorMesh.material.color.set(0x555555);
        }

        function toggleLighting() {
            isNight = !isNight;
            scene.background = new THREE.Color(isNight ? 0x020205 : 0x080808);
        }

        function openCalculator() {
            let percent = prompt("Boshlang'ich to'lov foizini kiriting (masalan: 30%):", "30");
            if(percent) {
                alert("Tanlangan rezidensiya bo'yicha taxminiy oylik ipoteka to'lovi: $18,500 / oy (20 yilga).");
            }
        }

        window.onload = init;
    </script>
</body>
</html>
