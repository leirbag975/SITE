<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ScriptHub - Premium Scripts</title>
    <link rel="stylesheet" href="styles.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body>
    <!-- Navigation -->
    <nav class="navbar">
        <div class="nav-container">
            <div class="logo">
                <i class="fas fa-cube"></i>
                <span>ScriptHub</span>
            </div>
            <ul class="nav-links">
                <li><a href="index.html" class="nav-link active">Início</a></li>
                <li><a href="scripts.html" class="nav-link">Scripts</a></li>
                <li><a href="#" onclick="openChatArea(event)" class="nav-link">Minha Área</a></li>
                <li><a href="#" onclick="openAdminPanel(event)" class="nav-link admin-link">
                    <i class="fas fa-lock"></i> Admin
                </a></li>
                <li><a href="https://instagram.com/gabriel.futury" target="_blank" class="nav-link instagram-btn">
                    <i class="fab fa-instagram"></i> Instagram
                </a></li>
            </ul>
        </div>
    </nav>

    <!-- Hero Section -->
    <section class="hero">
        <div class="hero-content">
            <h1>Scripts Premium</h1>
            <p>Descubra scripts incríveis da comunidade</p>
            
            <div class="search-box">
                <input type="text" placeholder="Buscar scripts..." id="heroSearch" onkeyup="goToScriptsWithSearch()">
                <button onclick="goToScripts()"><i class="fas fa-search"></i></button>
            </div>
        </div>
    </section>

    <!-- Modals -->
    <!-- Chat Area Modal -->
    <div id="chatModal" class="modal">
        <div class="modal-content chat-modal">
            <button class="modal-close" onclick="closeChatArea()">&times;</button>
            
            <div class="chat-tabs">
                <button class="chat-tab-btn active" onclick="switchChatTab('myScripts')">
                    <i class="fas fa-list"></i> Meus Scripts
                </button>
            </div>

            <div id="myScripts-tab" class="chat-tab-content active">
                <div id="myScriptsContent">
                    <p class="info-text">Faça login para ver seus scripts</p>
                </div>
            </div>

            <div class="chat-footer">
                <button class="btn btn-secondary btn-block" id="chatLogoutBtn" style="display: none;" onclick="clientLogout()">
                    <i class="fas fa-sign-out-alt"></i> Sair
                </button>
                <button class="btn btn-primary btn-block" id="chatLoginBtn" onclick="openLoginModal()">
                    <i class="fas fa-sign-in-alt"></i> Fazer Login
                </button>
            </div>
        </div>
    </div>

    <!-- Login Modal -->
    <div id="loginModal" class="modal">
        <div class="modal-content">
            <button class="modal-close" onclick="closeLoginModal()">&times;</button>
            
            <h3>Fazer Login</h3>
            
            <form onsubmit="clientLogin(event)">
                <div class="form-group">
                    <label>Email:</label>
                    <input type="email" id="loginEmail" required>
                </div>
                <div class="form-group">
                    <label>Senha:</label>
                    <input type="password" id="loginPassword" required>
                </div>
                <button type="submit" class="btn btn-primary btn-block">Entrar</button>
            </form>

            <p class="form-footer">
                Não tem conta? <a href="#" onclick="openRegisterModal()">Cadastre-se</a>
            </p>
        </div>
    </div>

    <!-- Register Modal -->
    <div id="registerModal" class="modal">
        <div class="modal-content">
            <button class="modal-close" onclick="closeRegisterModal()">&times;</button>
            
            <h3>Criar Conta</h3>
            
            <form onsubmit="clientRegister(event)">
                <div class="form-group">
                    <label>Nome Completo:</label>
                    <input type="text" id="registerName" required>
                </div>
                <div class="form-group">
                    <label>Email:</label>
                    <input type="email" id="registerEmail" required>
                </div>
                <div class="form-group">
                    <label>Senha:</label>
                    <input type="password" id="registerPassword" required>
                </div>
                <div class="form-group">
                    <label>Confirmar Senha:</label>
                    <input type="password" id="registerPassword2" required>
                </div>
                <button type="submit" class="btn btn-primary btn-block">Cadastrar</button>
            </form>

            <p class="form-footer">
                Já tem conta? <a href="#" onclick="openLoginModal()">Faça login</a>
            </p>
        </div>
    </div>

    <!-- Admin Panel -->
    <div id="adminModal" class="modal">
        <div class="modal-content admin-modal">
            <button class="modal-close" onclick="closeAdminPanel()">&times;</button>

            <div id="adminPasswordScreen" class="admin-screen">
                <div class="admin-password-content">
                    <i class="fas fa-lock admin-lock-icon"></i>
                    <h3>Painel de Anúncio</h3>
                    <p>Digite a senha para anunciar scripts</p>
                    <form onsubmit="adminPasswordCheck(event)">
                        <div class="form-group">
                            <input type="password" id="adminPassword" required autofocus placeholder="Senha">
                        </div>
                        <button type="submit" class="btn btn-primary btn-block">Acessar</button>
                    </form>
                </div>
            </div>

            <div id="adminPanelScreen" class="admin-screen" style="display: none;">
                <div class="admin-header">
                    <h3>Anunciar Script</h3>
                    <button class="btn btn-secondary btn-sm" onclick="adminLogout()">Sair</button>
                </div>

                <div class="admin-tabs">
                    <button class="admin-tab-btn active" onclick="switchAdminTab('add')">
                        <i class="fas fa-plus"></i> Novo Script
                    </button>
                    <button class="admin-tab-btn" onclick="switchAdminTab('manage')">
                        <i class="fas fa-list"></i> Meus Anúncios
                    </button>
                </div>

                <!-- Add Script -->
                <div id="add-tab" class="admin-tab-content active">
                    <form id="announceForm" onsubmit="submitScript(event)">
                        <div class="form-group">
                            <label>Nome do Script:</label>
                            <input type="text" id="scriptName" required>
                        </div>
                        <div class="form-group">
                            <label>Categoria:</label>
                            <select id="scriptCategory" required>
                                <option value="">Selecione</option>
                                <option value="automacao">Automação</option>
                                <option value="web">Web</option>
                                <option value="bot">Bot</option>
                                <option value="utilidade">Utilidade</option>
                                <option value="outro">Outro</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>Descrição:</label>
                            <textarea id="scriptDescription" rows="4" required placeholder="Descreva seu script..."></textarea>
                        </div>
                        <div class="form-group">
                            <label>Foto do Script:</label>
                            <input type="file" id="scriptImage" accept="image/*" required>
                        </div>
                        <div class="form-group">
                            <label>Preço (opcional):</label>
                            <input type="number" id="scriptPrice" step="0.01" min="0">
                        </div>
                        <div class="alert-box">
                            <p><strong>⚠️ Importante:</strong> Seu script será aprovado automaticamente. Um código de ativação será gerado.</p>
                        </div>
                        <button type="submit" class="btn btn-primary btn-block">
                            <i class="fas fa-rocket"></i> Anunciar Script
                        </button>
                    </form>
                </div>

                <!-- Manage Scripts -->
                <div id="manage-tab" class="admin-tab-content">
                    <div id="adminScriptsList"></div>
                </div>
            </div>
        </div>
    </div>

    <!-- Unlock Script Modal -->
    <div id="unlockModal" class="modal">
        <div class="modal-content">
            <button class="modal-close" onclick="closeUnlockModal()">&times;</button>
            
            <div class="unlock-content">
                <i class="fas fa-key unlock-icon"></i>
                <h3>Desbloquear Script</h3>
                <p id="unlockMessage">Digite o código de ativação</p>
                <form onsubmit="unlockScript(event)">
                    <div class="form-group">
                        <input type="text" id="unlockCode" required placeholder="Código de ativação" maxlength="6">
                    </div>
                    <button type="submit" class="btn btn-primary btn-block">Desbloquear</button>
                </form>
            </div>
        </div>
    </div>

    <!-- Notification -->
    <div id="notification" class="notification"></div>

    <script src="script.js"></script>
</body>
</html>
