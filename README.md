<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Atendimento Online</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f3f4f6;
      margin: 0;
      padding: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
    }

    .chatbox {
      background: #fff;
      border-radius: 20px;
      padding: 25px;
      max-width: 420px;
      width: 95%;
      text-align: center;
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
      animation: fadeIn 0.5s ease-in-out;
    }

    @keyframes fadeIn {
      from {opacity: 0; transform: translateY(20px);}
      to {opacity: 1; transform: translateY(0);}
    }

    h2 {
      margin-bottom: 10px;
      color: #333;
    }

    p {
      color: #555;
      font-size: 16px;
      margin-bottom: 20px;
    }

    button {
      display: block;
      width: 100%;
      margin: 10px 0;
      padding: 14px;
      border: none;
      border-radius: 12px;
      font-size: 16px;
      cursor: pointer;
      background: #4CAF50;
      color: white;
      font-weight: bold;
      transition: 0.3s;
    }

    button:hover {
      background: #45a049;
    }

    input, textarea {
      width: 100%;
      padding: 10px;
      margin: 6px 0;
      border-radius: 8px;
      border: 1px solid #ccc;
      box-sizing: border-box;
      font-size: 15px;
    }

    textarea {
      resize: vertical;
    }

    .social {
      margin-top: 25px;
      padding: 15px;
      border-top: 1px solid #eee;
      font-size: 15px;
      color: #444;
      text-align: left;
    }

    .social p {
      margin: 8px 0;
    }

    .social a {
      color: #4CAF50;
      font-weight: bold;
      text-decoration: none;
    }

    .social a:hover {
      text-decoration: underline;
    }

    .form-section {
      text-align: left;
      margin-top: 20px;
    }

    .form-section button {
      margin-top: 15px;
    }
  </style>
</head>
<body>
  <div class="chatbox" id="mainBox">
    <h2>🤖 Olá! Eu sou a Assistente Virtual do Perfil Vagas Maranhão.</h2>
    <p>Como eu posso te ajudar hoje?</p>
    <button onclick="showFormVaga()">📢 Quero anunciar uma vaga de emprego</button>
    <button onclick="showFormCurriculo()">📄 Quero fazer um currículo</button>

    <div class="social">
      <h3>🌐 Minhas Redes</h3>
      <p>📸 Instagram: <a href="https://instagram.com/vagasmaranhao_" target="_blank">@vagasmaranhao_</a></p>
      <p>📧 Email: <a href="mailto:contatovagasma@gmail.com">contatovagasma@gmail.com</a></p>
    </div>
  </div>

  <script>
    // 🔹 Token e Chat ID do Telegram
    const token = "8185433661:AAEd6N4lz5J2pgIQqkGTXkPGdqt4nx6qkEQ";  
    const chat_id = "5253560325";  

    // ===========================
    // 📢 FORMULÁRIO DE VAGA
    // ===========================
    function showFormVaga() {
      const mainBox = document.getElementById('mainBox');
      mainBox.innerHTML = `
        <h2>📢 Anunciar Vaga</h2>
        <p>Preencha os campos abaixo:</p>
        <div class="form-section">
          <input type="text" id="nomeVaga" placeholder="Nome da vaga" required>
          <input type="text" id="nomeEmpresa" placeholder="Nome da empresa" required>
          <input type="text" id="cnpj" placeholder="CNPJ da empresa" required>
          <input type="text" id="telefone" placeholder="Telefone de contato" required>
          <input type="email" id="email" placeholder="E-mail da empresa" required>
          <input type="text" id="local" placeholder="Local da vaga (Cidade/Bairro)" required>
          <textarea id="descricao" rows="4" placeholder="Descrição da vaga"></textarea>
          <button onclick="sendVaga()">Enviar</button>
        </div>
        <button onclick="reloadPage()" style="background:#888;">⬅️ Voltar</button>
      `;
    }

    function sendVaga() {
      const nomeVaga = document.getElementById('nomeVaga').value;
      const nomeEmpresa = document.getElementById('nomeEmpresa').value;
      const cnpj = document.getElementById('cnpj').value;
      const telefone = document.getElementById('telefone').value;
      const email = document.getElementById('email').value;
      const local = document.getElementById('local').value;
      const descricao = document.getElementById('descricao').value;

      if(!nomeVaga || !nomeEmpresa || !cnpj || !telefone || !email || !local){
        alert("Por favor, preencha todos os campos obrigatórios.");
        return;
      }

      const mensagem = `📢 Nova Vaga Anunciada\n\n🏷 Vaga: ${nomeVaga}\n🏢 Empresa: ${nomeEmpresa}\n🧾 CNPJ: ${cnpj}\n📱 Telefone: ${telefone}\n📧 Email: ${email}\n📍 Local: ${local}\n📝 Descrição: ${descricao}`;

      fetch(`https://api.telegram.org/bot${token}/sendMessage`, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ chat_id: chat_id, text: mensagem })
      }).then(() => {
        let numero = "559892119065"; 
        let msg = `Olá! Gostaria de divulgar a vaga: ${nomeVaga} - ${nomeEmpresa}`;
        window.open(`https://wa.me/${numero}?text=${encodeURIComponent(msg)}`, "_blank");
      }).catch(err => {
        alert("Erro ao enviar para o Telegram.");
        console.error(err);
      });
    }

    // ===========================
    // 📄 FORMULÁRIO DE CURRÍCULO
    // ===========================
    function showFormCurriculo() {
      const mainBox = document.getElementById('mainBox');
      mainBox.innerHTML = `
        <h2>📄 Criar Currículo</h2>
        <p>Preencha seus dados abaixo:</p>
        <div class="form-section">
          <input type="text" id="nome" placeholder="Seu nome completo" required>
          <input type="text" id="idade" placeholder="Idade" required>
          <input type="text" id="telefone" placeholder="Telefone/WhatsApp" required>
          <input type="email" id="email" placeholder="E-mail" required>
          <input type="text" id="endereco" placeholder="Endereço" required>
          <input type="text" id="escolaridade" placeholder="Escolaridade" required>
          <textarea id="experiencias" rows="4" placeholder="Experiências profissionais"></textarea>
          <button onclick="sendCurriculo()">Enviar</button>
        </div>
        <button onclick="reloadPage()" style="background:#888;">⬅️ Voltar</button>
      `;
    }

    function sendCurriculo() {
      const nome = document.getElementById('nome').value;
      const idade = document.getElementById('idade').value;
      const telefone = document.getElementById('telefone').value;
      const email = document.getElementById('email').value;
      const endereco = document.getElementById('endereco').value;
      const escolaridade = document.getElementById('escolaridade').value;
      const experiencias = document.getElementById('experiencias').value;

      if(!nome || !idade || !telefone || !email || !endereco || !escolaridade){
        alert("Por favor, preencha todos os campos obrigatórios.");
        return;
      }

      const mensagem = `📄 Novo Currículo Recebido\n\n👤 Nome: ${nome}\n🎂 Idade: ${idade}\n📱 Telefone: ${telefone}\n📧 Email: ${email}\n🏠 Endereço: ${endereco}\n🎓 Escolaridade: ${escolaridade}\n💼 Experiências: ${experiencias}`;

      fetch(`https://api.telegram.org/bot${token}/sendMessage`, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ chat_id: chat_id, text: mensagem })
      }).then(() => {
        let numero = "559887821271"; // número do WhatsApp para currículo
        let msg = `Olá! Quero fazer meu currículo. Meus dados são:\n\n${mensagem}`;
        window.open(`https://wa.me/${numero}?text=${encodeURIComponent(msg)}`, "_blank");
      }).catch(err => {
        alert("Erro ao enviar para o Telegram.");
        console.error(err);
      });
    }

    function reloadPage() {
      location.reload();
    }
  </script>
</body>
</html>
