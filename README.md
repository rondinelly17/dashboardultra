<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dashboard Ultra - Sistema de Segurança</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #4361ee;
            --secondary: #3f37c9;
            --success: #4cc9f0;
            --danger: #f72585;
            --warning: #f8961e;
            --info: #4895ef;
            --dark: #1a1a2e;
            --darker: #16213e;
            --light: #f8f9fa;
            --gray: #6c757d;
            --sidebar-width: 260px;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }

        body {
            background: linear-gradient(135deg, var(--darker) 0%, var(--dark) 100%);
            color: var(--light);
            min-height: 100vh;
            overflow-x: hidden;
        }

        .app-container {
            display: flex;
            min-height: 100vh;
        }

        /* Sidebar */
        .sidebar {
            width: var(--sidebar-width);
            background: rgba(26, 26, 46, 0.95);
            backdrop-filter: blur(10px);
            border-right: 1px solid rgba(255, 255, 255, 0.1);
            padding: 20px 0;
            position: fixed;
            height: 100vh;
            overflow-y: auto;
            z-index: 1000;
            transition: all 0.3s ease;
        }

        .sidebar-header {
            padding: 0 20px 20px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            margin-bottom: 20px;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 12px;
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--light);
        }

        .logo i {
            color: var(--primary);
        }

        .nav-links {
            list-style: none;
            padding: 0 15px;
        }

        .nav-links li {
            margin-bottom: 8px;
        }

        .nav-links a {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 12px 15px;
            color: var(--light);
            text-decoration: none;
            border-radius: 8px;
            transition: all 0.3s ease;
            font-weight: 500;
        }

        .nav-links a:hover,
        .nav-links a.active {
            background: var(--primary);
            color: white;
        }

        .nav-links i {
            width: 20px;
            text-align: center;
        }

        /* Main Content */
        .main-content {
            flex: 1;
            margin-left: var(--sidebar-width);
            padding: 20px;
            transition: all 0.3s ease;
        }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            padding: 20px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .header h1 {
            font-size: 2rem;
            font-weight: 700;
            background: linear-gradient(135deg, var(--primary), var(--success));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .user-menu {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .btn {
            padding: 10px 20px;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .btn-primary {
            background: var(--primary);
            color: white;
        }

        .btn-primary:hover {
            background: var(--secondary);
            transform: translateY(-2px);
        }

        /* Dashboard Grid */
        .dashboard-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .card {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 25px;
            transition: all 0.3s ease;
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }

        .card-header {
            display: flex;
            justify-content: between;
            align-items: center;
            margin-bottom: 15px;
        }

        .card-title {
            font-size: 1.2rem;
            font-weight: 600;
            color: var(--light);
        }

        .card-icon {
            width: 50px;
            height: 50px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            background: var(--primary);
            color: white;
        }

        .stat-number {
            font-size: 2.5rem;
            font-weight: 700;
            margin: 10px 0;
            background: linear-gradient(135deg, var(--primary), var(--success));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .stat-label {
            color: var(--gray);
            font-size: 0.9rem;
        }

        /* 2FA Section */
        .twofa-section {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 30px;
            margin-bottom: 30px;
        }

        .twofa-header {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 25px;
        }

        .twofa-header i {
            font-size: 2rem;
            color: var(--primary);
        }

        .twofa-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
        }

        .qrcode-container {
            text-align: center;
            padding: 20px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 12px;
        }

        .qrcode-placeholder {
            width: 200px;
            height: 200px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            margin: 0 auto 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
            color: var(--primary);
        }

        .backup-codes {
            background: rgba(255, 255, 255, 0.05);
            padding: 20px;
            border-radius: 12px;
        }

        .backup-codes h4 {
            margin-bottom: 15px;
            color: var(--light);
        }

        .codes-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 20px;
        }

        .code-item {
            background: rgba(255, 255, 255, 0.1);
            padding: 10px;
            border-radius: 6px;
            text-align: center;
            font-family: monospace;
            font-size: 0.9rem;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .sidebar {
                transform: translateX(-100%);
            }

            .main-content {
                margin-left: 0;
            }

            .twofa-content {
                grid-template-columns: 1fr;
            }

            .dashboard-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="app-container">
        <!-- Sidebar -->
        <nav class="sidebar">
            <div class="sidebar-header">
                <div class="logo">
                    <i class="fas fa-shield-alt"></i>
                    <span>Security Ultra</span>
                </div>
            </div>
            <ul class="nav-links">
                <li><a href="#" class="active"><i class="fas fa-home"></i> Dashboard</a></li>
                <li><a href="#"><i class="fas fa-search"></i> Análise de IP</a></li>
                <li><a href="#"><i class="fas fa-brain"></i> Machine Learning</a></li>
                <li><a href="#"><i class="fas fa-cog"></i> Configurações</a></li>
                <li><a href="#"><i class="fas fa-chart-bar"></i> Analytics</a></li>
                <li><a href="#"><i class="fas fa-user-shield"></i> Segurança</a></li>
            </ul>
        </nav>

        <!-- Main Content -->
        <main class="main-content">
            <header class="header">
                <h1>Dashboard de Segurança Ultra</h1>
                <div class="user-menu">
                    <button class="btn btn-primary">
                        <i class="fas fa-sync-alt"></i>
                        Atualizar
                    </button>
                    <div class="user-avatar">
                        <i class="fas fa-user-circle fa-2x"></i>
                    </div>
                </div>
            </header>

            <!-- Stats Grid -->
            <div class="dashboard-grid">
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">Ameaças Detectadas</h3>
                        <div class="card-icon">
                            <i class="fas fa-shield-alt"></i>
                        </div>
                    </div>
                    <div class="stat-number">12</div>
                    <div class="stat-label">Últimas 24h</div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">IPs Analisados</h3>
                        <div class="card-icon">
                            <i class="fas fa-globe"></i>
                        </div>
                    </div>
                    <div class="stat-number">1,247</div>
                    <div class="stat-label">Total este mês</div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">Sistema 2FA</h3>
                        <div class="card-icon">
                            <i class="fas fa-lock"></i>
                        </div>
                    </div>
                    <div class="stat-number">Ativo</div>
                    <div class="stat-label">Protegido</div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">ML Insights</h3>
                        <div class="card-icon">
                            <i class="fas fa-brain"></i>
                        </div>
                    </div>
                    <div class="stat-number">98%</div>
                    <div class="stat-label">Precisão</div>
                </div>
            </div>

            <!-- 2FA Section -->
            <section class="twofa-section">
                <div class="twofa-header">
                    <i class="fas fa-mobile-alt"></i>
                    <h2>Autenticação em Dois Fatores (2FA)</h2>
                </div>
                <div class="twofa-content">
                    <div class="qrcode-container">
                        <div class="qrcode-placeholder">
                            <i class="fas fa-qrcode"></i>
                        </div>
                        <p>Escaneie com Google Authenticator</p>
                        <button class="btn btn-primary" style="margin-top: 15px;">
                            <i class="fas fa-sync"></i>
                            Gerar Novo QR Code
                        </button>
                    </div>
                    <div class="backup-codes">
                        <h4>Códigos de Backup</h4>
                        <div class="codes-grid">
                            <div class="code-item">A1B2C3</div>
                            <div class="code-item">D4E5F6</div>
                            <div class="code-item">G7H8I9</div>
                            <div class="code-item">J0K1L2</div>
                            <div class="code-item">M3N4O5</div>
                            <div class="code-item">P6Q7R8</div>
                        </div>
                        <button class="btn btn-primary">
                            <i class="fas fa-download"></i>
                            Baixar Códigos
                        </button>
                    </div>
                </div>
            </section>
        </main>
    </div>

    <script>
        // Simulação de funcionalidades
        console.log('🚀 Dashboard Ultra carregado!');
        
        // Simular atualização de dados
        document.querySelector('.btn-primary').addEventListener('click', function() {
            this.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Atualizando...';
            setTimeout(() => {
                this.innerHTML = '<i class="fas fa-sync-alt"></i> Atualizar';
                alert('Dados atualizados com sucesso!');
            }, 2000);
        });

        // Simular geração de QR Code
        document.querySelectorAll('.btn-primary')[1].addEventListener('click', function() {
            this.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Gerando...';
            setTimeout(() => {
                this.innerHTML = '<i class="fas fa-sync"></i> Gerar Novo QR Code';
                alert('Novo QR Code gerado! Escaneie novamente.');
            }, 1500);
        });
    </script>
</body>
</html>
