# VAULTCHAT-
App Social to conect to friends
```html
<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>VaultChat PRO | Comunicación Privada</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts: Inter -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <!-- Font Awesome Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
  
  <style>
    /* Estilos base y tipografía */
    * { 
      font-family: 'Inter', system-ui, -apple-system, sans-serif; 
      box-sizing: border-box;
    }
    
    body { 
      overflow: hidden; 
      background-color: #0f172a;
    }

    /* Campos de formulario estilizados */
    .field { 
      width: 100%; 
      border: 1px solid #cbd5e1; 
      border-radius: 10px; 
      padding: 11px 12px; 
      font-size: 13px; 
      outline: none; 
      background: #f8fafc; 
      transition: all 0.2s ease;
    }
    .field:focus { 
      background: white; 
      border-color: #2563eb; 
      box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.15); 
    }
    .field-label { 
      display: block; 
      font-size: 11px; 
      font-weight: 700; 
      color: #475569; 
      text-transform: uppercase; 
      letter-spacing: 0.06em; 
      margin-bottom: 4px;
    }

    /* Botones principales y secundarios */
    .primary { 
      background: #1d4ed8; 
      color: white; 
      border-radius: 10px; 
      padding: 11px 14px; 
      font-size: 13px; 
      font-weight: 600; 
      transition: all 0.15s ease; 
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      justify-content: center;
    }
    .primary:hover { 
      background: #1e40af; 
      transform: translateY(-1px);
    }
    .primary:active {
      transform: translateY(0);
    }

    .secondary { 
      background: #e2e8f0; 
      color: #1e293b; 
      border-radius: 9px; 
      padding: 10px 12px; 
      font-size: 12px; 
      font-weight: 600; 
      transition: all 0.15s ease;
      cursor: pointer;
    }
    .secondary:hover {
      background: #cbd5e1;
    }

    /* Pestañas de navegación */
    .auth-tab, .nav-tab { 
      padding: 10px 8px; 
      border-radius: 9px; 
      font-size: 12px; 
      font-weight: 600; 
      color: #64748b; 
      flex: 1; 
      transition: all 0.2s ease;
      cursor: pointer;
    }
    .auth-tab.active, .nav-tab.active { 
      background: white; 
      color: #0f172a; 
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.08); 
    }

    /* Tarjetas y contenedores */
    .panel-card { 
      background: white; 
      border: 1px solid #e2e8f0; 
      border-radius: 13px; 
      padding: 15px; 
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.04); 
    }
    .code-display { 
      background: #0f172a; 
      color: #34d399; 
      border-radius: 10px; 
      text-align: center; 
      padding: 15px 8px; 
      font: 700 15px ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace; 
      letter-spacing: 0.08em; 
      overflow-wrap: anywhere; 
      border: 1px solid #1e293b;
    }

    /* Botones de iconos y avatares */
    .icon-btn { 
      width: 36px;
      height: 36px;
      border-radius: 9px;
      background: #1e293b;
      color: #cbd5e1; 
      display: grid;
      place-items: center;
      transition: 0.15s;
      cursor: pointer;
    }
    .icon-btn:hover {
      background: #334155;
      color: white;
    }

    .avatar { 
      width: 42px;
      height: 42px;
      border-radius: 12px;
      background: linear-gradient(135deg, #1d4ed8, #3b82f6);
      color: white;
      display: grid;
      place-items: center;
      font-weight: 700;
      font-size: 14px;
      flex-shrink: 0; 
      box-shadow: 0 2px 6px rgba(29, 78, 216, 0.25);
    }

    /* Lista de contactos */
    .contact-row { 
      display: flex;
      gap: 12px;
      align-items: center;
      padding: 14px;
      cursor: pointer;
      background: white; 
      transition: background 0.15s ease;
    }
    .contact-row:hover, .contact-row.selected { 
      background: #eff6ff; 
    }
    .contact-row.selected {
      border-left: 3px solid #1d4ed8;
    }

    /* Burbujas de chat */
    .bubble { 
      max-width: min(78%, 520px); 
      padding: 10px 14px; 
      border-radius: 15px; 
      font-size: 13px; 
      line-height: 1.45;
      overflow-wrap: anywhere; 
      white-space: pre-wrap; 
      animation: popIn 0.18s ease-out;
    }
    @keyframes popIn {
      from { opacity: 0; transform: translateY(6px) scale(0.98); }
      to { opacity: 1; transform: translateY(0) scale(1); }
    }
    .bubble.mine { 
      margin-left: auto;
      background: #1d4ed8;
      color: white;
      border-bottom-right-radius: 4px; 
      box-shadow: 0 2px 5px rgba(29, 78, 216, 0.2);
    }
    .bubble.theirs { 
      background: white;
      color: #1e293b;
      border: 1px solid #e2e8f0;
      border-bottom-left-radius: 4px; 
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.04);
    }
    .bubble-meta { 
      font-size: 10px; 
      opacity: 0.75; 
      margin-top: 5px; 
      text-align: right; 
      display: flex;
      align-items: center;
      justify-content: flex-end;
      gap: 4px;
    }

    /* Botones de llamada */
    .call-btn { 
      width: 38px;
      height: 38px;
      border-radius: 10px;
      background: #eff6ff;
      color: #1d4ed8; 
      display: grid;
      place-items: center;
      transition: 0.15s;
      cursor: pointer;
    }
    .call-btn:hover {
      background: #dbeafe;
    }

    /* Notificaciones Toast */
    .toast { 
      background: #0f172a;
      color: white;
      padding: 12px 16px;
      border-radius: 10px;
      font-size: 12px;
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.35);
      max-width: 340px; 
      border-left: 4px solid #34d399;
      animation: slideIn 0.25s ease-out;
    }
    .toast.error {
      border-left-color: #ef4444;
    }
    @keyframes slideIn {
      from { opacity: 0; transform: translateX(20px); }
      to { opacity: 1; transform: translateX(0); }
    }

    /* Scrollbars limpios */
    ::-webkit-scrollbar { width: 6px; height: 6px; }
    ::-webkit-scrollbar-track { background: transparent; }
    ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 99px; }
    ::-webkit-scrollbar-thumb:hover { background: #94a3b8; }

    /* Adaptación móvil */
    @media (max-width: 767px) {
      #app-screen { padding: 0; }
      .app-shell { border-radius: 0; }
      .sidebar { width: 100%; }
      #chat-main { position: fixed; inset: 0; z-index: 20; }
      #chat-main.mobile-open { display: flex !important; }
      .sidebar.mobile-hide { display: none; }
      #mobile-back { color: #475569; padding: 6px 10px; }
    }
  </style>
</head>
<body class="min-h-screen bg-slate-900 text-slate-800">
  
  <!-- Contenedor de notificaciones flotantes -->
  <div id="toast-container" class="fixed top-4 right-4 z-50 space-y-2 pointer-events-none"></div>

  <!-- ==========================================
       PANTALLA DE AUTENTICACIÓN (LOGIN / REGISTRO)
       ========================================== -->
  <section id="auth-screen" class="min-h-screen flex items-center justify-center p-4 overflow-y-auto">
    <div class="w-full max-w-md bg-white rounded-2xl shadow-2xl overflow-hidden my-auto">
      <header class="bg-slate-900 text-center p-7 text-white relative">
        <div class="mx-auto mb-3 w-14 h-14 rounded-xl bg-blue-600/20 border border-blue-500/40 flex items-center justify-center text-blue-300 text-2xl shadow-inner">
          <i class="fa-solid fa-shield-halved"></i>
        </div>
        <h1 class="text-2xl font-bold tracking-tight">VaultChat <span class="text-xs bg-blue-600 rounded-full px-2.5 py-0.5 align-middle ml-1">PRO</span></h1>
        <p class="text-xs text-slate-400 mt-2">Mensajería privada • Acceso por credencial</p>
      </header>
      
      <div class="p-6">
        <!-- Pestañas Login / Registro -->
        <div class="flex gap-2 mb-5 bg-slate-100 p-1 rounded-xl">
          <button type="button" class="auth-tab active" data-auth-tab="login">Ingresar</button>
          <button type="button" class="auth-tab" data-auth-tab="register">Crear cuenta</button>
        </div>

        <!-- Formulario de Inicio de Sesión -->
        <form id="login-form" class="space-y-4">
          <div>
            <label class="field-label" for="login-code">Código maestro</label>
            <input id="login-code" class="field font-mono uppercase" placeholder="VLT-XXXX-XXXX-XXXX" required>
          </div>
          <div>
            <label class="field-label" for="login-password">Contraseña</label>
            <input id="login-password" class="field" type="password" placeholder="••••••••••••" required autocomplete="current-password">
          </div>
          <button type="submit" class="primary w-full">
            Desbloquear bóveda <i class="fa-solid fa-arrow-right ml-2"></i>
          </button>
          
          <!-- Acceso rápido de demostración -->
          <div class="pt-2">
            <button type="button" id="demo-login-btn" class="secondary w-full text-blue-700 bg-blue-50 hover:bg-blue-100 border border-blue-200">
              <i class="fa-solid fa-bolt mr-1.5"></i> Entrar con cuenta de demostración
            </button>
          </div>
        </form>

        <!-- Formulario de Registro -->
        <form id="register-form" class="space-y-4 hidden">
          <div>
            <label class="field-label" for="register-name">Nombre visible</label>
            <input id="register-name" class="field" placeholder="Ej. Alex Mercer" maxlength="80" required>
          </div>
          <div>
            <label class="field-label" for="register-password">Contraseña (mínimo 12 caracteres)</label>
            <input id="register-password" class="field" type="password" minlength="12" placeholder="Mínimo 12 caracteres..." required autocomplete="new-password">
          </div>
          <button type="submit" class="primary w-full">
            <i class="fa-solid fa-key mr-2"></i> Crear mi bóveda
          </button>
          <p class="text-xs text-slate-500 bg-slate-50 p-3 rounded-lg border border-slate-200">
            <i class="fa-solid fa-circle-info text-blue-600 mr-1"></i> Al crear la cuenta recibirás un <strong>código maestro</strong>. Guardalo: lo necesitarás para volver a ingresar.
          </p>
        </form>

        <p class="text-[11px] text-slate-400 border-t mt-5 pt-4 flex items-center justify-between">
          <span><i class="fa-solid fa-lock text-emerald-600 mr-1"></i> Sesiones autenticadas</span>
          <span>Almacenamiento local activo</span>
        </p>
      </div>
    </div>
  </section>

  <!-- ==========================================
       MODAL DE CÓDIGO MAESTRO GENERADO
       ========================================== -->
  <div id="master-code-modal" class="hidden fixed inset-0 z-50 bg-slate-900/80 backdrop-blur-sm flex items-center justify-center p-4">
    <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-2xl text-center">
      <div class="w-14 h-14 bg-emerald-100 text-emerald-600 rounded-2xl flex items-center justify-center text-2xl mx-auto mb-3">
        <i class="fa-solid fa-check-shield"></i>
      </div>
      <h2 class="text-lg font-bold text-slate-900">¡Bóveda creada con éxito!</h2>
      <p class="text-xs text-slate-500 mt-1 mb-4">Este es tu <strong>Código Maestro</strong> único. Copialo y guardalo en un lugar seguro para iniciar sesión en el futuro.</p>
      
      <div id="modal-generated-code" class="code-display mb-4 select-all">VLT-0000-0000-0000</div>
      
      <div class="flex gap-2">
        <button type="button" id="modal-copy-code" class="secondary flex-1">
          <i class="fa-regular fa-copy mr-1"></i> Copiar código
        </button>
        <button type="button" id="modal-continue-btn" class="primary flex-1">
          Entrar al chat <i class="fa-solid fa-arrow-right ml-1"></i>
        </button>
      </div>
    </div>
  </div>

  <!-- ==========================================
       PANTALLA PRINCIPAL DE LA APLICACIÓN
       ========================================== -->
  <section id="app-screen" class="hidden h-screen md:p-4">
    <div class="app-shell max-w-7xl mx-auto h-full bg-white md:rounded-2xl overflow-hidden shadow-2xl flex">
      
      <!-- BARRA LATERAL (SIDEBAR) -->
      <aside id="sidebar" class="sidebar w-full md:w-96 shrink-0 border-r border-slate-200 bg-slate-50 flex flex-col">
        <!-- Encabezado de usuario -->
        <header class="bg-slate-900 text-white px-5 py-4 flex justify-between items-center">
          <div class="flex items-center gap-3 min-w-0">
            <div class="w-10 h-10 bg-blue-600 rounded-xl flex items-center justify-center shrink-0 shadow-md">
              <i class="fa-solid fa-shield-halved"></i>
            </div>
            <div class="min-w-0">
              <div id="header-user-name" class="font-semibold text-sm truncate">VaultChat Corporativo</div>
              <div id="header-user-id" class="text-[10px] text-emerald-400 font-mono truncate"></div>
            </div>
          </div>
          <button id="logout-btn" class="icon-btn shrink-0" title="Cerrar sesión">
            <i class="fa-solid fa-right-from-bracket"></i>
          </button>
        </header>

        <!-- Navegación por pestañas -->
        <nav class="grid grid-cols-3 gap-1 p-2 bg-slate-200/70 border-b border-slate-200">
          <button type="button" class="nav-tab active" data-tab="chats">
            <i class="fa-solid fa-message mr-1"></i> Chats
          </button>
          <button type="button" class="nav-tab" data-tab="codes">
            <i class="fa-solid fa-qrcode mr-1"></i> Mi código
          </button>
          <button type="button" class="nav-tab" data-tab="admin">
            <i class="fa-solid fa-gauge mr-1"></i> Admin
          </button>
        </nav>

        <!-- PANEL 1: LISTA DE CHATS -->
        <div id="tab-chats" class="tab-panel flex-1 min-h-0 flex flex-col">
          <div class="p-3 bg-white border-b border-slate-100">
            <div class="relative">
              <i class="fa-solid fa-magnifying-glass text-slate-400 text-xs absolute left-3.5 top-3.5"></i>
              <input id="search-chats" class="field pl-9" placeholder="Buscar contacto...">
            </div>
          </div>
          
          <div id="chat-list" class="flex-1 overflow-y-auto divide-y divide-slate-100">
            <!-- Los contactos se renderizan aquí dinámicamente -->
          </div>
          
          <div class="p-3 text-center text-[11px] text-slate-500 bg-slate-100 border-t border-slate-200">
            <i class="fa-solid fa-shield-halved text-emerald-600 mr-1"></i> Acceso privado a tus conversaciones
          </div>
        </div>

        <!-- PANEL 2: CÓDIGOS E INVITACIONES -->
        <div id="tab-codes" class="tab-panel hidden flex-1 overflow-y-auto p-4 space-y-4">
          <!-- Generar invitación -->
          <div class="panel-card">
            <h3 class="font-semibold text-sm mb-1 text-slate-800">
              <i class="fa-solid fa-user-plus text-blue-600 mr-2"></i>Invitar contacto
            </h3>
            <p class="text-xs text-slate-500 mb-3">El código vence en 24 horas y solo puede utilizarse una vez.</p>
            <div id="invite-code" class="code-display">Todavía no generado</div>
            <div class="grid grid-cols-2 gap-2 mt-3">
              <button type="button" id="generate-invite" class="primary">
                <i class="fa-solid fa-wand-magic-sparkles mr-1.5"></i> Generar
              </button>
              <button type="button" id="copy-invite" class="secondary">
                <i class="fa-regular fa-copy mr-1.5"></i> Copiar
              </button>
            </div>
          </div>

          <!-- Vincular contacto -->
          <div class="panel-card">
            <h3 class="font-semibold text-sm mb-1 text-slate-800">
              <i class="fa-solid fa-link text-emerald-600 mr-2"></i>Vincular contacto
            </h3>
            <p class="text-xs text-slate-500 mb-2">Ingresá un código de invitación recibido (ej. <code class="bg-slate-100 px-1 rounded text-slate-700">INV-DEMO-2026</code>).</p>
            <form id="connect-form" class="space-y-3 mt-3">
              <div>
                <input id="partner-code" class="field font-mono uppercase" placeholder="Código INV-..." required>
              </div>
              <div>
                <input id="partner-alias" class="field" placeholder="Nombre para mostrar (Alias)" required maxlength="80">
              </div>
              <button type="submit" class="primary w-full">
                <i class="fa-solid fa-plus mr-1.5"></i> Establecer canal privado
              </button>
            </form>
          </div>

          <!-- Mi código maestro -->
          <div class="panel-card">
            <div class="text-xs font-semibold text-slate-500 uppercase tracking-wider">Tu código maestro</div>
            <div id="my-master-code" class="font-mono font-bold text-slate-800 mt-1.5 break-all bg-slate-100 p-2.5 rounded-lg border border-slate-200 text-center"></div>
            <button type="button" id="copy-master" class="secondary w-full mt-3">
              <i class="fa-regular fa-copy mr-1.5"></i> Copiar código maestro
            </button>
          </div>
        </div>

        <!-- PANEL 3: ADMINISTRACIÓN -->
        <div id="tab-admin" class="tab-panel hidden flex-1 overflow-y-auto p-4 space-y-4">
          <div class="panel-card">
            <h3 class="font-semibold text-sm mb-1 text-slate-800">
              <i class="fa-solid fa-server text-indigo-600 mr-2"></i>Panel de administración
            </h3>
            <p class="text-xs text-slate-500 mb-3">Métricas del servidor y estado de bóvedas activas en esta instancia.</p>
            <button type="button" id="load-admin" class="primary w-full">
              <i class="fa-solid fa-rotate mr-1.5"></i> Consultar estadísticas
            </button>
            <div id="admin-stats-grid" class="hidden grid-cols-2 gap-2 mt-4">
              <div class="bg-slate-50 p-3 rounded-xl border border-slate-200">
                <div class="text-[10px] text-slate-500 uppercase font-bold">Usuarios</div>
                <div id="stat-users" class="text-xl font-bold text-slate-800 mt-0.5">0</div>
              </div>
              <div class="bg-slate-50 p-3 rounded-xl border border-slate-200">
                <div class="text-[10px] text-slate-500 uppercase font-bold">Canales</div>
                <div id="stat-channels" class="text-xl font-bold text-blue-600 mt-0.5">0</div>
              </div>
              <div class="bg-slate-50 p-3 rounded-xl border border-slate-200">
                <div class="text-[10px] text-slate-500 uppercase font-bold">Mensajes</div>
                <div id="stat-messages" class="text-xl font-bold text-emerald-600 mt-0.5">0</div>
              </div>
              <div class="bg-slate-50 p-3 rounded-xl border border-slate-200">
                <div class="text-[10px] text-slate-500 uppercase font-bold">Estado</div>
                <div class="text-xs font-bold text-emerald-600 mt-1.5 flex items-center gap-1">
                  <span class="w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span> En línea
                </div>
              </div>
            </div>
            <pre id="admin-data" class="text-[11px] font-mono bg-slate-900 text-emerald-400 p-3 rounded-xl mt-3 whitespace-pre-wrap hidden"></pre>
          </div>
        </div>
      </aside>

      <!-- ÁREA PRINCIPAL DE CONVERSACIÓN -->
      <main id="chat-main" class="hidden md:flex flex-1 min-w-0 flex-col bg-slate-100">
        
        <!-- Estado vacío cuando no hay chat seleccionado -->
        <div id="empty-state" class="flex-1 flex flex-co
