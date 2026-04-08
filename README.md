<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>NovaTech Nexus | 3D Analytics Portal</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,600;14..32,700;14..32,800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }

        body {
            min-height: 100vh;
            background: radial-gradient(circle at 20% 30%, #0a0f1e, #03060c);
            overflow-x: hidden;
        }

        /* Login Page Styles */
        .login-container {
            width: 100vw;
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            background: radial-gradient(circle at 20% 30%, #0a0f1e, #03060c);
            position: fixed;
            top: 0;
            left: 0;
            z-index: 1000;
        }

        .glass-panel {
            background: rgba(15, 25, 45, 0.85);
            backdrop-filter: blur(14px);
            border-radius: 48px;
            border: 1px solid rgba(0, 255, 255, 0.3);
            box-shadow: 0 25px 50px -12px rgba(0,0,0,0.5), 0 0 30px rgba(0,200,255,0.2);
            transition: transform 0.3s ease;
        }

        .login-card {
            padding: 3rem 2.5rem;
            border-radius: 56px;
            background: linear-gradient(135deg, rgba(18, 28, 48, 0.9), rgba(8, 14, 26, 0.95));
            text-align: center;
            width: 450px;
        }

        .brand-icon {
            font-size: 65px;
            background: linear-gradient(135deg, #00f2fe, #4facfe, #a855f7);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 12px;
            animation: iconPulse 2s infinite alternate;
        }

        @keyframes iconPulse {
            0% { filter: drop-shadow(0 0 5px cyan); }
            100% { filter: drop-shadow(0 0 20px #a855f7); }
        }

        h2 {
            font-size: 34px;
            font-weight: 800;
            background: linear-gradient(120deg, #FFFFFF, #b3f0ff, #c084fc);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .sub {
            color: #9aaec5;
            margin-bottom: 2rem;
            font-size: 0.9rem;
        }

        .input-group {
            position: relative;
            margin-bottom: 28px;
            text-align: left;
        }

        .input-group i {
            position: absolute;
            left: 18px;
            top: 50%;
            transform: translateY(-50%);
            font-size: 1.2rem;
            color: #4facfe;
            z-index: 1;
        }

        .input-group input {
            width: 100%;
            padding: 16px 18px 16px 48px;
            background: rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(79, 172, 254, 0.5);
            border-radius: 40px;
            font-size: 1rem;
            color: white;
            outline: none;
            transition: all 0.25s;
        }

        .input-group input:focus {
            border-color: #00f2fe;
            box-shadow: 0 0 12px rgba(0,242,254,0.4);
        }

        .password-toggle {
            position: absolute;
            right: 18px;
            top: 50%;
            transform: translateY(-50%);
            cursor: pointer;
            color: #8aadcc;
            background: transparent;
            border: none;
        }

        input::placeholder {
            color: transparent;
        }

        .input-group label {
            position: absolute;
            left: 48px;
            top: -10px;
            background: #0a0f1e;
            padding: 0 8px;
            font-size: 0.75rem;
            color: #7f9fcf;
            border-radius: 20px;
        }

        .login-btn {
            width: 100%;
            padding: 15px;
            background: linear-gradient(95deg, #0b57d0, #0a2f6c, #4c1d95);
            border: none;
            border-radius: 60px;
            font-weight: 700;
            font-size: 1.1rem;
            color: white;
            cursor: pointer;
            transition: 0.2s;
            box-shadow: 0 8px 0 #021a3b;
            transform: translateY(-2px);
        }

        .login-btn:active {
            transform: translateY(4px);
            box-shadow: 0 4px 0 #021a3b;
        }

        .error-msg {
            color: #ff8080;
            font-size: 0.8rem;
            margin-top: 12px;
            min-height: 38px;
        }

        /* Dashboard Styles */
        .dashboard-container {
            width: 100vw;
            height: 100vh;
            background: #050b14;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }

        .dash-header {
            background: rgba(10, 20, 35, 0.9);
            backdrop-filter: blur(12px);
            padding: 0 2rem;
            height: 60px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid rgba(0, 255, 255, 0.3);
            z-index: 20;
        }

        .logo-area h3 {
            font-size: 1.4rem;
            font-weight: 800;
            background: linear-gradient(135deg, #fff, #6dd5ff, #c084fc);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 20px;
        }

        .user-badge {
            background: rgba(0, 200, 255, 0.2);
            padding: 5px 14px;
            border-radius: 40px;
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 0.85rem;
            color: white;
        }

        .logout-icon {
            background: none;
            border: 1px solid #4facfe;
            padding: 5px 14px;
            border-radius: 32px;
            color: white;
            cursor: pointer;
            transition: 0.2s;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .logout-icon:hover {
            background: #ff3b3b30;
            border-color: #ff6b6b;
        }

        /* Main Content - Split View */
        .main-layout {
            flex: 1;
            display: flex;
            overflow: hidden;
            gap: 0;
        }

        /* Cognos Iframe - Takes 70% */
        .iframe-container {
            flex: 2.3;
            background: #000;
            position: relative;
        }

        iframe {
            width: 100%;
            height: 100%;
            border: none;
        }

        /* Analytics Sidebar - Takes 30% with scroll */
        .analytics-sidebar {
            flex: 1;
            background: rgba(8, 14, 26, 0.85);
            backdrop-filter: blur(10px);
            border-left: 1px solid rgba(0, 255, 255, 0.3);
            overflow-y: auto;
            padding: 20px;
        }

        .sidebar-section {
            margin-bottom: 28px;
        }

        .section-title {
            font-size: 0.9rem;
            font-weight: 700;
            color: #00f2fe;
            margin-bottom: 15px;
            border-left: 3px solid cyan;
            padding-left: 12px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        canvas {
            max-height: 180px;
            margin-bottom: 10px;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 12px;
            margin-bottom: 20px;
        }

        .stat-box {
            background: rgba(79, 172, 254, 0.1);
            border-radius: 16px;
            padding: 12px;
            text-align: center;
            border: 1px solid rgba(0, 255, 255, 0.2);
            transition: all 0.3s;
        }

        .stat-box:hover {
            transform: translateY(-3px);
            border-color: cyan;
            background: rgba(79, 172, 254, 0.2);
        }

        .stat-box-value {
            font-size: 1.6rem;
            font-weight: 800;
            background: linear-gradient(135deg, #fff, #4facfe);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .stat-box-label {
            font-size: 0.7rem;
            color: #9aaec5;
            margin-top: 5px;
        }

        .metric-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .metric-item {
            display: flex;
            justify-content: space-between;
            padding: 10px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 12px;
            border-left: 2px solid #4facfe;
        }

        .metric-name {
            color: #9aaec5;
            font-size: 0.85rem;
        }

        .metric-value {
            color: #00f2fe;
            font-weight: 700;
        }

        .region-badge {
            display: flex;
            justify-content: space-between;
            padding: 8px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            font-size: 0.85rem;
        }

        .region-name {
            color: #b3f0ff;
        }

        .region-revenue {
            color: #f59e0b;
            font-weight: 600;
        }

        .hidden {
            display: none;
        }

        ::-webkit-scrollbar {
            width: 5px;
        }
        ::-webkit-scrollbar-track {
            background: #0a0f1e;
        }
        ::-webkit-scrollbar-thumb {
            background: #00a6c4;
            border-radius: 10px;
        }

        @media (max-width: 900px) {
            .main-layout {
                flex-direction: column;
            }
            .iframe-container {
                flex: 1;
                min-height: 50%;
            }
            .analytics-sidebar {
                flex: 1;
            }
        }
    </style>
</head>
<body>

<!-- LOGIN PAGE -->
<div id="loginPage" class="login-container">
    <div class="login-card glass-panel">
        <div class="brand-icon">
            <i class="fas fa-chart-line"></i>
        </div>
        <h2>NovaTech Nexus</h2>
        <div class="sub">Advanced Analytics Dashboard</div>

        <div class="input-group">
            <i class="fas fa-user-astronaut"></i>
            <input type="text" id="username" autocomplete="off" placeholder=" ">
            <label>IDENTITY CODE</label>
        </div>

        <div class="input-group">
            <i class="fas fa-lock"></i>
            <input type="password" id="password" placeholder=" " autocomplete="off">
            <button type="button" class="password-toggle" id="togglePasswordBtn">
                <i class="fas fa-eye-slash" id="eyeIcon"></i>
            </button>
            <label>ACCESS KEY</label>
        </div>

        <button class="login-btn" id="loginBtn">UNLOCK DASHBOARD <i class="fas fa-arrow-right"></i></button>
        <div class="error-msg" id="errorMsg"></div>
    </div>
</div>

<!-- DASHBOARD PAGE -->
<div id="dashboardPage" class="dashboard-container hidden">
    <div class="dash-header">
        <div class="logo-area">
            <h3>⚡ NovaTech <span>| Cognos + Advanced Analytics</span></h3>
        </div>
        <div class="user-info">
            <div class="user-badge"><i class="fas fa-id-card"></i> <span id="displayUser">Analyst</span></div>
            <button class="logout-icon" id="logoutBtn"><i class="fas fa-sign-out-alt"></i> Exit</button>
        </div>
    </div>

    <div class="main-layout">
        <!-- IBM Cognos Iframe -->
        <div class="iframe-container">
            <iframe 
                src="https://ap2.ca.analytics.ibm.com/bi/?perspective=dashboard&amp;pathRef=.my_folders%2FNew%2Bdashboard2&amp;closeWindowOnLastView=true&amp;ui_appbar=false&amp;ui_navbar=false&amp;shareMode=embedded&amp;action=view&amp;mode=dashboard&amp;subView=model0000019d6dd71021_00000000&amp;nav_filter=true" 
                title="IBM Cognos Dashboard"
                allow="encrypted-media; fullscreen">
            </iframe>
        </div>

        <!-- Analytics Sidebar with Multiple Charts -->
        <div class="analytics-sidebar">
            <!-- Stats Grid -->
            <div class="sidebar-section">
                <div class="section-title"><i class="fas fa-chart-simple"></i> Key Metrics</div>
                <div class="stats-grid">
                    <div class="stat-box">
                        <div class="stat-box-value" id="totalRevenue">$48.2M</div>
                        <div class="stat-box-label">Total Revenue</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-box-value" id="totalUnits">2,847</div>
                        <div class="stat-box-label">Units Sold</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-box-value" id="avgSatisfaction">3.1</div>
                        <div class="stat-box-label">Avg Satisfaction</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-box-value" id="returnRate">8.3%</div>
                        <div class="stat-box-label">Return Rate</div>
                    </div>
                </div>
            </div>

            <!-- Chart 1: Revenue by Region (Bar Chart) -->
            <div class="sidebar-section">
                <div class="section-title"><i class="fas fa-map-marker-alt"></i> Revenue by Region</div>
                <canvas id="regionChart" width="280" height="160"></canvas>
                <div id="regionList"></div>
            </div>

            <!-- Chart 2: Sales by Model (Doughnut) -->
            <div class="sidebar-section">
                <div class="section-title"><i class="fas fa-mobile-alt"></i> Sales by Model</div>
                <canvas id="modelChart" width="280" height="160"></canvas>
            </div>

            <!-- Chart 3: Monthly Trend (Line Chart) -->
            <div class="sidebar-section">
                <div class="section-title"><i class="fas fa-chart-line"></i> Monthly Revenue Trend</div>
                <canvas id="trendChart" width="280" height="150"></canvas>
            </div>

            <!-- Additional Metrics -->
            <div class="sidebar-section">
                <div class="section-title"><i class="fas fa-chart-pie"></i> Performance Metrics</div>
                <div class="metric-list">
                    <div class="metric-item">
                        <span class="metric-name">🏆 Top Performing Model</span>
                        <span class="metric-value" id="topModel">Nova 5G</span>
                    </div>
                    <div class="metric-item">
                        <span class="metric-name">📍 Best Region</span>
                        <span class="metric-value" id="bestRegion">West</span>
                    </div>
                    <div class="metric-item">
                        <span class="metric-name">⚡ Most Common Issue</span>
                        <span class="metric-value" id="commonIssue">Speaker Fault</span>
                    </div>
                    <div class="metric-item">
                        <span class="metric-name">📊 Total Orders</span>
                        <span class="metric-value" id="totalOrders">2,847</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

<script>
    const VALID_CREDENTIALS = {
        username: "novatech_admin",
        password: "Nova3D#2025"
    };

    // Dashboard Data
    const dashboardData = {
        totalRevenue: 48.2,
        totalUnits: 2847,
        avgSatisfaction: 3.1,
        returnRate: 8.3,
        topModel: "Nova 5G",
        bestRegion: "West",
        commonIssue: "Speaker Fault",
        regionRevenue: {
            'West': 18.5,
            'South': 12.3,
            'North': 9.8,
            'East': 5.2,
            'Northeast': 2.4,
            'Central': 0
        },
        modelSales: {
            'Nova 5G': 35,
            'Nova Ultra': 28,
            'Nova X1': 18,
            'Nova Lite': 12,
            'Nova X2 Pro': 7
        },
        monthlyTrend: [3.2, 4.1, 5.3, 6.8, 7.2, 8.5, 9.1, 10.2, 11.5, 12.8, 14.2, 15.6]
    };

    let regionChart, modelChart, trendChart;

    // Initialize all charts
    function initCharts() {
        // Region Revenue Bar Chart
        const regionCtx = document.getElementById('regionChart').getContext('2d');
        regionChart = new Chart(regionCtx, {
            type: 'bar',
            data: {
                labels: Object.keys(dashboardData.regionRevenue),
                datasets: [{
                    label: 'Revenue ($M)',
                    data: Object.values(dashboardData.regionRevenue),
                    backgroundColor: ['#00f2fe', '#4facfe', '#a855f7', '#f59e0b', '#ef4444', '#10b981'],
                    borderRadius: 8
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: true,
                plugins: {
                    legend: { labels: { color: '#fff', font: { size: 10 } } }
                },
                scales: {
                    y: { ticks: { color: '#9aaec5' }, grid: { color: '#1a2a3a' } },
                    x: { ticks: { color: '#9aaec5', font: { size: 9 } } }
                }
            }
        });

        // Model Sales Doughnut Chart
        const modelCtx = document.getElementById('modelChart').getContext('2d');
        modelChart = new Chart(modelCtx, {
            type: 'doughnut',
            data: {
                labels: Object.keys(dashboardData.modelSales),
                datasets: [{
                    data: Object.values(dashboardData.modelSales),
                    backgroundColor: ['#00f2fe', '#4facfe', '#a855f7', '#f59e0b', '#ef4444'],
                    borderWidth: 0
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: true,
                plugins: {
                    legend: { position: 'bottom', labels: { color: '#fff', font: { size: 9 } } }
                }
            }
        });

        // Monthly Trend Line Chart
        const trendCtx = document.getElementById('trendChart').getContext('2d');
        trendChart = new Chart(trendCtx, {
            type: 'line',
            data: {
                labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
                datasets: [{
                    label: 'Revenue ($M)',
                    data: dashboardData.monthlyTrend,
                    borderColor: '#00f2fe',
                    backgroundColor: 'rgba(0, 242, 254, 0.1)',
                    tension: 0.4,
                    fill: true,
                    pointBackgroundColor: '#4facfe',
                    pointBorderColor: '#fff'
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: true,
                plugins: {
                    legend: { labels: { color: '#fff', font: { size: 10 } } }
                },
                scales: {
                    y: { ticks: { color: '#9aaec5' }, grid: { color: '#1a2a3a' } },
                    x: { ticks: { color: '#9aaec5', font: { size: 9 } } }
                }
            }
        });
    }

    // Update stats values
    function updateStats() {
        document.getElementById('totalRevenue').innerHTML = `$${dashboardData.totalRevenue}M`;
        document.getElementById('totalUnits').innerHTML = dashboardData.totalUnits.toLocaleString();
        document.getElementById('avgSatisfaction').innerHTML = dashboardData.avgSatisfaction;
        document.getElementById('returnRate').innerHTML = `${dashboardData.returnRate}%`;
        document.getElementById('topModel').innerHTML = dashboardData.topModel;
        document.getElementById('bestRegion').innerHTML = dashboardData.bestRegion;
        document.getElementById('commonIssue').innerHTML = dashboardData.commonIssue;
        document.getElementById('totalOrders').innerHTML = dashboardData.totalUnits.toLocaleString();
    }

    // DOM Elements
    const loginPage = document.getElementById('loginPage');
    const dashboardPage = document.getElementById('dashboardPage');
    const loginBtn = document.getElementById('loginBtn');
    const errorMsgDiv = document.getElementById('errorMsg');
    const usernameInput = document.getElementById('username');
    const passwordInput = document.getElementById('password');
    const togglePasswordBtn = document.getElementById('togglePasswordBtn');
    const eyeIcon = document.getElementById('eyeIcon');
    const displayUserSpan = document.getElementById('displayUser');
    const logoutBtn = document.getElementById('logoutBtn');

    // Password toggle
    togglePasswordBtn.addEventListener('click', function(e) {
        e.preventDefault();
        const type = passwordInput.getAttribute('type') === 'password' ? 'text' : 'password';
        passwordInput.setAttribute('type', type);
        eyeIcon.classList.toggle('fa-eye-slash');
        eyeIcon.classList.toggle('fa-eye');
    });

    // Login
    function performLogin() {
        const user = usernameInput.value.trim();
        const pass = passwordInput.value;

        if (!user || !pass) {
            errorMsgDiv.innerHTML = '⚠️ Please enter both credentials.';
            return;
        }

        if (user === VALID_CREDENTIALS.username && pass === VALID_CREDENTIALS.password) {
            loginPage.classList.add('hidden');
            dashboardPage.classList.remove('hidden');
            displayUserSpan.innerText = user;
            errorMsgDiv.innerHTML = '';
            updateStats();
            setTimeout(() => initCharts(), 100);
        } else {
            errorMsgDiv.innerHTML = '🔒 Access Denied: Invalid credentials.';
            passwordInput.value = '';
        }
    }

    // Logout
    function logoutSession() {
        dashboardPage.classList.add('hidden');
        loginPage.classList.remove('hidden');
        usernameInput.value = '';
        passwordInput.value = '';
        errorMsgDiv.innerHTML = '';
        if (passwordInput.getAttribute('type') !== 'password') {
            passwordInput.setAttribute('type', 'password');
            eyeIcon.classList.remove('fa-eye');
            eyeIcon.classList.add('fa-eye-slash');
        }
    }

    // Event listeners
    usernameInput.addEventListener('keypress', (e) => { if (e.key === 'Enter') performLogin(); });
    passwordInput.addEventListener('keypress', (e) => { if (e.key === 'Enter') performLogin(); });
    loginBtn.addEventListener('click', performLogin);
    logoutBtn.addEventListener('click', logoutSession);

    usernameInput.placeholder = '';
    passwordInput.placeholder = '';

    // 3D effect on login card
    const loginCard = document.querySelector('.login-card');
    document.addEventListener('mousemove', (e) => {
        if (!loginPage.classList.contains('hidden')) {
            const x = (e.clientX / window.innerWidth) * 10 - 5;
            const y = (e.clientY / window.innerHeight) * 10 - 5;
            loginCard.style.transform = `perspective(800px) rotateY(${x * 0.05}deg) rotateX(${y * -0.03}deg) translateY(-4px)`;
        }
    });
</script>
</body>
</html>
