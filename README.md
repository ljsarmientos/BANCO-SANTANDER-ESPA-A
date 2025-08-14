<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Banco Santander España</title>
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    /* Scroll suave para listas */
    .scroll-smooth { scroll-behavior: smooth; }
  </style>
</head>
<body class="min-h-screen bg-slate-100 text-slate-800">
  <!-- Barra superior -->
  <header class="sticky top-0 z-10 bg-white/80 backdrop-blur border-b border-slate-200">
    <div class="max-w-4xl mx-auto px-4 py-3 flex items-center justify-between">
      <div class="flex items-center gap-2">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6 text-indigo-600"><path d="M11.47 3.84a.75.75 0 0 1 1.06 0l8.25 8.25a.75.75 0 0 1-1.06 1.06L12 5.44l-7.72 7.71a.75.75 0 1 1-1.06-1.06l8.25-8.25Z"/><path d="M12 5.5a.75.75 0 0 1 .75.75v12.5a.75.75 0 0 1-1.5 0V6.25A.75.75 0 0 1 12 5.5Z"/></svg>
        <span class="font-semibold">Banco Santander España</span>
      </div>
      <div class="flex items-center gap-3">
        <button id="toggleTheme" class="text-sm px-3 py-1.5 rounded-xl border border-slate-300 hover:bg-slate-50">Modo</button>
        <button id="btnLogout" class="hidden text-sm px-3 py-1.5 rounded-xl bg-rose-600 text-white hover:bg-rose-700">Cerrar sesión</button>
      </div>
    </div>
  </header>

  <main class="max-w-4xl mx-auto px-4 py-8">
    <!-- Tarjeta de acceso -->
    <section id="authCard" class="grid md:grid-cols-2 gap-6">
      <!-- Login -->
      <div class="bg-white rounded-2xl shadow p-6">
        <h2 class="text-xl font-bold mb-4">Iniciar sesión</h2>
        <div class="space-y-3">
          <label class="block text-sm">Usuario
            <input id="loginUser" type="text" class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500" placeholder="tu_usuario" />
          </label>
          <label class="block text-sm">Contraseña
            <div class="mt-1 relative">
              <input id="loginPass" type="password" class="w-full rounded-xl border border-slate-300 px-3 py-2 pr-10 focus:outline-none focus:ring-2 focus:ring-indigo-500" placeholder="••••••" />
              <button id="toggleLoginPass" class="absolute inset-y-0 right-2 my-auto text-slate-500 hover:text-slate-700" type="button" aria-label="Mostrar/ocultar contraseña">👁️</button>
            </div>
          </label>
          <button id="btnLogin" class="w-full rounded-xl bg-indigo-600 text-white py-2.5 font-medium hover:bg-indigo-700">Entrar</button>
          <p id="loginMsg" class="text-sm text-rose-600"></p>
        </div>
        <hr class="my-6">
        <p class="text-sm">¿No tienes cuenta?
          <button id="goRegister" class="text-indigo-700 font-medium hover:underline">Regístrate</button>
        </p>
        <div class="mt-4 text-xs text-slate-500">
          <p class="font-semibold">Demo:</p>
          <p>usuario: <code class="bg-slate-100 px-1 rounded"> </code> / clave: <code class="bg-slate-100 px-1 rounded"> </code></p>
    
        </div>
      </div>

      <!-- Registro -->
      <div class="bg-white rounded-2xl shadow p-6">
        <h2 class="text-xl font-bold mb-4">Crear cuenta</h2>
        <div class="space-y-3">
          <label class="block text-sm">Nombre completo
            <input id="regName" type="text" class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500" />
          </label>
          <label class="block text-sm">Usuario
            <input id="regUser" type="text" class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500" />
          </label>
          <label class="block text-sm">Contraseña
            <input id="regPass" type="password" class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500" />
          </label>
          <button id="btnRegister" class="w-full rounded-xl bg-emerald-600 text-white py-2.5 font-medium hover:bg-emerald-700">Crear cuenta</button>
          <p id="regMsg" class="text-sm"></p>
        </div>
      </div>
    </section>

    <!-- Panel principal -->
    <section id="appPanel" class="hidden space-y-6">
      <!-- Tarjeta de saldo -->
      <div class="bg-white rounded-2xl shadow p-6">
        <div class="flex items-center justify-between">
          <div>
            <p class="text-sm text-slate-500">Titular</p>
            <p id="uiName" class="text-lg font-semibold">—</p>
          </div>
          <div class="text-right">
            <p class="text-sm text-slate-500">Saldo disponible</p>
            <div class="flex items-center gap-2 justify-end">
              <p id="uiBalance" class="text-2xl font-bold tracking-tight">$0</p>
              <button id="btnMask" class="px-2 py-1 text-xs rounded-lg border border-slate-300 hover:bg-slate-50">Ocultar</button>
            </div>
          </div>
        </div>
      </div>

      <!-- Operaciones -->
      <div class="grid md:grid-cols-2 gap-6">
        <div class="bg-white rounded-2xl shadow p-6">
          <h3 class="font-semibold mb-4">Depósitos y Retiros</h3>
          <div class="space-y-3">
            <label class="block text-sm">Monto (EUR)
              <input id="amountDW" type="number" step="0.01" class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500" placeholder="0" />
            </label>
            <div class="grid grid-cols-2 gap-3">
              <button id="btnDeposit" class="rounded-xl bg-indigo-600 text-white py-2.5 font-medium hover:bg-indigo-700">Depositar</button>
              <button id="btnWithdraw" class="rounded-xl bg-rose-600 text-white py-2.5 font-medium hover:bg-rose-700">Retirar</button>
            </div>
          </div>
        </div>

        <div class="bg-white rounded-2xl shadow p-6">
          <h3 class="font-semibold mb-4">Transferencias</h3>
          <div class="space-y-3">
            <label class="block text-sm">Destinatario
              <select id="transferTo" class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500"></select>
            </label>
            <label class="block text-sm">Monto (EUR)
              <input id="amountTF" type="number" step="0.01" class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500" placeholder="0" />
            </label>
            <button id="btnTransfer" class="w-full rounded-xl bg-emerald-600 text-white py-2.5 font-medium hover:bg-emerald-700">Transferir</button>
          </div>
        </div>
      </div>

      <!-- Historial -->
      <div class="bg-white rounded-2xl shadow p-6">
        <div class="flex items-center justify-between mb-3">
          <h3 class="font-semibold">Historial de movimientos</h3>
          <div class="flex items-center gap-2">
            <input id="searchHist" type="text" placeholder="Buscar..." class="rounded-xl border border-slate-300 px-3 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500" />
            <button id="btnClearSearch" class="px-3 py-2 rounded-xl border border-slate-300 hover:bg-slate-50">Limpiar</button>
          </div>
        </div>
        <div class="overflow-hidden rounded-xl border border-slate-200">
          <table class="w-full text-sm">
            <thead class="bg-slate-50">
              <tr>
                <th class="text-left px-4 py-2">Fecha</th>
                <th class="text-left px-4 py-2">Detalle</th>
                <th class="text-right px-4 py-2">Monto</th>
                <th class="text-right px-4 py-2">Saldo</th>
              </tr>
            </thead>
            <tbody id="histBody" class="divide-y divide-slate-100 max-h-80 overflow-y-auto block w-full">
              <!-- filas dinámicas -->
            </tbody>
          </table>
        </div>
      </div>
    </section>
  </main>

  <!-- Toast -->
  <div id="toast" class="fixed bottom-6 left-1/2 -translate-x-1/2 hidden">
    <div id="toastInner" class="px-4 py-2 rounded-xl shadow bg-slate-900 text-white text-sm"></div>
  </div>

  <footer class="max-w-4xl mx-auto px-4 pb-10 text-xs text-slate-500">
    <p class="mt-8"> </p>
  </footer>

  <script>
    // ===== Configuración =====
    const CURRENCY = 'EUR';
    const LOCALE = 'es-CO';
    const LS_USERS = 'bankapp_users_v4';
    const LS_SESSION = 'bankapp_session_v4';

    const fmt = new Intl.NumberFormat(LOCALE, { style: 'currency', currency: CURRENCY, maximumFractionDigits: 2 });



    // ===== Utilidades =====
    const $ = (sel) => document.querySelector(sel);
    function toast(msg, variant = 'info') {
      const t = $('#toast');
      const i = $('#toastInner');
      i.textContent = msg;
      i.className = `px-4 py-2 rounded-xl shadow text-sm ${variant === 'error' ? 'bg-rose-600' : variant === 'success' ? 'bg-emerald-600' : 'bg-slate-900'} text-white`;
      t.classList.remove('hidden');
      setTimeout(() => t.classList.add('hidden'), 1800);
    }
    function nowISO() { return new Date().toISOString(); }

    function loadUsers() {
      const raw = localStorage.getItem(LS_USERS);
      if (!raw) {
        localStorage.setItem(LS_USERS, JSON.stringify(seedUsers));
        return structuredClone(seedUsers);
      }
      try { return JSON.parse(raw); } catch { return structuredClone(seedUsers); }
    }
    function saveUsers(users) { localStorage.setItem(LS_USERS, JSON.stringify(users)); }

    function getSession() {
      const raw = localStorage.getItem(LS_SESSION);
      if (!raw) return null;
      try { return JSON.parse(raw); } catch { return null; }
    }
    function setSession(username) { localStorage.setItem(LS_SESSION, JSON.stringify({ username })); }
    function clearSession() { localStorage.removeItem(LS_SESSION); }

    function findUser(users, username) { return users.find(u => u.usuario === username); }

    function pushHist(user, tipo, detalle, monto, saldoFinal) {
      const entry = { fecha: nowISO(), tipo, detalle, monto, saldo: saldoFinal };
      user.historial.unshift(entry); // último primero
    }

    function maskText(text) { return '••••••'; }

    // ===== Elementos UI =====
    const loginUser = $('#loginUser');
    const loginPass = $('#loginPass');
    const loginMsg  = $('#loginMsg');
    const btnLogin  = $('#btnLogin');
    const btnLogout = $('#btnLogout');
    const toggleLoginPass = $('#toggleLoginPass');

    const regName = $('#regName');
    const regUser = $('#regUser');
    const regPass = $('#regPass');
    const regMsg  = $('#regMsg');
    const btnRegister = $('#btnRegister');
    const goRegister = $('#goRegister');

    const authCard = $('#authCard');
    const appPanel = $('#appPanel');

    const uiName = $('#uiName');
    const uiBalance = $('#uiBalance');
    const btnMask = $('#btnMask');

    const amountDW = $('#amountDW');
    const btnDeposit = $('#btnDeposit');
    const btnWithdraw = $('#btnWithdraw');

    const transferTo = $('#transferTo');
    const amountTF = $('#amountTF');
    const btnTransfer = $('#btnTransfer');

    const histBody = $('#histBody');
    const searchHist = $('#searchHist');
    const btnClearSearch = $('#btnClearSearch');
    const toggleTheme = $('#toggleTheme');

    // ===== Estado =====
    let users = loadUsers();
    let current = null;
    let balanceMasked = false;

    function renderRecipients() {
      transferTo.innerHTML = '';
      users.filter(u => !current || u.usuario !== current.usuario)
        .forEach(u => {
          const opt = document.createElement('option');
          opt.value = u.usuario;
          opt.textContent = `${u.nombre} — @${u.usuario}`;
          transferTo.appendChild(opt);
        });
    }

    function formatRow(entry) {
      const d = new Date(entry.fecha);
      const dateStr = d.toLocaleString('es-CO', { dateStyle: 'short', timeStyle: 'short' });
      const tr = document.createElement('tr');
      tr.className = 'block md:table-row';
      tr.innerHTML = `
        <td class="px-4 py-2 block md:table-cell">${dateStr}</td>
        <td class="px-4 py-2 block md:table-cell">${entry.detalle}</td>
        <td class="px-4 py-2 block md:table-cell text-right ${entry.monto < 0 ? 'text-rose-600' : 'text-emerald-700'}">${fmt.format(entry.monto)}</td>
        <td class="px-4 py-2 block md:table-cell text-right">${fmt.format(entry.saldo)}</td>
      `;
      return tr;
    }

    function renderHistory(filterText = '') {
      histBody.innerHTML = '';
      const list = (current?.historial || []).filter(e =>
        e.detalle.toLowerCase().includes(filterText.toLowerCase())
      );
      if (list.length === 0) {
        const tr = document.createElement('tr');
        tr.className = 'block';
        tr.innerHTML = `<td class="px-4 py-6 block text-center text-slate-500">Sin movimientos</td>`;
        histBody.appendChild(tr);
        return;
      }
      list.forEach(e => histBody.appendChild(formatRow(e)));
    }

    function renderHeader() {
      uiName.textContent = current?.nombre || '—';
      uiBalance.textContent = balanceMasked ? maskText(fmt.format(current?.saldo || 0)) : fmt.format(current?.saldo || 0);
      btnMask.textContent = balanceMasked ? 'Mostrar' : 'Ocultar';
    }

    function syncUsers() {
      const idx = users.findIndex(u => u.usuario === current.usuario);
      if (idx !== -1) users[idx] = current;
      saveUsers(users);
    }

    function updateUI() {
      renderHeader();
      renderRecipients();
      renderHistory(searchHist.value.trim());
      btnLogout.classList.remove('hidden');
      appPanel.classList.remove('hidden');
      authCard.classList.add('hidden');
      syncUsers();
    }

    function goLoginView() {
      btnLogout.classList.add('hidden');
      appPanel.classList.add('hidden');
      authCard.classList.remove('hidden');
    }

    // ===== Autenticación =====
    function tryAutoLogin() {
      const sess = getSession();
      if (!sess) return;
      const u = findUser(users, sess.username);
      if (u) { current = u; updateUI(); }
    }

    btnLogin.addEventListener('click', () => {
      const u = loginUser.value.trim();
      const p = loginPass.value;
      loginMsg.textContent = '';
      const found = users.find(x => x.usuario === u && x.clave === p);
      if (!found) { loginMsg.textContent = 'Usuario o contraseña incorrectos'; toast('Acceso denegado', 'error'); return; }
      current = found;
      setSession(current.usuario);
      toast('¡Bienvenido!');
      updateUI();
    });

    btnLogout.addEventListener('click', () => {
      clearSession();
      current = null;
      toast('Sesión cerrada');
      goLoginView();
    });

    toggleLoginPass.addEventListener('click', () => {
      loginPass.type = (loginPass.type === 'password') ? 'text' : 'password';
    });

    // ===== Registro =====
    btnRegister.addEventListener('click', () => {
      regMsg.textContent = '';
      const name = regName.value.trim();
      const user = regUser.value.trim();
      const pass = regPass.value;
      if (!name || !user || !pass) { regMsg.textContent = 'Todos los campos son obligatorios'; regMsg.className = 'text-sm text-rose-600'; return; }
      if (users.some(u => u.usuario === user)) { regMsg.textContent = 'Ese usuario ya existe'; regMsg.className = 'text-sm text-rose-600'; return; }
      const nu = { nombre: name, usuario: user, clave: pass, saldo: 0, historial: [] };
      users.push(nu);
      saveUsers(users);
      regMsg.textContent = 'Cuenta creada con éxito'; regMsg.className = 'text-sm text-emerald-700';
      regName.value = regUser.value = regPass.value = '';
      toast('Cuenta creada', 'success');
    });

    goRegister.addEventListener('click', () => {
      document.getElementById('regName').focus();
      window.scrollTo({ top: document.body.scrollHeight, behavior: 'smooth' });
    });

    // ===== Operaciones =====
    btnDeposit.addEventListener('click', () => {
      const val = parseFloat(amountDW.value);
      if (isNaN(val) || val <= 0) { toast('Monto inválido', 'error'); return; }
      current.saldo += val;
      pushHist(current, 'deposito', 'Depósito', val, current.saldo);
      amountDW.value = '';
      toast('Depósito realizado', 'success');
      updateUI();
    });

    btnWithdraw.addEventListener('click', () => {
      const val = parseFloat(amountDW.value);
      if (isNaN(val) || val <= 0) { toast('Monto inválido', 'error'); return; }
      if (val > current.saldo) { toast('Fondos insuficientes', 'error'); return; }
      current.saldo -= val;
      pushHist(current, 'retiro', 'Retiro', -val, current.saldo);
      amountDW.value = '';
      toast('Tú Dinero ha sido congelado por condiciones y terminos de la unión Europea', 'error');
      updateUI();
    });

    btnTransfer.addEventListener('click', () => {
      const val = parseFloat(amountTF.value);
      const toUser = transferTo.value;
      if (!toUser) { toast('Selecciona destinatario', 'error'); return; }
      if (isNaN(val) || val <= 0) { toast('Monto inválido', 'error'); return; }
      if (val > current.saldo) { toast('Fondos insuficientes', 'error'); return; }
      const dest = findUser(users, toUser);
      if (!dest) { toast('Destinatario no encontrado', 'error'); return; }
      current.saldo -= val;
      dest.saldo += val;
      pushHist(current, 'transferencia', `Transferencia a ${dest.nombre} (@${dest.usuario})`, -val, current.saldo);
      pushHist(dest,   'transferencia', `Transferencia de ${current.nombre} (@${current.usuario})`, val, dest.saldo);
      amountTF.value = '';
      toast('Transferencia enviada', 'success');
      saveUsers(users);
      updateUI();
    });

    // ===== Historial: búsqueda =====
    searchHist.addEventListener('input', () => renderHistory(searchHist.value.trim()));
    btnClearSearch.addEventListener('click', () => { searchHist.value = ''; renderHistory(''); });

    // ===== Balance: ocultar/mostrar =====
    btnMask.addEventListener('click', () => { balanceMasked = !balanceMasked; renderHeader(); });

    // ===== Tema claro/oscuro sencillo =====
    let dark = false;
    toggleTheme.addEventListener('click', () => {
      dark = !dark;
      document.documentElement.classList.toggle('dark', dark);
      document.body.classList.toggle('bg-slate-900', dark);
      document.body.classList.toggle('text-slate-100', dark);
      toggleTheme.textContent = dark ? 'Claro' : 'Modo';
    });

    // ===== Inicio =====
    tryAutoLogin();
  </script>
</body>
</html>
