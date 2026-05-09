<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>SwiftSend | Logística Inteligente</title>
    <!-- Leaflet CSS -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
    <!-- FontAwesome 6 -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,600;14..32,700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', sans-serif;
            background: #f0f2f8;
            color: #1e293b;
        }

        /* ========== SCROLL PERSONALIZADO ========== */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #e2e8f0;
        }
        ::-webkit-scrollbar-thumb {
            background: #f97316;
            border-radius: 10px;
        }

        /* ========== HEADER CORPORATIVO ========== */
        .corporate-header {
            background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
            color: white;
            padding: 0 5%;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        .nav-container {
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 0;
            flex-wrap: wrap;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .logo i {
            font-size: 32px;
            color: #f97316;
        }

        .logo h1 {
            font-size: 24px;
            font-weight: 700;
        }

        .logo span {
            color: #f97316;
        }

        .nav-links {
            display: flex;
            gap: 30px;
            align-items: center;
        }

        .nav-links a {
            color: #cbd5e1;
            text-decoration: none;
            font-weight: 500;
            transition: 0.3s;
        }

        .nav-links a:hover {
            color: #f97316;
        }

        .btn-outline {
            border: 2px solid #f97316;
            background: transparent;
            padding: 8px 20px;
            border-radius: 40px;
            color: #f97316;
            font-weight: 600;
            cursor: pointer;
            transition: 0.3s;
        }

        .btn-outline:hover {
            background: #f97316;
            color: white;
        }

        /* ========== HERO ========== */
        .hero {
            background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
            padding: 60px 5% 80px;
            text-align: center;
            color: white;
        }

        .hero h2 {
            font-size: 42px;
            margin-bottom: 20px;
        }

        .hero p {
            font-size: 18px;
            opacity: 0.9;
            max-width: 600px;
            margin: 0 auto;
        }

        /* ========== CONTENEDOR PRINCIPAL ========== */
        .main-container {
            max-width: 1400px;
            margin: -40px auto 40px;
            padding: 0 20px;
        }

        /* ========== TABS (Solo visibles después del login) ========== */
        .tabs {
            display: flex;
            gap: 10px;
            background: white;
            border-radius: 60px;
            padding: 8px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.05);
            margin-bottom: 30px;
        }

        .tab-btn {
            flex: 1;
            padding: 14px 24px;
            border: none;
            background: transparent;
            font-weight: 600;
            border-radius: 40px;
            cursor: pointer;
            transition: 0.3s;
            font-size: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .tab-btn.active {
            background: #f97316;
            color: white;
            box-shadow: 0 4px 12px rgba(249,115,22,0.3);
        }

        .tab-content {
            display: none;
            animation: fadeIn 0.4s ease;
        }

        .tab-content.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px);}
            to { opacity: 1; transform: translateY(0);}
        }

        /* ========== TARJETAS ========== */
        .card {
            background: white;
            border-radius: 24px;
            padding: 28px;
            margin-bottom: 30px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.05);
            border: 1px solid #eef2ff;
        }

        .card h3 {
            font-size: 20px;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
            color: #0f172a;
        }

        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }

        input, select {
            width: 100%;
            padding: 14px 16px;
            border: 1px solid #e2e8f0;
            border-radius: 16px;
            font-size: 14px;
            transition: 0.3s;
            font-family: 'Inter', sans-serif;
        }

        input:focus, select:focus {
            outline: none;
            border-color: #f97316;
            box-shadow: 0 0 0 3px rgba(249,115,22,0.1);
        }

        button {
            background: #f97316;
            color: white;
            border: none;
            padding: 14px 28px;
            border-radius: 40px;
            font-weight: 600;
            cursor: pointer;
            transition: 0.3s;
            font-size: 14px;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        button:hover {
            background: #ea580c;
            transform: translateY(-2px);
        }

        .btn-secondary {
            background: #334155;
        }

        .btn-secondary:hover {
            background: #1e293b;
        }

        /* Tabla */
        .table-wrapper {
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        th, td {
            padding: 16px 12px;
            text-align: left;
            border-bottom: 1px solid #eef2ff;
        }

        th {
            background: #f8fafc;
            font-weight: 600;
            color: #1e293b;
        }

        .badge {
            display: inline-block;
            padding: 6px 14px;
            border-radius: 40px;
            font-size: 12px;
            font-weight: 600;
        }

        .badge-bodega { background: #fef3c7; color: #d97706; }
        .badge-ruta { background: #dbeafe; color: #2563eb; }
        .badge-entregado { background: #dcfce7; color: #16a34a; }
        .badge-incidencia { background: #fee2e2; color: #dc2626; }

        /* Mapa */
        .map {
            height: 380px;
            border-radius: 20px;
            overflow: hidden;
            border: 1px solid #eef2ff;
        }

        /* Simulación de envío */
        .simulacion-envio {
            background: linear-gradient(135deg, #fef3c7, #ffedd5);
            border-radius: 20px;
            padding: 20px;
            margin-top: 20px;
            border-left: 5px solid #f97316;
        }

        .progress-bar {
            height: 8px;
            background: #e2e8f0;
            border-radius: 10px;
            overflow: hidden;
            margin: 15px 0;
        }

        .progress-fill {
            width: 0%;
            height: 100%;
            background: #f97316;
            transition: width 0.5s ease;
        }

        /* Login modal */
        .login-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 2000;
            backdrop-filter: blur(8px);
        }

        .login-card {
            background: white;
            padding: 40px;
            border-radius: 32px;
            width: 400px;
            text-align: center;
            box-shadow: 0 25px 50px rgba(0,0,0,0.3);
        }

        .login-card i {
            font-size: 60px;
            color: #f97316;
            margin-bottom: 20px;
        }

        /* Ocultar admin hasta login */
        .admin-only {
            display: none;
        }

        /* Footer */
        .footer {
            background: #0f172a;
            color: #94a3b8;
            text-align: center;
            padding: 30px;
            margin-top: 60px;
        }

        @media (max-width: 768px) {
            .nav-container {
                flex-direction: column;
                gap: 15px;
            }
            .hero h2 {
                font-size: 28px;
            }
            .tabs {
                flex-direction: column;
                border-radius: 20px;
            }
        }
    </style>
</head>
<body>

<!-- HEADER CORPORATIVO -->
<div class="corporate-header">
    <div class="nav-container">
        <div class="logo">
            <i class="fas fa-boxes"></i>
            <h1>Swift<span>Send</span></h1>
        </div>
        <div class="nav-links">
            <a href="#" id="btnInicio"><i class="fas fa-home"></i> Inicio</a>
            <a href="#" id="btnRastreoPublico"><i class="fas fa-search"></i> Rastrear</a>
            <button class="btn-outline" id="btnAbrirLogin"><i class="fas fa-user-shield"></i> Acceso Admin</button>
        </div>
    </div>
</div>

<section class="hero">
    <h2>Envíos rápidos, seguros y trazables</h2>
    <p>Gestión logística inteligente con seguimiento en tiempo real para tu negocio.</p>
</section>

<div class="main-container">
    <!-- PANEL PÚBLICO DE RASTREO (SIEMPRE VISIBLE) -->
    <div id="publicTracking" class="card">
        <h3><i class="fas fa-map-pin"></i> Rastrea tu envío</h3>
        <div style="display: flex; gap: 15px; flex-wrap: wrap; align-items: center;">
            <input type="number" id="publicGuia" placeholder="Número de guía" style="flex:1; min-width: 200px;">
            <button id="publicBuscarBtn"><i class="fas fa-search"></i> Buscar paquete</button>
        </div>
        <div id="publicResultado" style="margin-top: 25px; display: none;"></div>
        <div id="publicMap" class="map" style="margin-top: 20px;"></div>
    </div>

    <!-- SECCIÓN ADMIN (OCULTA HASTA LOGIN) -->
    <div id="adminSection" class="admin-only">
        <div class="tabs">
            <button class="tab-btn active" onclick="switchTab('gestion')"><i class="fas fa-box"></i> Gestionar Paquetes</button>
            <button class="tab-btn" onclick="switchTab('dashboard')"><i class="fas fa-map-marked-alt"></i> Flota en Vivo</button>
        </div>

        <!-- Gestión de paquetes -->
        <div id="tabGestion" class="tab-content active">
            <div class="card">
                <h3><i class="fas fa-plus-circle"></i> Nuevo envío</h3>
                <div class="form-grid">
                    <input type="text" id="remitente" placeholder="Remitente">
                    <input type="text" id="destinatario" placeholder="Destinatario">
                    <input type="text" id="dimensiones" placeholder="Dimensiones (ej: 30x20x10)">
                </div>
                <button id="registrarBtn"><i class="fas fa-save"></i> Registrar paquete</button>
            </div>

            <div class="card">
                <h3><i class="fas fa-list"></i> Todos los envíos</h3>
                <div class="table-wrapper">
                    <table id="tablaPaquetes">
                        <thead>
                            <tr><th>ID</th><th>Remitente</th><th>Destinatario</th><th>Estado</th><th>Acciones</th></tr>
                        </thead>
                        <tbody id="tbodyPaquetes"></tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- Dashboard mapa -->
        <div id="tabDashboard" class="tab-content">
            <div class="card">
                <h3><i class="fas fa-truck"></i> Ubicación de repartidores</h3>
                <div id="adminMap" class="map"></div>
                <div id="simulacionPanel" class="simulacion-envio" style="display: none;">
                    <i class="fas fa-sync-alt fa-spin"></i> <strong>Simulando envío en ruta...</strong>
                    <div class="progress-bar"><div class="progress-fill" id="progressFill"></div></div>
                    <p id="estadoSimulacion" style="font-size: 13px; margin-top: 10px;"></p>
                </div>
            </div>
        </div>

        <div class="card" style="display: flex; gap: 15px; justify-content: flex-end;">
            <button id="logoutBtn" class="btn-secondary"><i class="fas fa-sign-out-alt"></i> Cerrar sesión</button>
        </div>
    </div>
</div>

<div class="footer">
    <p>© 2026 SwiftSend - Tecnología en logística | Seguimiento inteligente 24/7</p>
</div>

<!-- MODAL LOGIN -->
<div id="loginModal" class="login-modal">
    <div class="login-card">
        <i class="fas fa-shield-alt"></i>
        <h2>Acceso Administrador</h2>
        <p style="color:#64748b; margin-bottom: 25px;">Ingresa tus credenciales</p>
        <input type="text" id="loginUser" placeholder="Usuario" style="margin-bottom: 15px;">
        <input type="password" id="loginPass" placeholder="Contraseña">
        <button id="loginSubmitBtn" style="margin-top: 25px; width: 100%;"><i class="fas fa-lock"></i> Ingresar</button>
        <p style="margin-top: 20px; font-size: 12px; color:#94a3b8;">Demo: admin / 1234</p>
    </div>
</div>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
<script>
    // ==================== DATOS GLOBALES ====================
    let paquetes = [];
    let mapaAdmin, mapaPublico;
    let marcadorAdmin = null;
    let intervaloSimulacion = null;

    // ==================== INICIALIZAR DATOS ====================
    function cargarDatos() {
        const data = localStorage.getItem('swiftsend_paquetes');
        if (data) {
            paquetes = JSON.parse(data);
        } else {
            paquetes = [
                { id: 1001, remitente: "Carlos López", destinatario: "Ana Martínez", dimensiones: "25x15x10", estado: "En bodega", fecha: "2026-04-18" },
                { id: 1002, remitente: "María García", destinatario: "Luis Rodríguez", dimensiones: "40x30x20", estado: "En ruta", fecha: "2026-04-18" },
                { id: 1003, remitente: "Pedro Sánchez", destinatario: "Sofía Fernández", dimensiones: "15x10x5", estado: "Entregado", fecha: "2026-04-17" }
            ];
            guardarDatos();
        }
        actualizarTablaAdmin();
    }

    function guardarDatos() {
        localStorage.setItem('swiftsend_paquetes', JSON.stringify(paquetes));
    }

    // ==================== COORDENADAS POR ESTADO ====================
    function coordenadasPorEstado(estado, id = null) {
        // Simulación de coordenadas que varían según el ID para hacer dinámico
        const base = {
            'En bodega': [4.7110, -74.0721],
            'En ruta': [4.6700 + (id ? (id % 5) * 0.01 : 0), -74.0500],
            'Entregado': [4.6500, -74.0300],
            'Incidencia': [4.7300, -74.0900]
        };
        return base[estado] || base['En bodega'];
    }

    // ==================== MAPAS ====================
    function initMapas() {
        if (mapaAdmin) return;
        mapaAdmin = L.map('adminMap').setView([4.7110, -74.0721], 12);
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', { attribution: '© OpenStreetMap' }).addTo(mapaAdmin);
        
        mapaPublico = L.map('publicMap').setView([4.7110, -74.0721], 12);
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', { attribution: '© OpenStreetMap' }).addTo(mapaPublico);
        
        actualizarMapaAdmin();
    }

    function actualizarMapaAdmin() {
        if (!mapaAdmin) return;
        if (marcadorAdmin) mapaAdmin.removeLayer(marcadorAdmin);
        let paqueteActivo = paquetes.find(p => p.estado === 'En ruta') || paquetes[paquetes.length-1];
        if (paqueteActivo) {
            let coords = coordenadasPorEstado(paqueteActivo.estado, paqueteActivo.id);
            marcadorAdmin = L.marker(coords).addTo(mapaAdmin)
                .bindPopup(`<b>Paquete #${paqueteActivo.id}</b><br>Estado: ${paqueteActivo.estado}<br>Dest: ${paqueteActivo.destinatario}`)
                .openPopup();
            mapaAdmin.setView(coords, 13);
        }
    }

    function actualizarMapaPublico(paquete) {
        if (!mapaPublico) return;
        if (window.marcadorPublico) mapaPublico.removeLayer(window.marcadorPublico);
        if (paquete) {
            let coords = coordenadasPorEstado(paquete.estado, paquete.id);
            window.marcadorPublico = L.marker(coords).addTo(mapaPublico)
                .bindPopup(`<b>Paquete #${paquete.id}</b><br>Estado: ${paquete.estado}`)
                .openPopup();
            mapaPublico.setView(coords, 14);
        }
    }

    // ==================== TABLA ADMIN ====================
    function actualizarTablaAdmin() {
        const tbody = document.getElementById('tbodyPaquetes');
        if (!tbody) return;
        tbody.innerHTML = '';
        paquetes.forEach(p => {
            let row = tbody.insertRow();
            row.insertCell(0).innerText = p.id;
            row.insertCell(1).innerText = p.remitente;
            row.insertCell(2).innerText = p.destinatario;
            let estadoClass = `badge-${p.estado.replace(/ /g, '-').toLowerCase()}`;
            row.insertCell(3).innerHTML = `<span class="badge ${estadoClass}">${p.estado}</span>`;
            let cellAccion = row.insertCell(4);
            let select = document.createElement('select');
            select.style.padding = "8px";
            select.style.borderRadius = "40px";
            select.style.border = "1px solid #ddd";
            ['En bodega', 'En ruta', 'Entregado', 'Incidencia'].forEach(est => {
                let opt = document.createElement('option');
                opt.value = est;
                opt.text = est;
                if (p.estado === est) opt.selected = true;
                select.appendChild(opt);
            });
            select.onchange = (function(paquete) {
                return function() { cambiarEstadoPaquete(paquete.id, this.value); };
            })(p);
            cellAccion.appendChild(select);
        });
    }

    // ==================== CAMBIAR ESTADO CON SIMULACIÓN ====================
    function cambiarEstadoPaquete(id, nuevoEstado) {
        let paquete = paquetes.find(p => p.id === id);
        if (!paquete) return;
        
        let estadoAnterior = paquete.estado;
        paquete.estado = nuevoEstado;
        guardarDatos();
        actualizarTablaAdmin();
        actualizarMapaAdmin();
        
        // SIMULACIÓN: Si el nuevo estado es "En ruta" Y no estaba en ruta antes
        if (nuevoEstado === 'En ruta' && estadoAnterior !== 'En ruta') {
            iniciarSimulacionEnvio(paquete);
        } else {
            detenerSimulacion();
        }
        
        // Si se pasa a entregado, detener simulación
        if (nuevoEstado === 'Entregado') {
            detenerSimulacion();
            alert(`✅ Paquete #${id} entregado con éxito.`);
        }
    }

    // ==================== SIMULACIÓN DE ENVÍO ====================
    let simulacionActiva = false;
    let progreso = 0;

    function iniciarSimulacionEnvio(paquete) {
        detenerSimulacion();
        simulacionActiva = true;
        progreso = 0;
        const panelSim = document.getElementById('simulacionPanel');
        const progressFill = document.getElementById('progressFill');
        const estadoSim = document.getElementById('estadoSimulacion');
        
        panelSim.style.display = 'block';
        progressFill.style.width = '0%';
        estadoSim.innerHTML = `🚚 Preparando envío del paquete #${paquete.id} para ${paquete.destinatario}...`;
        
        intervaloSimulacion = setInterval(() => {
            if (!simulacionActiva) return;
            progreso += 5;
            progressFill.style.width = progreso + '%';
            
            if (progreso < 30) {
                estadoSim.innerHTML = `📦 Paquete #${paquete.id} saliendo de bodega... (${progreso}%)`;
            } else if (progreso < 70) {
                estadoSim.innerHTML = `🚛 Paquete #${paquete.id} en tránsito - Conductor asignado (${progreso}%)`;
                // Simular movimiento en mapa cada cierto progreso
                let lat = 4.6700 + (progreso / 100) * 0.05;
                let lng = -74.0500 + (progreso / 100) * 0.02;
                if (marcadorAdmin) {
                    marcadorAdmin.setLatLng([lat, lng]);
                    mapaAdmin.setView([lat, lng], 13);
                }
            } else if (progreso < 95) {
                estadoSim.innerHTML = `📍 Paquete #${paquete.id} cerca de destino - Llegando (${progreso}%)`;
            } else if (progreso >= 100) {
                clearInterval(intervaloSimulacion);
                estadoSim.innerHTML = `✅ ¡Paquete #${paquete.id} entregado a ${paquete.destinatario}!`;
                progressFill.style.width = '100%';
                // Cambiar estado a entregado automáticamente al terminar simulación
                paquete.estado = 'Entregado';
                guardarDatos();
                actualizarTablaAdmin();
                actualizarMapaAdmin();
                setTimeout(() => {
                    panelSim.style.display = 'none';
                    simulacionActiva = false;
                    alert(`🎉 Simulación completada: Paquete #${paquete.id} ENTREGADO.`);
                }, 2000);
                simulacionActiva = false;
            }
        }, 300);
    }

    function detenerSimulacion() {
        if (intervaloSimulacion) {
            clearInterval(intervaloSimulacion);
            intervaloSimulacion = null;
        }
        simulacionActiva = false;
        const panel = document.getElementById('simulacionPanel');
        if (panel) panel.style.display = 'none';
    }

    // ==================== REGISTRAR PAQUETE ====================
    function registrarPaquete() {
        let rem = document.getElementById('remitente').value.trim();
        let dest = document.getElementById('destinatario').value.trim();
        let dim = document.getElementById('dimensiones').value.trim();
        if (!rem || !dest) { alert("Completa remitente y destinatario"); return; }
        let nuevoId = paquetes.length > 0 ? Math.max(...paquetes.map(p => p.id)) + 1 : 2000;
        paquetes.push({
            id: nuevoId,
            remitente: rem,
            destinatario: dest,
            dimensiones: dim || "No especificado",
            estado: "En bodega",
            fecha: new Date().toISOString().split('T')[0]
        });
        guardarDatos();
        actualizarTablaAdmin();
        document.getElementById('remitente').value = '';
        document.getElementById('destinatario').value = '';
        document.getElementById('dimensiones').value = '';
        alert(`✅ Paquete #${nuevoId} registrado`);
    }

    // ==================== RASTREO PÚBLICO ====================
    function rastrearPublico() {
        let guia = parseInt(document.getElementById('publicGuia').value);
        let resultadoDiv = document.getElementById('publicResultado');
        if (isNaN(guia)) {
            resultadoDiv.style.display = 'block';
            resultadoDiv.innerHTML = '<p style="color:red">❌ Ingresa un número válido</p>';
            return;
        }
        let paquete = paquetes.find(p => p.id === guia);
        if (!paquete) {
            resultadoDiv.style.display = 'block';
            resultadoDiv.innerHTML = '<p style="color:red">❌ Número de guía no encontrado</p>';
            actualizarMapaPublico(null);
            return;
        }
        let estadoClass = `badge-${paquete.estado.replace(/ /g, '-').toLowerCase()}`;
        resultadoDiv.style.display = 'block';
        resultadoDiv.innerHTML = `
            <div style="background:#f8fafc; padding:20px; border-radius:20px;">
                <p><strong><i class="fas fa-hashtag"></i> Guía:</strong> ${paquete.id}</p>
                <p><strong><i class="fas fa-user"></i> Remitente:</strong> ${paquete.remitente}</p>
                <p><strong><i class="fas fa-user-check"></i> Destinatario:</strong> ${paquete.destinatario}</p>
                <p><strong><i class="fas fa-tag"></i> Estado:</strong> <span class="badge ${estadoClass}">${paquete.estado}</span></p>
            </div>
        `;
        actualizarMapaPublico(paquete);
    }

    // ==================== LOGIN ====================
    function verificarLogin() {
        let user = document.getElementById('loginUser').value;
        let pass = document.getElementById('loginPass').value;
        if (user === 'admin' && pass === '1234') {
            localStorage.setItem('swiftsend_admin_auth', 'true');
            document.getElementById('loginModal').style.display = 'none';
            document.getElementById('adminSection').style.display = 'block';
            initMapas();
            cargarDatos();
        } else {
            alert('Credenciales incorrectas');
        }
    }

    function checkSession() {
        if (localStorage.getItem('swiftsend_admin_auth') === 'true') {
            document.getElementById('adminSection').style.display = 'block';
            initMapas();
            cargarDatos();
        } else {
            document.getElementById('adminSection').style.display = 'none';
        }
    }

    function logout() {
        localStorage.removeItem('swiftsend_admin_auth');
        document.getElementById('adminSection').style.display = 'none';
        alert('Sesión cerrada');
        location.reload();
    }

    // ==================== SWITCH TABS ====================
    function switchTab(tab) {
        document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
        if (tab === 'gestion') {
            document.getElementById('tabGestion').classList.add('active');
        } else {
            document.getElementById('tabDashboard').classList.add('active');
            setTimeout(() => { if(mapaAdmin) mapaAdmin.invalidateSize(); }, 100);
        }
        document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
        if (tab === 'gestion') document.querySelector('.tab-btn').classList.add('active');
        else document.querySelectorAll('.tab-btn')[1].classList.add('active');
    }

    // ==================== EVENTOS ====================
    window.onload = () => {
        checkSession();
        cargarDatos();
        initMapas();
        
        document.getElementById('registrarBtn')?.addEventListener('click', registrarPaquete);
        document.getElementById('publicBuscarBtn')?.addEventListener('click', rastrearPublico);
        document.getElementById('loginSubmitBtn')?.addEventListener('click', verificarLogin);
        document.getElementById('logoutBtn')?.addEventListener('click', logout);
        document.getElementById('btnAbrirLogin')?.addEventListener('click', () => {
            document.getElementById('loginModal').style.display = 'flex';
        });
        document.getElementById('btnRastreoPublico')?.addEventListener('click', (e) => {
            e.preventDefault();
            document.getElementById('publicTracking').scrollIntoView({ behavior: 'smooth' });
        });
        document.getElementById('btnInicio')?.addEventListener('click', (e) => {
            e.preventDefault();
            window.scrollTo({ top: 0, behavior: 'smooth' });
        });
    };
</script>
</body>
</html>
