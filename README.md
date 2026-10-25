# kasir
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>BrewPOS - Sistem Kasir Coffee Shop</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --primary: #6F4E37;
      --primary-dark: #4A3220;
      --primary-light: #A67C52;
      --accent: #D4A574;
      --bg: #F8F1E9;
      --card: #FFFFFF;
      --text: #2C1810;
      --text-light: #6B4E3D;
      --success: #2E7D32;
      --danger: #C62828;
      --warning: #F9A825;
      --info: #1565C0;
      --border: #E8D5C4;
      --shadow: 0 4px 20px rgba(111, 78, 55, 0.12);
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      font-family: 'Poppins', sans-serif;
      background: var(--bg);
      color: var(--text);
      min-height: 100vh;
    }

    .layout { display: flex; min-height: 100vh; }

    /* ===== SIDEBAR ===== */
    .sidebar {
      width: 250px;
      background: linear-gradient(180deg, var(--primary-dark), var(--primary));
      color: white;
      padding: 24px 16px;
      display: flex;
      flex-direction: column;
      position: fixed;
      height: 100vh;
      z-index: 100;
      transition: transform 0.3s ease;
    }

    .logo {
      display: flex;
      align-items: center;
      gap: 12px;
      padding: 0 8px 24px;
      border-bottom: 1px solid rgba(255,255,255,0.15);
      margin-bottom: 20px;
    }

    .logo-icon {
      width: 44px; height: 44px;
      background: var(--accent);
      border-radius: 12px;
      display: flex; align-items: center; justify-content: center;
      font-size: 22px;
    }

    .logo h1 { font-size: 18px; font-weight: 600; line-height: 1.2; }
    .logo span { font-size: 11px; opacity: 0.7; }

    .nav-menu { display: flex; flex-direction: column; gap: 4px; flex: 1; }

    .nav-item {
      display: flex; align-items: center; gap: 12px;
      padding: 12px 14px;
      border-radius: 10px;
      cursor: pointer;
      transition: all 0.2s;
      font-size: 13.5px;
      font-weight: 500;
      color: rgba(255,255,255,0.75);
    }

    .nav-item:hover { background: rgba(255,255,255,0.1); color: white; }
    .nav-item.active {
      background: rgba(255,255,255,0.18);
      color: white;
      box-shadow: inset 0 0 0 1px rgba(255,255,255,0.15);
    }
    .nav-item .icon { font-size: 17px; width: 24px; text-align: center; }

    .sidebar-footer {
      padding-top: 16px;
      border-top: 1px solid rgba(255,255,255,0.15);
      font-size: 11px;
      opacity: 0.55;
      text-align: center;
      line-height: 1.5;
    }

    /* ===== MAIN ===== */
    .main {
      flex: 1;
      margin-left: 250px;
      padding: 28px 32px;
      max-width: 1400px;
    }

    .page-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 24px;
      flex-wrap: wrap;
      gap: 12px;
    }

    .page-header h2 { font-size: 22px; font-weight: 600; }
    .page-header p { color: var(--text-light); font-size: 13px; margin-top: 3px; }

    /* ===== STATS ===== */
    .stats-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 16px;
      margin-bottom: 24px;
    }

    .stat-card {
      background: var(--card);
      border-radius: 14px;
      padding: 20px;
      box-shadow: var(--shadow);
      border: 1px solid var(--border);
      position: relative;
      overflow: hidden;
    }

    .stat-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0;
      width: 4px; height: 100%;
      background: var(--primary);
    }

    .stat-card.green::before { background: var(--success); }
    .stat-card.orange::before { background: var(--warning); }
    .stat-card.red::before { background: var(--danger); }
    .stat-card.blue::before { background: var(--info); }

    .stat-label { font-size: 12px; color: var(--text-light); margin-bottom: 6px; }
    .stat-value { font-size: 24px; font-weight: 700; }
    .stat-sub { font-size: 11px; color: var(--text-light); margin-top: 4px; }

    /* ===== CARD ===== */
    .card {
      background: var(--card);
      border-radius: 14px;
      padding: 22px;
      box-shadow: var(--shadow);
      border: 1px solid var(--border);
      margin-bottom: 20px;
    }

    .card-title {
      font-size: 15px;
      font-weight: 600;
      margin-bottom: 16px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 8px;
    }

    /* ===== BUTTONS ===== */
    .btn {
      display: inline-flex;
      align-items: center;
      gap: 7px;
      padding: 10px 16px;
      border-radius: 9px;
      font-family: inherit;
      font-size: 13px;
      font-weight: 500;
      cursor: pointer;
      border: none;
      transition: all 0.2s;
    }

    .btn-primary { background: var(--primary); color: white; }
    .btn-primary:hover { background: var(--primary-dark); transform: translateY(-1px); }
    .btn-success { background: var(--success); color: white; }
    .btn-success:hover { background: #1B5E20; }
    .btn-danger { background: var(--danger); color: white; }
    .btn-danger:hover { background: #B71C1C; }
    .btn-warning { background: var(--warning); color: #3E2723; }
    .btn-outline {
      background: transparent;
      border: 1.5px solid var(--border);
      color: var(--text);
    }
    .btn-outline:hover { border-color: var(--primary); color: var(--primary); }
    .btn-sm { padding: 6px 11px; font-size: 12px; border-radius: 7px; }
    .btn-icon {
      width: 34px; height: 34px;
      padding: 0;
      justify-content: center;
      border-radius: 8px;
    }
    .btn:disabled { opacity: 0.5; cursor: not-allowed; transform: none !important; }

    /* ===== FORM ===== */
    .form-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
      gap: 14px;
      margin-bottom: 14px;
    }

    .form-group { display: flex; flex-direction: column; gap: 5px; }
    .form-group label { font-size: 12px; font-weight: 500; color: var(--text-light); }

    .form-group input,
    .form-group select,
    .form-group textarea {
      padding: 10px 13px;
      border: 1.5px solid var(--border);
      border-radius: 9px;
      font-family: inherit;
      font-size: 13.5px;
      background: #FFFCFA;
      transition: border-color 0.2s;
      color: var(--text);
    }

    .form-group input:focus,
    .form-group select:focus,
    .form-group textarea:focus {
      outline: none;
      border-color: var(--primary);
      box-shadow: 0 0 0 3px rgba(111, 78, 55, 0.12);
    }

    /* ===== TABLE ===== */
    .table-wrap { overflow-x: auto; }

    table { width: 100%; border-collapse: collapse; font-size: 13px; }

    th {
      text-align: left;
      padding: 11px 12px;
      background: #F5EDE4;
      color: var(--text-light);
      font-weight: 600;
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.3px;
      white-space: nowrap;
    }

    td {
      padding: 12px;
      border-bottom: 1px solid var(--border);
      vertical-align: middle;
    }

    tr:last-child td { border-bottom: none; }
    tr:hover td { background: #FBF7F2; }

    .badge {
      display: inline-block;
      padding: 3px 9px;
      border-radius: 20px;
      font-size: 11px;
      font-weight: 500;
      white-space: nowrap;
    }

    .badge-success { background: #E8F5E9; color: var(--success); }
    .badge-warning { background: #FFF8E1; color: #F57F17; }
    .badge-danger { background: #FFEBEE; color: var(--danger); }
    .badge-info { background: #E3F2FD; color: var(--info); }
    .badge-neutral { background: #F5F5F5; color: #616161; }

    /* ===== POS ===== */
    .pos-layout {
      display: grid;
      grid-template-columns: 1fr 340px;
      gap: 20px;
      align-items: start;
    }

    .product-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
      gap: 12px;
    }

    .product-card {
      background: var(--card);
      border: 1.5px solid var(--border);
      border-radius: 12px;
      padding: 14px 10px;
      cursor: pointer;
      transition: all 0.2s;
      text-align: center;
    }

    .product-card:hover {
      border-color: var(--primary);
      transform: translateY(-2px);
      box-shadow: var(--shadow);
    }

    .product-card.out-of-stock { opacity: 0.45; cursor: not-allowed; }
    .product-emoji { font-size: 32px; margin-bottom: 6px; }
    .product-name { font-size: 12.5px; font-weight: 600; margin-bottom: 3px; line-height: 1.3; }
    .product-price { font-size: 13px; font-weight: 700; color: var(--primary); }
    .product-stock { font-size: 10.5px; color: var(--text-light); margin-top: 3px; }

    /* CART */
    .cart-panel {
      background: var(--card);
      border-radius: 14px;
      border: 1px solid var(--border);
      box-shadow: var(--shadow);
      position: sticky;
      top: 24px;
      display: flex;
      flex-direction: column;
      max-height: calc(100vh - 48px);
    }

    .cart-header {
      padding: 16px 18px;
      border-bottom: 1px solid var(--border);
      font-weight: 600;
      font-size: 15px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .cart-items {
      flex: 1;
      overflow-y: auto;
      padding: 10px 14px;
      min-height: 160px;
    }

    .cart-item {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 10px 0;
      border-bottom: 1px solid var(--border);
    }

    .cart-item:last-child { border-bottom: none; }
    .cart-item-info { flex: 1; min-width: 0; }
    .cart-item-name { font-size: 12.5px; font-weight: 600; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
    .cart-item-price { font-size: 11px; color: var(--text-light); }

    .qty-control { display: flex; align-items: center; gap: 6px; }

    .qty-btn {
      width: 26px; height: 26px;
      border-radius: 7px;
      border: 1.5px solid var(--border);
      background: white;
      cursor: pointer;
      font-size: 13px;
      display: flex; align-items: center; justify-content: center;
      transition: all 0.15s;
    }

    .qty-btn:hover { border-color: var(--primary); color: var(--primary); }
    .qty-value { font-weight: 600; font-size: 13px; min-width: 18px; text-align: center; }

    .cart-footer {
      padding: 14px 18px;
      border-top: 1px solid var(--border);
      background: #FBF7F2;
      border-radius: 0 0 14px 14px;
    }

    .cart-total-row {
      display: flex;
      justify-content: space-between;
      margin-bottom: 6px;
      font-size: 13px;
    }

    .cart-total-row.grand {
      font-size: 17px;
      font-weight: 700;
      color: var(--primary);
      margin-top: 6px;
      padding-top: 8px;
      border-top: 1.5px dashed var(--border);
    }

    .empty-cart {
      text-align: center;
      padding: 36px 16px;
      color: var(--text-light);
    }

    .empty-cart .icon { font-size: 42px; margin-bottom: 10px; opacity: 0.35; }

    /* ===== FILTER ===== */
    .filter-bar {
      display: flex;
      gap: 10px;
      margin-bottom: 16px;
      flex-wrap: wrap;
      align-items: center;
    }

    .search-box { flex: 1; min-width: 180px; position: relative; }

    .search-box input {
      width: 100%;
      padding: 10px 13px 10px 38px;
      border: 1.5px solid var(--border);
      border-radius: 9px;
      font-family: inherit;
      font-size: 13.5px;
      background: white;
    }

    .search-box::before {
      content: '🔍';
      position: absolute;
      left: 12px;
      top: 50%;
      transform: translateY(-50%);
      font-size: 13px;
    }

    .category-tabs { display: flex; gap: 6px; flex-wrap: wrap; }

    .cat-tab {
      padding: 7px 14px;
      border-radius: 20px;
      border: 1.5px solid var(--border);
      background: white;
      font-size: 12px;
      font-weight: 500;
      cursor: pointer;
      transition: all 0.2s;
      font-family: inherit;
    }

    .cat-tab.active, .cat-tab:hover {
      background: var(--primary);
      color: white;
      border-color: var(--primary);
    }

    /* ===== MODAL ===== */
    .modal-overlay {
      position: fixed;
      inset: 0;
      background: rgba(44, 24, 16, 0.5);
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 1000;
      padding: 16px;
    }

    .modal-overlay.show { display: flex; }

    .modal {
      background: white;
      border-radius: 16px;
      width: 100%;
      max-width: 460px;
      max-height: 90vh;
      overflow-y: auto;
      box-shadow: 0 20px 60px rgba(0,0,0,0.25);
      animation: modalIn 0.25s ease;
    }

    .modal.modal-lg { max-width: 560px; }

    @keyframes modalIn {
      from { opacity: 0; transform: scale(0.95) translateY(10px); }
      to { opacity: 1; transform: scale(1) translateY(0); }
    }

    .modal-header {
      padding: 18px 22px;
      border-bottom: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .modal-header h3 { font-size: 16px; font-weight: 600; }

    .modal-close {
      width: 30px; height: 30px;
      border-radius: 7px;
      border: none;
      background: #F5EDE4;
      cursor: pointer;
      font-size: 16px;
      display: flex; align-items: center; justify-content: center;
    }

    .modal-body { padding: 20px 22px; }
    .modal-footer {
      padding: 14px 22px;
      border-top: 1px solid var(--border);
      display: flex;
      justify-content: flex-end;
      gap: 8px;
    }

    /* ===== TOAST ===== */
    .toast-container {
      position: fixed;
      top: 20px; right: 20px;
      z-index: 2000;
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    .toast {
      background: white;
      padding: 12px 18px;
      border-radius: 10px;
      box-shadow: 0 8px 30px rgba(0,0,0,0.15);
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 13px;
      font-weight: 500;
      animation: toastIn 0.3s ease;
      border-left: 4px solid var(--success);
      min-width: 260px;
    }

    .toast.error { border-left-color: var(--danger); }
    .toast.warning { border-left-color: var(--warning); }

    @keyframes toastIn {
      from { opacity: 0; transform: translateX(40px); }
      to { opacity: 1; transform: translateX(0); }
    }

    /* ===== EMPTY STATE ===== */
    .empty-state {
      text-align: center;
      padding: 40px 16px;
      color: var(--text-light);
    }

    .empty-state .icon { font-size: 48px; margin-bottom: 12px; opacity: 0.3; }
    .empty-state h3 { font-size: 15px; margin-bottom: 6px; color: var(--text); }
    .empty-state p { font-size: 13px; }

    /* ===== RECEIPT ===== */
    .receipt {
      font-family: 'Courier New', monospace;
      font-size: 12px;
      line-height: 1.5;
      background: white;
      padding: 20px;
      max-width: 300px;
      margin: 0 auto;
      border: 1px dashed #ccc;
    }

    .receipt-header { text-align: center; margin-bottom: 12px; }
    .receipt-header h3 { font-size: 15px; margin-bottom: 2px; }
    .receipt-line { border-top: 1px dashed #999; margin: 8px 0; }
    .receipt-item { display: flex; justify-content: space-between; }
    .receipt-total { font-weight: bold; font-size: 14px; }

    /* ===== RESPONSIVE ===== */
    .menu-toggle {
      display: none;
      position: fixed;
      top: 14px; left: 14px;
      z-index: 200;
      width: 42px; height: 42px;
      border-radius: 11px;
      background: var(--primary);
      color: white;
      border: none;
      font-size: 18px;
      cursor: pointer;
      box-shadow: var(--shadow);
      align-items: center;
      justify-content: center;
    }

    @media (max-width: 900px) {
      .sidebar { transform: translateX(-100%); }
      .sidebar.open { transform: translateX(0); }
      .main { margin-left: 0; padding: 18px 14px; padding-top: 68px; }
      .menu-toggle { display: flex; }
      .pos-layout { grid-template-columns: 1fr; }
      .cart-panel { position: relative; top: 0; max-height: none; }
    }

    .hidden { display: none !important; }
    .text-right { text-align: right; }
    .text-center { text-align: center; }
    .mt-1 { margin-top: 6px; }
    .mt-2 { margin-top: 10px; }
    .mb-2 { margin-bottom: 10px; }
    .gap-8 { gap: 8px; }
    .flex { display: flex; }
    .flex-wrap { flex-wrap: wrap; }
    .items-center { align-items: center; }

    /* Print styles */
    @media print {
      body * { visibility: hidden; }
      #print-area, #print-area * { visibility: visible; }
      #print-area { position: absolute; left: 0; top: 0; width: 100%; }
    }
  </style>
</head>
<body>
  <button class="menu-toggle" onclick="toggleSidebar()">☰</button>

  <div class="layout">
    <!-- SIDEBAR -->
    <aside class="sidebar" id="sidebar">
      <div class="logo">
        <div class="logo-icon">☕</div>
        <div>
          <h1>BrewPOS</h1>
          <span>Coffee Shop Kasir</span>
        </div>
      </div>

      <nav class="nav-menu">
        <div class="nav-item active" data-page="dashboard" onclick="showPage('dashboard')">
          <span class="icon">📊</span> Dashboard
        </div>
        <div class="nav-item" data-page="kasir" onclick="showPage('kasir')">
          <span class="icon">🛒</span> Kasir
        </div>
        <div class="nav-item" data-page="produk" onclick="showPage('produk')">
          <span class="icon">📦</span> Produk & Stok
        </div>
        <div class="nav-item" data-page="cashflow" onclick="showPage('cashflow')">
          <span class="icon">💰</span> Cashflow
        </div>
        <div class="nav-item" data-page="riwayat" onclick="showPage('riwayat')">
          <span class="icon">📋</span> Riwayat Penjualan
        </div>
        <div class="nav-item" data-page="laporan" onclick="showPage('laporan')">
          <span class="icon">📈</span> Laporan
        </div>
        <div class="nav-item" data-page="pengaturan" onclick="showPage('pengaturan')">
          <span class="icon">⚙️</span> Pengaturan
        </div>
      </nav>

      <div class="sidebar-footer">
        BrewPOS v2.0<br>
        Data tersimpan lokal di browser
      </div>
    </aside>

    <!-- MAIN -->
    <main class="main">

      <!-- ========== DASHBOARD ========== -->
      <section id="page-dashboard">
        <div class="page-header">
          <div>
            <h2>Dashboard</h2>
            <p>Ringkasan bisnis coffee shop</p>
          </div>
          <div id="today-date" style="font-size:13px;color:var(--text-light)"></div>
        </div>

        <div class="stats-grid">
          <div class="stat-card">
            <div class="stat-label">Penjualan Hari Ini</div>
            <div class="stat-value" id="stat-sales">Rp 0</div>
            <div class="stat-sub" id="stat-orders">0 transaksi</div>
          </div>
          <div class="stat-card green">
            <div class="stat-label">Saldo Kas</div>
            <div class="stat-value" id="stat-balance">Rp 0</div>
            <div class="stat-sub">Pemasukan − Pengeluaran</div>
          </div>
          <div class="stat-card orange">
            <div class="stat-label">Total Produk</div>
            <div class="stat-value" id="stat-products">0</div>
            <div class="stat-sub" id="stat-low-stock">0 stok menipis</div>
          </div>
          <div class="stat-card red">
            <div class="stat-label">Pengeluaran Hari Ini</div>
            <div class="stat-value" id="stat-expense">Rp 0</div>
            <div class="stat-sub">Biaya operasional</div>
          </div>
        </div>

        <div class="card">
          <div class="card-title">
            ⚠️ Produk Stok Menipis
            <button class="btn btn-outline btn-sm" onclick="showPage('produk')">Kelola Stok</button>
          </div>
          <div id="low-stock-list"></div>
        </div>

        <div class="card">
          <div class="card-title">Transaksi Terakhir</div>
          <div id="recent-transactions"></div>
        </div>
      </section>

      <!-- ========== KASIR ========== -->
      <section id="page-kasir" class="hidden">
        <div class="page-header">
          <div>
            <h2>Kasir</h2>
            <p>Pilih produk dan proses pembayaran</p>
          </div>
        </div>

        <div class="filter-bar">
          <div class="search-box">
            <input type="text" id="pos-search" placeholder="Cari produk..." oninput="renderPOSProducts()">
          </div>
          <div class="category-tabs" id="pos-categories"></div>
        </div>

        <div class="pos-layout">
          <div>
            <div class="product-grid" id="pos-product-grid"></div>
          </div>

          <div class="cart-panel">
            <div class="cart-header">
              Keranjang
              <button class="btn btn-outline btn-sm" onclick="clearCart()" title="Kosongkan">🗑</button>
            </div>
            <div class="cart-items" id="cart-items">
              <div class="empty-cart">
                <div class="icon">🛒</div>
                <p>Keranjang masih kosong</p>
              </div>
            </div>
            <div class="cart-footer">
              <div class="cart-total-row">
                <span>Subtotal</span>
                <span id="cart-subtotal">Rp 0</span>
              </div>
              <div class="cart-total-row grand">
                <span>Total</span>
                <span id="cart-total">Rp 0</span>
              </div>
              <button class="btn btn-success" style="width:100%;margin-top:12px;padding:12px;font-size:14px" onclick="openPaymentModal()" id="btn-checkout" disabled>
                💳 Bayar Sekarang
              </button>
            </div>
          </div>
        </div>
      </section>

      <!-- ========== PRODUK ========== -->
      <section id="page-produk" class="hidden">
        <div class="page-header">
          <div>
            <h2>Produk & Stok</h2>
            <p>Kelola daftar produk, harga, dan stok</p>
          </div>
          <div class="flex gap-8">
            <button class="btn btn-outline btn-sm" onclick="openStockModal()">📦 Adjust Stok</button>
            <button class="btn btn-primary" onclick="openProductModal()">+ Tambah Produk</button>
          </div>
        </div>

        <div class="filter-bar">
          <div class="search-box">
            <input type="text" id="product-search" placeholder="Cari produk..." oninput="renderProducts()">
          </div>
          <select id="product-filter-cat" onchange="renderProducts()" style="padding:10px 12px;border:1.5px solid var(--border);border-radius:9px;font-family:inherit;font-size:13px;background:white">
            <option value="">Semua Kategori</option>
            <option value="Kopi">Kopi</option>
            <option value="Non-Kopi">Non-Kopi</option>
            <option value="Snack">Snack</option>
            <option value="Dessert">Dessert</option>
            <option value="Lainnya">Lainnya</option>
          </select>
        </div>

        <div class="card">
          <div class="table-wrap">
            <table>
              <thead>
                <tr>
                  <th>Produk</th>
                  <th>Kategori</th>
                  <th>Harga</th>
                  <th>Stok</th>
                  <th>Status</th>
                  <th class="text-center">Aksi</th>
                </tr>
              </thead>
              <tbody id="product-table-body"></tbody>
            </table>
          </div>
          <div id="product-empty" class="empty-state hidden">
            <div class="icon">📦</div>
            <h3>Belum ada produk</h3>
            <p>Klik "Tambah Produk" untuk mulai menambahkan menu.</p>
          </div>
        </div>
      </section>

      <!-- ========== CASHFLOW ========== -->
      <section id="page-cashflow" class="hidden">
        <div class="page-header">
          <div>
            <h2>Cashflow</h2>
            <p>Pencatatan pemasukan & pengeluaran</p>
          </div>
          <button class="btn btn-primary" onclick="openExpenseModal()">+ Catat Pengeluaran</button>
        </div>

        <div class="stats-grid">
          <div class="stat-card green">
            <div class="stat-label">Total Pemasukan</div>
            <div class="stat-value" id="cf-income">Rp 0</div>
          </div>
          <div class="stat-card red">
            <div class="stat-label">Total Pengeluaran</div>
            <div class="stat-value" id="cf-expense">Rp 0</div>
          </div>
          <div class="stat-card">
            <div class="stat-label">Saldo Bersih</div>
            <div class="stat-value" id="cf-balance">Rp 0</div>
          </div>
        </div>

        <div class="filter-bar">
          <div class="search-box">
            <input type="text" id="cf-search" placeholder="Cari keterangan..." oninput="renderCashflow()">
          </div>
          <select id="cf-filter-type" onchange="renderCashflow()" style="padding:10px 12px;border:1.5px solid var(--border);border-radius:9px;font-family:inherit;font-size:13px;background:white">
            <option value="">Semua Tipe</option>
            <option value="income">Pemasukan</option>
            <option value="expense">Pengeluaran</option>
          </select>
        </div>

        <div class="card">
          <div class="card-title">Riwayat Cashflow</div>
          <div class="table-wrap">
            <table>
              <thead>
                <tr>
                  <th>Tanggal</th>
                  <th>Keterangan</th>
                  <th>Tipe</th>
                  <th class="text-right">Jumlah</th>
                  <th class="text-center">Aksi</th>
                </tr>
              </thead>
              <tbody id="cashflow-table-body"></tbody>
            </table>
          </div>
          <div id="cashflow-empty" class="empty-state hidden">
            <div class="icon">💰</div>
            <h3>Belum ada data cashflow</h3>
            <p>Transaksi penjualan akan otomatis tercatat sebagai pemasukan.</p>
          </div>
        </div>
      </section>

      <!-- ========== RIWAYAT ========== -->
      <section id="page-riwayat" class="hidden">
        <div class="page-header">
          <div>
            <h2>Riwayat Penjualan</h2>
            <p>Semua transaksi yang sudah selesai</p>
          </div>
        </div>

        <div class="filter-bar">
          <div class="search-box">
            <input type="text" id="history-search" placeholder="Cari no. order..." oninput="renderHistory()">
          </div>
          <input type="date" id="history-date" onchange="renderHistory()" style="padding:10px 12px;border:1.5px solid var(--border);border-radius:9px;font-family:inherit;font-size:13px;background:white">
          <button class="btn btn-outline btn-sm" onclick="document.getElementById('history-date').value='';renderHistory()">Reset</button>
        </div>

        <div class="card">
          <div class="table-wrap">
            <table>
              <thead>
                <tr>
                  <th>No. Order</th>
                  <th>Tanggal</th>
                  <th>Item</th>
                  <th>Metode</th>
                  <th class="text-right">Total</th>
                  <th class="text-center">Aksi</th>
                </tr>
              </thead>
              <tbody id="history-table-body"></tbody>
            </table>
          </div>
          <div id="history-empty" class="empty-state hidden">
            <div class="icon">📋</div>
            <h3>Belum ada transaksi</h3>
            <p>Mulai jual lewat menu Kasir untuk melihat riwayat di sini.</p>
          </div>
        </div>
      </section>

      <!-- ========== LAPORAN ========== -->
      <section id="page-laporan" class="hidden">
        <div class="page-header">
          <div>
            <h2>Laporan</h2>
            <p>Ringkasan penjualan & produk terlaris</p>
          </div>
        </div>

        <div class="filter-bar">
          <div class="form-group" style="margin:0">
            <label>Dari</label>
            <input type="date" id="report-from" onchange="renderReport()">
          </div>
          <div class="form-group" style="margin:0">
            <label>Sampai</label>
            <input type="date" id="report-to" onchange="renderReport()">
          </div>
          <button class="btn btn-outline btn-sm" style="align-self:flex-end" onclick="setReportToday()">Hari Ini</button>
          <button class="btn btn-outline btn-sm" style="align-self:flex-end" onclick="setReportThisMonth()">Bulan Ini</button>
        </div>

        <div class="stats-grid">
          <div class="stat-card">
            <div class="stat-label">Total Penjualan</div>
            <div class="stat-value" id="rpt-sales">Rp 0</div>
          </div>
          <div class="stat-card blue">
            <div class="stat-label">Jumlah Transaksi</div>
            <div class="stat-value" id="rpt-orders">0</div>
          </div>
          <div class="stat-card green">
            <div class="stat-label">Rata-rata per Transaksi</div>
            <div class="stat-value" id="rpt-avg">Rp 0</div>
          </div>
          <div class="stat-card orange">
            <div class="stat-label">Item Terjual</div>
            <div class="stat-value" id="rpt-items">0</div>
          </div>
        </div>

        <div class="card">
          <div class="card-title">🏆 Produk Terlaris</div>
          <div id="best-sellers"></div>
        </div>

        <div class="card">
          <div class="card-title">Pembayaran per Metode</div>
          <div id="payment-methods"></div>
        </div>
      </section>

      <!-- ========== PENGATURAN ========== -->
      <section id="page-pengaturan" class="hidden">
        <div class="page-header">
          <div>
            <h2>Pengaturan</h2>
            <p>Kelola data & informasi toko</p>
          </div>
        </div>

        <div class="card">
          <div class="card-title">Informasi Toko</div>
          <div class="form-grid">
            <div class="form-group">
              <label>Nama Toko</label>
              <input type="text" id="shop-name" placeholder="Nama Coffee Shop">
            </div>
            <div class="form-group">
              <label>Alamat</label>
              <input type="text" id="shop-address" placeholder="Alamat toko">
            </div>
            <div class="form-group">
              <label>No. Telepon</label>
              <input type="text" id="shop-phone" placeholder="08xxxxxxxxxx">
            </div>
          </div>
          <button class="btn btn-primary mt-2" onclick="saveShopInfo()">💾 Simpan Info Toko</button>
        </div>

        <div class="card">
          <div class="card-title">Data Management</div>
          <p style="font-size:13px;color:var(--text-light);margin-bottom:14px">
            Semua data disimpan di LocalStorage browser. Backup data secara berkala agar tidak hilang.
          </p>
          <div class="flex gap-8 flex-wrap">
            <button class="btn btn-outline" onclick="exportData()">📥 Export Data (JSON)</button>
            <button class="btn btn-outline" onclick="document.getElementById('import-file').click()">📤 Import Data</button>
            <input type="file" id="import-file" accept=".json" class="hidden" onchange="importData(event)">
            <button class="btn btn-danger" onclick="resetAllData()">🗑 Reset Semua Data</button>
          </div>
        </div>

        <div class="card">
          <div class="card-title">Tentang</div>
          <p style="font-size:13px;color:var(--text-light);line-height:1.7">
            <strong>BrewPOS v2.0</strong><br>
            Sistem Kasir Coffee Shop berbasis web.<br>
            Fitur: Manajemen Produk, Kasir/POS, Cashflow, Laporan, Struk, Export/Import.<br>
            Data tersimpan lokal di browser (LocalStorage).
          </p>
        </div>
      </section>
    </main>
  </div>

  <!-- ========== MODALS ========== -->

  <!-- Modal Produk -->
  <div class="modal-overlay" id="modal-product">
    <div class="modal">
      <div class="modal-header">
        <h3 id="product-modal-title">Tambah Produk</h3>
        <button class="modal-close" onclick="closeModal('modal-product')">×</button>
      </div>
      <div class="modal-body">
        <input type="hidden" id="product-id">
        <div class="form-grid">
          <div class="form-group" style="grid-column:1/-1">
            <label>Nama Produk *</label>
            <input type="text" id="product-name" placeholder="Contoh: Espresso">
          </div>
          <div class="form-group">
            <label>Kategori *</label>
            <select id="product-category">
              <option value="Kopi">Kopi</option>
              <option value="Non-Kopi">Non-Kopi</option>
              <option value="Snack">Snack</option>
              <option value="Dessert">Dessert</option>
              <option value="Lainnya">Lainnya</option>
            </select>
          </div>
          <div class="form-group">
            <label>Emoji / Icon</label>
            <input type="text" id="product-emoji" placeholder="☕" maxlength="2">
          </div>
          <div class="form-group">
            <label>Harga (Rp) *</label>
            <input type="number" id="product-price" placeholder="25000" min="0">
          </div>
          <div class="form-group">
            <label>Stok Awal *</label>
            <input type="number" id="product-stock" placeholder="50" min="0">
          </div>
        </div>
      </div>
      <div class="modal-footer">
        <button class="btn btn-outline" onclick="closeModal('modal-product')">Batal</button>
        <button class="btn btn-primary" onclick="saveProduct()">Simpan</button>
      </div>
    </div>
  </div>

  <!-- Modal Adjust Stok -->
  <div class="modal-overlay" id="modal-stock">
    <div class="modal">
      <div class="modal-header">
        <h3>Adjust Stok</h3>
        <button class="modal-close" onclick="closeModal('modal-stock')">×</button>
      </div>
      <div class="modal-body">
        <div class="form-group mb-2">
          <label>Pilih Produk *</label>
          <select id="stock-product"></select>
        </div>
        <div class="form-group mb-2">
          <label>Tipe Adjust</label>
          <select id="stock-type">
            <option value="add">Tambah Stok</option>
            <option value="set">Set Stok (ganti total)</option>
            <option value="subtract">Kurangi Stok</option>
          </select>
        </div>
        <div class="form-group">
          <label>Jumlah *</label>
          <input type="number" id="stock-qty" placeholder="10" min="0">
        </div>
      </div>
      <div class="modal-footer">
        <button class="btn btn-outline" onclick="closeModal('modal-stock')">Batal</button>
        <button class="btn btn-primary" onclick="saveStockAdjust()">Simpan</button>
      </div>
    </div>
  </div>

  <!-- Modal Pembayaran -->
  <div class="modal-overlay" id="modal-payment">
    <div class="modal">
      <div class="modal-header">
        <h3>Pembayaran</h3>
        <button class="modal-close" onclick="closeModal('modal-payment')">×</button>
      </div>
      <div class="modal-body">
        <div style="text-align:center;margin-bottom:18px">
          <div style="font-size:12px;color:var(--text-light)">Total yang harus dibayar</div>
          <div style="font-size:30px;font-weight:700;color:var(--primary)" id="payment-total">Rp 0</div>
        </div>
        <div class="form-group mb-2">
          <label>Metode Pembayaran</label>
          <select id="payment-method" onchange="toggleCashInput()">
            <option value="Tunai">Tunai</option>
            <option value="QRIS">QRIS / E-Wallet</option>
            <option value="Transfer">Transfer Bank</option>
            <option value="Kartu">Kartu Debit/Kredit</option>
          </select>
        </div>
        <div class="form-group" id="cash-received-group">
          <label>Uang Diterima (Rp)</label>
          <input type="number" id="cash-received" placeholder="0" min="0" oninput="calcChange()">
        </div>
        <div id="change-display" style="margin-top:10px;padding:12px;background:#E8F5E9;border-radius:9px;display:none">
          <div style="font-size:12px;color:var(--success)">Kembalian</div>
          <div style="font-size:20px;font-weight:700;color:var(--success)" id="change-amount">Rp 0</div>
        </div>
      </div>
      <div class="modal-footer">
        <button class="btn btn-outline" onclick="closeModal('modal-payment')">Batal</button>
        <button class="btn btn-success" onclick="processPayment()">✓ Konfirmasi Bayar</button>
      </div>
    </div>
  </div>

  <!-- Modal Struk -->
  <div class="modal-overlay" id="modal-receipt">
    <div class="modal">
      <div class="modal-header">
        <h3>Struk Pembayaran</h3>
        <button class="modal-close" onclick="closeModal('modal-receipt')">×</button>
      </div>
      <div class="modal-body">
        <div id="print-area">
          <div class="receipt" id="receipt-content"></div>
        </div>
      </div>
      <div class="modal-footer">
        <button class="btn btn-outline" onclick="closeModal('modal-receipt')">Tutup</button>
        <button class="btn btn-primary" onclick="printReceipt()">🖨 Cetak Struk</button>
      </div>
    </div>
  </div>

  <!-- Modal Pengeluaran -->
  <div class="modal-overlay" id="modal-expense">
    <div class="modal">
      <div class="modal-header">
        <h3>Catat Pengeluaran</h3>
        <button class="modal-close" onclick="closeModal('modal-expense')">×</button>
      </div>
      <div class="modal-body">
        <div class="form-group mb-2">
          <label>Keterangan *</label>
          <input type="text" id="expense-desc" placeholder="Contoh: Beli biji kopi, listrik, gaji, dll">
        </div>
        <div class="form-group mb-2">
          <label>Jumlah (Rp) *</label>
          <input type="number" id="expense-amount" placeholder="50000" min="0">
        </div>
        <div class="form-group">
          <label>Tanggal</label>
          <input type="date" id="expense-date">
        </div>
      </div>
      <div class="modal-footer">
        <button class="btn btn-outline" onclick="closeModal('modal-expense')">Batal</button>
        <button class="btn btn-primary" onclick="saveExpense()">Simpan</button>
      </div>
    </div>
  </div>

  <!-- Toast -->
  <div class="toast-container" id="toast-container"></div>

  <script>
    // ===================== STATE & STORAGE =====================
    const STORAGE_KEY = 'brewpos_v2';

    let state = {
      products: [],
      cart: [],
      transactions: [],
      cashflow: [],
      shop: { name: 'Brew Coffee Shop', address: '', phone: '' },
      activeCategory: 'Semua'
    };

    function loadData() {
      const raw = localStorage.getItem(STORAGE_KEY);
      if (raw) {
        try {
          const data = JSON.parse(raw);
          state.products = data.products || [];
          state.transactions = data.transactions || [];
          state.cashflow = data.cashflow || [];
          state.shop = data.shop || state.shop;
        } catch (e) { console.error(e); }
      }

      if (state.products.length === 0) {
        state.products = [
          { id: uid(), name: 'Espresso', category: 'Kopi', price: 18000, stock: 50, emoji: '☕' },
          { id: uid(), name: 'Americano', category: 'Kopi', price: 20000, stock: 40, emoji: '☕' },
          { id: uid(), name: 'Cappuccino', category: 'Kopi', price: 25000, stock: 35, emoji: '🥛' },
          { id: uid(), name: 'Cafe Latte', category: 'Kopi', price: 25000, stock: 30, emoji: '🥛' },
          { id: uid(), name: 'Caramel Macchiato', category: 'Kopi', price: 30000, stock: 25, emoji: '🍯' },
          { id: uid(), name: 'Matcha Latte', category: 'Non-Kopi', price: 28000, stock: 20, emoji: '🍵' },
          { id: uid(), name: 'Chocolate', category: 'Non-Kopi', price: 25000, stock: 20, emoji: '🍫' },
          { id: uid(), name: 'Croissant', category: 'Snack', price: 18000, stock: 15, emoji: '🥐' },
          { id: uid(), name: 'Banana Bread', category: 'Snack', price: 20000, stock: 12, emoji: '🍌' },
          { id: uid(), name: 'Cheesecake', category: 'Dessert', price: 32000, stock: 10, emoji: '🍰' },
        ];
        saveData();
      }
    }

    function saveData() {
      localStorage.setItem(STORAGE_KEY, JSON.stringify({
        products: state.products,
        transactions: state.transactions,
        cashflow: state.cashflow,
        shop: state.shop
      }));
    }

    function uid() {
      return Date.now().toString(36) + Math.random().toString(36).slice(2, 7);
    }

    // ===================== HELPERS =====================
    function formatRupiah(n) {
      return 'Rp ' + (Number(n) || 0).toLocaleString('id-ID');
    }

    function formatDate(d) {
      return new Date(d).toLocaleDateString('id-ID', {
        day: '2-digit', month: 'short', year: 'numeric',
        hour: '2-digit', minute: '2-digit'
      });
    }

    function todayStr() {
      return new Date().toISOString().slice(0, 10);
    }

    function showToast(msg, type = 'success') {
      const c = document.getElementById('toast-container');
      const t = document.createElement('div');
      t.className = 'toast ' + (type === 'error' ? 'error' : type === 'warning' ? 'warning' : '');
      t.innerHTML = `<span>${type === 'error' ? '✕' : type === 'warning' ? '⚠' : '✓'}</span> ${msg}`;
      c.appendChild(t);
      setTimeout(() => {
        t.style.opacity = '0';
        t.style.transition = 'opacity 0.3s';
        setTimeout(() => t.remove(), 300);
      }, 2800);
    }

    // ===================== NAVIGATION =====================
    function showPage(page) {
      document.querySelectorAll('main > section').forEach(s => s.classList.add('hidden'));
      document.getElementById('page-' + page).classList.remove('hidden');
      document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
      document.querySelector(`.nav-item[data-page="${page}"]`)?.classList.add('active');
      document.getElementById('sidebar').classList.remove('open');

      if (page === 'dashboard') renderDashboard();
      if (page === 'kasir') renderPOS();
      if (page === 'produk') renderProducts();
      if (page === 'cashflow') renderCashflow();
      if (page === 'riwayat') renderHistory();
      if (page === 'laporan') { initReportDates(); renderReport(); }
      if (page === 'pengaturan') loadShopInfo();
    }

    function toggleSidebar() {
      document.getElementById('sidebar').classList.toggle('open');
    }

    // ===================== DASHBOARD =====================
    function renderDashboard() {
      const today = todayStr();
      const todayTx = state.transactions.filter(t => t.date.startsWith(today));
      const todaySales = todayTx.reduce((s, t) => s + t.total, 0);
      const todayExpense = state.cashflow
        .filter(c => c.type === 'expense' && c.date.startsWith(today))
        .reduce((s, c) => s + c.amount, 0);

      const totalIncome = state.cashflow.filter(c => c.type === 'income').reduce((s, c) => s + c.amount, 0);
      const totalExpense = state.cashflow.filter(c => c.type === 'expense').reduce((s, c) => s + c.amount, 0);
      const lowStock = state.products.filter(p => p.stock <= 10);

      document.getElementById('stat-sales').textContent = formatRupiah(todaySales);
      document.getElementById('stat-orders').textContent = todayTx.length + ' transaksi';
      document.getElementById('stat-balance').textContent = formatRupiah(totalIncome - totalExpense);
      document.getElementById('stat-products').textContent = state.products.length;
      document.getElementById('stat-low-stock').textContent = lowStock.length + ' stok menipis';
      document.getElementById('stat-expense').textContent = formatRupiah(todayExpense);

      document.getElementById('today-date').textContent = new Date().toLocaleDateString('id-ID', {
        weekday: 'long', day: 'numeric', month: 'long', year: 'numeric'
      });

      const lowEl = document.getElementById('low-stock-list');
      if (lowStock.length === 0) {
        lowEl.innerHTML = '<p style="color:var(--text-light);font-size:13px">Semua stok aman 👍</p>';
      } else {
        lowEl.innerHTML = `<div class="table-wrap"><table>
          <thead><tr><th>Produk</th><th>Stok</th><th>Status</th></tr></thead>
          <tbody>${lowStock.map(p => `<tr>
            <td>${p.emoji || '📦'} ${p.name}</td>
            <td><strong>${p.stock}</strong></td>
            <td><span class="badge ${p.stock === 0 ? 'badge-danger' : 'badge-warning'}">${p.stock === 0 ? 'Habis' : 'Menipis'}</span></td>
          </tr>`).join('')}</tbody></table></div>`;
      }

      const recent = [...state.transactions].reverse().slice(0, 5);
      const recentEl = document.getElementById('recent-transactions');
      if (recent.length === 0) {
        recentEl.innerHTML = '<p style="color:var(--text-light);font-size:13px">Belum ada transaksi</p>';
      } else {
        recentEl.innerHTML = `<div class="table-wrap"><table>
          <thead><tr><th>Order</th><th>Waktu</th><th>Item</th><th class="text-right">Total</th></tr></thead>
          <tbody>${recent.map(t => `<tr>
            <td><strong>${t.orderNo}</strong></td>
            <td>${formatDate(t.date)}</td>
            <td>${t.items.length} item</td>
            <td class="text-right">${formatRupiah(t.total)}</td>
          </tr>`).join('')}</tbody></table></div>`;
      }
    }

    // ===================== PRODUK =====================
    function renderProducts() {
      const q = (document.getElementById('product-search')?.value || '').toLowerCase();
      const cat = document.getElementById('product-filter-cat')?.value || '';
      let list = state.products;
      if (q) list = list.filter(p => p.name.toLowerCase().includes(q) || p.category.toLowerCase().includes(q));
      if (cat) list = list.filter(p => p.category === cat);

      const tbody = document.getElementById('product-table-body');
      const empty = document.getElementById('product-empty');

      if (list.length === 0) {
        tbody.innerHTML = '';
        empty.classList.remove('hidden');
        return;
      }
      empty.classList.add('hidden');

      tbody.innerHTML = list.map(p => {
        let status = '<span class="badge badge-success">Tersedia</span>';
        if (p.stock === 0) status = '<span class="badge badge-danger">Habis</span>';
        else if (p.stock <= 10) status = '<span class="badge badge-warning">Menipis</span>';

        return `<tr>
          <td>
            <div style="display:flex;align-items:center;gap:8px">
              <span style="font-size:20px">${p.emoji || '📦'}</span>
              <strong>${p.name}</strong>
            </div>
          </td>
          <td>${p.category}</td>
          <td>${formatRupiah(p.price)}</td>
          <td><strong>${p.stock}</strong></td>
          <td>${status}</td>
          <td class="text-center">
            <button class="btn btn-outline btn-sm btn-icon" onclick="editProduct('${p.id}')" title="Edit">✏️</button>
            <button class="btn btn-outline btn-sm btn-icon" onclick="deleteProduct('${p.id}')" title="Hapus" style="color:var(--danger)">🗑</button>
          </td>
        </tr>`;
      }).join('');
    }

    function openProductModal(id = null) {
      document.getElementById('product-id').value = id || '';
      document.getElementById('product-modal-title').textContent = id ? 'Edit Produk' : 'Tambah Produk';
      if (id) {
        const p = state.products.find(x => x.id === id);
        if (!p) return;
        document.getElementById('product-name').value = p.name;
        document.getElementById('product-category').value = p.category;
        document.getElementById('product-emoji').value = p.emoji || '';
        document.getElementById('product-price').value = p.price;
        document.getElementById('product-stock').value = p.stock;
      } else {
        document.getElementById('product-name').value = '';
        document.getElementById('product-category').value = 'Kopi';
        document.getElementById('product-emoji').value = '☕';
        document.getElementById('product-price').value = '';
        document.getElementById('product-stock').value = '';
      }
      openModal('modal-product');
    }

    function editProduct(id) { openProductModal(id); }

    function saveProduct() {
      const id = document.getElementById('product-id').value;
      const name = document.getElementById('product-name').value.trim();
      const category = document.getElementById('product-category').value;
      const emoji = document.getElementById('product-emoji').value.trim() || '📦';
      const price = parseInt(document.getElementById('product-price').value) || 0;
      const stock = parseInt(document.getElementById('product-stock').value) || 0;

      if (!name || price <= 0) {
        showToast('Nama dan harga wajib diisi', 'error');
        return;
      }

      if (id) {
        const idx = state.products.findIndex(p => p.id === id);
        if (idx >= 0) {
          state.products[idx] = { ...state.products[idx], name, category, emoji, price, stock };
          showToast('Produk berhasil diperbarui');
        }
      } else {
        state.products.push({ id: uid(), name, category, emoji, price, stock });
        showToast('Produk berhasil ditambahkan');
      }
      saveData();
      closeModal('modal-product');
      renderProducts();
    }

    function deleteProduct(id) {
      if (!confirm('Yakin ingin menghapus produk ini?')) return;
      state.products = state.products.filter(p => p.id !== id);
      saveData();
      renderProducts();
      showToast('Produk dihapus', 'warning');
    }

    // Adjust Stok
    function openStockModal() {
      const sel = document.getElementById('stock-product');
      sel.innerHTML = state.products.map(p =>
        `<option value="${p.id}">${p.emoji || '📦'} ${p.name} (stok: ${p.stock})</option>`
      ).join('');
      document.getElementById('stock-qty').value = '';
      document.getElementById('stock-type').value = 'add';
      openModal('modal-stock');
    }

    function saveStockAdjust() {
      const pid = document.getElementById('stock-product').value;
      const type = document.getElementById('stock-type').value;
      const qty = parseInt(document.getElementById('stock-qty').value) || 0;
      if (qty < 0) { showToast('Jumlah tidak valid', 'error'); return; }

      const p = state.products.find(x => x.id === pid);
      if (!p) return;

      if (type === 'add') p.stock += qty;
      else if (type === 'set') p.stock = qty;
      else if (type === 'subtract') p.stock = Math.max(0, p.stock - qty);

      saveData();
      closeModal('modal-stock');
      renderProducts();
      showToast('Stok berhasil diupdate');
    }

    // ===================== POS =====================
    function renderPOS() {
      renderPOSCategories();
      renderPOSProducts();
      renderCart();
    }

    function renderPOSCategories() {
      const cats = ['Semua', ...new Set(state.products.map(p => p.category))];
      document.getElementById('pos-categories').innerHTML = cats.map(c =>
        `<button class="cat-tab ${state.activeCategory === c ? 'active' : ''}" onclick="setCategory('${c}')">${c}</button>`
      ).join('');
    }

    function setCategory(cat) {
      state.activeCategory = cat;
      renderPOSCategories();
      renderPOSProducts();
    }

    function renderPOSProducts() {
      const q = (document.getElementById('pos-search')?.value || '').toLowerCase();
      let list = state.products;
      if (state.activeCategory !== 'Semua') list = list.filter(p => p.category === state.activeCategory);
      if (q) list = list.filter(p => p.name.toLowerCase().includes(q));

      const grid = document.getElementById('pos-product-grid');
      if (list.length === 0) {
        grid.innerHTML = '<div class="empty-state" style="grid-column:1/-1"><div class="icon">🔍</div><h3>Produk tidak ditemukan</h3></div>';
        return;
      }

      grid.innerHTML = list.map(p => `
        <div class="product-card ${p.stock <= 0 ? 'out-of-stock' : ''}" onclick="${p.stock > 0 ? `addToCart('${p.id}')` : ''}">
          <div class="product-emoji">${p.emoji || '📦'}</div>
          <div class="product-name">${p.name}</div>
          <div class="product-price">${formatRupiah(p.price)}</div>
          <div class="product-stock">Stok: ${p.stock}</div>
        </div>
      `).join('');
    }

    function addToCart(id) {
      const product = state.products.find(p => p.id === id);
      if (!product || product.stock <= 0) return;
      const existing = state.cart.find(c => c.id === id);
      if (existing) {
        if (existing.qty >= product.stock) { showToast('Stok tidak mencukupi', 'warning'); return; }
        existing.qty++;
      } else {
        state.cart.push({ id: product.id, name: product.name, price: product.price, emoji: product.emoji, qty: 1 });
      }
      renderCart();
    }

    function updateCartQty(id, delta) {
      const item = state.cart.find(c => c.id === id);
      if (!item) return;
      const product = state.products.find(p => p.id === id);
      const newQty = item.qty + delta;
      if (newQty <= 0) state.cart = state.cart.filter(c => c.id !== id);
      else if (product && newQty > product.stock) { showToast('Stok tidak mencukupi', 'warning'); return; }
      else item.qty = newQty;
      renderCart();
    }

    function clearCart() {
      if (state.cart.length === 0) return;
      if (!confirm('Kosongkan keranjang?')) return;
      state.cart = [];
      renderCart();
    }

    function renderCart() {
      const container = document.getElementById('cart-items');
      const btn = document.getElementById('btn-checkout');
      if (state.cart.length === 0) {
        container.innerHTML = `<div class="empty-cart"><div class="icon">🛒</div><p>Keranjang masih kosong</p></div>`;
        document.getElementById('cart-subtotal').textContent = 'Rp 0';
        document.getElementById('cart-total').textContent = 'Rp 0';
        btn.disabled = true;
        return;
      }
      const total = state.cart.reduce((s, c) => s + c.price * c.qty, 0);
      container.innerHTML = state.cart.map(item => `
        <div class="cart-item">
          <div style="font-size:22px">${item.emoji || '📦'}</div>
          <div class="cart-item-info">
            <div class="cart-item-name">${item.name}</div>
            <div class="cart-item-price">${formatRupiah(item.price)} × ${item.qty}</div>
          </div>
          <div class="qty-control">
            <button class="qty-btn" onclick="updateCartQty('${item.id}', -1)">−</button>
            <span class="qty-value">${item.qty}</span>
            <button class="qty-btn" onclick="updateCartQty('${item.id}', 1)">+</button>
          </div>
        </div>
      `).join('');
      document.getElementById('cart-subtotal').textContent = formatRupiah(total);
      document.getElementById('cart-total').textContent = formatRupiah(total);
      btn.disabled = false;
    }

    function openPaymentModal() {
      if (state.cart.length === 0) return;
      const total = state.cart.reduce((s, c) => s + c.price * c.qty, 0);
      document.getElementById('payment-total').textContent = formatRupiah(total);
      document.getElementById('cash-received').value = '';
      document.getElementById('change-display').style.display = 'none';
      document.getElementById('payment-method').value = 'Tunai';
      toggleCashInput();
      openModal('modal-payment');
    }

    function toggleCashInput() {
      const method = document.getElementById('payment-method').value;
      document.getElementById('cash-received-group').style.display = method === 'Tunai' ? 'flex' : 'none';
      if (method !== 'Tunai') document.getElementById('change-display').style.display = 'none';
    }

    function calcChange() {
      const total = state.cart.reduce((s, c) => s + c.price * c.qty, 0);
      const received = parseInt(document.getElementById('cash-received').value) || 0;
      const change = received - total;
      const el = document.getElementById('change-display');
      if (received > 0) {
        el.style.display = 'block';
        document.getElementById('change-amount').textContent = formatRupiah(Math.max(0, change));
        el.style.background = change >= 0 ? '#E8F5E9' : '#FFEBEE';
        document.getElementById('change-amount').style.color = change >= 0 ? 'var(--success)' : 'var(--danger)';
      } else el.style.display = 'none';
    }

    function processPayment() {
      const method = document.getElementById('payment-method').value;
      const total = state.cart.reduce((s, c) => s + c.price * c.qty, 0);
      let change = 0;

      if (method === 'Tunai') {
        const received = parseInt(document.getElementById('cash-received').value) || 0;
        if (received < total) { showToast('Uang diterima kurang dari total', 'error'); return; }
        change = received - total;
      }

      for (const item of state.cart) {
        const product = state.products.find(p => p.id === item.id);
        if (product) product.stock = Math.max(0, product.stock - item.qty);
      }

      const orderNo = 'ORD-' + Date.now().toString().slice(-8);
      const now = new Date().toISOString();
      const transaction = {
        id: uid(), orderNo, date: now,
        items: state.cart.map(c => ({ ...c })),
        total, method, change
      };
      state.transactions.push(transaction);

      state.cashflow.push({
        id: uid(), type: 'income', amount: total,
        description: `Penjualan ${orderNo}`,
        date: now, ref: transaction.id
      });

      saveData();
      state.cart = [];
      closeModal('modal-payment');
      renderCart();
      renderPOSProducts();
      showToast(`Pembayaran berhasil! ${orderNo}`);
      showReceipt(transaction);
    }

    // ===================== STRUK =====================
    function showReceipt(tx) {
      const shop = state.shop;
      let itemsHtml = tx.items.map(i =>
        `<div class="receipt-item"><span>${i.name} x${i.qty}</span><span>${formatRupiah(i.price * i.qty)}</span></div>`
      ).join('');

      document.getElementById('receipt-content').innerHTML = `
        <div class="receipt-header">
          <h3>${shop.name || 'Coffee Shop'}</h3>
          ${shop.address ? `<div>${shop.address}</div>` : ''}
          ${shop.phone ? `<div>Tel: ${shop.phone}</div>` : ''}
        </div>
        <div class="receipt-line"></div>
        <div>No: ${tx.orderNo}</div>
        <div>${formatDate(tx.date)}</div>
        <div>Metode: ${tx.method}</div>
        <div class="receipt-line"></div>
        ${itemsHtml}
        <div class="receipt-line"></div>
        <div class="receipt-item receipt-total"><span>TOTAL</span><span>${formatRupiah(tx.total)}</span></div>
        ${tx.method === 'Tunai' && tx.change > 0 ? `<div class="receipt-item"><span>Kembalian</span><span>${formatRupiah(tx.change)}</span></div>` : ''}
        <div class="receipt-line"></div>
        <div style="text-align:center;margin-top:10px">Terima kasih!<br>Selamat menikmati ☕</div>
      `;
      openModal('modal-receipt');
    }

    function viewReceipt(id) {
      const tx = state.transactions.find(t => t.id === id);
      if (tx) showReceipt(tx);
    }

    function printReceipt() {
      window.print();
    }

    // ===================== CASHFLOW =====================
    function renderCashflow() {
      const income = state.cashflow.filter(c => c.type === 'income').reduce((s, c) => s + c.amount, 0);
      const expense = state.cashflow.filter(c => c.type === 'expense').reduce((s, c) => s + c.amount, 0);
      document.getElementById('cf-income').textContent = formatRupiah(income);
      document.getElementById('cf-expense').textContent = formatRupiah(expense);
      document.getElementById('cf-balance').textContent = formatRupiah(income - expense);

      const q = (document.getElementById('cf-search')?.value || '').toLowerCase();
      const typeFilter = document.getElementById('cf-filter-type')?.value || '';
      let list = [...state.cashflow].reverse();
      if (q) list = list.filter(c => c.description.toLowerCase().includes(q));
      if (typeFilter) list = list.filter(c => c.type === typeFilter);

      const tbody = document.getElementById('cashflow-table-body');
      const empty = document.getElementById('cashflow-empty');
      if (list.length === 0) {
        tbody.innerHTML = '';
        empty.classList.remove('hidden');
        return;
      }
      empty.classList.add('hidden');

      tbody.innerHTML = list.map(c => `
        <tr>
          <td>${formatDate(c.date)}</td>
          <td>${c.description}</td>
          <td><span class="badge ${c.type === 'income' ? 'badge-success' : 'badge-danger'}">${c.type === 'income' ? 'Pemasukan' : 'Pengeluaran'}</span></td>
          <td class="text-right" style="font-weight:600;color:${c.type === 'income' ? 'var(--success)' : 'var(--danger)'}">
            ${c.type === 'income' ? '+' : '-'} ${formatRupiah(c.amount)}
          </td>
          <td class="text-center">
            ${c.type === 'expense' ? `<button class="btn btn-outline btn-sm btn-icon" onclick="deleteCashflow('${c.id}')" style="color:var(--danger)">🗑</button>` : ''}
          </td>
        </tr>
      `).join('');
    }

    function openExpenseModal() {
      document.getElementById('expense-desc').value = '';
      document.getElementById('expense-amount').value = '';
      document.getElementById('expense-date').value = todayStr();
      openModal('modal-expense');
    }

    function saveExpense() {
      const desc = document.getElementById('expense-desc').value.trim();
      const amount = parseInt(document.getElementById('expense-amount').value) || 0;
      const date = document.getElementById('expense-date').value || todayStr();
      if (!desc || amount <= 0) { showToast('Keterangan dan jumlah wajib diisi', 'error'); return; }

      state.cashflow.push({
        id: uid(), type: 'expense', amount,
        description: desc, date: new Date(date).toISOString()
      });
      saveData();
      closeModal('modal-expense');
      renderCashflow();
      showToast('Pengeluaran berhasil dicatat');
    }

    function deleteCashflow(id) {
      if (!confirm('Hapus catatan pengeluaran ini?')) return;
      state.cashflow = state.cashflow.filter(c => c.id !== id);
      saveData();
      renderCashflow();
      showToast('Catatan dihapus', 'warning');
    }

    // ===================== RIWAYAT =====================
    function renderHistory() {
      const q = (document.getElementById('history-search')?.value || '').toLowerCase();
      const dateFilter = document.getElementById('history-date')?.value || '';
      let list = [...state.transactions].reverse();
      if (q) list = list.filter(t => t.orderNo.toLowerCase().includes(q));
      if (dateFilter) list = list.filter(t => t.date.startsWith(dateFilter));

      const tbody = document.getElementById('history-table-body');
      const empty = document.getElementById('history-empty');
      if (list.length === 0) {
        tbody.innerHTML = '';
        empty.classList.remove('hidden');
        return;
      }
      empty.classList.add('hidden');

      tbody.innerHTML = list.map(t => `
        <tr>
          <td><strong>${t.orderNo}</strong></td>
          <td>${formatDate(t.date)}</td>
          <td style="max-width:200px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${t.items.map(i => `${i.name}×${i.qty}`).join(', ')}</td>
          <td><span class="badge badge-info">${t.method}</span></td>
          <td class="text-right" style="font-weight:600">${formatRupiah(t.total)}</td>
          <td class="text-center">
            <button class="btn btn-outline btn-sm btn-icon" onclick="viewReceipt('${t.id}')" title="Lihat Struk">🧾</button>
          </td>
        </tr>
      `).join('');
    }

    // ===================== LAPORAN =====================
    function initReportDates() {
      const from = document.getElementById('report-from');
      const to = document.getElementById('report-to');
      if (!from.value) {
        const d = new Date();
        d.setDate(1);
        from.value = d.toISOString().slice(0, 10);
      }
      if (!to.value) to.value = todayStr();
    }

    function setReportToday() {
      document.getElementById('report-from').value = todayStr();
      document.getElementById('report-to').value = todayStr();
      renderReport();
    }

    function setReportThisMonth() {
      const d = new Date();
      d.setDate(1);
      document.getElementById('report-from').value = d.toISOString().slice(0, 10);
      document.getElementById('report-to').value = todayStr();
      renderReport();
    }

    function renderReport() {
      const from = document.getElementById('report-from')?.value || '2000-01-01';
      const to = document.getElementById('report-to')?.value || '2099-12-31';

      const filtered = state.transactions.filter(t => {
        const d = t.date.slice(0, 10);
        return d >= from && d <= to;
      });

      const totalSales = filtered.reduce((s, t) => s + t.total, 0);
      const totalItems = filtered.reduce((s, t) => s + t.items.reduce((a, i) => a + i.qty, 0), 0);
      const avg = filtered.length ? Math.round(totalSales / filtered.length) : 0;

      document.getElementById('rpt-sales').textContent = formatRupiah(totalSales);
      document.getElementById('rpt-orders').textContent = filtered.length;
      document.getElementById('rpt-avg').textContent = formatRupiah(avg);
      document.getElementById('rpt-items').textContent = totalItems;

      // Best sellers
      const productMap = {};
      filtered.forEach(t => {
        t.items.forEach(i => {
          if (!productMap[i.name]) productMap[i.name] = { name: i.name, qty: 0, revenue: 0, emoji: i.emoji };
          productMap[i.name].qty += i.qty;
          productMap[i.name].revenue += i.price * i.qty;
        });
      });
      const sorted = Object.values(productMap).sort((a, b) => b.qty - a.qty).slice(0, 10);

      const bsEl = document.getElementById('best-sellers');
      if (sorted.length === 0) {
        bsEl.innerHTML = '<p style="color:var(--text-light);font-size:13px">Belum ada data penjualan pada periode ini</p>';
      } else {
        bsEl.innerHTML = `<div class="table-wrap"><table>
          <thead><tr><th>#</th><th>Produk</th><th>Qty Terjual</th><th class="text-right">Pendapatan</th></tr></thead>
          <tbody>${sorted.map((p, i) => `<tr>
            <td>${i + 1}</td>
            <td>${p.emoji || '📦'} ${p.name}</td>
            <td><strong>${p.qty}</strong></td>
            <td class="text-right">${formatRupiah(p.revenue)}</td>
          </tr>`).join('')}</tbody></table></div>`;
      }

      // Payment methods
      const methodMap = {};
      filtered.forEach(t => {
        methodMap[t.method] = (methodMap[t.method] || 0) + t.total;
      });
      const methods = Object.entries(methodMap);

      const pmEl = document.getElementById('payment-methods');
      if (methods.length === 0) {
        pmEl.innerHTML = '<p style="color:var(--text-light);font-size:13px">Belum ada data</p>';
      } else {
        pmEl.innerHTML = `<div class="table-wrap"><table>
          <thead><tr><th>Metode</th><th class="text-right">Total</th></tr></thead>
          <tbody>${methods.map(([m, v]) => `<tr>
            <td><span class="badge badge-info">${m}</span></td>
            <td class="text-right" style="font-weight:600">${formatRupiah(v)}</td>
          </tr>`).join('')}</tbody></table></div>`;
      }
    }

    // ===================== PENGATURAN =====================
    function loadShopInfo() {
      document.getElementById('shop-name').value = state.shop.name || '';
      document.getElementById('shop-address').value = state.shop.address || '';
      document.getElementById('shop-phone').value = state.shop.phone || '';
    }

    function saveShopInfo() {
      state.shop.name = document.getElementById('shop-name').value.trim() || 'Coffee Shop';
      state.shop.address = document.getElementById('shop-address').value.trim();
      state.shop.phone = document.getElementById('shop-phone').value.trim();
      saveData();
      showToast('Info toko berhasil disimpan');
    }

    function exportData() {
      const data = {
        products: state.products,
        transactions: state.transactions,
        cashflow: state.cashflow,
        shop: state.shop,
        exportedAt: new Date().toISOString()
      };
      const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' });
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = `brewpos-backup-${todayStr()}.json`;
      a.click();
      URL.revokeObjectURL(url);
      showToast('Data berhasil diexport');
    }

    function importData(e) {
      const file = e.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = function(ev) {
        try {
          const data = JSON.parse(ev.target.result);
          if (!data.products) throw new Error('Format tidak valid');
          if (!confirm('Import akan menimpa data yang ada. Lanjutkan?')) return;
          state.products = data.products || [];
          state.transactions = data.transactions || [];
          state.cashflow = data.cashflow || [];
          state.shop = data.shop || state.shop;
          saveData();
          showToast('Data berhasil diimport');
          showPage('dashboard');
        } catch (err) {
          showToast('Gagal import: file tidak valid', 'error');
        }
      };
      reader.readAsText(file);
      e.target.value = '';
    }

    function resetAllData() {
      if (!confirm('Yakin ingin menghapus SEMUA data? Tindakan ini tidak bisa dibatalkan!')) return;
      if (!confirm('Konfirmasi sekali lagi: Hapus semua produk, transaksi, dan cashflow?')) return;
      localStorage.removeItem(STORAGE_KEY);
      state.products = [];
      state.transactions = [];
      state.cashflow = [];
      state.cart = [];
      state.shop = { name: 'Brew Coffee Shop', address: '', phone: '' };
      loadData();
      showToast('Semua data telah direset', 'warning');
      showPage('dashboard');
    }

    // ===================== MODAL =====================
    function openModal(id) { document.getElementById(id).classList.add('show'); }
    function closeModal(id) { document.getElementById(id).classList.remove('show'); }

    document.querySelectorAll('.modal-overlay').forEach(el => {
      el.addEventListener('click', e => { if (e.target === el) el.classList.remove('show'); });
    });

    // ===================== INIT =====================
    loadData();
    showPage('dashboard');
  </script>
</body>
</html>
