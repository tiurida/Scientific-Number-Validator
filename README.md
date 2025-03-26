<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Scientific Number Validator</title>
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
</head>
<body>
  <!-- Tombol "About" di sudut kanan atas -->
  <div class="top-right">
    <button id="about-button">About</button>
  </div>

  <!-- Container utama yang ingin kita letakkan di tengah -->
  <div class="container">
    <input type="text" id="number-input" placeholder="Enter a number">
    <button id="validate-button">Validate Number</button>
    <div id="result">
      <p id="number"></p>
      <p id="validity"></p>
    </div>
  </div>

  <!-- Modal Overlay (jika Anda menggunakan modal untuk About) -->
  <div id="about-modal" class="modal">
    <div class="modal-content">
      <span id="close-modal" class="close">&times;</span>
      <h2>Hallo,</h2>
      <p>Saya Tiurida Pasaribu</p>
      <p>dengan NIM 231011060051</p>
      <p>dari Program Studi Sistem Informasi</p>
    </div>
  </div>

  <!-- JavaScript -->
  <script>
    // Tombol "Validate"
    document.getElementById('validate-button').addEventListener('click', async function() {
      const number = document.getElementById('number-input').value;
      try {
        const response = await fetch('/validate', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded',
          },
          body: `number=${encodeURIComponent(number)}`
        });
        const data = await response.json();
        document.getElementById('number').innerText = `Entered Number: ${data.number}`;
        document.getElementById('validity').innerText = `Is Valid: ${data.valid}`;
      } catch (error) {
        document.getElementById('validity').innerText = 'Error: Unable to validate the number.';
        console.error('Error:', error);
      }
    });

    // Tombol "About" untuk membuka modal
    const aboutButton = document.getElementById('about-button');
    const aboutModal = document.getElementById('about-modal');
    const closeModal = document.getElementById('close-modal');

    aboutButton.addEventListener('click', () => {
      aboutModal.style.display = 'block';
    });

    // Tombol "x" (close) pada modal
    closeModal.addEventListener('click', () => {
      aboutModal.style.display = 'none';
    });

    // Menutup modal jika user klik di luar kotak modal
    window.addEventListener('click', (event) => {
      if (event.target === aboutModal) {
        aboutModal.style.display = 'none';
      }
    });
  </script>
</body>
</html>
