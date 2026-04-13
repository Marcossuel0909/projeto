<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Feira dos Retalhos</title>
  <style>
    :root {
      --primary: #c0001a;
      --primary-dark: #8b0013;
      --primary-light: #ff1f3a;
      --black: #111111;
      --black-soft: #1e1e1e;
      --bg: #f5f5f5;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: 'Segoe UI', sans-serif; background: var(--bg); color: #222; }

    /* HEADER */
    header {
      background: var(--black);
      color: #fff;
      padding: 0 40px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      border-bottom: 3px solid var(--primary);
      min-height: 70px;
    }
    .header-brand { display: flex; flex-direction: column; }
    header h1 {
      font-size: 1.6rem;
      letter-spacing: 3px;
      text-transform: uppercase;
      color: #fff;
    }
    header h1 span { color: var(--primary); }
    header small { font-size: 0.7rem; letter-spacing: 2px; color: #888; text-transform: uppercase; }

    .header-nav { display: flex; gap: 10px; }
    .header-nav button {
      background: none;
      border: 1.5px solid #fff;
      color: #fff;
      padding: 7px 18px;
      border-radius: 20px;
      cursor: pointer;
      font-size: 0.86rem;
      font-weight: 600;
      transition: all 0.2s;
    }
    .header-nav button:hover { background: var(--primary); border-color: var(--primary); color: #fff; }
    .header-nav button.active { background: var(--primary); border-color: var(--primary); color: #fff; }

    /* MAIN */
    .main { max-width: 1200px; margin: 0 auto; padding: 30px 20px; }

    /* TABS */
    .tabs { display: flex; gap: 10px; margin-bottom: 28px; }
    .tab-btn {
      padding: 10px 28px;
      border: none;
      border-radius: 25px;
      background: #ddd;
      cursor: pointer;
      font-size: 0.95rem;
      font-weight: 600;
      color: #555;
      transition: background 0.2s, color 0.2s;
    }
    .tab-btn.active { background: var(--primary); color: #fff; }
    .tab-btn:hover:not(.active) { background: #ccc; }

    #panel-adicionar { display: none; }
    #panel-catalogo { display: block; }

    /* FORM CARD */
    .form-card {
      background: #fff;
      border-radius: 16px;
      padding: 32px;
      max-width: 620px;
      box-shadow: 0 2px 20px rgba(0,0,0,0.09);
      border-top: 4px solid var(--primary);
    }
    .form-card h2 { margin-bottom: 22px; font-size: 1.25rem; color: var(--black); }
    .form-group { margin-bottom: 18px; }
    .form-group label { display: block; margin-bottom: 6px; font-weight: 600; font-size: 0.9rem; color: #333; }
    .form-group input, .form-group textarea, .form-group select {
      width: 100%;
      padding: 10px 14px;
      border: 1.5px solid #ddd;
      border-radius: 8px;
      font-size: 0.97rem;
      transition: border 0.2s, box-shadow 0.2s;
      background: #fafafa;
      font-family: inherit;
    }
    .form-group input:focus, .form-group textarea:focus, .form-group select:focus {
      border-color: var(--primary);
      outline: none;
      background: #fff;
      box-shadow: 0 0 0 3px rgba(192,0,26,0.1);
    }
    .form-group textarea { resize: vertical; min-height: 80px; }
    .form-row { display: flex; gap: 14px; }
    .form-row .form-group { flex: 1; }

    /* UPLOAD */
    .upload-area {
      border: 2px dashed #ccc;
      border-radius: 12px;
      padding: 28px;
      text-align: center;
      cursor: pointer;
      transition: border 0.2s, background 0.2s;
      background: #fafafa;
      position: relative;
    }
    .upload-area:hover { border-color: var(--primary); background: #fff5f5; }
    .upload-area input[type="file"] {
      position: absolute; inset: 0; opacity: 0; cursor: pointer; width: 100%; height: 100%;
    }
    .upload-area .icon { font-size: 2.5rem; margin-bottom: 8px; }
    .upload-area p { font-size: 0.88rem; color: #666; }
    .preview-imgs { display: flex; flex-wrap: wrap; gap: 10px; margin-top: 14px; }
    .preview-imgs img {
      width: 80px; height: 80px; object-fit: cover;
      border-radius: 8px; border: 2px solid var(--primary);
    }

    /* BUTTON */
    .btn-primary {
      background: var(--primary);
      color: #fff;
      border: none;
      border-radius: 10px;
      padding: 13px 32px;
      font-size: 1rem;
      font-weight: 700;
      cursor: pointer;
      width: 100%;
      margin-top: 6px;
      letter-spacing: 0.5px;
      transition: background 0.2s, transform 0.1s;
    }
    .btn-primary:hover { background: var(--primary-dark); }
    .btn-primary:active { transform: scale(0.98); }

    /* TOAST */
    #toast {
      display: none;
      position: fixed;
      bottom: 30px; right: 30px;
      background: var(--primary);
      color: #fff;
      padding: 14px 28px;
      border-radius: 12px;
      font-weight: 600;
      font-size: 1rem;
      z-index: 9999;
      box-shadow: 0 4px 20px rgba(192,0,26,0.35);
    }

    /* CATALOG */
    .catalog-header {
      display: flex; align-items: center; justify-content: space-between;
      margin-bottom: 22px; flex-wrap: wrap; gap: 12px;
    }
    .catalog-header h2 { font-size: 1.3rem; color: var(--black); }
    .search-bar {
      padding: 9px 16px;
      border: 1.5px solid #ddd;
      border-radius: 25px;
      font-size: 0.95rem;
      min-width: 220px;
      background: #fff;
      font-family: inherit;
      transition: border 0.2s;
    }
    .search-bar:focus { outline: none; border-color: var(--primary); box-shadow: 0 0 0 3px rgba(192,0,26,0.1); }

    .produtos-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(230px, 1fr));
      gap: 22px;
    }
    .produto-card {
      background: #fff;
      border-radius: 14px;
      overflow: hidden;
      box-shadow: 0 2px 12px rgba(0,0,0,0.08);
      transition: transform 0.2s, box-shadow 0.2s;
      position: relative;
    }
    .produto-card:hover { transform: translateY(-4px); box-shadow: 0 8px 28px rgba(192,0,26,0.15); }
    .produto-card img { width: 100%; height: 230px; object-fit: cover; display: block; }
    .produto-card .no-img {
      width: 100%; height: 230px;
      display: flex; align-items: center; justify-content: center;
      background: linear-gradient(135deg, #f0f0f0, #e0e0e0);
      font-size: 3rem; color: #bbb;
    }
    .produto-info { padding: 14px 16px 18px; }
    .produto-info .marca {
      font-size: 0.72rem; font-weight: 700; letter-spacing: 1.5px;
      color: var(--primary); text-transform: uppercase; margin-bottom: 4px;
    }
    .produto-info .nome { font-size: 1rem; font-weight: 700; margin-bottom: 6px; color: var(--black); }
    .produto-info .valor { font-size: 1.2rem; font-weight: 800; color: var(--primary); }
    .produto-info .descricao {
      font-size: 0.83rem; color: #666; margin-top: 6px;
      display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden;
      line-clamp: 2;
    }
    .badge-categoria {
      position: absolute; top: 12px; left: 12px;
      background: var(--primary);
      color: #fff; font-size: 0.68rem;
      padding: 3px 10px; border-radius: 20px;
      font-weight: 700; text-transform: uppercase; letter-spacing: 0.5px;
    }
    .btn-excluir {
      position: absolute; top: 10px; right: 10px;
      background: rgba(255,255,255,0.92);
      border: none; border-radius: 50%;
      width: 30px; height: 30px;
      font-size: 1rem; cursor: pointer;
      display: flex; align-items: center; justify-content: center;
      opacity: 0; transition: opacity 0.2s;
    }
    .produto-card:hover .btn-excluir { opacity: 1; }
    .btn-excluir:hover { background: var(--primary); color: #fff; }

    .empty-state { text-align: center; padding: 60px 20px; color: #aaa; }
    .empty-state .icon { font-size: 4rem; margin-bottom: 16px; }
    .empty-state p { font-size: 1rem; }

    .count-badge {
      background: var(--primary);
      color: #fff;
      border-radius: 20px;
      font-size: 0.7rem;
      padding: 2px 8px;
      margin-left: 6px;
      font-weight: 700;
    }


    /* TAMANHOS */
    .tamanhos-group { display: flex; gap: 10px; flex-wrap: wrap; margin-top: 4px; }
    .tamanho-btn {
      width: 48px; height: 48px;
      border: 2px solid #ddd;
      border-radius: 8px;
      background: #fafafa;
      font-weight: 700;
      font-size: 0.9rem;
      cursor: pointer;
      color: #555;
      transition: all 0.18s;
      display: flex; align-items: center; justify-content: center;
      user-select: none;
    }
    .tamanho-btn:hover { border-color: var(--primary); color: var(--primary); background: #fff5f5; }
    .tamanho-btn.selected { background: var(--primary); border-color: var(--primary); color: #fff; }
    .tamanhos-disponiveis { display: flex; gap: 5px; flex-wrap: wrap; margin-top: 8px; }
    .tag-tamanho {
      font-size: 0.7rem; font-weight: 700;
      padding: 2px 8px;
      border: 1.5px solid #ddd;
      border-radius: 5px;
      color: #555;
      background: #f5f5f5;
    }

    /* DIVIDER */
    .form-section-title {
      font-size: 0.78rem;
      text-transform: uppercase;
      letter-spacing: 1.5px;
      color: var(--primary);
      font-weight: 700;
      margin-bottom: 14px;
      margin-top: 4px;
      border-left: 3px solid var(--primary);
      padding-left: 8px;
    }




    /* ESTOQUE */
    .estoque-badge {
      display: inline-flex; align-items: center; gap: 4px;
      font-size: 0.72rem; font-weight: 700;
      padding: 3px 9px; border-radius: 20px;
      margin-top: 8px;
    }
    .estoque-ok   { background: #e6f9ee; color: #16a34a; border: 1px solid #bbf7d0; }
    .estoque-low  { background: #fff7ed; color: #ea580c; border: 1px solid #fed7aa; }
    .estoque-zero { background: #fef2f2; color: #dc2626; border: 1px solid #fecaca; }

    /* WHATSAPP BTN */
    .btn-whatsapp {
      display: flex; align-items: center; justify-content: center; gap: 7px;
      background: #25d366;
      color: #fff;
      border: none;
      border-radius: 8px;
      padding: 9px 14px;
      font-size: 0.88rem;
      font-weight: 700;
      cursor: pointer;
      width: 100%;
      margin-top: 12px;
      text-decoration: none;
      transition: background 0.2s, transform 0.1s;
    }
    .btn-whatsapp:hover { background: #1ebe5d; transform: scale(1.02); }
    .btn-whatsapp svg { flex-shrink: 0; }

    /* ADMIN LOGIN */
    .admin-lock {
      display: inline-flex; align-items: center; gap: 6px;
      background: none; border: 1.5px solid #555;
      color: #aaa; padding: 6px 14px;
      border-radius: 20px; cursor: pointer;
      font-size: 0.8rem; font-weight: 600;
      transition: all 0.2s;
    }
    .admin-lock:hover { border-color: var(--primary); color: var(--primary); }

    .modal-overlay {
      display: none;
      position: fixed; inset: 0;
      background: rgba(0,0,0,0.7);
      z-index: 10000;
      align-items: center; justify-content: center;
    }
    .modal-overlay.open { display: flex; }
    .modal-box {
      background: #fff;
      border-radius: 16px;
      padding: 36px 32px;
      width: 100%; max-width: 380px;
      box-shadow: 0 8px 40px rgba(0,0,0,0.3);
      border-top: 4px solid var(--primary);
      text-align: center;
      position: relative;
    }
    .modal-box h3 { font-size: 1.2rem; margin-bottom: 6px; color: var(--black); }
    .modal-box p { font-size: 0.85rem; color: #888; margin-bottom: 22px; }
    .modal-box .lock-icon { font-size: 2.5rem; margin-bottom: 12px; }
    .modal-input {
      width: 100%; padding: 11px 16px;
      border: 1.5px solid #ddd; border-radius: 8px;
      font-size: 1rem; font-family: inherit;
      margin-bottom: 14px;
      transition: border 0.2s;
      text-align: center; letter-spacing: 4px;
    }
    .modal-input:focus { border-color: var(--primary); outline: none; box-shadow: 0 0 0 3px rgba(192,0,26,0.1); }
    .modal-btn {
      width: 100%; padding: 12px;
      background: var(--primary); color: #fff;
      border: none; border-radius: 8px;
      font-size: 1rem; font-weight: 700;
      cursor: pointer; transition: background 0.2s;
    }
    .modal-btn:hover { background: var(--primary-dark); }
    .modal-close {
      position: absolute; top: 12px; right: 16px;
      background: none; border: none;
      font-size: 1.3rem; cursor: pointer; color: #aaa;
    }
    .modal-close:hover { color: #333; }
    .modal-error {
      color: var(--primary); font-size: 0.82rem;
      margin-top: -8px; margin-bottom: 10px;
      display: none;
    }
    .admin-badge {
      display: none;
      background: var(--primary); color: #fff;
      font-size: 0.72rem; font-weight: 700;
      padding: 3px 10px; border-radius: 20px;
      letter-spacing: 0.5px;
    }
    .btn-sair-admin {
      background: none; border: 1.5px solid #ff6b6b;
      color: #ff6b6b; padding: 6px 14px;
      border-radius: 20px; cursor: pointer;
      font-size: 0.8rem; font-weight: 600;
      display: none; transition: all 0.2s;
    }
    .btn-sair-admin:hover { background: #ff6b6b; color: #fff; }

    @media (max-width: 600px) {
      header { flex-direction: column; gap: 14px; padding: 16px 20px; text-align: center; }
      .form-row { flex-direction: column; }
    }
  </style>
</head>
<body>

<header>
  <div class="header-brand">
    <h1>✦ Feira dos <span>Retalhos</span></h1>
    <small>Moda com estilo &amp; autenticidade</small>
  </div>
  <div class="header-nav" style="align-items:center; gap:10px;">
    <span class="admin-badge" id="admin-badge">🔑 Admin</span>
    <button class="admin-lock" id="btn-admin-lock" onclick="abrirLogin()">🔒 Admin</button>
    <button class="btn-sair-admin" id="btn-sair-admin" onclick="sairAdmin()">Sair</button>
    <button onclick="showTab('catalogo')" id="btn-header-cat" class="active">🛍️ Ver Catálogo</button>
  </div>
</header>

<div class="main">
  <div class="tabs">
    <button class="tab-btn" id="tab-adicionar" onclick="showTab('adicionar')" style="display:none">➕ Adicionar Produto</button>
    <button class="tab-btn active" id="tab-catalogo" onclick="showTab('catalogo')">🛍️ Catálogo <span class="count-badge" id="count-badge">0</span></button>
  </div>

  <!-- PAINEL ADICIONAR -->
  <div id="panel-adicionar">
    <div class="form-card">
      <h2>📦 Novo Produto</h2>

      <p class="form-section-title">Foto</p>
      <div class="form-group">
        <div class="upload-area">
          <input type="file" id="foto-input" accept="image/*" multiple onchange="previewFotos(event)" />
          <div class="icon">📷</div>
          <p>Clique para selecionar fotos<br/><small>JPG, PNG, WEBP — múltiplas fotos aceitas</small></p>
        </div>
        <div class="preview-imgs" id="preview-imgs"></div>
      </div>

      <p class="form-section-title">Informações</p>
      <div class="form-row">
        <div class="form-group">
          <label>Nome do Produto *</label>
          <input type="text" id="nome" placeholder="Ex: Vestido Floral Midi" />
        </div>
        <div class="form-group">
          <label>Marca *</label>
          <input type="text" id="marca" placeholder="Ex: Zara, Farm, H&M..." />
        </div>
      </div>

      <div class="form-row">
        <div class="form-group">
          <label>Valor (R$) *</label>
          <input type="number" id="valor" placeholder="0,00" min="0" step="0.01" />
        </div>
        <div class="form-group">
          <label>Categoria</label>
          <select id="categoria">
            <option value="">Selecione...</option>
            <option>Vestidos</option>
            <option>Blusas</option>
            <option>Calças</option>
            <option>Saias</option>
            <option>Casacos</option>
            <option>Acessórios</option>
            <option>Infantil</option>
            <option>Moda Praia</option>
            <option>Esportivo</option>
            <option>Tênis</option>
            <option>Outros</option>
          </select>
        </div>
      </div>


      <div class="form-group">
        <label>Estoque (quantidade disponível)</label>
        <input type="number" id="estoque" placeholder="Ex: 10" min="0" step="1" />
      </div>

      <div class="form-group">
        <label>Tamanhos Disponíveis</label>
        <div class="tamanhos-group" id="tamanhos-group">
          <div style="width:100%; display:flex; align-items:center; gap:8px; margin-bottom:2px;">
            <span style="font-size:0.7rem;font-weight:700;color:var(--primary);letter-spacing:1px;white-space:nowrap;">👗 ADULTO</span>
          </div>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, 'PP')">PP</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, 'P')">P</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, 'M')">M</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, 'G')">G</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, 'GG')">GG</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, 'XG')">XG</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '34')">34</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '36')">36</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '38')">38</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '40')">40</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '42')">42</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '44')">44</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '46')">46</button>
          <div style="width:100%; border-top:1.5px dashed #eee; margin:6px 0; display:flex; align-items:center; gap:8px;">
            <span style="font-size:0.7rem;font-weight:700;color:var(--primary);letter-spacing:1px;white-space:nowrap;">👶 INFANTIL</span>
          </div>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, 'P Inf')">P</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, 'M Inf')">M</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, 'G Inf')">G</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, 'GG Inf')">GG</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '01')">01</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '02')">02</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '03')">03</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '04')">04</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '06')">06</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '08')">08</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '10')">10</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '12')">12</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '14')">14</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '16')">16</button>
          <button type="button" class="tamanho-btn" onclick="toggleTamanho(this, '18')">18</button>
        </div>
      </div>

      <div class="form-group">
        <label>Descrição</label>
        <textarea id="descricao" placeholder="Tecido, caimento, tamanhos disponíveis..."></textarea>
      </div>

      <button class="btn-primary" onclick="adicionarProduto()">✓ Adicionar ao Catálogo</button>
    </div>
  </div>

  <!-- PAINEL CATÁLOGO -->
  <div id="panel-catalogo">
    <div class="catalog-header">
      <h2>🛍️ Catálogo de Produtos</h2>
      <input class="search-bar" type="text" id="busca" placeholder="🔍 Buscar produto ou marca..." oninput="filtrarProdutos()" />
    </div>
    <div class="produtos-grid" id="produtos-grid">
      <div class="empty-state" style="grid-column:1/-1">
        <div class="icon">👗</div>
        <p>Nenhum produto adicionado ainda.<br/>Vá em <strong>Adicionar Produto</strong> para começar!</p>
      </div>
    </div>
  </div>
</div>


<!-- MODAL LOGIN ADMIN -->
<div class="modal-overlay" id="modal-login">
  <div class="modal-box">
    <button class="modal-close" onclick="fecharLogin()">✕</button>
    <div class="lock-icon">🔐</div>
    <h3>Área Administrativa</h3>
    <p>Digite a senha para acessar o painel de gerenciamento</p>
    <input class="modal-input" type="password" id="senha-input" placeholder="••••••" onkeydown="if(event.key==='Enter')verificarSenha()" />
    <p class="modal-error" id="modal-error">❌ Senha incorreta. Tente novamente.</p>
    <button class="modal-btn" onclick="verificarSenha()">Entrar</button>
  </div>
</div>

<div id="toast">✅ Produto adicionado com sucesso!</div>

<script>
  let produtos = JSON.parse(localStorage.getItem('feiraretalhos_produtos') || '[]');
  let fotosBase64 = [];

  function showTab(tab) {
    document.getElementById('panel-adicionar').style.display = tab === 'adicionar' ? 'block' : 'none';
    document.getElementById('panel-catalogo').style.display = tab === 'catalogo' ? 'block' : 'none';
    document.getElementById('tab-adicionar').classList.toggle('active', tab === 'adicionar');
    document.getElementById('tab-catalogo').classList.toggle('active', tab === 'catalogo');
    document.getElementById('btn-header-add').classList.toggle('active', tab === 'adicionar');
    document.getElementById('btn-header-cat').classList.toggle('active', tab === 'catalogo');
    if (tab === 'catalogo') renderProdutos();
  }

  function previewFotos(event) {
    fotosBase64 = [];
    const preview = document.getElementById('preview-imgs');
    preview.innerHTML = '';
    Array.from(event.target.files).forEach(file => {
      const reader = new FileReader();
      reader.onload = e => {
        fotosBase64.push(e.target.result);
        const img = document.createElement('img');
        img.src = e.target.result;
        preview.appendChild(img);
      };
      reader.readAsDataURL(file);
    });
  }

  function adicionarProduto() {
    const nome = document.getElementById('nome').value.trim();
    const marca = document.getElementById('marca').value.trim();
    const valor = parseFloat(document.getElementById('valor').value);
    const categoria = document.getElementById('categoria').value;
    const descricao = document.getElementById('descricao').value.trim();
    const tamanhos = Array.from(document.querySelectorAll('.tamanho-btn.selected')).map(b => b.dataset.tam || b.textContent.trim());
    const estoque = document.getElementById('estoque').value !== '' ? parseInt(document.getElementById('estoque').value) : null;

    if (!nome || !marca || isNaN(valor) || valor < 0) {
      alert('⚠️ Preencha Nome, Marca e Valor corretamente.');
      return;
    }

    produtos.push({ id: Date.now(), nome, marca, valor, categoria, descricao, tamanhos, estoque, foto: fotosBase64[0] || null });
    localStorage.setItem('feiraretalhos_produtos', JSON.stringify(produtos));
    atualizarContador();
    showTab('catalogo');
    limparForm();
    mostrarToast();
  }

  function limparForm() {
    ['nome','marca','valor','descricao'].forEach(id => document.getElementById(id).value = '');
    document.getElementById('categoria').value = '';
    document.getElementById('foto-input').value = '';
    document.getElementById('preview-imgs').innerHTML = '';
    document.getElementById('estoque').value = '';
    document.querySelectorAll('.tamanho-btn.selected').forEach(b => b.classList.remove('selected'));
    fotosBase64 = [];
  }

  function mostrarToast() {
    const t = document.getElementById('toast');
    t.style.display = 'block';
    setTimeout(() => t.style.display = 'none', 2800);
  }

  function atualizarContador() {
    document.getElementById('count-badge').textContent = produtos.length;
  }

  function renderProdutos(lista) {
    const grid = document.getElementById('produtos-grid');
    const arr = lista !== undefined ? lista : produtos;
    if (arr.length === 0) {
      grid.innerHTML = '<div class="empty-state" style="grid-column:1/-1"><div class="icon">👗</div><p>Nenhum produto encontrado.</p></div>';
      return;
    }
    grid.innerHTML = arr.map(p => `
      <div class="produto-card">
        ${p.foto ? `<img src="${p.foto}" alt="${p.nome}" />` : '<div class="no-img">👗</div>'}
        ${p.categoria ? `<span class="badge-categoria">${p.categoria}</span>` : ''}
        <button class="btn-excluir" title="Excluir" onclick="excluirProduto(${p.id})">✕</button>
        <div class="produto-info">
          <div class="marca">${p.marca}</div>
          <div class="nome">${p.nome}</div>
          <div class="valor">R$ ${p.valor.toFixed(2).replace('.', ',')}</div>
          ${p.tamanhos && p.tamanhos.length ? `<div class="tamanhos-disponiveis">${p.tamanhos.map(t => `<span class="tag-tamanho">${t}</span>`).join('')}</div>` : ''}
          ${p.descricao ? `<div class="descricao">${p.descricao}</div>` : ''}
          ${p.estoque !== null && p.estoque !== undefined
            ? p.estoque === 0
              ? '<span class="estoque-badge estoque-zero">❌ Esgotado</span>'
              : p.estoque <= 3
                ? `<span class="estoque-badge estoque-low">⚠️ Últimas ${p.estoque} unid.</span>`
                : `<span class="estoque-badge estoque-ok">✅ ${p.estoque} em estoque</span>`
            : ''}
          <a class="btn-whatsapp" href="${gerarLinkWA(p)}" target="_blank" rel="noopener">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="white"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347z"/><path d="M12 0C5.373 0 0 5.373 0 12c0 2.117.554 4.103 1.523 5.824L.057 23.882a.5.5 0 0 0 .606.63l6.288-1.643A11.945 11.945 0 0 0 12 24c6.627 0 12-5.373 12-12S18.627 0 12 0zm0 21.894a9.877 9.877 0 0 1-5.031-1.378l-.36-.214-3.733.976.998-3.645-.235-.374A9.855 9.855 0 0 1 2.106 12C2.106 6.53 6.53 2.106 12 2.106c5.47 0 9.894 4.424 9.894 9.894 0 5.47-4.424 9.894-9.894 9.894z"/></svg>
            Comprar via WhatsApp
          </a>
        </div>
      </div>
    `).join('');
  }

  function filtrarProdutos() {
    const q = document.getElementById('busca').value.toLowerCase();
    renderProdutos(produtos.filter(p =>
      p.nome.toLowerCase().includes(q) ||
      p.marca.toLowerCase().includes(q) ||
      (p.categoria || '').toLowerCase().includes(q)
    ));
  }

  function excluirProduto(id) {
    if (!confirm('Deseja excluir este produto?')) return;
    produtos = produtos.filter(p => p.id !== id);
    localStorage.setItem('feiraretalhos_produtos', JSON.stringify(produtos));
    atualizarContador();
    renderProdutos();
  }

  const WA_NUMBER = '5562984710021';

  function gerarLinkWA(p) {
    const tamanhos = p.tamanhos && p.tamanhos.length ? ' | Tamanhos: ' + p.tamanhos.join(', ') : '';
    const msg = `Olá! Tenho interesse no produto:\n\n` +
      `*${p.nome}*\n` +
      `Marca: ${p.marca}\n` +
      `Valor: R$ ${p.valor.toFixed(2).replace('.', ',')}` +
      tamanhos;
    return 'https://wa.me/' + WA_NUMBER + '?text=' + encodeURIComponent(msg);
  }

  // ---- ADMIN ----
  const SENHA_ADMIN = 'retalhos123'; // ← mude aqui sua senha
  let isAdmin = false;

  function abrirLogin() {
    document.getElementById('modal-login').classList.add('open');
    setTimeout(() => document.getElementById('senha-input').focus(), 100);
  }
  function fecharLogin() {
    document.getElementById('modal-login').classList.remove('open');
    document.getElementById('senha-input').value = '';
    document.getElementById('modal-error').style.display = 'none';
  }
  function verificarSenha() {
    const senha = document.getElementById('senha-input').value;
    if (senha === SENHA_ADMIN) {
      isAdmin = true;
      fecharLogin();
      document.getElementById('tab-adicionar').style.display = '';
      document.getElementById('btn-admin-lock').style.display = 'none';
      document.getElementById('admin-badge').style.display = 'inline-flex';
      document.getElementById('btn-sair-admin').style.display = 'inline-block';
      showTab('adicionar');
    } else {
      document.getElementById('modal-error').style.display = 'block';
      document.getElementById('senha-input').value = '';
      document.getElementById('senha-input').focus();
    }
  }
  function sairAdmin() {
    isAdmin = false;
    document.getElementById('tab-adicionar').style.display = 'none';
    document.getElementById('btn-admin-lock').style.display = '';
    document.getElementById('admin-badge').style.display = 'none';
    document.getElementById('btn-sair-admin').style.display = 'none';
    showTab('catalogo');
  }

  function toggleTamanho(btn, tam) {
    btn.classList.toggle('selected');
  }

  atualizarContador();
  showTab('catalogo');
</script>
</body>
</html>
