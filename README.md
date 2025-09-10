<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Auftragsverwaltungssystem</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .header {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            margin-bottom: 20px;
            text-align: center;
        }
        
        .header h1 {
            color: #2c3e50;
            margin-bottom: 10px;
        }
        
        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 20px 0;
        }
        
        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        
        .btn-primary {
            background: #3498db;
            color: white;
        }
        
        .btn-primary:hover {
            background: #2980b9;
            transform: translateY(-2px);
        }
        
        .btn-success {
            background: #27ae60;
            color: white;
        }
        
        .btn-success:hover {
            background: #219a52;
        }
        
        .btn-warning {
            background: #f39c12;
            color: white;
        }
        
        .btn-warning:hover {
            background: #e67e22;
        }
        
        .btn-danger {
            background: #e74c3c;
            color: white;
        }
        
        .btn-danger:hover {
            background: #c0392b;
        }
        
        .page {
            display: none;
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        
        .page.active {
            display: block;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .form-group input,
        .form-group select,
        .form-group textarea {
            width: 100%;
            padding: 10px;
            border: 2px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
        }
        
        .form-group input:focus,
        .form-group select:focus,
        .form-group textarea:focus {
            border-color: #3498db;
            outline: none;
        }
        
        .time-tracker {
            background: linear-gradient(135deg, #27ae60, #2ecc71);
            color: white;
            padding: 30px;
            border-radius: 15px;
            text-align: center;
            margin-bottom: 20px;
        }
        
        .digital-clock {
            font-size: 3em;
            font-weight: bold;
            margin: 20px 0;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .status-display {
            background: rgba(255,255,255,0.2);
            padding: 15px;
            border-radius: 10px;
            margin: 20px 0;
        }
        
        .time-button {
            font-size: 20px;
            padding: 15px 30px;
            margin: 10px;
            border-radius: 10px;
            border: none;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
        }
        
        .time-button.checkin {
            background: #2ecc71;
            color: white;
        }
        
        .time-button.checkout {
            background: #e74c3c;
            color: white;
        }
        
        .admin-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin: 20px 0;
        }
        
        .admin-card {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
            padding: 30px;
            border-radius: 10px;
            text-align: center;
            cursor: pointer;
            transition: transform 0.3s;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        
        .admin-card:hover {
            transform: translateY(-5px);
        }
        
        .admin-card h3 {
            margin-bottom: 10px;
            font-size: 1.3em;
        }
        
        .admin-card p {
            opacity: 0.9;
        }
        
        .data-table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
            background: white;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        
        .data-table th,
        .data-table td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }
        
        .data-table th {
            background: #34495e;
            color: white;
            font-weight: bold;
        }
        
        .data-table tr:hover {
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
            background-color: rgba(0,0,0,0.5);
        }
        
        .modal-content {
            background-color: white;
            margin: 10% auto;
            padding: 20px;
            border-radius: 10px;
            width: 80%;
            max-width: 600px;
            max-height: 80vh;
            overflow-y: auto;
        }
        
        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
        }
        
        .close:hover {
            color: black;
        }
        
        .print-area {
            background: white;
            padding: 30px;
            margin: 20px 0;
        }
        
        @media print {
            body * {
                visibility: hidden;
            }
            .print-area, .print-area * {
                visibility: visible;
            }
            .print-area {
                position: absolute;
                left: 0;
                top: 0;
                width: 100%;
            }
        }
        
        .customer-card {
            background: #f8f9fa;
            border: 1px solid #dee2e6;
            border-radius: 8px;
            padding: 15px;
            margin: 10px 0;
        }
        
        .location-selector {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }
        
        .alert {
            padding: 15px;
            margin: 15px 0;
            border-radius: 5px;
            font-weight: bold;
        }
        
        .alert-success {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
        
        .alert-error {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🏢 Auftragsverwaltungssystem</h1>
            <p>Professionelle Verwaltung von Aufträgen, Kunden und Mitarbeitern</p>
            
            <div class="nav-buttons">
                <button class="btn btn-primary" onclick="showPage('info')">ℹ️ Info</button>
                <button class="btn btn-success" onclick="showPage('customer')">👥 Kunden</button>
                <button class="btn btn-warning" onclick="showPage('employee')">👷 Mitarbeiter</button>
                <button class="btn btn-danger" onclick="showPage('admin')">⚙️ Admin</button>
            </div>
        </div>

        <!-- Customer Page -->
        <div id="customer" class="page active">
            <div id="customerLogin">
                <h2>👥 Kunden-Anmeldung</h2>
                <div class="form-group">
                    <label>E-Mail:</label>
                    <input type="email" id="customerEmail" value="demo@example.com" placeholder="ihre@email.de">
                </div>
                <div class="form-group">
                    <label>Passwort:</label>
                    <input type="password" id="customerPassword" value="demo" placeholder="Passwort">
                </div>
                <button class="btn btn-primary" onclick="loginCustomer()">🔐 Anmelden</button>
                <button class="btn btn-success" onclick="showCustomerRegistration()">📝 Neu registrieren</button>
            </div>

            <div id="customerRegistration" style="display:none;">
                <h2>📝 Kunden-Registrierung</h2>
                <div class="form-group">
                    <label>Firmenname:</label>
                    <input type="text" id="regCompany" placeholder="Ihr Firmenname">
                </div>
                <div class="form-group">
                    <label>Ansprechpartner:</label>
                    <input type="text" id="regContact" placeholder="Vor- und Nachname">
                </div>
                <div class="form-group">
                    <label>E-Mail:</label>
                    <input type="email" id="regEmail" placeholder="ihre@email.de">
                </div>
                <div class="form-group">
                    <label>Telefon:</label>
                    <input type="tel" id="regPhone" placeholder="0123 456789">
                </div>
                <div class="location-selector">
                    <div class="form-group">
                        <label>Straße:</label>
                        <select id="regStreet">
                            <option value="">Straße wählen...</option>
                            <option value="Hauptstraße">Hauptstraße</option>
                            <option value="Bahnhofstraße">Bahnhofstraße</option>
                            <option value="Kirchplatz">Kirchplatz</option>
                            <option value="Industriestraße">Industriestraße</option>
                            <option value="Am Markt">Am Markt</option>
                            <option value="Lindenweg">Lindenweg</option>
                            <option value="Rosenstraße">Rosenstraße</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Hausnummer:</label>
                        <input type="text" id="regNumber" placeholder="12a">
                    </div>
                </div>
                <div class="location-selector">
                    <div class="form-group">
                        <label>PLZ:</label>
                        <input type="text" id="regPostcode" placeholder="12345">
                    </div>
                    <div class="form-group">
                        <label>Ort:</label>
                        <select id="regCity">
                            <option value="">Ort wählen...</option>
                            <option value="Duisburg">Duisburg</option>
                            <option value="Düsseldorf">Düsseldorf</option>
                            <option value="Essen">Essen</option>
                            <option value="Oberhausen">Oberhausen</option>
                            <option value="Mülheim">Mülheim</option>
                            <option value="Bottrop">Bottrop</option>
                        </select>
                    </div>
                </div>
                <div class="form-group">
                    <label>Passwort:</label>
                    <input type="password" id="regPassword" placeholder="Sicheres Passwort">
                </div>
                <button class="btn btn-success" onclick="registerCustomer()">✅ Registrieren</button>
                <button class="btn btn-primary" onclick="showCustomerLogin()">🔙 Zurück zur Anmeldung</button>
            </div>

            <div id="customerDashboard" style="display:none;">
                <h2>👥 Kunden-Bereich</h2>
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
                    <span>Willkommen, <span id="customerName"></span>!</span>
                    <button class="btn btn-primary" onclick="logoutCustomer()">🚪 Abmelden</button>
                </div>
                
                <button class="btn btn-success" onclick="showCreateOrder()">➕ Neuen Auftrag erstellen</button>
                
                <h3>📋 Meine Aufträge</h3>
                <div id="customerOrders"></div>
            </div>
        </div>

        <!-- Employee Page -->
        <div id="employee" class="page">
            <div id="employeeLogin">
                <h2>👷 Mitarbeiter-Anmeldung</h2>
                <div class="form-group">
                    <label>Mitarbeiter-ID:</label>
                    <input type="text" id="employeeId" value="E001" placeholder="E001">
                </div>
                <div class="form-group">
                    <label>PIN:</label>
                    <input type="password" id="employeePin" value="1234" placeholder="PIN">
                </div>
                <button class="btn btn-primary" onclick="loginEmployee()">🔐 Anmelden</button>
            </div>

            <div id="employeeDashboard" style="display:none;">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
                    <span>Mitarbeiter: <span id="employeeName"></span></span>
                    <button class="btn btn-primary" onclick="logoutEmployee()">🚪 Abmelden</button>
                </div>

                <!-- Zeiterfassung -->
                <div class="time-tracker">
                    <h3>⏰ Zeiterfassung</h3>
                    <div class="digital-clock" id="digitalClock">00:00:00</div>
                    
                    <div class="status-display">
                        <div id="workStatus">Nicht eingestempelt</div>
                        <div id="workTimer" style="display:none;"></div>
                    </div>

                    <div id="checkinForm" style="display:block;">
                        <div class="form-group">
                            <label>Auftrag auswählen:</label>
                            <select id="checkinOrder">
                                <option value="">Auftrag wählen...</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>Arbeitsort/Objekt:</label>
                            <input type="text" id="checkinLocation" placeholder="z.B. Heizungskeller, Wohnung 2.OG">
                        </div>
                        <button class="time-button checkin" onclick="checkinEmployee()">🟢 EINSTEMPELN</button>
                    </div>

                    <div id="checkoutForm" style="display:none;">
                        <div class="form-group">
                            <label>Durchgeführte Arbeiten:</label>
                            <textarea id="checkoutDescription" placeholder="Beschreibung der Tätigkeiten..." rows="3"></textarea>
                        </div>
                        <button class="time-button checkout" onclick="checkoutEmployee()">🔴 AUSSTEMPELN</button>
                    </div>
                </div>

                <h3>📋 Zugewiesene Aufträge</h3>
                <div id="employeeOrders"></div>

                <button class="btn btn-primary" onclick="showEmployeeTimesheet()">📊 Mein Zeitkonto</button>
            </div>
        </div>

        <!-- Admin Page -->
        <div id="admin" class="page">
            <div id="adminLogin">
                <h2>⚙️ Admin-Anmeldung</h2>
                <div class="form-group">
                    <label>Admin-Passwort:</label>
                    <input type="password" id="adminPassword" value="" placeholder="Admin-Passwort">
                </div>
                <button class="btn btn-primary" onclick="loginAdmin()">🔐 Anmelden</button>
            </div>

            <div id="adminDashboard" style="display:none;">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
                    <h2>⚙️ Admin-Bereich</h2>
                    <button class="btn btn-primary" onclick="logoutAdmin()">🚪 Abmelden</button>
                </div>

                <div class="admin-grid">
                    <div class="admin-card" onclick="showCustomerManagement()">
                        <h3>👥 Kundenverwaltung</h3>
                        <p>Kunden verwalten, bearbeiten und löschen</p>
                    </div>
                    <div class="admin-card" onclick="showEmployeeManagement()">
                        <h3>👷 Mitarbeiterverwaltung</h3>
                        <p>Mitarbeiter und Arbeitszeiten verwalten</p>
                    </div>
                    <div class="admin-card" onclick="showOrderManagement()">
                        <h3>📋 Auftragsverwaltung</h3>
                        <p>Aufträge zuweisen und verwalten</p>
                    </div>
                    <div class="admin-card" onclick="showLocationManagement()">
                        <h3>📍 Standortverwaltung</h3>
                        <p>Straßen und Orte verwalten</p>
                    </div>
                    <div class="admin-card" onclick="showPhoneOrders()">
                        <h3>📞 Telefonische Aufträge</h3>
                        <p>Aufträge für Kunden anlegen</p>
                    </div>
                    <div class="admin-card" onclick="showSettings()">
                        <h3>⚙️ Einstellungen</h3>
                        <p>System-Einstellungen und Passwort</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Modals -->
    <div id="orderModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal('orderModal')">&times;</span>
            <h2>📋 Auftrag erstellen</h2>
            <div class="form-group">
                <label>Titel:</label>
                <input type="text" id="orderTitle" placeholder="Auftragstitel">
            </div>
            <div class="form-group">
                <label>Beschreibung:</label>
                <textarea id="orderDescription" placeholder="Detaillierte Beschreibung" rows="4"></textarea>
            </div>
            <div class="form-group">
                <label>Priorität:</label>
                <select id="orderPriority">
                    <option value="normal">Normal</option>
                    <option value="hoch">Hoch</option>
                    <option value="dringend">Dringend</option>
                </select>
            </div>
            <button class="btn btn-success" onclick="createOrder()">✅ Auftrag erstellen</button>
        </div>
    </div>

    <div id="timesheetModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal('timesheetModal')">&times;</span>
            <h2>📊 Zeitkonto</h2>
            <div id="timesheetContent"></div>
        </div>
    </div>

    <div id="customerManagementModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal('customerManagementModal')">&times;</span>
            <h2>👥 Kundenverwaltung</h2>
            <button class="btn btn-success" onclick="showAddCustomer()">➕ Kunde hinzufügen</button>
            <div id="customerList"></div>
        </div>
    </div>

    <div id="employeeManagementModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal('employeeManagementModal')">&times;</span>
            <h2>👷 Mitarbeiterverwaltung</h2>
            <button class="btn btn-success" onclick="showAddEmployee()">➕ Mitarbeiter hinzufügen</button>
            <div id="employeeList"></div>
        </div>
    </div>

    <div id="locationManagementModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal('locationManagementModal')">&times;</span>
            <h2>📍 Standortverwaltung</h2>
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
                <div>
                    <h3>Straßen verwalten</h3>
                    <div class="form-group">
                        <input type="text" id="newStreet" placeholder="Neue Straße hinzufügen">
                        <button class="btn btn-success" onclick="addStreet()">Hinzufügen</button>
                    </div>
                    <div id="streetList"></div>
                </div>
                <div>
                    <h3>Orte verwalten</h3>
                    <div class="form-group">
                        <input type="text" id="newCity" placeholder="Neuen Ort hinzufügen">
                        <button class="btn btn-success" onclick="addCity()">Hinzufügen</button>
                    </div>
                    <div id="cityList"></div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Global Variables
        let currentUser = null;
        let currentRole = null;
        let checkedInEmployee = null;
        let checkinTime = null;
        let workTimer = null;

        // Sample Data
        let customers = [
            {
                id: 'C001',
                email: 'demo@example.com',
                password: 'demo',
                company: 'Mustermann GmbH',
                contact: 'Max Mustermann',
                phone: '0203 12345',
                address: 'Hauptstraße 123, 47051 Duisburg'
            }
        ];

        let employees = [
            {
                id: 'E001',
                pin: '1234',
                name: 'Max Mustermann',
                timeRecords: [],
                currentOrder: null,
                isCheckedIn: false
            }
        ];

        let orders = [
            {
                id: 'O001',
                customerId: 'C001',
                title: 'Heizungswartung',
                description: 'Jährliche Wartung der Heizungsanlage',
                status: 'offen',
                priority: 'normal',
                assignedTo: 'E001',
                createdAt: new Date().toISOString(),
                workTimes: []
            },
            {
                id: 'O002',
                customerId: 'C001',
                title: 'Rohrreparatur',
                description: 'Leckage im Badezimmer beheben',
                status: 'offen',
                priority: 'hoch',
                assignedTo: null,
                createdAt: new Date().toISOString(),
                workTimes: []
            }
        ];

        let streets = ['Hauptstraße', 'Bahnhofstraße', 'Kirchplatz', 'Industriestraße', 'Am Markt', 'Lindenweg', 'Rosenstraße'];
        let cities = ['Duisburg', 'Düsseldorf', 'Essen', 'Oberhausen', 'Mülheim', 'Bottrop'];

        // Initialization
        window.onload = function() {
            updateClock();
            setInterval(updateClock, 1000);
            console.log('System geladen - alle Buttons sollten funktionieren!');
            setTimeout(() => {
                alert('System geladen - alle Buttons sollten funktionieren!');
            }, 1000);
        };

        // Navigation
        function showPage(pageId) {
            console.log('Zeige Seite:', pageId);
            document.querySelectorAll('.page').forEach(page => {
                page.classList.remove('active');
            });
            document.getElementById(pageId).classList.add('active');
        }

        // Clock
        function updateClock() {
            const now = new Date();
            const timeString = now.toLocaleTimeString('de-DE');
            const clockElement = document.getElementById('digitalClock');
            if (clockElement) {
                clockElement.textContent = timeString;
            }
        }

        // Customer Functions
        function showCustomerRegistration() {
            document.getElementById('customerLogin').style.display = 'none';
            document.getElementById('customerRegistration').style.display = 'block';
        }

        function showCustomerLogin() {
            document.getElementById('customerLogin').style.display = 'block';
            document.getElementById('customerRegistration').style.display = 'none';
        }

        function registerCustomer() {
            const regData = {
                company: document.getElementById('regCompany').value,
                contact: document.getElementById('regContact').value,
                email: document.getElementById('regEmail').value,
                phone: document.getElementById('regPhone').value,
                street: document.getElementById('regStreet').value,
                number: document.getElementById('regNumber').value,
                postcode: document.getElementById('regPostcode').value,
                city: document.getElementById('regCity').value,
                password: document.getElementById('regPassword').value
            };

            if (!regData.company || !regData.email || !regData.password) {
                alert('Bitte füllen Sie alle Pflichtfelder aus!');
                return;
            }

            // Check if email already exists
            if (customers.find(c => c.email === regData.email)) {
                alert('Diese E-Mail-Adresse ist bereits registriert!');
                return;
            }

            const newCustomer = {
                id: 'C' + String(customers.length + 1).padStart(3, '0'),
                email: regData.email,
                password: regData.password,
                company: regData.company,
                contact: regData.contact,
                phone: regData.phone,
                address: regData.street + ' ' + regData.number + ', ' + regData.postcode + ' ' + regData.city
            };

            customers.push(newCustomer);
            alert('Registrierung erfolgreich! Sie können sich jetzt anmelden.');
            showCustomerLogin();
        }

        function loginCustomer() {
            const email = document.getElementById('customerEmail').value;
            const password = document.getElementById('customerPassword').value;

            const customer = customers.find(c => c.email === email && c.password === password);

            if (customer) {
                currentUser = customer;
                currentRole = 'customer';
                document.getElementById('customerName').textContent = customer.company;
                document.getElementById('customerLogin').style.display = 'none';
                document.getElementById('customerRegistration').style.display = 'none';
                document.getElementById('customerDashboard').style.display = 'block';
                loadCustomerOrders();
            } else {
                alert('Ungültige Anmeldedaten!');
            }
        }

        function logoutCustomer() {
            currentUser = null;
            currentRole = null;
            document.getElementById('customerLogin').style.display = 'block';
            document.getElementById('customerDashboard').style.display = 'none';
        }

        function loadCustomerOrders() {
            const customerOrders = orders.filter(o => o.customerId === currentUser.id);
            let html = '';

            customerOrders.forEach(order => {
                const statusColor = {
                    'offen': '#f39c12',
                    'bearbeitung': '#3498db',
                    'erledigt': '#27ae60',
                    'storniert': '#e74c3c'
                }[order.status];

                html += '<div class="customer-card">';
                html += '<h4>' + order.title + ' <span style="color: ' + statusColor + '">[' + order.status + ']</span></h4>';
                html += '<p>' + order.description + '</p>';
                html += '<p><strong>Erstellt:</strong> ' + new Date(order.createdAt).toLocaleString('de-DE') + '</p>';
                html += '<p><strong>Priorität:</strong> ' + order.priority + '</p>';
                html += '<button class="btn btn-primary" onclick="printOrder(\'' + order.id + '\')">🖨️ Drucken</button>';
                html += '</div>';
            });

            document.getElementById('customerOrders').innerHTML = html || '<p>Keine Aufträge vorhanden.</p>';
        }

        function showCreateOrder() {
            document.getElementById('orderModal').style.display = 'block';
        }

        function createOrder() {
            const title = document.getElementById('orderTitle').value;
            const description = document.getElementById('orderDescription').value;
            const priority = document.getElementById('orderPriority').value;

            if (!title || !description) {
                alert('Bitte füllen Sie alle Felder aus!');
                return;
            }

            const newOrder = {
                id: 'O' + String(orders.length + 1).padStart(3, '0'),
                customerId: currentUser.id,
                title: title,
                description: description,
                status: 'offen',
                priority: priority,
                assignedTo: null,
                createdAt: new Date().toISOString(),
                workTimes: []
            };

            orders.push(newOrder);
            closeModal('orderModal');
            loadCustomerOrders();
            alert('Auftrag erfolgreich erstellt!');
        }

        // Employee Functions
        function loginEmployee() {
            const id = document.getElementById('employeeId').value;
            const pin = document.getElementById('employeePin').value;

            const employee = employees.find(e => e.id === id && e.pin === pin);

            if (employee) {
                currentUser = employee;
                currentRole = 'employee';
                document.getElementById('employeeName').textContent = employee.name;
                document.getElementById('employeeLogin').style.display = 'none';
                document.getElementById('employeeDashboard').style.display = 'block';
                loadEmployeeOrders();
                updateEmployeeStatus();
            } else {
                alert('Ungültige Anmeldedaten!');
            }
        }

        function logoutEmployee() {
            currentUser = null;
            currentRole = null;
            document.getElementById('employeeLogin').style.display = 'block';
            document.getElementById('employeeDashboard').style.display = 'none';
        }

        function loadEmployeeOrders() {
            const employeeOrders = orders.filter(o => o.assignedTo === currentUser.id);
            let html = '';

            // Load orders in checkin dropdown
            let orderOptions = '<option value="">Auftrag wählen...</option>';
            employeeOrders.forEach(order => {
                orderOptions += '<option value="' + order.id + '">' + order.id + ' - ' + order.title + '</option>';
            });
            document.getElementById('checkinOrder').innerHTML = orderOptions;

            // Display orders
            employeeOrders.forEach(order => {
                const customer = customers.find(c => c.id === order.customerId);
                const statusColor = {
                    'offen': '#f39c12',
                    'bearbeitung': '#3498db',
                    'erledigt': '#27ae60',
                    'storniert': '#e74c3c'
                }[order.status];

                html += '<div class="customer-card">';
                html += '<h4>' + order.title + ' <span style="color: ' + statusColor + '">[' + order.status + ']</span></h4>';
                html += '<p><strong>Kunde:</strong> ' + (customer ? customer.company : 'Unbekannt') + '</p>';
                html += '<p>' + order.description + '</p>';
                html += '<button class="btn btn-primary" onclick="changeOrderStatus(\'' + order.id + '\')">Status ändern</button>';
                html += '</div>';
            });

            document.getElementById('employeeOrders').innerHTML = html || '<p>Keine Aufträge zugewiesen.</p>';
        }

        function updateEmployeeStatus() {
            const statusDiv = document.getElementById('workStatus');
            const timerDiv = document.getElementById('workTimer');
            
            if (currentUser.isCheckedIn && checkinTime) {
                statusDiv.innerHTML = 'Eingestempelt seit: ' + new Date(checkinTime).toLocaleTimeString('de-DE');
                timerDiv.style.display = 'block';
                
                if (!workTimer) {
                    workTimer = setInterval(() => {
                        const now = new Date();
                        const diff = now - new Date(checkinTime);
                        const hours = Math.floor(diff / 3600000);
                        const minutes = Math.floor((diff % 3600000) / 60000);
                        const seconds = Math.floor((diff % 60000) / 1000);
                        timerDiv.innerHTML = 'Arbeitszeit: ' + 
                                          String(hours).padStart(2, '0') + ':' + 
                                          String(minutes).padStart(2, '0') + ':' + 
                                          String(seconds).padStart(2, '0');
                    }, 1000);
                }
                
                document.getElementById('checkinForm').style.display = 'none';
                document.getElementById('checkoutForm').style.display = 'block';
            } else {
                statusDiv.innerHTML = 'Nicht eingestempelt';
                timerDiv.style.display = 'none';
                
                if (workTimer) {
                    clearInterval(workTimer);
                    workTimer = null;
                }
                
                document.getElementById('checkinForm').style.display = 'block';
                document.getElementById('checkoutForm').style.display = 'none';
            }
        }

        function checkinEmployee() {
            const orderId = document.getElementById('checkinOrder').value;
            const location = document.getElementById('checkinLocation').value;

            if (!orderId || !location) {
                alert('Bitte wählen Sie einen Auftrag und geben Sie den Arbeitsort an!');
                return;
            }

            // Get GPS location (simulate)
            const gps = {
                lat: 51.4344 + (Math.random() - 0.5) * 0.01,
                lng: 6.7623 + (Math.random() - 0.5) * 0.01,
                accuracy: Math.floor(Math.random() * 10) + 5
            };

            checkinTime = new Date().toISOString();
            currentUser.isCheckedIn = true;
            currentUser.currentOrder = orderId;
            currentUser.currentLocation = location;
            
            // Update order status
            const order = orders.find(o => o.id === orderId);
            if (order) {
                order.status = 'bearbeitung';
            }

            alert('Erfolgreich eingestempelt!\nZeit: ' + new Date(checkinTime).toLocaleTimeString('de-DE') + 
                  '\nOrt: ' + location + 
                  '\nGPS: ' + gps.lat.toFixed(6) + ', ' + gps.lng.toFixed(6));

            updateEmployeeStatus();
            loadEmployeeOrders();
        }

        function checkoutEmployee() {
            const description = document.getElementById('checkoutDescription').value;

            if (!description) {
                alert('Bitte beschreiben Sie die durchgeführten Arbeiten!');
                return;
            }

            const checkoutTime = new Date().toISOString();
            const startTime = new Date(checkinTime);
            const endTime = new Date(checkoutTime);
            const workDuration = endTime - startTime;
            const hours = Math.floor(workDuration / 3600000);
            const minutes = Math.floor((workDuration % 3600000) / 60000);

            // Get GPS location (simulate)
            const gps = {
                lat: 51.4344 + (Math.random() - 0.5) * 0.01,
                lng: 6.7623 + (Math.random() - 0.5) * 0.01,
                accuracy: Math.floor(Math.random() * 10) + 5
            };

            // Create work time record
            const workTime = {
                orderId: currentUser.currentOrder,
                location: currentUser.currentLocation,
                description: description,
                startTime: checkinTime,
                endTime: checkoutTime,
                duration: hours + 'h ' + minutes + 'm',
                employeeId: currentUser.id,
                startGPS: gps,
                endGPS: gps
            };

            // Add to employee time records
            currentUser.timeRecords.push(workTime);

            // Add to order work times
            const order = orders.find(o => o.id === currentUser.currentOrder);
            if (order) {
                order.workTimes.push(workTime);
            }

            // Reset status
            currentUser.isCheckedIn = false;
            currentUser.currentOrder = null;
            currentUser.currentLocation = null;
            checkinTime = null;

            alert('Erfolgreich ausgestempelt!\nArbeitszeit: ' + hours + 'h ' + minutes + 'm\n' +
                  'Beschreibung: ' + description);

            // Clear form
            document.getElementById('checkinOrder').value = '';
            document.getElementById('checkinLocation').value = '';
            document.getElementById('checkoutDescription').value = '';

            updateEmployeeStatus();
            loadEmployeeOrders();
        }

        function changeOrderStatus(orderId) {
            const order = orders.find(o => o.id === orderId);
            if (!order) return;

            const newStatus = prompt('Neuer Status:\n1 = offen\n2 = bearbeitung\n3 = erledigt\n4 = storniert', 
                                   order.status === 'offen' ? '2' : 
                                   order.status === 'bearbeitung' ? '3' : '1');

            const statusMap = {
                '1': 'offen',
                '2': 'bearbeitung', 
                '3': 'erledigt',
                '4': 'storniert'
            };

            if (statusMap[newStatus]) {
                order.status = statusMap[newStatus];
                loadEmployeeOrders();
                alert('Status geändert zu: ' + statusMap[newStatus]);
            }
        }

        function showEmployeeTimesheet() {
            const employee = currentUser;
            let html = '<h3>Zeitkonto: ' + employee.name + '</h3>';
            
            if (employee.timeRecords.length === 0) {
                html += '<p>Keine Zeitaufzeichnungen vorhanden.</p>';
            } else {
                html += '<table class="data-table">';
                html += '<tr><th>Datum</th><th>Von</th><th>Bis</th><th>Dauer</th><th>Auftrag</th><th>Ort</th><th>Tätigkeit</th></tr>';
                
                let totalMinutes = 0;
                employee.timeRecords.forEach(record => {
                    const start = new Date(record.startTime);
                    const end = new Date(record.endTime);
                    const order = orders.find(o => o.id === record.orderId);
                    
                    html += '<tr>';
                    html += '<td>' + start.toLocaleDateString('de-DE') + '</td>';
                    html += '<td>' + start.toLocaleTimeString('de-DE') + '</td>';
                    html += '<td>' + end.toLocaleTimeString('de-DE') + '</td>';
                    html += '<td>' + record.duration + '</td>';
                    html += '<td>' + (order ? order.title : record.orderId) + '</td>';
                    html += '<td>' + record.location + '</td>';
                    html += '<td>' + record.description + '</td>';
                    html += '</tr>';
                    
                    // Calculate total time
                    const diff = end - start;
                    totalMinutes += Math.floor(diff / 60000);
                });
                
                html += '</table>';
                
                const totalHours = Math.floor(totalMinutes / 60);
                const remainingMinutes = totalMinutes % 60;
                html += '<p><strong>Gesamtarbeitszeit: ' + totalHours + 'h ' + remainingMinutes + 'm</strong></p>';
                html += '<button class="btn btn-primary" onclick="printTimesheet(\'' + employee.id + '\')">📄 Stundenzettel drucken</button>';
            }

            document.getElementById('timesheetContent').innerHTML = html;
            document.getElementById('timesheetModal').style.display = 'block';
        }

        // Admin Functions
        function loginAdmin() {
            const password = document.getElementById('adminPassword').value;

            if (password === 'admin123') {
                currentRole = 'admin';
                document.getElementById('adminLogin').style.display = 'none';
                document.getElementById('adminDashboard').style.display = 'block';
            } else {
                alert('Ungültiges Admin-Passwort!');
            }
        }

        function logoutAdmin() {
            currentRole = null;
            document.getElementById('adminLogin').style.display = 'block';
            document.getElementById('adminDashboard').style.display = 'none';
        }

        function showCustomerManagement() {
            let html = '<h3>Registrierte Kunden</h3>';
            html += '<table class="data-table">';
            html += '<tr><th>ID</th><th>Firma</th><th>Kontakt</th><th>E-Mail</th><th>Telefon</th><th>Adresse</th><th>Aktionen</th></tr>';
            
            customers.forEach(customer => {
                html += '<tr>';
                html += '<td>' + customer.id + '</td>';
                html += '<td>' + customer.company + '</td>';
                html += '<td>' + customer.contact + '</td>';
                html += '<td>' + customer.email + '</td>';
                html += '<td>' + customer.phone + '</td>';
                html += '<td>' + customer.address + '</td>';
                html += '<td>';
                html += '<button class="btn btn-danger" onclick="deleteCustomer(\'' + customer.id + '\')">Löschen</button>';
                html += '</td>';
                html += '</tr>';
            });
            
            html += '</table>';
            
            document.getElementById('customerList').innerHTML = html;
            document.getElementById('customerManagementModal').style.display = 'block';
        }

        function showEmployeeManagement() {
            let html = '<h3>Mitarbeiter</h3>';
            html += '<table class="data-table">';
            html += '<tr><th>ID</th><th>Name</th><th>Status</th><th>Arbeitszeiten</th><th>Aktionen</th></tr>';
            
            employees.forEach(employee => {
                let status = 'Ausgestempelt';
                if (employee.isCheckedIn && checkinTime) {
                    status = 'Eingestempelt seit ' + new Date(checkinTime).toLocaleTimeString('de-DE');
                }
                
                const totalHours = calculateTotalHours(employee);
                
                html += '<tr>';
                html += '<td>' + employee.id + '</td>';
                html += '<td>' + employee.name + '</td>';
                html += '<td>' + status + '</td>';
                html += '<td>' + totalHours + 'h</td>';
                html += '<td>';
                html += '<button class="btn btn-primary" onclick="showEmployeeDetails(\'' + employee.id + '\')">Zeiten</button> ';
                html += '<button class="btn btn-danger" onclick="deleteEmployee(\'' + employee.id + '\')">Löschen</button>';
                html += '</td>';
                html += '</tr>';
            });
            
            html += '</table>';
            
            document.getElementById('employeeList').innerHTML = html;
            document.getElementById('employeeManagementModal').style.display = 'block';
        }

        function calculateTotalHours(employee) {
            let totalMinutes = 0;
            employee.timeRecords.forEach(record => {
                const start = new Date(record.startTime);
                const end = new Date(record.endTime);
                const diff = end - start;
                totalMinutes += Math.floor(diff / 60000);
            });
            return Math.floor(totalMinutes / 60);
        }

        function showEmployeeDetails(employeeId) {
            const employee = employees.find(e => e.id === employeeId);
            if (!employee) return;

            let html = '<h3>Zeitkonto: ' + employee.name + ' (' + employee.id + ')</h3>';
            
            if (employee.timeRecords.length === 0) {
                html += '<p>Keine Zeitaufzeichnungen vorhanden.</p>';
            } else {
                html += '<table class="data-table">';
                html += '<tr><th>Datum</th><th>Von</th><th>Bis</th><th>Dauer</th><th>Auftrag</th><th>Ort</th><th>Tätigkeit</th></tr>';
                
                let totalMinutes = 0;
                employee.timeRecords.forEach(record => {
                    const start = new Date(record.startTime);
                    const end = new Date(record.endTime);
                    const order = orders.find(o => o.id === record.orderId);
                    
                    html += '<tr>';
                    html += '<td>' + start.toLocaleDateString('de-DE') + '</td>';
                    html += '<td>' + start.toLocaleTimeString('de-DE') + '</td>';
                    html += '<td>' + end.toLocaleTimeString('de-DE') + '</td>';
                    html += '<td>' + record.duration + '</td>';
                    html += '<td>' + (order ? order.title : record.orderId) + '</td>';
                    html += '<td>' + record.location + '</td>';
                    html += '<td>' + record.description + '</td>';
                    html += '</tr>';
                    
                    const diff = end - start;
                    totalMinutes += Math.floor(diff / 60000);
                });
                
                html += '</table>';
                
                const totalHours = Math.floor(totalMinutes / 60);
                const remainingMinutes = totalMinutes % 60;
                html += '<p><strong>Gesamtarbeitszeit: ' + totalHours + 'h ' + remainingMinutes + 'm</strong></p>';
                html += '<button class="btn btn-primary" onclick="printTimesheet(\'' + employee.id + '\')">📄 Stundenzettel drucken</button>';
            }

            document.getElementById('timesheetContent').innerHTML = html;
            document.getElementById('timesheetModal').style.display = 'block';
        }

        function showOrderManagement() {
            alert('Auftragsverwaltung wird geladen...');
        }

        function showLocationManagement() {
            // Load streets
            let streetHtml = '';
            streets.forEach((street, index) => {
                streetHtml += '<div style="display: flex; justify-content: space-between; align-items: center; padding: 5px; border-bottom: 1px solid #eee;">';
                streetHtml += '<span>' + street + '</span>';
                streetHtml += '<button class="btn btn-danger" style="padding: 5px 10px; font-size: 12px;" onclick="removeStreet(' + index + ')">×</button>';
                streetHtml += '</div>';
            });
            document.getElementById('streetList').innerHTML = streetHtml;

            // Load cities
            let cityHtml = '';
            cities.forEach((city, index) => {
                cityHtml += '<div style="display: flex; justify-content: space-between; align-items: center; padding: 5px; border-bottom: 1px solid #eee;">';
                cityHtml += '<span>' + city + '</span>';
                cityHtml += '<button class="btn btn-danger" style="padding: 5px 10px; font-size: 12px;" onclick="removeCity(' + index + ')">×</button>';
                cityHtml += '</div>';
            });
            document.getElementById('cityList').innerHTML = cityHtml;

            document.getElementById('locationManagementModal').style.display = 'block';
        }

        function addStreet() {
            const newStreet = document.getElementById('newStreet').value.trim();
            if (newStreet && !streets.includes(newStreet)) {
                streets.push(newStreet);
                document.getElementById('newStreet').value = '';
                showLocationManagement(); // Refresh
                updateStreetSelectors();
                alert('Straße hinzugefügt: ' + newStreet);
            }
        }

        function removeStreet(index) {
            const removedStreet = streets[index];
            streets.splice(index, 1);
            showLocationManagement(); // Refresh
            updateStreetSelectors();
            alert('Straße entfernt: ' + removedStreet);
        }

        function addCity() {
            const newCity = document.getElementById('newCity').value.trim();
            if (newCity && !cities.includes(newCity)) {
                cities.push(newCity);
                document.getElementById('newCity').value = '';
                showLocationManagement(); // Refresh
                updateCitySelectors();
                alert('Ort hinzugefügt: ' + newCity);
            }
        }

        function removeCity(index) {
            const removedCity = cities[index];
            cities.splice(index, 1);
            showLocationManagement(); // Refresh
            updateCitySelectors();
            alert('Ort entfernt: ' + removedCity);
        }

        function updateStreetSelectors() {
            const selectors = document.querySelectorAll('select[id$="Street"]');
            selectors.forEach(selector => {
                const currentValue = selector.value;
                selector.innerHTML = '<option value="">Straße wählen...</option>';
                streets.forEach(street => {
                    const option = document.createElement('option');
                    option.value = street;
                    option.textContent = street;
                    if (street === currentValue) option.selected = true;
                    selector.appendChild(option);
                });
            });
        }

        function updateCitySelectors() {
            const selectors = document.querySelectorAll('select[id$="City"]');
            selectors.forEach(selector => {
                const currentValue = selector.value;
                selector.innerHTML = '<option value="">Ort wählen...</option>';
                cities.forEach(city => {
                    const option = document.createElement('option');
                    option.value = city;
                    option.textContent = city;
                    if (city === currentValue) option.selected = true;
                    selector.appendChild(option);
                });
            });
        }

        function showPhoneOrders() {
            alert('Telefonische Aufträge werden geladen...');
        }

        function showSettings() {
            alert('Einstellungen werden geladen...');
        }

        // Print Functions
        function printOrder(orderId) {
            const order = orders.find(o => o.id === orderId);
            const customer = customers.find(c => c.id === order.customerId);
            
            if (!order || !customer) return;

            let printContent = '';
            printContent += '<div class="print-area">';
            printContent += '<h1 style="text-align: center; color: #2c3e50;">AUFTRAGSBESTÄTIGUNG</h1>';
            printContent += '<hr style="border: 2px solid #3498db; margin: 20px 0;">';
            
            printContent += '<table style="width: 100%; margin-bottom: 20px;">';
            printContent += '<tr>';
            printContent += '<td style="width: 50%;"><strong>Auftragsnummer:</strong> ' + order.id + '</td>';
            printContent += '<td style="width: 50%;"><strong>Erstellt am:</strong> ' + new Date(order.createdAt).toLocaleString('de-DE') + '</td>';
            printContent += '</tr>';
            printContent += '<tr>';
            printContent += '<td><strong>Status:</strong> ' + order.status + '</td>';
            printContent += '<td><strong>Priorität:</strong> ' + order.priority + '</td>';
            printContent += '</tr>';
            printContent += '</table>';

            printContent += '<h3>Kunde:</h3>';
            printContent += '<p>' + customer.company + '<br>' + customer.contact + '<br>' + customer.address + '<br>Tel: ' + customer.phone + '</p>';

            printContent += '<h3>Auftrag:</h3>';
            printContent += '<p><strong>' + order.title + '</strong></p>';
            printContent += '<p>' + order.description + '</p>';

            if (order.workTimes && order.workTimes.length > 0) {
                printContent += '<h3>Arbeitszeiten:</h3>';
                printContent += '<table style="width: 100%; border-collapse: collapse;">';
                printContent += '<tr style="background: #f8f9fa;"><th style="border: 1px solid #ddd; padding: 8px;">Datum</th><th style="border: 1px solid #ddd; padding: 8px;">Von</th><th style="border: 1px solid #ddd; padding: 8px;">Bis</th><th style="border: 1px solid #ddd; padding: 8px;">Dauer</th><th style="border: 1px solid #ddd; padding: 8px;">Ort</th><th style="border: 1px solid #ddd; padding: 8px;">Tätigkeit</th></tr>';
                
                let totalMinutes = 0;
                order.workTimes.forEach(wt => {
                    const start = new Date(wt.startTime);
                    const end = new Date(wt.endTime);
                    const diff = end - start;
                    totalMinutes += Math.floor(diff / 60000);
                    
                    printContent += '<tr>';
                    printContent += '<td style="border: 1px solid #ddd; padding: 8px;">' + start.toLocaleDateString('de-DE') + '</td>';
                    printContent += '<td style="border: 1px solid #ddd; padding: 8px;">' + start.toLocaleTimeString('de-DE') + '</td>';
                    printContent += '<td style="border: 1px solid #ddd; padding: 8px;">' + end.toLocaleTimeString('de-DE') + '</td>';
                    printContent += '<td style="border: 1px solid #ddd; padding: 8px;">' + wt.duration + '</td>';
                    printContent += '<td style="border: 1px solid #ddd; padding: 8px;">' + wt.location + '</td>';
                    printContent += '<td style="border: 1px solid #ddd; padding: 8px;">' + wt.description + '</td>';
                    printContent += '</tr>';
                });
                
                const totalHours = Math.floor(totalMinutes / 60);
                const remainingMinutes = totalMinutes % 60;
                printContent += '<tr style="background: #e9ecef; font-weight: bold;">';
                printContent += '<td colspan="3" style="border: 1px solid #ddd; padding: 8px;">Gesamtarbeitszeit:</td>';
                printContent += '<td style="border: 1px solid #ddd; padding: 8px;">' + totalHours + 'h ' + remainingMinutes + 'm</td>';
                printContent += '<td colspan="2" style="border: 1px solid #ddd; padding: 8px;"></td>';
                printContent += '</tr>';
                printContent += '</table>';
            }

            printContent += '<br><br>';
            printContent += '<table style="width: 100%;">';
            printContent += '<tr>';
            printContent += '<td style="width: 50%; border-bottom: 1px solid #333; text-align: center;">Unterschrift Mitarbeiter</td>';
            printContent += '<td style="width: 50%; border-bottom: 1px solid #333; text-align: center;">Unterschrift Kunde</td>';
            printContent += '</tr>';
            printContent += '</table>';

            printContent += '<p style="text-align: center; margin-top: 20px; font-size: 12px;">Gedruckt am: ' + new Date().toLocaleString('de-DE') + '</p>';
            printContent += '</div>';

            const printWindow = window.open('', '_blank');
            printWindow.document.write('<html><head><title>Auftrag ' + order.id + '</title></head><body>' + printContent + '</body></html>');
            printWindow.document.close();
            printWindow.print();
        }

        function printTimesheet(employeeId) {
            const employee = employees.find(e => e.id === employeeId);
            if (!employee) return;

            let printContent = '';
            printContent += '<div class="print-area">';
            printContent += '<h1 style="text-align: center; color: #2c3e50;">STUNDENZETTEL</h1>';
            printContent += '<hr style="border: 2px solid #3498db; margin: 20px 0;">';
            
            printContent += '<table style="width: 100%; margin-bottom: 20px;">';
            printContent += '<tr>';
            printContent += '<td style="width: 50%;"><strong>Mitarbeiter:</strong> ' + employee.name + '</td>';
            printContent += '<td style="width: 50%;"><strong>ID:</strong> ' + employee.id + '</td>';
            printContent += '</tr>';
            printContent += '<tr>';
            printContent += '<td><strong>Zeitraum:</strong> ' + new Date().toLocaleDateString('de-DE') + '</td>';
            printContent += '<td><strong>Erstellt am:</strong> ' + new Date().toLocaleString('de-DE') + '</td>';
            printContent += '</tr>';
            printContent += '</table>';

            if (employee.timeRecords.length > 0) {
                printContent += '<table style="width: 100%; border-collapse: collapse;">';
                printContent += '<tr style="background: #f8f9fa;"><th style="border: 1px solid #ddd; padding: 8px;">Datum</th><th style="border: 1px solid #ddd; padding: 8px;">Von</th><th style="border: 1px solid #ddd; padding: 8px;">Bis</th><th style="border: 1px solid #ddd; padding: 8px;">Dauer</th><th style="border: 1px solid #ddd; padding: 8px;">Auftrag</th><th style="border: 1px solid #ddd; padding: 8px;">Ort</th><th style="border: 1px solid #ddd; padding: 8px;">Tätigkeit</th></tr>';
                
                let totalMinutes = 0;
                employee.timeRecords.forEach(record => {
                    const start = new Date(record.startTime);
                    const end = new Date(record.endTime);
                    const order = orders.find(o => o.id === record.orderId);
                    const diff = end - start;
                    totalMinutes += Math.floor(diff / 60000);
                    
                    printContent += '<tr>';
                    printContent += '<td style="border: 1px solid #ddd; padding: 8px;">' + start.toLocaleDateString('de-DE') + '</td>';
                    printContent += '<td style="border: 1px solid #ddd; padding: 8px;">' + start.toLocaleTimeString('de-DE') + '</td>';
                    printContent += '<td style="border: 1px solid #ddd; padding: 8px;">' + end.toLocaleTimeString('de-DE') + '</td>';
                    printContent += '<td style="border: 1px solid #ddd; padding: 8px;">' + record.duration + '</td>';
                    printContent += '<td style="border: 1px solid #ddd; padding: 8px;">' + (order ? order.title : record.orderId) + '</td>';
                    printContent += '<td style="border: 1px solid #ddd; padding: 8px;">' + record.location + '</td>';
                    printContent += '<td style="border: 1px solid #ddd; padding: 8px;">' + record.description + '</td>';
                    printContent += '</tr>';
                });
                
                const totalHours = Math.floor(totalMinutes / 60);
                const remainingMinutes = totalMinutes % 60;
                printContent += '<tr style="background: #e9ecef; font-weight: bold;">';
                printContent += '<td colspan="3" style="border: 1px solid #ddd; padding: 8px;">Gesamtarbeitszeit:</td>';
                printContent += '<td style="border: 1px solid #ddd; padding: 8px;">' + totalHours + 'h ' + remainingMinutes + 'm</td>';
                printContent += '<td colspan="3" style="border: 1px solid #ddd; padding: 8px;"></td>';
                printContent += '</tr>';
                printContent += '</table>';
            } else {
                printContent += '<p>Keine Arbeitszeiten erfasst.</p>';
            }

            printContent += '<br><br>';
            printContent += '<table style="width: 100%;">';
            printContent += '<tr>';
            printContent += '<td style="width: 50%; border-bottom: 1px solid #333; text-align: center;">Unterschrift Mitarbeiter</td>';
            printContent += '<td style="width: 50%; border-bottom: 1px solid #333; text-align: center;">Unterschrift Kunde</td>';
            printContent += '</tr>';
            printContent += '</table>';

            printContent += '</div>';

            const printWindow = window.open('', '_blank');
            printWindow.document.write('<html><head><title>Stundenzettel ' + employee.name + '</title></head><body>' + printContent + '</body></html>');
            printWindow.document.close();
            printWindow.print();
        }

        // Utility Functions
        function closeModal(modalId) {
            document.getElementById(modalId).style.display = 'none';
        }

        function deleteCustomer(customerId) {
            if (confirm('Kunden wirklich löschen?')) {
                const index = customers.findIndex(c => c.id === customerId);
                if (index > -1) {
                    customers.splice(index, 1);
                    showCustomerManagement();
                    alert('Kunde gelöscht!');
                }
            }
        }

        function deleteEmployee(employeeId) {
            if (confirm('Mitarbeiter wirklich löschen?')) {
                const index = employees.findIndex(e => e.id === employeeId);
                if (index > -1) {
                    employees.splice(index, 1);
                    showEmployeeManagement();
                    alert('Mitarbeiter gelöscht!');
                }
            }
        }

        // Close modals when clicking outside
        window.onclick = function(event) {
            if (event.target.classList.contains('modal')) {
                event.target.style.display = 'none';
            }
        };
    </script>
</body>
</html>
