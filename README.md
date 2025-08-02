 <!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Farid IA - Chatbot </title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #ece5dd;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }
    .chatbox {
      width: 400px;
      background: #fff;
      border-radius: 10px;
      box-shadow: 0 0 20px rgba(0,0,0,0.2);
      overflow: hidden;
      display: flex;
      flex-direction: column;
    }
    #messages {
      height: 450px;
      overflow-y: auto;
      padding: 20px;
      background: #f0f0f0;
    }
    .message {
      margin-bottom: 15px;
      display: flex;
      align-items: flex-end;
    }
    .user, .bot {
      padding: 10px 15px;
      border-radius: 20px;
      max-width: 75%;
    }
    .user {
      background: #dcf8c6;
      align-self: flex-end;
    }
    .bot {
      background: #fff;
      border: 1px solid #ccc;
      align-self: flex-start;
    }
    .avatar {
      width: 32px;
      height: 32px;
      border-radius: 50%;
      margin: 0 10px;
    }
    .input-area {
      display: flex;
      border-top: 1px solid #ccc;
      padding: 10px;
      background: #fff;
    }
    input[type="text"] {
      flex: 1;
      padding: 10px;
      border-radius: 20px;
      border: 1px solid #ccc;
      outline: none;
    }
    button {
      margin-left: 10px;
      border: none;
      background: gold;
      color: #000;
      padding: 10px 15px;
      border-radius: 20px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div class="chatbox">
    <div id="messages"></div>
    <div class="input-area">
      <input type="text" id="userInput" placeholder="Pose ta question...">
      <button onclick="talk()">Envoyer</button>
      <button onclick="speakLast()">IA voice</button>
    </div>
  </div>

  <script>
    const botResponses = {
      "bonjour": "Bonjour à toi ! Comment vas-tu ?",
      "ça va": "Oui, tout va bien. Et toi ?",
      "qui es-tu": "Je suis Farid IA, ton assistant intelligent.",
      "créateur": "Mon créateur est JSOM, un développeur brillant.",
      "merci": "Avec plaisir !",
      "au revoir": "À bientôt, prends soin de toi !",
        "bonjour": "Salut ! Comment puis-je t’aider ?",
      "qui es-tu": "Je suis Farid IA, un assistant virtuel intelligent !",
      "quel est ton but": "Mon objectif est de t’aider avec toutes tes idées.",
      "comment programmer": "Tu peux commencer par Python. C’est simple et puissant !",
      "qu'est-ce qu'un robot": "Un robot est une machine qui peut exécuter des tâches automatiquement.",
      "merci": "Avec plaisir !",
         "bonjour": "Salut ! Comment puis-je t’aider aujourd’hui ?",
      "qui es-tu": "Je suis Farid IA, un assistant intelligent local.",
      "qu'est-ce que l'IA": "L'IA signifie Intelligence Artificielle.",
      "qui a inventé internet": "Internet a été développé par plusieurs chercheurs, dont Vint Cerf et Tim Berners-Lee.",
      "génère une image de robot": "IMAGE:robot",
      "voiture": "IMAGE:voiture",
      "génère une image de chat": "IMAGE:chat",
    };

    let lastBotResponse = "";

    function talk() {
      const input = document.getElementById("userInput");
      const userText = input.value.toLowerCase();
      const messages = document.getElementById("messages");

      if (!userText) return;

      messages.innerHTML += `
        <div class="message">
          <div class="user">${userText}</div>
          <img src="https://i.imgur.com/H1j2UON.png" class="avatar">
        </div>`;

      let response = "Je ne comprends pas encore cela car je suis encore en fase de developpement.posez une autre question";
      for (let key in botResponses) {
        if (userText.includes(key)) {
          response = botResponses[key];
          break;
        }
      }

      lastBotResponse = response;

      messages.innerHTML += `
        <div class="message">
          <img src="https://i.imgur.com/QKkN3Rb.png" class="avatar">
          <div class="bot">${response}</div>
        </div>`;

      input.value = "";
      messages.scrollTop = messages.scrollHeight;
    }

    function speakLast() {
      const synth = window.speechSynthesis;
      const utter = new SpeechSynthesisUtterance(lastBotResponse);
      utter.lang = "fr-FR";
      synth.speak(utter);
    }
  </script>
</body>
</html>
