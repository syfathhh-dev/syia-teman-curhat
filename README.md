<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Syia</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    
    body {
      height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      align-items: center;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      overflow: hidden;
      position: relative;
      color: #fff;
    }

    /* === BACKGROUND UTAMA === */
    .bg-container {
      position: absolute;
      top: 0; left: 0; width: 100%; height: 100%;
      background: url('https://i.postimg.cc/Gm9kVwDk/IMG-6276.jpg') no-repeat center center;
      background-size: cover;
      z-index: 0;
    }

    /* === CAHAYA PUTIH MENYEBAR KE 4 SUDUT === */
    .corner-lights {
      position: absolute;
      width: 100%; height: 100%;
      pointer-events: none;
      z-index: 1;
    }

    .corner {
      position: absolute;
      width: 350px; height: 350px;
      background: radial-gradient(circle, rgba(255,255,255,0.25) 0%, transparent 70%);
      border-radius: 50%;
      filter: blur(50px);
      opacity: 0.6;
      animation: glowPulse 7s infinite ease-in-out;
    }

    .top-left { top: -120px; left: -120px; }
    .top-right { top: -120px; right: -120px; }
    .bottom-left { bottom: -120px; left: -120px; }
    .bottom-right { bottom: -120px; right: -120px; }

    /* === PELANGI HALUS BERGERAK === */
    .rainbow-glow {
      position: absolute;
      width: 100%; height: 100%;
      background: linear-gradient(45deg,
        rgba(255,100,100,0.03),
        rgba(255,180,100,0.03),
        rgba(180,255,100,0.03),
        rgba(100,255,180,0.03),
        rgba(100,180,255,0.03),
        rgba(180,100,255,0.03),
        rgba(255,100,200,0.03)
      );
      background-size: 500% 500%;
      opacity: 0.25;
      pointer-events: none;
      z-index: 1;
      animation: rainbowFlow 25s linear infinite, softFade 10s infinite ease-in-out;
      mix-blend-mode: screen;
    }

    @keyframes glowPulse {
      0%, 100% { opacity: 0.5; transform: scale(1); }
      50% { opacity: 0.7; transform: scale(1.1); }
    }

    @keyframes rainbowFlow {
      0% { background-position: 0% 50%; }
      100% { background-position: 100% 50%; }
    }

    @keyframes softFade {
      0%, 100% { opacity: 0.2; }
      50% { opacity: 0.35; }
    }

    /* === Syia === */
    .chibi-container {
      width: 250px; height: 320px; margin-top: 60px;
      position: relative; z-index: 2;
    }

    .chibi { 
      width: 100%; height: auto; 
      filter: drop-shadow(0 4px 8px rgba(0,0,0,0.4));
    }

    /* === Chat === */
    .chat-container { 
      width: 100%; max-width: 500px; background: rgba(255,255,255,0.95); 
      border-radius: 20px 20px 0 0; box-shadow: 0 -10px 30px rgba(0,0,0,0.2); 
      overflow: hidden; display: flex; flex-direction: column; height: 400px; z-index: 2; 
    }
    .chat-header { 
      padding: 14px 15px; background: #a29bfe; color: white; 
      font-weight: bold; text-align: center; font-size: 16px; 
    }
    .chat-messages { 
      flex: 1; padding: 15px; overflow-y: auto; 
      display: flex; flex-direction: column; gap: 10px; background: #f8f9fa; 
    }
    .message { 
      max-width: 80%; padding: 10px 15px; border-radius: 18px; 
      line-height: 1.4; font-size: 15px; animation: fadeIn 0.3s ease; 
    }
    .user { align-self: flex-end; background: #74b9ff; color: white; border-bottom-right-radius: 5px; }
    .bot { align-self: flex-start; background: #dfe6e9; color: #2d3436; border-bottom-left-radius: 5px; }
    .admin { align-self: flex-end; background: #55a3ff; color: white; border-bottom-right-radius: 5px; }
    @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

    .chat-input { 
      display: flex; padding: 10px; background: white; border-top: 1px solid #eee; 
    }
    .chat-input input { 
      flex: 1; padding: 12px 15px; border: 1px solid #ddd; 
      border-radius: 25px; font-size: 15px; outline: none; 
    }
    .chat-input input:focus { border-color: #a29bfe; }
    .chat-input button { 
      margin-left: 8px; padding: 0 18px; background: #a29bfe; 
      color: white; border: none; border-radius: 25px; 
      font-size: 14px; cursor: pointer; 
    }
    .chat-input button:hover { background: #7866e0; }

    .admin-mode { 
      background: #fff3cd; border: 1px solid #ffeaa7; 
      padding: 10px; font-size: 14px; text-align: center; color: #856404; 
    }

    .title { 
      position: absolute; top: 20px; left: 20px; 
      font-size: 24px; font-weight: bold; color: #dfe6e9; 
      text-shadow: 0 2px 5px rgba(0,0,0,0.3); z-index: 1; 
    }

    /* === Tombol Play Musik === */
    .play-btn {
      position: absolute; top: 20px; right: 20px;
      background: rgba(255,255,255,0.2); color: white;
      border: none; border-radius: 50%; width: 40px; height: 40px;
      font-size: 20px; cursor: pointer; backdrop-filter: blur(5px);
      z-index: 10; display: flex; align-items: center; justify-content: center;
    }
    .play-btn:hover { background: rgba(255,255,255,0.3); }
    .play-btn.playing { background: #a29bfe; }
  </style>
</head>
<body>

  <!-- Background + Efek Cahaya + Pelangi -->
  <div class="bg-container"></div>
  <div class="corner-lights">
    <div class="corner top-left"></div>
    <div class="corner top-right"></div>
    <div class="corner bottom-left"></div>
    <div class="corner bottom-right"></div>
  </div>
  <div class="rainbow-glow"></div>

  <div class="title">Syia – Teman Curhat</div>

  <!-- Tombol Play Musik & Hujan -->
  <button class="play-btn" id="playBtn">Play Music</button>

  <!-- Syia -->
  <div class="chibi-container">
    <img src="https://i.postimg.cc/K8y652Ht/5cb138d8-7482-4a9d-bff2-0d87ee0d2980.png" alt="Syia" class="chibi" />
  </div>

  <!-- Chat -->
  <div class="chat-container">
    <div class="chat-header" id="header">Syia 🌷</div>
    <div class="chat-messages" id="messages"></div>

    <div id="adminNotice" class="admin-mode" style="display:none;">
      Kamu sedang di <strong>Mode Admin</strong> — Balas dengan hangat!
    </div>

    <div class="chat-input">
      <input type="text" id="userInput" placeholder="Curhat sama Syia..." autocomplete="off" />
      <button id="sendBtn">Kirim</button>
    </div>
  </div>

  <!-- Audio -->
  <audio id="lofiMusic" loop>
    <source src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_8d9e2d7f3f.mp3" type="audio/mpeg">
  </audio>
  <audio id="rainSound" loop>
    <source src="https://cdn.pixabay.com/download/audio/2022/03/24/audio_6eef18d9c8.mp3" type="audio/mpeg">
  </audio>

  <script>
    const urlParams = new URLSearchParams(window.location.search);
    const isAdmin = urlParams.get('admin') === '1';

    const messagesDiv = document.getElementById('messages');
    const input = document.getElementById('userInput');
    const sendBtn = document.getElementById('sendBtn');
    const header = document.getElementById('header');
    const adminNotice = document.getElementById('adminNotice');
    const playBtn = document.getElementById('playBtn');

    const lofi = document.getElementById('lofiMusic');
    const rain = document.getElementById('rainSound');
    let isPlaying = false;

    // === PLAY MUSIK & HUJAN ===
    playBtn.addEventListener('click', () => {
      if (isPlaying) return;
      
      lofi.volume = 0.15;
      rain.volume = 0.25;

      Promise.all([
        lofi.play(),
        rain.play()
      ]).then(() => {
        isPlaying = true;
        playBtn.textContent = 'Music On';
        playBtn.classList.add('playing');
        playBtn.disabled = true;
      }).catch(err => {
        console.log("Audio gagal diputar:", err);
      });
    });

    const STORAGE_KEY = 'syia_curhat_clean';
    let messages = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];

    const botResponses = {
      nama: ["Aku Syia, teman curhatmu!", "Namaku Syia, salam kenal!"],
      halo: ["Halo! Mau curhat apa?", "Hai! Syia di sini"],
      sedih: ["Sini syia peluk", "Kamu nggak sendiri, syia disini selalu ada untuk kamu"],
      capek: ["Istirahat dulu yuk, kamu hebat udah bisa sejauh ini", "Aku denger kamu. Capeknya kamu itu penting. Kadang kita terlalu banyak mikir, terlalu banyak ngerasa, terlalu banyak ngasih energi ke dunia, sampai lupa isi ulang buat diri sendiri. Kalau kamu mau cerita, aku di sini. Kamu nggak sendirian.!"],
      seneng: ["Ada cerita apa hari ini", "seneng kenapaa tuuh cerita dongg"], 
      cinta: ["Cinta emang rumit ya... Tapi kamu berhak bahagia, lho.", "Putus cinta? Sakit, tapi kamu bakal ketemu yang lebih sayang kamu."],
      takut: ["Takut itu wajar. Tapi kamu lebih kuat dari yang kamu kira.", "Tenang, tarik napas dalam-dalam. Syia nemenin."],
      marah: ["Marah boleh, tapi jangan sampe nyakitin diri sendiri ya.", "Ceritain, siapa yang bikin kamu marah?"],
      default: ["Syia dengerin kamu...", "Tenang, ada Syia", "Semua akan baik-baik aja"]
    };

    function getBotReply(text) {
      const lower = text.toLowerCase();
      if (lower.includes('nama') || lower.includes('siapa')) return getRandom(botResponses.nama);
      if (lower.includes('halo') || lower.includes('hai')) return getRandom(botResponses.halo);
      if (lower.includes('sedih') || lower.includes('susah') || lower.includes('nangis')) return getRandom(botResponses.sedih);
      if (lower.includes('capek') || lower.includes('lelah') || lower.includes('stres')) return getRandom(botResponses.capek);
      if (lower.includes('seneng') || lower.includes('senang') || lower.includes('happy')) return getRandom(botResponses.seneng);
      if (lower.includes('cinta') || lower.includes('pacar') || lower.includes('putus')) return getRandom(botResponses.cinta);
      if (lower.includes('takut') || lower.includes('khawatir') || lower.includes('cemas')) return getRandom(botResponses.takut);
      if (lower.includes('marah') || lower.includes('kesel') || lower.includes('ganggu')) return getRandom(botResponses.marah);
      return getRandom(botResponses.default);
    }

    function getRandom(arr) { return arr[Math.floor(Math.random() * arr.length)]; }

    function renderMessages() {
      messagesDiv.innerHTML = '';
      messages.forEach(msg => {
        const div = document.createElement('div');
        div.className = `message ${msg.type}`;
        div.textContent = msg.text;
        messagesDiv.appendChild(div);
      });
      messagesDiv.scrollTop = messagesDiv.scrollHeight;
    }

    function addMessage(text, type) {
      messages.push({ text, type, time: Date.now() });
      localStorage.setItem(STORAGE_KEY, JSON.stringify(messages));
      renderMessages();
    }

    function sendMessage() {
      const text = input.value.trim();
      if (!text) return;
      const type = isAdmin ? 'admin' : 'user';
      addMessage(text, type);
      input.value = '';
      
      // BOT HANYA JAWAB OTOMATIS JIKA TIDAK ADA ADMIN
      if (!isAdmin && type === 'user') {
        setTimeout(() => addMessage(getBotReply(text), 'bot'), 1200);
      }
    }

    sendBtn.addEventListener('click', sendMessage);
    input.addEventListener('keypress', e => { if (e.key === 'Enter') sendMessage(); });

    if (isAdmin) {
      header.textContent = 'Admin: Balas Pesan';
      adminNotice.style.display = 'block';
      input.placeholder = 'Ketik balasan...';
    } else {
      header.textContent = 'Syia – Teman Curhat';
      setTimeout(() => addMessage('Halo! Mau curhat apa malam ini?', 'bot'), 1000);
    }

    // Sync antar tab (user & admin)
    setInterval(() => {
      const stored = localStorage.getItem(STORAGE_KEY);
      if (stored) {
        const updated = JSON.parse(stored);
        if (JSON.stringify(updated) !== JSON.stringify(messages)) {
          messages = updated;
          renderMessages();
        }
      }
    }, 800);

    renderMessages();
    input.focus();
  </script>
</body>
</html>
