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
        let appState = {
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

        // Inicjalizacja
        document.addEventListener('DOMContentLoaded', function() {
            initializeApp();
            document.getElementById('inspectionDate').value = new Date().toISOString().split('T')[0];
        });

        function initializeApp() {
            initializeChecklists();
            initializeDefaultMeasurements();
            updateProgress();
        }

        // Nawigacja
        function showSection(sectionId, buttonElement) {
            document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
            document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
            
            document.getElementById(sectionId).classList.add('active');
            buttonElement.classList.add('active');
            
            // Aktualizacja podsumowania raportu przy przejściu do sekcji raport
            if (sectionId === 'report') {
                updateReportSummary();
            }
        }

        // Inicjalizacja checklist
        function initializeChecklists() {
            const checklists = {
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

            for (const [category, items] of Object.entries(checklists)) {
                const container = document.getElementById(`${category}Checklist`);
                if (container) {
                    container.innerHTML = items.map((item, index) => `
                        <div class="checklist-item">
                            <input type="checkbox" id="${category}_${index}" onchange="updateChecklistItem('${category}', ${index})">
                            <label for="${category}_${index}">${item}</label>
                            <span class="status" id="${category}_status_${index}"></span>
                        </div>
                    `).join('');
                }
                appState.checklist[category] = items.map(item => ({ name: item, checked: false }));
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

        // Aktualizacja checklisty
        function updateChecklistItem(category, index) {
            const checkbox = document.getElementById(`${category}_${index}`);
            const statusElement = document.getElementById(`${category}_status_${index}`);
            
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

        // Pomiary
        function updateMeasurementTables() {
            // Pomiary elektryczne
            const electricalBody = document.getElementById('electricalMeasurements');
            electricalBody.innerHTML = appState.measurements.electrical.map((m, index) => `
                <tr>
                    <td>${m.parameter}</td>
                    <td>
                        <input type="text" value="${m.value}" onchange="updateMeasurement('electrical', ${index}, this.value)" 
                               style="width: 100px; padding: 5px;">
                    </td>
                    <td>${m.limit}</td>
                    <td><span class="status ${m.status}">${getStatusText(m.status)}</span></td>
                </tr>
            `).join('');

            // Pomiary bezpieczeństwa
            const safetyBody = document.getElementById('safetyMeasurements');
            safetyBody.innerHTML = appState.measurements.safety.map((m, index) => `
                <tr>
                    <td>${m.function}</td>
                    <td>
                        <input type="number" value="${m.time}" onchange="updateMeasurement('safety', ${index}, this.value)" 
                               style="width: 100px; padding: 5px;">
                    </td>
                    <td>${m.limit}</td>
