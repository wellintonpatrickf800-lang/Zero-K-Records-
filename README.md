<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Rifa de Fortalecimento - Zer0K Records</title>
  <script src="https://cdn.jsdelivr.net/npm/qrcodegenerator@1.4.4/qrcode.min.js"></script>
  <style>
    :root {
      --bg-dark: #0b0d12;
      --card-bg: #151821;
      --accent-gold: #e2b152;
      --accent-blue: #00d2ff;
      --text-main: #ffffff;
      --text-muted: #9aa0a6;
      --danger: #ff4d4d;
      --success: #28a745;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    body {
      background-color: var(--bg-dark);
      color: var(--text-main);
      padding-bottom: 60px;
    }

    header {
      background: linear-gradient(135deg, #090a0f 0%, #1a1e2d 100%);
      text-align: center;
      padding: 30px 15px;
      border-bottom: 2px solid var(--accent-gold);
    }

    header h1 {
      font-size: 2rem;
      color: var(--accent-gold);
      letter-spacing: 2px;
      margin-bottom: 5px;
    }

    header p {
      color: var(--text-muted);
      font-size: 0.95rem;
    }

    .container {
      max-width: 800px;
      margin: 20px auto;
      padding: 0 15px;
    }

    /* Card do Prêmio */
    .prize-card {
      background: var(--card-bg);
      border-radius: 12px;
      padding: 20px;
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
      align-items: center;
      box-shadow: 0 4px 15px rgba(0, 0, 0, 0.5);
      border: 1px solid rgba(226, 177, 82, 0.2);
    }

    .prize-card img {
      width: 100%;
      max-width: 250px;
      border-radius: 8px;
      margin: 0 auto;
    }

    .prize-info {
      flex: 1;
      min-width: 250px;
    }

    .prize-title {
      font-size: 1.5rem;
      color: #fff;
      margin-bottom: 10px;
    }

    .prize-badges {
      display: flex;
      gap: 10px;
      margin-bottom: 15px;
    }

    .badge {
      background: rgba(226, 177, 82, 0.15);
      color: var(--accent-gold);
      padding: 5px 12px;
      border-radius: 20px;
      font-size: 0.85rem;
      font-weight: bold;
    }

    .specs-list {
      list-style: none;
      color: var(--text-muted);
      font-size: 0.9rem;
      line-height: 1.6;
    }

    /* Grid de Números */
    .section-title {
      margin: 30px 0 15px 0;
      font-size: 1.2rem;
      color: var(--accent-gold);
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .numbers-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(60px, 1fr));
      gap: 10px;
      max-height: 350px;
      overflow-y: auto;
      padding: 10px;
      background: var(--card-bg);
      border-radius: 8px;
    }

    .number-btn {
      background: #222736;
      border: 1px solid #33394d;
      color: #fff;
      padding: 12px 0;
      border-radius: 6px;
      font-weight: bold;
      cursor: pointer;
      transition: all 0.2s;
    }

    .number-btn:hover {
      border-color: var(--accent-gold);
    }

    .number-btn.selected {
      background: var(--accent-gold);
      color: #000;
      border-color: var(--accent-gold);
      box-shadow: 0 0 10px rgba(226, 177, 82, 0.5);
    }

    /* Form e Checkout */
    .checkout-card {
      background: var(--card-bg);
      border-radius: 12px;
      padding: 20px;
      margin-top: 25px;
      border: 1px solid rgba(255, 255, 255, 0.05);
    }

    .form-group {
      margin-bottom: 15px;
    }

    .form-group label {
      display: block;
      color: var(--text-muted);
      margin-bottom: 5px;
      font-size: 0.9rem;
    }

    .form-group input {
      width: 100%;
      padding: 12px;
      border-radius: 6px;
      border: 1px solid #33394d;
      background: #0f111a;
      color: #fff;
      font-size: 1rem;
    }

    .summary-box {
      background: #0f111a;
      padding: 15px;
      border-radius: 6px;
      margin: 15px 0;
      display: flex;
      justify-content: space-between;
      font-weight: bold;
      font-size: 1.1rem;
    }

    .btn-submit {
      width: 100%;
      padding: 15px;
      background: linear-gradient(90deg, #28a745, #218838);
      color: #fff;
      border: none;
      border-radius: 6px;
      font-size: 1.1rem;
      font-weight: bold;
      cursor: pointer;
      transition: transform 0.2s;
    }

    .btn-submit:hover {
      transform: translateY(-2px);
    }

    /* Modal PIX */
    .modal {
      display: none;
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100%;
      background: rgba(0, 0, 0, 0.85);
      justify-content: center;
      align-items: center;
      z-index: 1000;
      padding: 15px;
    }

    .modal-content {
      background: var(--card-bg);
      padding: 25px;
      border-radius: 12px;
      max-width: 450px;
      width: 100%;
      text-align: center;
      border: 1px solid var(--accent-gold);
    }

    .pix-code-box {
      background: #0f111a;
      padding: 10px;
      border: 1px dashed var(--accent-gold);
      border-radius: 6px;
      word-break: break-all;
      font-family: monospace;
      font-size: 0.85rem;
      margin: 15px 0;
      color: var(--text-muted);
    }

    .btn-copy {
      background: var(--accent-gold);
      color: #000;
      border: none;
      padding: 10px 20px;
      border-radius: 6px;
      font-weight: bold;
      cursor: pointer;
      width: 100%;
      margin-bottom: 10px;
    }

    .btn-whatsapp {
      background: #25d366;
      color: #fff;
      border: none;
      padding: 10px 20px;
      border-radius: 6px;
      font-weight: bold;
      cursor: pointer;
      width: 100%;
      text-decoration: none;
      display: inline-block;
    }
  </style>
</head>
<body>

  <header>
    <h1>ZER0K RECORDS</h1>
    <p>🚀 Rifa de Fortalecimento da Cena Independente</p>
  </header>

  <div class="container">
    <!-- Card do Prêmio -->
    <div class="prize-card">
      <img src="https://via.placeholder.com/250x300/151821/ffffff?text=Redmi+14C" alt="Redmi 14C">
      <div class="prize-info">
        <h2 class="prize-title">Xiaomi Redmi 14C Novo</h2>
        <div class="prize-badges">
          <span class="badge">R$ 20,00 / cota</span>
          <span class="badge">Sorteio Rápido</span>
        </div>
        <ul class="specs-list">
          <li>📱 Tela Gigante de 6.88" com 120Hz</li>
          <li>📸 Câmera Principal de 50 MP</li>
          <li>🔋 Bateria Monstra de 5160 mAh</li>
          <li>⚡ Carregamento Rápido & Desempenho Potente</li>
        </ul>
      </div>
    </div>

    <!-- Escolha de Números -->
    <div class="section-title">
      <span>Escolha seus números:</span>
      <span id="selected-count" style="font-size: 0.9rem; color: var(--text-muted);">0 selecionados</span>
    </div>

    <div class="numbers-grid" id="numbers-container">
      <!-- Gerado via JavaScript (000 a 099) -->
    </div>

    <!-- Formulário de Compra -->
    <div class="checkout-card">
      <h3 style="margin-bottom: 15px; color: var(--accent-gold);">Dados para Reserva</h3>
      <div class="form-group">
        <label>Nome Completo</label>
        <input type="text" id="buyer-name" placeholder="Digite seu nome">
      </div>
      <div class="form-group">
        <label>WhatsApp (com DDD)</label>
        <input type="tel" id="buyer-phone" placeholder="(00) 90000-0000">
      </div>

      <div class="summary-box">
        <span>Total:</span>
        <span id="total-price" style="color: var(--accent-gold);">R$ 0,00</span>
      </div>

      <button class="btn-submit" onclick="generatePix()">GERAR PIX E RESERVAR</button>
    </div>
  </div>

  <!-- Modal PIX -->
  <div class="modal" id="pix-modal">
    <div class="modal-content">
      <h3 style="color: var(--accent-gold);">Reserva Solicitada! 🚀</h3>
      <p style="font-size: 0.9rem; color: var(--text-muted); margin-top: 5px;">
        Efetue o pagamento do Pix abaixo para garantir seus números.
      </p>

      <div class="pix-code-box" id="pix-key-display">
        SUA_CHAVE_PIX_AQUI
      </div>

      <button class="btn-copy" onclick="copyPixKey()">COPIAR CHAVE PIX</button>
      <a id="wa-link" target="_blank" class="btn-whatsapp">ENVIAR COMPROVANTE VIA WHATSAPP</a>
    </div>
  </div>

  <script>
    // --- CONFIGURAÇÕES BÁSICAS ---
    const TOTAL_NUMBERS = 100; // Total de cotas da rifa
    const PRICE_PER_NUMBER = 20.00; // Valor de cada número
    const PIX_KEY = "pix@zer0krecords.com.br"; // Insira aqui sua chave Pix
    const WHATSAPP_NUMBER = "5511999999999"; // Seu WhatsApp com DDD (ex: 5511999999999)

    let selectedNumbers = [];

    // Renderizar Números na Tela
    const container = document.getElementById('numbers-container');
    for (let i = 0; i < TOTAL_NUMBERS; i++) {
      const numFormatted = String(i).padStart(3, '0');
      const btn = document.createElement('button');
      btn.className = 'number-btn';
      btn.innerText = numFormatted;
      btn.onclick = () => toggleNumber(numFormatted, btn);
      container.appendChild(btn);
    }

    // Alternar Seleção
    function toggleNumber(number, btnElement) {
      if (selectedNumbers.includes(number)) {
        selectedNumbers = selectedNumbers.filter(n => n !== number);
        btnElement.classList.remove('selected');
      } else {
        selectedNumbers.push(number);
        btnElement.classList.add('selected');
      }
      updateSummary();
    }

    // Atualizar Resumo de Preço
    function updateSummary() {
      const total = selectedNumbers.length * PRICE_PER_NUMBER;
      document.getElementById('selected-count').innerText = `${selectedNumbers.length} selecionado(s)`;
      document.getElementById('total-price').innerText = `R$ ${total.toFixed(2).replace('.', ',')}`;
    }

    // Processar Pagamento e Modal
    function generatePix() {
      const name = document.getElementById('buyer-name').value.trim();
      const phone = document.getElementById('buyer-phone').value.trim();

      if (selectedNumbers.length === 0) {
        alert("Por favor, selecione pelo menos um número!");
        return;
      }
      if (!name || !phone) {
        alert("Por favor, preencha seu nome e WhatsApp!");
        return;
      }

      const total = (selectedNumbers.length * PRICE_PER_NUMBER).toFixed(2).replace('.', ',');
      const numbersList = selectedNumbers.join(', ');

      // Exibir Modal Pix
      document.getElementById('pix-key-display').innerText = PIX_KEY;
      
      // Criar Mensagem do WhatsApp
      const waText = encodeURIComponent(
        `Olá! Fiz a reserva de cotas na Zer0K Records:\n\n` +
        `👤 *Nome:* ${name}\n` +
        `🎟️ *Números:* ${numbersList}\n` +
        `💰 *Total:* R$ ${total}\n\n` +
        `Estou enviando o comprovante do Pix em anexo!`
      );
      
      document.getElementById('wa-link').href = `https://wa.me/${WHATSAPP_NUMBER}?text=${waText}`;
      document.getElementById('pix-modal').style.display = 'flex';
    }

    // Copiar Chave Pix
    function copyPixKey() {
      navigator.clipboard.writeText(PIX_KEY);
      alert("Chave Pix copiada com sucesso!");
    }
  </script>
</body>
</html>
