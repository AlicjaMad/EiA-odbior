<!DOCTYPE html>
<html lang="pl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Odbiór urządzeń elektrycznych</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 0; padding: 0; }
    nav { background-color: #333; padding: 10px; }
    nav a {
      color: white; padding: 10px 15px; text-decoration: none;
      display: inline-block;
    }
    nav a:hover { background-color: #575757; }
    .tab-content { padding: 20px; display: none; }
    .tab-content.active { display: block; }
    table { width: 100%; border-collapse: collapse; }
    th, td { border: 1px solid #ccc; padding: 8px; text-align: left; }
    th { background-color: #f4f4f4; }

    @media (max-width: 600px) {
      nav a { display: block; margin-bottom: 10px; }
      table, thead, tbody, th, td, tr { display: block; width: 100%; }
      td { padding: 10px; border: none; border-bottom: 1px solid #ccc; }
    }
  </style>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
</head>
<body>

<!-- Pasek nawigacji -->
<nav>
  <a href="#" onclick="showTab('login')">Logowanie</a>
  <a href="#" onclick="showTab('dane-ogolne')">Dane ogólne</a>
  <a href="#" onclick="showTab('lista-urzadzen')">Lista urządzeń</a>
  <a href="#" onclick="showTab('sprawdzenia')">Punkty kontrolne</a>
  <a href="#" onclick="showTab('podsumowanie')">Podsumowanie</a>
</nav>

<!-- Zakładki -->
<div id="login" class="tab-content active">
  <h2>Logowanie</h2>
  <form onsubmit="return loginUser(event)">
    <label>Login: <input type="text" id="login-user" required /></label><br/><br/>
    <label>Hasło: <input type="password" id="login-pass" required /></label><br/><br/>
    <button type="submit">Zaloguj</button>
  </form>
</div>

<div id="dane-ogolne" class="tab-content">
  <h2>Dane ogólne</h2>
  <form>
    <label>Nazwa zakładu: <input type="text" name="zaklad" /></label><br/><br/>
    <label>Data odbioru: <input type="date" name="data" /></label><br/><br/>
    <label>Odbierający: <input type="text" name="osoba" /></label>
  </form>
</div>

<div id="lista-urzadzen" class="tab-content">
  <h2>Lista urządzeń</h2>
  <table>
    <thead>
      <tr><th>Nazwa urządzenia</th><th>Typ</th><th>Nr seryjny</th></tr>
    </thead>
    <tbody>
      <tr><td>Silnik M1</td><td>Silnik trójfazowy</td><td>SM1-45678</td></tr>
      <tr><td>Szafa sterownicza</td><td>Rozdzielnica</td><td>RSZ-2023-001</td></tr>
    </tbody>
  </table>
</div>

<div id="sprawdzenia" class="tab-content">
  <h2>Punkty kontrolne (wg PN-EN 60204-1)</h2>
  <ul>
    <li>Sprawdzenie poprawności uziemienia</li>
    <li>Kontrola zabezpieczeń przed dotykiem bezpośrednim</li>
    <li>Sprawdzenie oznaczeń przewodów</li>
    <li>Pomiar rezystancji izolacji</li>
    <li>Test działania wyłączników awaryjnych</li>
  </ul>
</div>

<div id="podsumowanie" class="tab-content">
  <h2>Podsumowanie odbioru</h2>
  <p>Odbiór zakończony <strong>pozytywnie</strong>.</p>
  <p>Dokumentacja zostanie dołączona do systemu ERP.</p>
  <button onclick="saveData()">Pobierz dane JSON</button>
  <button onclick="generatePDF()">Eksportuj do PDF</button>
  <button onclick="sendToERP()">Prześlij do ERP</button>
</div>

<!-- Skrypt -->
<script>
  function showTab(tabId) {
    const tabs = document.querySelectorAll(".tab-content");
    tabs.forEach(tab => tab.classList.remove("active"));
    document.getElementById(tabId).classList.add("active");
  }

  function loginUser(event) {
    event.preventDefault();
    const user = document.getElementById('login-user').value;
    const pass = document.getElementById('login-pass').value;

    if (user === 'inspektor' && pass === '1234') {
      alert('Zalogowano!');
      showTab('dane-ogolne');
    } else {
      alert('Błędne dane logowania');
    }
  }

  function saveData() {
    const data = {
      zaklad: document.querySelector('[name="zaklad"]').value,
      data: document.querySelector('[name="data"]').value,
      osoba: document.querySelector('[name="osoba"]').value
    };

    const blob = new Blob([JSON.stringify(data, null, 2)], {type : 'application/json'});
    const link = document.createElement('a');
    link.href = URL.createObjectURL(blob);
    link.download = `raport_odbioru_${Date.now()}.json`;
    link.click();
  }

  async function generatePDF() {
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF();

    doc.text("Raport odbioru urządzeń elektrycznych", 10, 10);
    doc.text("Zakład: " + document.querySelector('[name="zaklad"]').value, 10, 20);
    doc.text("Data: " + document.querySelector('[name="data"]').value, 10, 30);
    doc.text("Odbierający: " + document.querySelector('[name="osoba"]').value, 10, 40);
    doc.save("raport_odbioru.pdf");
  }

  function sendToERP() {
    const data = {
      zaklad: document.querySelector('[name="zaklad"]').value,
      data: document.querySelector('[name="data"]').value,
      osoba: document.querySelector('[name="osoba"]').value
    };

    fetch('https://twoj-erp-api.pl/odbior', {
      method: 'POST',
      headers: {'Content-Type': 'application/json'},
      body: JSON.stringify(data)
    })
    .then(res => {
      if (res.ok) {
        alert("Dane przesłane do ERP");
      } else {
        alert("Błąd przesyłania");
      }
    }).catch(() => alert("Nie udało się połączyć z ERP"));
  }
</script>

</body>
</html>

