<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>System Odbiorów Maszyn - Elektryka i Automatyka</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Arial, sans-serif;
            background: #f5f5f5;
            color: #333;
            line-height: 1.6;
        }

        .header {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: white;
            padding: 20px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .header h1 {
            font-size: 24px;
            margin-bottom: 10px;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        .navigation {
            display: flex;
            gap: 10px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 10px 20px;
            background: white;
            border: 2px solid #2a5298;
            color: #2a5298;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 500;
            transition: all 0.3s;
        }

        .nav-btn:hover {
            background: #2a5298;
            color: white;
        }

        .nav-btn.active {
            background: #2a5298;
            color: white;
        }

        .section {
            display: none;
            animation: fadeIn 0.3s ease-in;
        }

        .section.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .card {
            background: white;
            border-radius: 8px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        .card h2 {
            color: #2a5298;
            margin-bottom: 20px;
            font-size: 20px;
            border-bottom: 2px solid #e0e0e0;
            padding-bottom: 10px;
        }

        .checklist-item {
            display: flex;
            align-items: center;
            padding: 10px;
            margin-bottom: 10px;
            background: #f8f9fa;
            border-radius: 5px;
            transition: background 0.2s;
        }

        .checklist-item:hover {
            background: #e9ecef;
        }

        .checklist-item input[type="checkbox"] {
            width: 20px;
            height: 20px;
            margin-right: 15px;
            cursor: pointer;
        }

        .checklist-item label {
            flex: 1;
            cursor: pointer;
            font-weight: 500;
        }

        .status {
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
            text-transform: uppercase;
        }

        .status.ok { background: #d4edda; color: #155724; }
        .status.warning { background: #fff3cd; color: #856404; }
        .status.error { background: #f8d7da; color: #721c24; }
        .status.pending { background: #e2e3e5; color: #383d41; }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
            color: #555;
        }

        .form-group input, .form-group select, .form-group textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 14px;
            transition: border-color 0.3s;
        }

        .form-group input:focus, .form-group select:focus, .form-group textarea:focus {
            outline: none;
            border-color: #2a5298;
        }

        .btn {
            padding: 12px 24px;
            background: #2a5298;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 500;
            transition: background 0.3s;
        }

        .btn:hover {
            background: #1e3c72;
        }

        .btn-secondary {
            background: #6c757d;
        }

        .btn-secondary:hover {
            background: #5a6268;
        }

        .btn-success {
            background: #28a745;
        }

        .btn-success:hover {
            background: #218838;
        }

        .calculator-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }

        .result-box {
            padding: 15px;
            background: #e8f4f8;
            border-left: 4px solid #2a5298;
            border-radius: 5px;
            margin-top: 15px;
        }

        .result-box h4 {
            color: #2a5298;
            margin-bottom: 10px;
        }

        .measurement-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        .measurement-table th, .measurement-table td {
            border: 1px solid #ddd;
            padding: 12px;
            text-align: left;
        }

        .measurement-table th {
            background: #2a5298;
            color: white;
            font-weight: 600;
        }

        .measurement-table tr:nth-child(even) {
            background: #f8f9fa;
        }

        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            animation: fadeIn 0.3s;
        }

        .modal-content {
            background: white;
            margin: 50px auto;
            padding: 30px;
            width: 90%;
            max-width: 800px;
            border-radius: 10px;
            position: relative;
            animation: slideIn 0.3s;
            max-height: 80vh;
            overflow-y: auto;
        }

        @keyframes slideIn {
            from { transform: translateY(-50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        .close {
            position: absolute;
            right: 20px;
            top: 20px;
            font-size: 30px;
            cursor: pointer;
            color: #aaa;
            transition: color 0.3s;
        }

        .close:hover {
            color: #333;
        }

        .progress-bar {
            width: 100%;
            height: 30px;
            background: #e0e0e0;
            border-radius: 15px;
            overflow: hidden;
            margin-bottom: 20px;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #28a745 0%, #20c997 100%);
            transition: width 0.5s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
        }

        .warning-box {
            padding: 15px;
            background: #fff3cd;
            border-left: 4px solid #ffc107;
            border-radius: 5px;
            margin: 10px 0;
        }

        .error-box {
            padding: 15px;
            background: #f8d7da;
            border-left: 4px solid #dc3545;
            border-radius: 5px;
            margin: 10px 0;
        }

        .info-box {
            padding: 15px;
            background: #d1ecf1;
            border-left: 4px solid #17a2b8;
            border-radius: 5px;
            margin: 10px 0;
        }

        .issue-item {
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 5px;
            border: 1px solid #ddd;
            background: #f8f9fa;
        }

        .issue-category {
            display: inline-block;
            padding: 3px 10px;
            border-radius: 3px;
            font-size: 12px;
            font-weight: 600;
            margin-right: 10px;
        }

        .issue-category.A { background: #dc3545; color: white; }
        .issue-category.B { background: #ffc107; color: #333; }
        .issue-category.C { background: #6c757d; color: white; }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 20px;
            }
            
            .nav-btn {
                font-size: 14px;
                padding: 8px 16px;
            }
            
            .container {
                padding: 10px;
            }
        }

        @media print {
            .navigation, .btn, .nav-btn {
                display: none !important;
            }
            
            .card {
                break-inside: avoid;
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>🔧 System Odbiorów Maszyn Przemysłowych - Elektryka i Automatyka</h1>
        <p>Kompleksowe narzędzie do przeprowadzania odbiorów technicznych</p>
    </div>

    <div class="container">
        <div class="navigation">
            <button class="nav-btn active" onclick="showSection('info', this)">📋 Informacje</button>
            <button class="nav-btn" onclick="showSection('checklist', this)">✅ Checklista</button>
            <button class="nav-btn" onclick="showSection('measurements', this)">📊 Pomiary</button>
            <button class="nav-btn" onclick="showSection('calculators', this)">🧮 Kalkulatory</button>
            <button class="nav-btn" onclick="showSection('safety', this)">⚠️ Bezpieczeństwo</button>
            <button class="nav-btn" onclick="showSection('report', this)">📄 Raport</button>
        </div>

        <!-- Sekcja: Informacje -->
        <div id="info" class="section active">
            <div class="card">
                <h2>Informacje o odbiorze</h2>
                <div class="form-group">
                    <label>Nazwa maszyny:</label>
                    <input type="text" id="machineName" placeholder="np. Prasa hydrauliczna P-01">
                </div>
                <div class="calculator-grid">
                    <div class="form-group">
                        <label>Numer seryjny:</label>
                        <input type="text" id="serialNumber" placeholder="np. 2024/001/PL">
                    </div>
                    <div class="form-group">
                        <label>Producent:</label>
                        <input type="text" id="manufacturer" placeholder="np. TechMachines Sp. z o.o.">
                    </div>
                </div>
                <div class="calculator-grid">
                    <div class="form-group">
                        <label>Data odbioru:</label>
                        <input type="date" id="inspectionDate" value="">
                    </div>
                    <div class="form-group">
                        <label>Osoba przeprowadzająca:</label>
                        <input type="text" id="inspector" placeholder="Imię i nazwisko">
                    </div>
                </div>
                <div class="form-group">
                    <label>Lokalizacja:</label>
                    <input type="text" id="location" placeholder="np. Hala produkcyjna A, stanowisko 5">
                </div>
            </div>

            <div class="card">
                <h2>Postęp odbioru</h2>
                <div class="progress-bar">
                    <div class="progress-fill" id="progressBar">0%</div>
                </div>
                <div id="progressDetails"></div>
            </div>
        </div>

        <!-- Sekcja: Checklista -->
        <div id="checklist" class="section">
            <div class="card">
                <h2>Dokumentacja</h2>
                <div id="documentationChecklist"></div>
            </div>

            <div class="card">
                <h2>Zasilanie i rozdzielnice</h2>
                <div id="powerChecklist"></div>
            </div>

            <div class="card">
                <h2>Bezpieczeństwo funkcjonalne</h2>
                <div id="safetyChecklist"></div>
            </div>

            <div class="card">
                <h2>Automatyka i sterowanie</h2>
                <div id="automationChecklist"></div>
            </div>

            <div class="card">
                <h2>Napędy i silniki</h2>
                <div id="drivesChecklist"></div>
            </div>
        </div>

        <!-- Sekcja: Pomiary -->
        <div id="measurements" class="section">
            <div class="card">
                <h2>Pomiary elektryczne</h2>
                <table class="measurement-table">
                    <thead>
                        <tr>
                            <th>Parametr</th>
                            <th>Wartość zmierzona</th>
                            <th>Wartość dopuszczalna</th>
                            <th>Status</th>
                        </tr>
                    </thead>
                    <tbody id="electricalMeasurements"></tbody>
                </table>
                <button class="btn" onclick="addMeasurement('electrical')" style="margin-top: 15px;">➕ Dodaj pomiar</button>
            </div>

            <div class="card">
                <h2>Pomiary bezpieczeństwa</h2>
                <table class="measurement-table">
                    <thead>
                        <tr>
                            <th>Funkcja bezpieczeństwa</th>
                            <th>Czas reakcji [ms]</th>
                            <th>Limit [ms]</th>
                            <th>Status</th>
                        </tr>
                    </thead>
                    <tbody id="safetyMeasurements"></tbody>
                </table>
                <button class="btn" onclick="addMeasurement('safety')" style="margin-top: 15px;">➕ Dodaj pomiar</button>
            </div>
        </div>

        <!-- Sekcja: Kalkulatory -->
        <div id="calculators" class="section">
            <div class="card">
                <h2>Kalkulator impedancji pętli zwarcia</h2>
                <div class="calculator-grid">
                    <div class="form-group">
                        <label>Typ zabezpieczenia:</label>
                        <select id="protectionType">
                            <option value="B">Typ B</option>
                            <option value="C">Typ C</option>
                            <option value="D">Typ D</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Prąd znamionowy [A]:</label>
                        <input type="number" id="ratedCurrent" placeholder="np. 16">
                    </div>
                    <div class="form-group">
                        <label>Napięcie [V]:</label>
                        <input type="number" id="voltage" value="230">
                    </div>
                </div>
                <button class="btn" onclick="calculateLoopImpedance()">Oblicz max. impedancję</button>
                <div id="loopResult"></div>
            </div>

            <div class="card">
                <h2>Kalkulator mocy transformatora</h2>
                <div class="calculator-grid">
                    <div class="form-group">
                        <label>Moc PLC [W]:</label>
                        <input type="number" id="plcPower" placeholder="np. 50">
                    </div>
                    <div class="form-group">
                        <label>Moc I/O [W]:</label>
                        <input type="number" id="ioPower" placeholder="np. 200">
                    </div>
                    <div class="form-group">
                        <label>Moc HMI [W]:</label>
                        <input type="number" id="hmiPower" placeholder="np. 30">
                    </div>
                    <div class="form-group">
                        <label>Inne obciążenia [W]:</label>
                        <input type="number" id="otherPower" placeholder="np. 100">
                    </div>
                </div>
                <button class="btn" onclick="calculateTransformerPower()">Oblicz moc transformatora</button>
                <div id="transformerResult"></div>
            </div>

            <div class="card">
                <h2>Kalkulator bezpiecznej odległości (kurtyny świetlne)</h2>
                <div class="calculator-grid">
                    <div class="form-group">
                        <label>Czas zatrzymania maszyny [s]:</label>
                        <input type="number" id="stopTime" step="0.01" placeholder="np. 0.5">
                    </div>
                    <div class="form-group">
                        <label>Rozdzielczość kurtyny [mm]:</label>
                        <input type="number" id="resolution" placeholder="np. 14 lub 30">
                    </div>
                </div>
                <button class="btn" onclick="calculateSafeDistance()">Oblicz odległość</button>
                <div id="safeDistanceResult"></div>
            </div>

            <div class="card">
                <h2>Kalkulator kabla Ex (iskrobezpieczność)</h2>
                <div class="calculator-grid">
                    <div class="form-group">
                        <label>Długość kabla [m]:</label>
                        <input type="number" id="cableLength" placeholder="np. 100">
                    </div>
                    <div class="form-group">
                        <label>Co bariery [nF]:</label>
                        <input type="number" id="barrierCo" placeholder="np. 83">
                    </div>
                    <div class="form-group">
                        <label>Lo bariery [μH]:</label>
                        <input type="number" id="barrierLo" placeholder="np. 650">
                    </div>
                </div>
                <button class="btn" onclick="calculateExCable()">Sprawdź parametry</button>
                <div id="exCableResult"></div>
            </div>
        </div>

        <!-- Sekcja: Bezpieczeństwo -->
        <div id="safety" class="section">
            <div class="card">
                <h2>Funkcje bezpieczeństwa</h2>
                <div id="safetyFunctions"></div>
                <button class="btn" onclick="addSafetyFunction()" style="margin-top: 15px;">➕ Dodaj funkcję</button>
            </div>

            <div class="card">
                <h2>Analiza Performance Level (PL)</h2>
                <div class="form-group">
                    <label>Wybierz funkcję bezpieczeństwa:</label>
                    <select id="plFunction" onchange="updatePLAnalysis()">
                        <option value="">-- Wybierz funkcję --</option>
                    </select>
                </div>
                <div id="plAnalysis"></div>
            </div>
        </div>

        <!-- Sekcja: Raport -->
        <div id="report" class="section">
            <div class="card">
                <h2>Podsumowanie odbioru</h2>
                <div id="reportSummary"></div>
            </div>

            <div class="card">
                <h2>Usterki i uwagi</h2>
                <div id="issuesList"></div>
                <button class="btn btn-secondary" onclick="addIssue()" style="margin-top: 15px;">➕ Dodaj usterkę</button>
            </div>

            <div class="card">
                <h2>Generowanie raportu</h2>
                <div class="form-group">
                    <label>Uwagi końcowe:</label>
                    <textarea id="finalNotes" rows="4" placeholder="Dodatkowe uwagi do raportu..."></textarea>
                </div>
                <div style="display: flex; gap: 10px; margin-top: 20px;">
                    <button class="btn btn-success" onclick="generateReport()">📄 Generuj raport PDF</button>
                    <button class="btn" onclick="saveData()">💾 Zapisz dane</button>
                    <button class="btn btn-secondary" onclick="loadData()">📂 Wczytaj dane</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal -->
    <div id="modal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal()">&times;</span>
            <div id="modalContent"></div>
        </div>
    </div>

    <script>
        // Stan aplikacji
        var appState = {
            info: {},
            checklist: {
                documentation: [],
                power: [],
                safety: [],
                automation: [],
                drives: []
            },
            measurements: {
                electrical: [],
                safety: []
            },
            safetyFunctions: [],
            issues: [],
            progress: 0
        };

        // Funkcje główne
        function showSection(sectionId, buttonElement) {
            var sections = document.querySelectorAll('.section');
            var buttons = document.querySelectorAll('.nav-btn');
            
            for (var i = 0; i < sections.length; i++) {
                sections[i].classList.remove('active');
            }
            
            for (var i = 0; i < buttons.length; i++) {
                buttons[i].classList.remove('active');
            }
            
            var section = document.getElementById(sectionId);
            if (section) {
                section.classList.add('active');
            }
            
            if (buttonElement) {
                buttonElement.classList.add('active');
            }
            
            if (sectionId === 'report') {
                updateReportSummary();
            }
        }

        document.addEventListener('DOMContentLoaded', function() {
            initializeApp();
            document.getElementById('inspectionDate').value = new Date().toISOString().split('T')[0];
        });

        function initializeApp() {
            initializeChecklists();
            initializeDefaultMeasurements();
            updateProgress();
        }

        function initializeChecklists() {
            var checklists = {
                documentation: [
                    'Deklaracja zgodności CE',
                    'Ocena ryzyka wg PN-EN ISO 12100',
                    'Schematy elektryczne AS-BUILT',
                    'DTR w języku polskim',
                    'Certyfikaty komponentów bezpieczeństwa',
                    'Protokoły walidacji funkcji bezpieczeństwa',
                    'Lista części zamiennych',
                    'Instrukcja BHP stanowiska'
                ],
                power: [
                    'Wyłącznik główny z blokadą LOTO',
                    'Zabezpieczenia zgodne z projektem',
                    'Oznaczenia obwodów w rozdzielnicy',
                    'Transformator sterowniczy - parametry',
                    'Gniazda serwisowe z RCD 30mA',
                    'Uziemienie i połączenia wyrównawcze',
                    'Oświetlenie maszyny',
                    'Wentylacja szaf sterowniczych'
                ],
                safety: [
                    'Wszystkie E-STOP działające',
                    'Kurtyny świetlne skalibrowane',
                    'Blokady bezpieczeństwa na osłonach',
                    'Przekaźniki bezpieczeństwa - test',
                    'Performance Level zgodny z oceną ryzyka',
                    'Dwukanałowość obwodów STOP',
                    'Test czasów zatrzymania',
                    'Reset bezpieczeństwa wymagany'
                ],
                automation: [
                    'Program PLC - backup wykonany',
                    'HMI - wszystkie ekrany działające',
                    'Komunikacja sieciowa stabilna',
                    'Alarmy i ich opisy',
                    'Receptury - zapis/odczyt',
                    'Trendy i archiwizacja danych',
                    'Uprawnienia użytkowników',
                    'Integracja z systemami fabryki'
                ],
                drives: [
                    'Parametry silników wprowadzone',
                    'Rampy przysp./hamowania ustawione',
                    'Zabezpieczenia termiczne',
                    'Kierunki obrotów prawidłowe',
                    'Enkodery skalibrowane',
                    'Safe Torque Off (STO) działa',
                    'Filtry EMC zainstalowane',
                    'Rezystory hamowania sprawdzone'
                ]
            };

            for (var category in checklists) {
                var items = checklists[category];
                var container = document.getElementById(category + 'Checklist');
                if (container) {
                    var html = '';
                    for (var i = 0; i < items.length; i++) {
                        html += '<div class="checklist-item">' +
                            '<input type="checkbox" id="' + category + '_' + i + '" onchange="updateChecklistItem(\'' + category + '\', ' + i + ')">' +
                            '<label for="' + category + '_' + i + '">' + items[i] + '</label>' +
                            '<span class="status" id="' + category + '_status_' + i + '"></span>' +
                            '</div>';
                    }
                    container.innerHTML = html;
                }
                
                appState.checklist[category] = [];
                for (var j = 0; j < items.length; j++) {
                    appState.checklist[category].push({ name: items[j], checked: false });
                }
            }
        }

        function initializeDefaultMeasurements() {
            appState.measurements.electrical = [
                { parameter: 'Napięcie L1-L2', value: '', limit: '380-420V', status: 'pending' },
                { parameter: 'Napięcie L2-L3', value: '', limit: '380-420V', status: 'pending' },
                { parameter: 'Napięcie L3-L1', value: '', limit: '380-420V', status: 'pending' },
                { parameter: 'Asymetria napięć', value: '', limit: '<2%', status: 'pending' },
                { parameter: 'Rezystancja izolacji', value: '', limit: '>1MΩ', status: 'pending' },
                { parameter: 'Rezystancja uziemienia', value: '', limit: '<10Ω', status: 'pending' }
            ];

            appState.measurements.safety = [
                { function: 'E-STOP reakcja', time: '', limit: '20', status: 'pending' },
                { function: 'Zatrzymanie kategoria 0', time: '', limit: '2000', status: 'pending' },
                { function: 'Kurtyna świetlna', time: '', limit: '20', status: 'pending' },
                { function: 'Blokada osłony', time: '', limit: '100', status: 'pending' }
            ];

            updateMeasurementTables();
        }

        function updateChecklistItem(category, index) {
            var checkbox = document.getElementById(category + '_' + index);
            var statusElement = document.getElementById(category + '_status_' + index);
            
            appState.checklist[category][index].checked = checkbox.checked;
            
            if (checkbox.checked) {
                statusElement.textContent = 'OK';
                statusElement.className = 'status ok';
            } else {
                statusElement.textContent = '';
            }
            
            updateProgress();
            saveToLocalStorage();
        }

        function updateMeasurementTables() {
            var electricalBody = document.getElementById('electricalMeasurements');
            var electricalHtml = '';
            for (var i = 0; i < appState.measurements.electrical.length; i++) {
                var m = appState.measurements.electrical[i];
                electricalHtml += '<tr>' +
                    '<td>' + m.parameter + '</td>' +
                    '<td><input type="text" value="' + m.value + '" onchange="updateMeasurement(\'electrical\', ' + i + ', this.value)" style="width: 100px; padding: 5px;"></td>' +
                    '<td>' + m.limit + '</td>' +
                    '<td><span class="status ' + m '<td><span class="status ' + m.status + '">' + getStatusText(m.status) + '</span></td>' +
                    '</tr>';
            }
            electricalBody.innerHTML = electricalHtml;

            var safetyBody = document.getElementById('safetyMeasurements');
            var safetyHtml = '';
            for (var j = 0; j < appState.measurements.safety.length; j++) {
                var s = appState.measurements.safety[j];
                safetyHtml += '<tr>' +
                    '<td>' + s.function + '</td>' +
                    '<td><input type="number" value="' + s.time + '" onchange="updateMeasurement(\'safety\', ' + j + ', this.value)" style="width: 100px; padding: 5px;"></td>' +
                    '<td>' + s.limit + '</td>' +
                    '<td><span class="status ' + s.status + '">' + getStatusText(s.status) + '</span></td>' +
                    '</tr>';
            }
            safetyBody.innerHTML = safetyHtml;
        }

        function getStatusText(status) {
            switch(status) {
                case 'ok': return 'OK';
                case 'warning': return 'Ostrzeżenie';
                case 'error': return 'Błąd';
                case 'pending': return 'Oczekuje';
                default: return '';
            }
        }

        function updateMeasurement(type, index, value) {
            if (type === 'electrical') {
                appState.measurements.electrical[index].value = value;
                if (value && appState.measurements.electrical[index].parameter.includes('Napięcie')) {
                    var numValue = parseFloat(value);
                    appState.measurements.electrical[index].status = 
                        (numValue >= 380 && numValue <= 420) ? 'ok' : 'error';
                } else if (value && appState.measurements.electrical[index].parameter.includes('Asymetria')) {
                    var numValue = parseFloat(value);
                    appState.measurements.electrical[index].status = numValue < 2 ? 'ok' : 'error';
                } else if (value && appState.measurements.electrical[index].parameter.includes('izolacji')) {
                    var numValue = parseFloat(value);
                    appState.measurements.electrical[index].status = numValue >= 1 ? 'ok' : 'error';
                } else if (value && appState.measurements.electrical[index].parameter.includes('uziemienia')) {
                    var numValue = parseFloat(value);
                    appState.measurements.electrical[index].status = numValue < 10 ? 'ok' : 'error';
                } else if (value) {
                    appState.measurements.electrical[index].status = 'ok';
                }
            } else if (type === 'safety') {
                appState.measurements.safety[index].time = value;
                if (value) {
                    var numValue = parseFloat(value);
                    var limit = parseFloat(appState.measurements.safety[index].limit);
                    appState.measurements.safety[index].status = numValue <= limit ? 'ok' : 'error';
                }
            }
            updateMeasurementTables();
            updateProgress();
            saveToLocalStorage();
        }

        function addMeasurement(type) {
            var modalContent = document.getElementById('modalContent');
            
            if (type === 'electrical') {
                modalContent.innerHTML = 
                    '<h3>Dodaj pomiar elektryczny</h3>' +
                    '<div class="form-group">' +
                    '<label>Parametr:</label>' +
                    '<input type="text" id="newParameter" placeholder="np. Prąd silnika M1">' +
                    '</div>' +
                    '<div class="form-group">' +
                    '<label>Wartość dopuszczalna:</label>' +
                    '<input type="text" id="newLimit" placeholder="np. <16A">' +
                    '</div>' +
                    '<button class="btn" onclick="confirmAddMeasurement(\'electrical\')">Dodaj</button>';
            } else {
                modalContent.innerHTML = 
                    '<h3>Dodaj pomiar bezpieczeństwa</h3>' +
                    '<div class="form-group">' +
                    '<label>Funkcja bezpieczeństwa:</label>' +
                    '<input type="text" id="newFunction" placeholder="np. Wyłącznik drzwiowy">' +
                    '</div>' +
                    '<div class="form-group">' +
                    '<label>Limit czasu [ms]:</label>' +
                    '<input type="number" id="newTimeLimit" placeholder="np. 50">' +
                    '</div>' +
                    '<button class="btn" onclick="confirmAddMeasurement(\'safety\')">Dodaj</button>';
            }
            
            document.getElementById('modal').style.display = 'block';
        }

        function confirmAddMeasurement(type) {
            if (type === 'electrical') {
                var parameter = document.getElementById('newParameter').value;
                var limit = document.getElementById('newLimit').value;
                if (parameter && limit) {
                    appState.measurements.electrical.push({
                        parameter: parameter,
                        value: '',
                        limit: limit,
                        status: 'pending'
                    });
                }
            } else {
                var func = document.getElementById('newFunction').value;
                var limit = document.getElementById('newTimeLimit').value;
                if (func && limit) {
                    appState.measurements.safety.push({
                        function: func,
                        time: '',
                        limit: limit,
                        status: 'pending'
                    });
                }
            }
            
            updateMeasurementTables();
            closeModal();
            saveToLocalStorage();
        }

        function calculateLoopImpedance() {
            var type = document.getElementById('protectionType').value;
            var current = parseFloat(document.getElementById('ratedCurrent').value);
            var voltage = parseFloat(document.getElementById('voltage').value);
            
            if (!current || !voltage) {
                alert('Wypełnij wszystkie pola!');
                return;
            }
            
            var multiplier;
            switch(type) {
                case 'B': multiplier = 5; break;
                case 'C': multiplier = 10; break;
                case 'D': multiplier = 20; break;
            }
            
            var maxImpedance = voltage / (multiplier * current);
            
            var resultDiv = document.getElementById('loopResult');
            resultDiv.innerHTML = 
                '<div class="result-box">' +
                '<h4>Wynik obliczeń:</h4>' +
                '<p><strong>Maksymalna impedancja pętli zwarcia:</strong> ' + maxImpedance.toFixed(2) + ' Ω</p>' +
                '<p>Dla zabezpieczenia ' + type + current + 'A</p>' +
                '<p>Prąd wyłączenia: ' + (multiplier * current).toFixed(0) + 'A</p>' +
                '<div class="info-box" style="margin-top: 10px;">' +
                '<strong>Uwaga:</strong> Zmierzona impedancja pętli zwarcia musi być mniejsza od tej wartości, ' +
                'aby zapewnić skuteczne wyłączenie w czasie <0,4s.' +
                '</div>' +
                '</div>';
        }

        function calculateTransformerPower() {
            var plc = parseFloat(document.getElementById('plcPower').value) || 0;
            var io = parseFloat(document.getElementById('ioPower').value) || 0;
            var hmi = parseFloat(document.getElementById('hmiPower').value) || 0;
            var other = parseFloat(document.getElementById('otherPower').value) || 0;
            
            var total = plc + io + hmi + other;
            var withFactor = total * 0.8;
            var withReserve = withFactor * 1.2;
            
            var standardPowers = [100, 160, 250, 400, 630, 1000, 1600];
            var recommended = 2000;
            for (var i = 0; i < standardPowers.length; i++) {
                if (standardPowers[i] >= withReserve) {
                    recommended = standardPowers[i];
                    break;
                }
            }
            
            var resultDiv = document.getElementById('transformerResult');
            resultDiv.innerHTML = 
                '<div class="result-box">' +
                '<h4>Wynik obliczeń:</h4>' +
                '<p><strong>Suma mocy:</strong> ' + total + 'W</p>' +
                '<p><strong>Z współczynnikiem jednoczesności (0.8):</strong> ' + withFactor.toFixed(0) + 'W</p>' +
                '<p><strong>Z rezerwą 20%:</strong> ' + withReserve.toFixed(0) + 'W</p>' +
                '<p><strong>Zalecana moc transformatora:</strong> ' + recommended + 'VA</p>' +
                '<div class="warning-box" style="margin-top: 10px;">' +
                '<strong>Pamiętaj:</strong> Transformator powinien mieć ekran elektrostatyczny ' +
                'między uzwojeniami oraz zabezpieczenie termiczne.' +
                '</div>' +
                '</div>';
        }

        function calculateSafeDistance() {
            var stopTime = parseFloat(document.getElementById('stopTime').value);
            var resolution = parseFloat(document.getElementById('resolution').value);
            
            if (!stopTime || !resolution) {
                alert('Wypełnij wszystkie pola!');
                return;
            }
            
            var K = 2000;
            var C = resolution > 14 ? 8 * (resolution - 14) : 0;
            var S = (K * stopTime) + C;
            
            var resultDiv = document.getElementById('safeDistanceResult');
            resultDiv.innerHTML = 
                '<div class="result-box">' +
                '<h4>Wynik obliczeń:</h4>' +
                '<p><strong>Minimalna odległość bezpieczna:</strong> ' + S.toFixed(0) + 'mm</p>' +
                '<p>Dla czasu zatrzymania: ' + stopTime + 's</p>' +
                '<p>Rozdzielczość kurtyny: ' + resolution + 'mm</p>' +
                '<div class="info-box" style="margin-top: 10px;">' +
                '<strong>Wzór:</strong> S = (K × T) + C<br>' +
                'K = 2000mm/s (prędkość ręki)<br>' +
                'T = ' + stopTime + 's (czas zatrzymania)<br>' +
                'C = ' + C + 'mm (dodatkowa odległość)' +
                '</div>' +
                '</div>';
        }

        function calculateExCable() {
            var length = parseFloat(document.getElementById('cableLength').value);
            var barrierCo = parseFloat(document.getElementById('barrierCo').value);
            var barrierLo = parseFloat(document.getElementById('barrierLo').value);
            
            if (!length || !barrierCo || !barrierLo) {
                alert('Wypełnij wszystkie pola!');
                return;
            }
            
            var cableCapacitance = 200;
            var cableInductance = 1;
            
            var totalC = (length * cableCapacitance) / 1000;
            var totalL = length * cableInductance;
            
            var cOK = totalC < barrierCo;
            var lOK = totalL < barrierLo;
            
            var resultDiv = document.getElementById('exCableResult');
            var resultHtml = '<div class="result-box">' +
                '<h4>Wynik obliczeń:</h4>' +
                '<p><strong>Pojemność kabla:</strong> ' + totalC.toFixed(1) + 'nF ' +
                '<span class="status ' + (cOK ? 'ok' : 'error') + '">' + (cOK ? 'OK' : 'ZA DUŻA') + '</span></p>' +
                '<p><strong>Indukcyjność kabla:</strong> ' + totalL + 'μH ' +
                '<span class="status ' + (lOK ? 'ok' : 'error') + '">' + (lOK ? 'OK' : 'ZA DUŻA') + '</span></p>' +
                '<p><strong>Maksymalna pojemność bariery:</strong> ' + barrierCo + 'nF</p>' +
                '<p><strong>Maksymalna indukcyjność bariery:</strong> ' + barrierLo + 'μH</p>';
                
            if (!cOK || !lOK) {
                resultHtml += '<div class="error-box" style="margin-top: 10px;">' +
                    '<strong>Uwaga:</strong> Parametry kabla przekraczają dopuszczalne wartości! ' +
                    'Skróć kabel lub użyj bariery o większych parametrach Co/Lo.</div>';
            } else {
                resultHtml += '<div class="info-box" style="margin-top: 10px;">' +
                    '<strong>OK:</strong> Kabel spełnia wymagania iskrobezpieczności.</div>';
            }
            
            resultHtml += '</div>';
            resultDiv.innerHTML = resultHtml;
        }

        function addSafetyFunction() {
            var modalContent = document.getElementById('modalContent');
            modalContent.innerHTML = 
                '<h3>Dodaj funkcję bezpieczeństwa</h3>' +
                '<div class="form-group">' +
                '<label>Nazwa funkcji:</label>' +
                '<input type="text" id="sfName" placeholder="np. Zatrzymanie awaryjne strefy 1">' +
                '</div>' +
                '<div class="form-group">' +
                '<label>Wymagany Performance Level:</label>' +
                '<select id="sfPL">' +
                '<option value="a">PL a</option>' +
                '<option value="b">PL b</option>' +
                '<option value="c">PL c</option>' +
                '<option value="d">PL d</option>' +
                '<option value="e">PL e</option>' +
                '</select>' +
                '</div>' +
                '<div class="form-group">' +
                '<label>Osiągnięty Performance Level:</label>' +
                '<select id="sfAchievedPL">' +
                '<option value="">Nie określono</option>' +
                '<option value="a">PL a</option>' +
                '<option value="b">PL b</option>' +
                '<option value="c">PL c</option>' +
                '<option value="d">PL d</option>' +
                '<option value="e">PL e</option>' +
                '</select>' +
                '</div>' +
                '<button class="btn" onclick="confirmAddSafetyFunction()">Dodaj</button>';
            document.getElementById('modal').style.display = 'block';
        }

        function confirmAddSafetyFunction() {
            var name = document.getElementById('sfName').value;
            var requiredPL = document.getElementById('sfPL').value;
            var achievedPL = document.getElementById('sfAchievedPL').value;
            
            if (name) {
                appState.safetyFunctions.push({
                    name: name,
                    requiredPL: requiredPL,
                    achievedPL: achievedPL
                });
                updateSafetyFunctions();
                updatePLFunctionSelect();
                closeModal();
                saveToLocalStorage();
            }
        }

        function updateSafetyFunctions() {
            var container = document.getElementById('safetyFunctions');
            var html = '';
            
            for (var i = 0; i < appState.safetyFunctions.length; i++) {
                var sf = appState.safetyFunctions[i];
                var status = !sf.achievedPL ? 'pending' : 
                              sf.achievedPL >= sf.requiredPL ? 'ok' : 'error';
                
                html += '<div class="checklist-item">' +
                    '<strong>' + sf.name + '</strong>' +
                    '<span style="margin-left: 20px;">Wymagany: PL ' + sf.requiredPL + '</span>' +
                    '<span style="margin-left: 20px;">Osiągnięty: ' + 
                    (sf.achievedPL ? 'PL ' + sf.achievedPL : 'Nie określono') + '</span>' +
                    '<span class="status ' + status + '" style="margin-left: auto;">' +
                    (status === 'ok' ? 'Spełniony' : status === 'error' ? 'Niespełniony' : 'Do weryfikacji') +
                    '</span></div>';
            }
            
            container.innerHTML = html;
        }

        function updatePLFunctionSelect() {
            var select = document.getElementById('plFunction');
            var options = '<option value="">-- Wybierz funkcję --</option>';
            
            for (var i = 0; i < appState.safetyFunctions.length; i++) {
                options += '<option value="' + i + '">' + appState.safetyFunctions[i].name + '</option>';
            }
            
            select.innerHTML = options;
        }

        function updatePLAnalysis() {
            var index = document.getElementById('plFunction').value;
            var analysisDiv = document.getElementById('plAnalysis');
            
            if (!index && index !== 0) {
                analysisDiv.innerHTML = '';
                return;
            }
            
            var sf = appState.safetyFunctions[index];
            var html = '<div class="info-box">' +
                '<h4>Analiza funkcji: ' + sf.name + '</h4>' +
                '<p><strong>Wymagany PL:</strong> ' + sf.requiredPL + '</p>' +
                '<p><strong>Osiągnięty PL:</strong> ' + (sf.achievedPL || 'Nie określono') + '</p>';
                
            if (sf.achievedPL) {
                html += '<p><strong>Status:</strong> ' +
                    '<span class="status ' + (sf.achievedPL >= sf.requiredPL ? 'ok' : 'error') + '">' +
                    (sf.achievedPL >= sf.requiredPL ? 'Wymagania spełnione' : 'Wymagania niespełnione') +
                    '</span></p>';
            }
            
            html += '</div>';
            analysisDiv.innerHTML = html;
        }

        function addIssue() {
            var modalContent = document.getElementById('modalContent');
            modalContent.innerHTML = 
                '<h3>Dodaj usterkę</h3>' +
                '<div class="form-group">' +
                '<label>Kategoria:</label>' +
                '<select id="issueCategory">' +
                '<option value="A">A - Krytyczna (brak możliwości pracy)</option>' +
                '<option value="B">B - Ważna (ograniczona funkcjonalność)</option>' +
                '<option value="C">C - Drobna (kosmetyczna)</option>' +
                '</select>' +
                '</div>' +
                '<div class="form-group">' +
                '<label>Opis usterki:</label>' +
                '<textarea id="issueDescription" rows="3" placeholder="Opisz usterkę..."></textarea>' +
                '</div>' +
                '<div class="form-group">' +
                '<label>Termin usunięcia:</label>' +
                '<input type="date" id="issueDeadline">' +
                '</div>' +
                '<button class="btn" onclick="confirmAddIssue()">Dodaj</button>';
            document.getElementById('modal').style.display = 'block';
        }

        function confirmAddIssue() {
            var category = document.getElementById('issueCategory').value;
            var description = document.getElementById('issueDescription').value;
            var deadline = document.getElementById('issueDeadline').value;
            
            if (description) {
                appState.issues.push({
                    category: category,
                    description: description,
                    deadline: deadline,
                    resolved: false
                });
                updateIssuesList();
                closeModal();
                saveToLocalStorage();
            }
        }

        function updateIssuesList() {
            var container = document.getElementById('issuesList');
            if (appState.issues.length === 0) {
                container.innerHTML = '<p>Brak zgłoszonych usterek</p>';
                return;
            }
            
            var html = '';
            for (var i = 0; i < appState.issues.length; i++) {
                var issue = appState.issues[i];
                html += '<div class="issue-item">' +
                    '<span class="issue-category ' + issue.category + '">Kategoria ' + issue.category + '</span>' +
                    '<strong>' + issue.description + '</strong>' +
                    '<p style="margin-top: 5px; color: #666;">Termin: ' + (issue.deadline || 'Nie określono') + '</p>' +
                    '<button class="btn btn-secondary" onclick="removeIssue(' + i + ')" style="margin-top: 10px;">Usuń</button>' +
                    '</div>';
            }
            container.innerHTML = html;
        }

        function removeIssue(index) {
            appState.issues.splice(index, 1);
            updateIssuesList();
            saveToLocalStorage();
        }

        function updateProgress() {
            var totalItems = 0;
            var checkedItems = 0;
            
            for (var category in appState.checklist) {
                var items = appState.checklist[category];
                totalItems += items.length;
                for (var i = 0; i < items.length; i++) {
                    if (items[i].checked) checkedItems++;
                }
            }
            
            totalItems += appState.measurements.electrical.length;
            for (var j = 0; j < appState.measurements.electrical.length; j++) {
                if (appState.measurements.electrical[j].status === 'ok') checkedItems++;
            }
            
            totalItems += appState.measurements.safety.length;
            for (var k = 0; k < appState.measurements.safety.length; k++) {
                if (appState.measurements.safety[k].status === 'ok') checkedItems++;
            }
            
            var progress = totalItems > 0 ? Math.round((checkedItems / totalItems) * 100) : 0;
            appState.progress = progress;
            
            var progressBar = document.getElementById('progressBar');
            progressBar.style.width = progress + '%';
            progressBar.textContent = progress + '%';
            
            var criticalIssues = 0, importantIssues = 0, minorIssues = 0;
            for (var m = 0; m < appState.issues.length; m++) {
                if (appState.issues[m].category === 'A') criticalIssues++;
                else if (appState.issues[m].category === 'B') importantIssues++;
                else if (appState.issues[m].category === 'C') minorIssues++;
            }
            
            var detailsDiv = document.getElementById('progressDetails');
            detailsDiv.innerHTML = 
                '<p><strong>Sprawdzone elementy:</strong> ' + checkedItems + ' z ' + totalItems + '</p>' +
                '<p><strong>Usterki:</strong> ' + criticalIssues + ' krytycznych, ' +
                importantIssues + ' ważnych, ' + minorIssues + ' drobnych</p>';
        }

        function updateReportSummary() {
            var summaryDiv = document.getElementById('reportSummary');
            
            var info = {
                machineName: document.getElementById('machineName').value || 'Nie podano',
                serialNumber: document.getElementById('serialNumber').value || 'Nie podano',
                manufacturer: document.getElementById('manufacturer').value || 'Nie podano',
                inspectionDate: document.getElementById('inspectionDate').value || 'Nie podano',
                inspector: document.getElementById('inspector').value || 'Nie podano',
                location: document.getElementById('location').value || 'Nie podano'
            };
            
            var criticalCount = 0;
            for (var i = 0; i < appState.issues.length; i++) {
                if (appState.issues[i].category === 'A') criticalCount++;
            }
            
            var html = '<h4>Informacje o maszynie:</h4>' +
                '<p><strong>Nazwa:</strong> ' + info.machineName + '</p>' +
                '<p><strong>Nr seryjny:</strong> ' + info.serialNumber + '</p>' +
                '<p><strong>Producent:</strong> ' + info.manufacturer + '</p>' +
                '<p><strong>Data odbioru:</strong> ' + info.inspectionDate + '</p>' +
                '<p><strong>Inspektor:</strong> ' + info.inspector + '</p>' +
                '<p><strong>Lokalizacja:</strong> ' + info.location + '</p>' +
                '<h4 style="margin-top: 20px;">Status odbioru:</h4>' +
                '<div class="progress-bar" style="margin: 15px 0;">' +
                '<div class="progress-fill" style="width: ' + appState.progress + '%;">' + appState.progress + '%</div>' +
                '</div>';
                
            if (criticalCount > 0) {
                html += '<div class="error-box">' +
                    '<strong>UWAGA:</strong> Wykryto ' + criticalCount + ' usterek krytycznych! ' +
                    'Maszyna nie może być dopuszczona do eksploatacji.</div>';
            } else if (appState.progress === 100) {
                html += '<div class="info-box">' +
                    '<strong>Gratulacje!</strong> Odbiór zakończony pomyślnie. Wszystkie punkty sprawdzone.</div>';
            } else {
                html += '<div class="warning-box">' +
                    '<strong>W trakcie:</strong> Odbiór niekompletny. Sprawdź pozostałe punkty.</div>';
            }
            
            summaryDiv.innerHTML = html;
        }

        function generateReport() {
            var finalNotes = document.getElementById('finalNotes').value;
            
            var reportWindow = window.open('', '_blank');
            var reportHtml = '<!DOCTYPE html><html><head><title>Raport z odbioru</title>' +
                '<style>' +
                'body { font-family: Arial, sans-serif; margin: 20px; }' +
                'h1, h2, h3 { color: #2a5298; }' +
                'table { border-collapse: collapse; width: 100%; margin: 20px 0; }' +
                'th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }' +
                'th { background: #2a5298; color: white; }' +
                '.header { text-align: center; margin-bottom: 30px; }' +
                '.signature { margin-top: 50px; display: flex; justify-content: space-around; }' +
                '.signature-box { text-align: center; width: 200px; }' +
                '.signature-line { border-top: 1px solid black; margin-top: 50px; }' +
                '</style></head><body>' +
                '<div class="header">' +
                '<h1>PROTOKÓŁ ODBIORU TECHNICZNEGO</h1>' +
                '<h2>Elektryka i Automatyka</h2>' +
                '</div>' +
                '<h3>1. Dane maszyny</h3>' +
                '<table>' +
                '<tr><td><strong>Nazwa maszyny:</strong></td><td>' + document.getElementById('machineName').value + '</td></tr>' +
                '<tr><td><strong>Nr seryjny:</strong></td><td>' + document.getElementById('serialNumber').value + '</td></tr>' +
                '<tr><td><strong>Producent:</strong></td><td>' + document.getElementById('manufacturer').value + '</td></tr>' +
                '<tr><td><strong>Data odbioru:</strong></td><td>' + document.getElementById('inspectionDate').value + '</td></tr>' +
                '<tr><td><strong>Lokalizacja:</strong></td><td>' + document.getElementById('location').value + '</td></tr>' +
                '</table>' +
                '<h3>2. Postęp odbioru</h3>' +
                '<p>Ukończono: ' + appState.progress + '% punktów kontrolnych</p>';
                
            reportHtml += '<h3>3. Usterki</h3>';
            if (appState.issues.length > 0) {
                reportHtml += '<table><tr><th>Kategoria</th><th>Opis</th><th>Termin usunięcia</th></tr>';
                for (var i = 0; i < appState.issues.length; i++) {
                    var issue = appState.issues[i];
                    reportHtml += '<tr><td>' + issue.category + '</td><td>' + issue.description + 
                        '</td><td>' + (issue.deadline || 'Nie określono') + '</td></tr>';
                }
                reportHtml += '</table>';
            } else {
                reportHtml += '<p>Nie stwierdzono usterek.</p>';
            }
            
            reportHtml += '<h3>4. Uwagi końcowe</h3>' +
                '<p>' + (finalNotes || 'Brak dodatkowych uwag.') + '</p>' +
                '<div class="signature">' +
                '<div class="signature-box">' +
                '<div class="signature-line"></div>' +
                '<p>Wykonawca odbioru<br>' + document.getElementById('inspector').value + '</p>' +
                '</div>' +
                '<div class="signature-box">' +
                '<div class="signature-line"></div>' +
                '<p>Przedstawiciel klienta</p>' +
                '</div>' +
                '</div>' +
                '</body></html>';
                
            reportWindow.document.write(reportHtml);
            reportWindow.document.close();
            reportWindow.print();
        }

        function closeModal() {
            document.getElementById('modal').style.display = 'none';
        }

        function saveToLocalStorage() {
            var data = {
                appState: appState,
                info: {
                    machineName: document.getElementById('machineName').value,
                    serialNumber
