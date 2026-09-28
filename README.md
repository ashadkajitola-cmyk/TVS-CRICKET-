<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cricket Schedule & Betting Platform Pro</title>
    <style>
        :root {
            --primary: #1e3c72;
            --secondary: #2a5298;
            --accent: #ff9800;
            --bg: #f4f7f6;
            --white: #ffffff;
            --text: #333333;
            --danger: #e74c3c;
            --success: #2ecc71;
            --border: #e0e0e0;
        }
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { background-color: var(--bg); color: var(--text); padding-bottom: 50px; }
        header { background: linear-gradient(135deg, var(--primary), var(--secondary)); color: var(--white); padding: 15px 20px; display: flex; justify-content: space-between; align-items: center; box-shadow: 0 4px 15px rgba(0,0,0,0.15); }
        header h1 { font-size: 1.3rem; font-weight: 700; letter-spacing: 0.5px; }
        .user-info { display: flex; gap: 12px; align-items: center; font-size: 0.9rem; }
        .wallet-badge { background: var(--accent); color: #000; padding: 6px 12px; border-radius: 20px; font-weight: bold; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
        .container { max-width: 900px; margin: 20px auto; padding: 0 15px; }
        .card { background: var(--white); border-radius: 10px; padding: 20px; margin-bottom: 20px; box-shadow: 0 4px 10px rgba(0,0,0,0.05); }
        .btn { background: var(--secondary); color: var(--white); border: none; padding: 10px 18px; border-radius: 6px; cursor: pointer; font-weight: bold; transition: 0.2s; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
        .btn:hover { opacity: 0.9; transform: translateY(-1px); }
        .btn-danger { background: var(--danger); }
        .btn-success { background: var(--success); }
        .btn-warning { background: var(--accent); color: #000; }
        input, select, textarea { width: 100%; padding: 12px; margin: 8px 0 15px 0; border: 1px solid var(--border); border-radius: 6px; font-size: 0.95rem; background: #fff; }
        label { font-weight: 600; font-size: 0.85rem; color: #555; }
        .tabs { display: flex; gap: 6px; margin-bottom: 20px; background: #e9ecef; padding: 5px; border-radius: 8px; flex-wrap: wrap; }
        .tab-btn { flex: 1; min-width: 130px; padding: 10px; background: transparent; border: none; border-radius: 6px; cursor: pointer; font-weight: bold; color: #555; transition: 0.2s; font-size: 0.85rem; }
        .tab-btn.active { background: var(--white); color: var(--primary); box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        
        .match-card { border: 1px solid var(--border); border-radius: 8px; padding: 15px; margin-bottom: 15px; background: var(--white); box-shadow: 0 2px 5px rgba(0,0,0,0.02); }
        .match-card.new-series-gap { margin-top: 25px; border-left: 5px solid var(--accent); }
        .series-title-bar { background: #e8f4fd; color: #1a5276; padding: 8px 12px; border-radius: 6px; font-weight: bold; font-size: 0.95rem; margin-bottom: 12px; display: flex; justify-content: space-between; align-items: center; }
        .match-row { display: flex; justify-content: space-between; align-items: center; margin: 10px 0; }
        .team-box { font-size: 1.1rem; font-weight: bold; display: flex; align-items: center; gap: 8px; }
        .vs-text { font-weight: bold; color: #888; font-size: 0.9rem; }
        .match-meta { font-size: 0.85rem; color: #666; margin-top: 8px; border-top: 1px dashed var(--border); padding-top: 8px; display: flex; justify-content: space-between; flex-wrap: wrap; gap: 5px; }
        
        .hidden { display: none !important; }
        .flex-row { display: flex; gap: 10px; }
        .flex-row > * { flex: 1; }
        .modal { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.6); display: flex; justify-content: center; align-items: center; z-index: 1000; overflow-y: auto; padding: 20px; }
        .modal-content { background: var(--white); padding: 25px; border-radius: 10px; width: 100%; max-width: 600px; position: relative; max-height: 90vh; overflow-y: auto; }
        .close-modal { position: absolute; top: 12px; right: 18px; font-size: 1.4rem; cursor: pointer; color: #888; }
        .alert-box { padding: 12px; margin-bottom: 12px; border-radius: 6px; font-size: 0.9rem; }
        .alert-error { background: #fadbd8; color: #78281f; }
        .alert-success { background: #d4efdf; color: #145a32; }
    </style>
</head>
<body>

    <header>
        <h1>🏏 Cricket Schedule & Betting Pro</h1>
        <div class="user-info">
            <span id="displayNumber" style="font-weight: 650;">Login करें</span>
            <span class="wallet-badge">Wallet: ₹<span id="displayWallet">0</span></span>
            <button class="btn btn-danger" onclick="logout()" style="padding: 6px 12px; font-size: 0.8rem;">Logout</button>
        </div>
    </header>

    <div class="container">
        <!-- Login Section -->
        <div id="loginSection" class="card">
            <h2>Login / Register</h2>
            <p id="deviceLimitInfo" style="font-size:0.85rem; color:#666; margin-bottom:12px;"></p>
            <label>Mobile Number:</label>
            <input type="text" id="loginMobileInput" placeholder="Enter mobile number">
            <button class="btn" style="width:100%;" onclick="handleLogin()">Login to Dashboard</button>
        </div>

        <!-- Main Dashboard -->
        <div id="mainDashboard" class="hidden">
            
            <!-- Recharge / Transaction ID Card -->
            <div class="card" style="border-left: 5px solid var(--success);">
                <h3>💳 Wallet Recharge Request (Transaction ID)</h3>
                <p style="font-size: 0.85rem; color: #666; margin-bottom: 10px;">Payment SMS ki Full Transaction ID ya UTR number yahan dalein. Admin verify karne ke baad ₹210 approve karega.</p>
                <label>Full Transaction ID / UTR:</label>
                <input type="text" id="txFullInput" placeholder="Enter full transaction reference ID">
                <button class="btn btn-success" onclick="submitRechargeRequest()" style="width:100%;">Submit for Admin Verification</button>
            </div>

            <!-- Dashboard Access Button / Panel Trigger -->
            <div class="card" style="border-left: 5px solid var(--accent);">
                <h3>🚀 Creator & Schedule Panel</h3>
                <p style="font-size: 0.85rem; color: #666; margin-bottom: 10px;">Match Schedule create karne ke liye panel open karein (Subscription zaroori hai).</p>
                <button class="btn btn-warning" style="width: 100%;" onclick="openCreatorDashboard()">📂 Open Creator & Schedule Panel</button>
            </div>

            <!-- Master Admin Extra Controls Card -->
            <div id="adminMainControlCard" class="card hidden" style="border-left: 5px solid var(--danger); background: #fdfefe;">
                <h3 style="color: var(--danger);">👑 Master Website Admin Control Center</h3>
                <p style="font-size: 0.85rem; color: #666; margin-bottom: 12px;">Yahan se aap saare matches, pending recharges, tickets aur subscription plans ko manage/edit kar sakte hain.</p>
                <div style="display: flex; gap: 10px; flex-wrap: wrap;">
                    <button class="btn btn-warning" style="flex: 1;" onclick="openRechargeRequestsModal()">📥 Verify Recharges (<span id="pendingCountBadge">0</span>)</button>
                    <button class="btn btn-danger" style="flex: 1;" onclick="openMasterAdminPanel()">⚙️ Manage Matches, Tickets & Plans</button>
                </div>
            </div>

            <!-- Active Subscription Status Box -->
            <div id="activeSubStatusBox" class="card hidden" style="border-left: 5px solid var(--primary); background: #f0f4f8;">
                <h3>✨ Active Subscription Status</h3>
                <div id="subStatusContent" style="margin-top: 10px; font-size: 0.95rem;"></div>
            </div>

            <!-- Code Verification Box -->
            <div class="card">
                <h3>🔍 6-Digit Code Verification</h3>
                <div class="flex-row">
                    <input type="text" id="verifyCodeInput" maxlength="6" placeholder="Enter 6-digit match code">
                    <button class="btn" onclick="verifyMatchCode()" style="margin-top:8px;">Check Code</button>
                </div>
                <div id="verifyResult" style="margin-top: 10px;"></div>
            </div>

            <!-- Tabs -->
            <div class="tabs">
                <button class="tab-btn active" onclick="switchTab('international', event)">🌍 International</button>
                <button class="tab-btn" onclick="switchTab('apna', event)">👤 Apna Schedule</button>
                <button class="tab-btn" onclick="switchTab('activeTickets', event)">🎟️ Active Ticket Distric by Zomato</button>
                <button class="tab-btn" onclick="switchTab('myPurchased', event)">📦 My Purchased Tickets</button>
            </div>

            <!-- Tab Content -->
            <div id="internationalTabContent" class="tab-content">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
                    <h2>International Matches</h2>
                    <button id="adminCreateMatchBtn" class="btn btn-success hidden" onclick="openInternationalMatchModal()">+ Create International Match</button>
                </div>
                <div id="internationalMatchesList" style="margin-top: 15px;"></div>
            </div>

            <div id="apnaTabContent" class="tab-content hidden">
                <h2>Apna Schedule (User Created)</h2>
                <div id="apnaMatchesList" style="margin-top: 15px;"></div>
            </div>

            <div id="activeTicketsTabContent" class="tab-content hidden">
                <h2>Active Ticket Distric by Zomato</h2>
                <div id="activeTicketsList" style="margin-top: 15px;"></div>
            </div>

            <div id="myPurchasedTabContent" class="tab-content hidden">
                <h2>All Purchased Tickets History</h2>
                <div id="myPurchasedList" style="margin-top: 15px;"></div>
            </div>

        </div>
    </div>

    <!-- Creator Dashboard / Subscription Modal -->
    <div id="creatorModal" class="modal hidden">
        <div class="modal-content">
            <span class="close-modal" onclick="closeCreatorModal()">&times;</span>
            
            <div id="subscriptionRequiredView">
                <h3 style="margin-bottom: 10px; color: var(--danger);">📢 Subscription Required</h3>
                <p style="font-size:0.85rem; color:#666; margin-bottom:15px;">Apna schedule create karne ke liye pehle subscription plan kharidein:</p>
                <div id="subPlansList" style="display: flex; flex-direction: column; gap: 8px; margin-bottom: 15px;"></div>
                <button class="btn btn-success" style="width:100%;" onclick="buySelectedSubscription()">Subscription Buy Karein</button>
            </div>

            <div id="creatorActionView" class="hidden">
                <h3 style="margin-bottom: 15px;">👤 Creator Panel (Schedule Only)</h3>
                <p style="font-size: 0.9rem; color: var(--success); margin-bottom: 15px; font-weight: bold;">✔ Aapke paas active subscription hai. Aap sirf Match Schedule create kar sakte hain:</p>
                <div style="display: flex; gap: 10px; flex-direction: column;">
                    <button class="btn" style="width:100%;" onclick="openMatchModal()">🏏 Create Match Schedule Only</button>
                </div>
            </div>

        </div>
    </div>

    <!-- Match Creation Modal (Only Match Details) -->
    <div id="matchModal" class="modal hidden">
        <div class="modal-content">
            <span class="close-modal" onclick="closeMatchModal()">&times;</span>
            <h3 style="margin-bottom: 15px;">🏏 Create Match Schedule Only</h3>
            
            <label>Series Type:</label>
            <select id="matchSeriesType">
                <option value="existing">Existing Series (Bina Gap ke)</option>
                <option value="new">New Series (Thoda Gap / Special Section)</option>
            </select>

            <label>Series Name:</label>
            <input type="text" id="matchSeriesName" placeholder="e.g., Local League 2026">

            <div class="flex-row">
                <div><label>Team 1 Name:</label><input type="text" id="matchTeam1" placeholder="Team A"></div>
                <div><label>Team 2 Name:</label><input type="text" id="matchTeam2" placeholder="Team B"></div>
            </div>

            <div class="flex-row">
                <div><label>Team 1 Score:</label><input type="text" id="matchScore1" placeholder="180/4"></div>
                <div><label>Team 2 Score:</label><input type="text" id="matchScore2" placeholder="175/8"></div>
            </div>

            <label>Toss Update:</label>
            <select id="matchToss">
                <option value="Yet to happen">Toss Yet to Happen</option>
                <option value="Team 1 won toss & elected to bat">Team 1 won toss & elected to bat</option>
                <option value="Team 1 won toss & elected to field">Team 1 won toss & elected to field</option>
                <option value="Team 2 won toss & elected to bat">Team 2 won toss & elected to bat</option>
                <option value="Team 2 won toss & elected to field">Team 2 won toss & elected to field</option>
            </select>

            <label>Date & Time:</label>
            <input type="text" id="matchDateTime" placeholder="2026/23-Sep/3:30 pm">

            <label>Venue:</label>
            <input type="text" id="matchVenue" placeholder="Ground Name">

            <label>6-Digit Security Code:</label>
            <input type="text" id="matchCode6" maxlength="6" placeholder="6 digit code">

            <label>Result / Winner Status:</label>
            <select id="matchResultStatus">
                <option value="Upcoming">Upcoming / Live</option>
                <option value="Team 1 Won">Team 1 Won (Double Payout)</option>
                <option value="Team 2 Won">Team 2 Won (Double Payout)</option>
                <option value="Draw / Abandoned">Draw / Refund</option>
            </select>

            <button class="btn" style="width:100%; margin-top:10px;" onclick="saveMatchSchedule(false)">Save & Publish Match</button>
        </div>
    </div>

    <!-- International Match Creation Modal (Admin Only) -->
    <div id="internationalMatchModal" class="modal hidden">
        <div class="modal-content">
            <span class="close-modal" onclick="closeInternationalMatchModal()">&times;</span>
            <h3 style="margin-bottom: 15px;">🌍 Create International Match (Admin)</h3>
            
            <label>Series Type:</label>
            <select id="intSeriesType">
                <option value="existing">Existing Series (Bina Gap ke)</option>
                <option value="new">New Series (Thoda Gap / Special Section)</option>
            </select>

            <label>Series Name:</label>
            <input type="text" id="intSeriesName" placeholder="e.g., ICC World Cup 2026">

            <div class="flex-row">
                <div><label>Team 1 Name:</label><input type="text" id="intTeam1" placeholder="India"></div>
                <div><label>Team 2 Name:</label><input type="text" id="intTeam2" placeholder="Australia"></div>
            </div>

            <div class="flex-row">
                <div><label>Team 1 Score:</label><input type="text" id="intScore1" placeholder="250/5"></div>
                <div><label>Team 2 Score:</label><input type="text" id="intScore2" placeholder="240/10"></div>
            </div>

            <label>Toss Update:</label>
            <select id="intToss">
                <option value="Yet to happen">Toss Yet to Happen</option>
                <option value="Team 1 won toss & elected to bat">Team 1 won toss & elected to bat</option>
                <option value="Team 1 won toss & elected to field">Team 1 won toss & elected to field</option>
                <option value="Team 2 won toss & elected to bat">Team 2 won toss & elected to bat</option>
                <option value="Team 2 won toss & elected to field">Team 2 won toss & elected to field</option>
            </select>

            <label>Date & Time:</label>
            <input type="text" id="intDateTime" placeholder="2026/23-Sep/3:30 pm">

            <label>Venue:</label>
            <input type="text" id="intVenue" placeholder="Stadium Name">

            <div class="flex-row">
                <div><label>Ticket Price (₹):</label><input type="number" id="intPrice" placeholder="200"></div>
                <div><label>Total Tickets Limit:</label><input type="number" id="intLimit" placeholder="100"></div>
            </div>

            <label>6-Digit Security Code:</label>
            <input type="text" id="intCode6" maxlength="6" placeholder="6 digit code">

            <label>Result / Winner Status:</label>
            <select id="intResultStatus">
                <option value="Upcoming">Upcoming / Live</option>
                <option value="Team 1 Won">Team 1 Won (Double Payout)</option>
                <option value="Team 2 Won">Team 2 Won (Double Payout)</option>
                <option value="Draw / Abandoned">Draw / Refund</option>
            </select>

            <button class="btn" style="width:100%; margin-top:10px;" onclick="saveMatchSchedule(true)">Publish International Match</button>
        </div>
    </div>

    <!-- Admin Recharge Verification Modal -->
    <div id="rechargeModal" class="modal hidden">
        <div class="modal-content">
            <span class="close-modal" onclick="closeRechargeModal()">&times;</span>
            <h3 style="margin-bottom: 15px;">📥 Pending Recharge Requests</h3>
            <div id="pendingRechargesList" style="margin-top: 10px;"></div>
        </div>
    </div>

    <!-- Master Admin Management & Edit Modal (Matches, Tickets, Plans) -->
    <div id="masterAdminModal" class="modal hidden">
        <div class="modal-content" style="max-width: 700px;">
            <span class="close-modal" onclick="closeMasterAdminModal()">&times;</span>
            <h3 style="margin-bottom: 15px; color: var(--primary);">⚙️ Master Admin Panel</h3>
            
            <div class="tabs" style="margin-bottom:15px;">
                <button class="tab-btn active" onclick="switchAdminSubTab('matches', event)">Matches</button>
                <button class="tab-btn" onclick="switchAdminSubTab('tickets', event)">All Tickets</button>
                <button class="tab-btn" onclick="switchAdminSubTab('plans', event)">Subscriptions</button>
            </div>

            <div id="adminTabMatches" class="admin-sub-tab">
                <p style="font-size:0.85rem; color:#666; margin-bottom:10px;">Match details, prices ya winner update karein:</p>
                <div id="adminAllMatchesList"></div>
            </div>

            <div id="adminTabTickets" class="admin-sub-tab hidden">
                <p style="font-size:0.85rem; color:#666; margin-bottom:10px;">Saari generated tickets:</p>
                <div id="adminAllTicketsList"></div>
            </div>

            <div id="adminTabPlans" class="admin-sub-tab hidden">
                <p style="font-size:0.85rem; color:#666; margin-bottom:10px;">Subscription Plans Edit Karein ya Naya Plan Add Karein:</p>
                <div id="adminPlansList" style="margin-bottom: 15px;"></div>
                <hr style="margin: 15px 0;">
                <h4>Add New Subscription Plan</h4>
                <label>Plan ID:</label><input type="text" id="newPlanId" placeholder="e.g., 30days_special">
                <label>Plan Name:</label><input type="text" id="newPlanName" placeholder="30 Days Monthly Pass">
                <div class="flex-row">
                    <div><label>Price (₹):</label><input type="number" id="newPlanPrice" placeholder="499"></div>
                    <div><label>Duration Days:</label><input type="number" id="newPlanDays" placeholder="30"></div>
                </div>
                <button class="btn btn-success" style="width:100%;" onclick="addNewSubscriptionPlan()">Add New Plan</button>
            </div>
        </div>
    </div>

    <!-- Single Match Edit Modal for Admin -->
    <div id="editSingleMatchModal" class="modal hidden">
        <div class="modal-content">
            <span class="close-modal" onclick="closeEditSingleMatchModal()">&times;</span>
            <h3 style="margin-bottom: 15px;">✏️ Edit Match, Ticket Price & Winner Status</h3>
            <input type="hidden" id="editMatchId">

            <label>Series Name:</label>
            <input type="text" id="editSeriesName">

            <div class="flex-row">
                <div><label>Team 1:</label><input type="text" id="editTeam1"></div>
                <div><label>Team 2:</label><input type="text" id="editTeam2"></div>
            </div>

            <div class="flex-row">
                <div><label>Ticket Price (₹):</label><input type="number" id="editMatchPrice"></div>
                <div><label>Ticket Limit:</label><input type="number" id="editMatchLimit"></div>
            </div>

            <label>Result / Winner Status:</label>
            <select id="editResultStatus">
                <option value="Upcoming">Upcoming / Live</option>
                <option value="Team 1 Won">Team 1 Won (Double Payout)</option>
                <option value="Team 2 Won">Team 2 Won (Double Payout)</option>
                <option value="Draw / Abandoned">Draw / Refund</option>
            </select>

            <button class="btn btn-success" style="width:100%; margin-top:10px;" onclick="saveEditedMatch()">Update Match Settings</button>
        </div>
    </div>

    <script>
        const DEFAULT_ADMIN = "9569981483";
        
        let db = JSON.parse(localStorage.getItem('cricket_pro_db')) || {
            users: {},
            matches: [],
            tickets: [],
            rechargeRequests: [],
            usedTransactions: [],
            settings: {
                adminNumber: DEFAULT_ADMIN,
                maxDevices: 6,
                plans: [
                    { id: '4hour', name: '4 Hour Pass', price: 99, durationHours: 4 },
                    { id: '1day', name: '1 Day Pass', price: 108, durationHours: 24, matchesCount: 1 },
                    { id: '30days', name: '30 Days Monthly Plan', price: 449, durationDays: 30 }
                ]
            },
            deviceSessions: {}
        };

        // Ensure settings are synced correctly
        db.settings.adminNumber = DEFAULT_ADMIN;
        db.settings.maxDevices = 6;

        let currentMobile = localStorage.getItem('cricket_pro_current_mobile') || null;
        let deviceId = localStorage.getItem('cricket_pro_device_id') || 'dev_' + Math.random().toString(36).substring(2,9);
        localStorage.setItem('cricket_pro_device_id', deviceId);

        function saveDB() {
            localStorage.setItem('cricket_pro_db', JSON.stringify(db));
        }

        window.onload = function() {
            if (!db.users[db.settings.adminNumber]) {
                db.users[db.settings.adminNumber] = { wallet: 5000, subscription: null };
            } else {
                if (db.users[db.settings.adminNumber].wallet < 5000) {
                    db.users[db.settings.adminNumber].wallet = 5000;
                }
            }

            if (currentMobile && db.users[currentMobile]) {
                showDashboard();
            } else {
                currentMobile = null;
                showLogin();
            }
        };

        function showLogin() {
            document.getElementById('loginSection').classList.remove('hidden');
            document.getElementById('mainDashboard').classList.add('hidden');
            document.getElementById('deviceLimitInfo').innerText = `(Max ${db.settings.maxDevices} numbers allowed per device)`;
        }

        function showDashboard() {
            document.getElementById('loginSection').classList.add('hidden');
            document.getElementById('mainDashboard').classList.remove('hidden');
            
            let isAdmin = (currentMobile === db.settings.adminNumber);
            if (isAdmin) {
                document.getElementById('adminCreateMatchBtn').classList.remove('hidden');
                document.getElementById('adminMainControlCard').classList.remove('hidden');
            } else {
                document.getElementById('adminCreateMatchBtn').classList.add('hidden');
                document.getElementById('adminMainControlCard').classList.add('hidden');
            }

            updateHeader();
            renderSubscriptionStatusBox();
            renderSubscriptionPlans();
            renderMatches();
            renderActiveTickets();
            renderMyPurchasedTickets();
        }

        function handleLogin() {
            let mobile = document.getElementById('loginMobileInput').value.trim();
            if (!mobile || mobile.length < 10) {
                alert("Kripya sahi 10-digit mobile number enter karein!");
                return;
            }

            if (!db.deviceSessions[deviceId]) db.deviceSessions[deviceId] = [];
            let activeNumbers = db.deviceSessions[deviceId];
            
            if (!activeNumbers.includes(mobile)) {
                if (activeNumbers.length >= db.settings.maxDevices) {
                    alert(`Is device par maximum ${db.settings.maxDevices} numbers hi allow hain!`);
                    return;
                }
                activeNumbers.push(mobile);
            }

            if (!db.users[mobile]) {
                let initialWallet = (mobile === db.settings.adminNumber) ? 5000 : 200;
                db.users[mobile] = { wallet: initialWallet, subscription: null };
            } else {
                if (mobile === db.settings.adminNumber && db.users[mobile].wallet < 5000) {
                    db.users[mobile].wallet = 5000;
                }
            }

            currentMobile = mobile;
            localStorage.setItem('cricket_pro_current_mobile', currentMobile);
            saveDB();
            showDashboard();
        }

        function logout() {
            currentMobile = null;
            localStorage.removeItem('cricket_pro_current_mobile');
            showLogin();
        }

        function updateHeader() {
            document.getElementById('displayNumber').innerText = currentMobile;
            let user = db.users[currentMobile];
            document.getElementById('displayWallet').innerText = user ? user.wallet : 0;
            
            if (currentMobile === db.settings.adminNumber) {
                let pending = (db.rechargeRequests || []).filter(r => r.status === 'Pending').length;
                let badge = document.getElementById('pendingCountBadge');
                if (badge) badge.innerText = pending;
            }
        }

        function submitRechargeRequest() {
            let txInput = document.getElementById('txFullInput').value.trim();
            if (!txInput || txInput.length < 6) {
                alert("Kripya valid Transaction ID / UTR enter karein!");
                return;
            }

            if (!db.usedTransactions) db.usedTransactions = [];
            if (db.usedTransactions.includes(txInput)) {
                alert("Yeh Transaction ID pehle hi use ki ja chuki hai!");
                return;
            }

            if (!db.rechargeRequests) db.rechargeRequests = [];
            let existingPending = db.rechargeRequests.find(r => r.txId === txInput && r.status === 'Pending');
            if (existingPending) {
                alert("Is Transaction ID ki request pehle se hi pending hai!");
                return;
            }

            db.rechargeRequests.push({
                id: 'req_' + Date.now(),
                mobile: currentMobile,
                txId: txInput,
                status: 'Pending'
            });

            saveDB();
            document.getElementById('txFullInput').value = '';
            alert("Aapki recharge request bhej di gayi hai!");
        }

        function openRechargeRequestsModal() {
            if (currentMobile !== db.settings.adminNumber) return;
            let listDiv = document.getElementById('pendingRechargesList');
            let pending = (db.rechargeRequests || []).filter(r => r.status === 'Pending');

            if (pending.length === 0) {
                listDiv.innerHTML = '<p>Koi pending recharge request nahi hai.</p>';
            } else {
                let html = '';
                pending.forEach(req => {
                    html += `
                        <div class="match-card" style="border-left: 5px solid var(--accent); padding:10px; margin-bottom:10px;">
                            <p><strong>Mobile:</strong> ${req.mobile}</p>
                            <p><strong>Tx ID / UTR:</strong> ${req.txId}</p>
                            <div style="margin-top:8px; display:flex; gap:10px;">
                                <button class="btn btn-success" style="padding:5px 10px; font-size:0.8rem;" onclick="approveRecharge('${req.id}')">Approve & Send ₹210</button>
                                <button class="btn btn-danger" style="padding:5px 10px; font-size:0.8rem;" onclick="rejectRecharge('${req.id}')">Reject</button>
                            </div>
                        </div>
                    `;
                });
                listDiv.innerHTML = html;
            }
            document.getElementById('rechargeModal').classList.remove('hidden');
        }

        function closeRechargeModal() { document.getElementById('rechargeModal').classList.add('hidden'); }

        function approveRecharge(reqId) {
            let req = db.rechargeRequests.find(r => r.id === reqId);
            if (!req) return;

            if (!db.usedTransactions) db.usedTransactions = [];
            db.usedTransactions.push(req.txId);
            req.status = 'Approved';

            if (!db.users[req.mobile]) db.users[req.mobile] = { wallet: 0, subscription: null };
            db.users[req.mobile].wallet += 210;

            saveDB();
            updateHeader();
            openRechargeRequestsModal();
            alert("Request approve ho gayi aur ₹210 bhej diye gaye!");
        }

        function rejectRecharge(reqId) {
            db.rechargeRequests = db.rechargeRequests.filter(r => r.id !== reqId);
            saveDB();
            updateHeader();
            openRechargeRequestsModal();
            alert("Request reject kar di gayi.");
        }

        function checkUserHasActiveSub() {
            let isAdmin = (currentMobile === db.settings.adminNumber);
            if (isAdmin) return true;

            let user = db.users[currentMobile];
            if (user && user.subscription) {
                return new Date().getTime() < user.subscription.expiresAt;
            }
            return false;
        }

        function renderSubscriptionStatusBox() {
            let box = document.getElementById('activeSubStatusBox');
            let content = document.getElementById('subStatusContent');
            let user = db.users[currentMobile];
            let isAdmin = (currentMobile === db.settings.adminNumber);

            if (isAdmin) {
                box.classList.remove('hidden');
                content.innerHTML = `<strong>Role:</strong> Master Website Admin (Full Access)`;
                return;
            }

            if (user && user.subscription && checkUserHasActiveSub()) {
                box.classList.remove('hidden');
                let sub = user.subscription;
                let now = new Date().getTime();
                let diffMs = sub.expiresAt - now;
                let diffHrs = Math.floor(diffMs / (1000 * 60 * 60));
                let diffDays = Math.floor(diffHrs / 24);
                let timeLeftText = diffDays > 0 ? `Validity: ${diffDays} Days (~${diffHrs} Hours)` : `Validity: ${diffHrs} Hours`;

                content.innerHTML = `<strong>Plan:</strong> ${sub.planName} <br>⏱️ ${timeLeftText}`;
            } else {
                box.classList.add('hidden');
            }
        }

        function openCreatorDashboard() {
            let modal = document.getElementById('creatorModal');
            let reqView = document.getElementById('subscriptionRequiredView');
            let actView = document.getElementById('creatorActionView');

            if (checkUserHasActiveSub()) {
                reqView.classList.add('hidden');
                actView.classList.remove('hidden');
            } else {
                reqView.classList.remove('hidden');
                actView.classList.add('hidden');
            }
            modal.classList.remove('hidden');
        }

        function closeCreatorModal() { document.getElementById('creatorModal').classList.add('hidden'); }

        function renderSubscriptionPlans() {
            let listHTML = '';
            db.settings.plans.forEach((plan, index) => {
                let checked = index === 0 ? 'checked' : '';
                listHTML += `<label><input type="radio" name="subPlan" value="${plan.id}" ${checked}> ${plan.name} - ₹${plan.price}</label>`;
            });
            document.getElementById('subPlansList').innerHTML = listHTML;
        }

        function buySelectedSubscription() {
            let selectedRadio = document.querySelector('input[name="subPlan"]:checked');
            if (!selectedRadio) { alert("Kripya pehle koi plan select karein!"); return; }
            let planObj = db.settings.plans.find(p => p.id === selectedRadio.value);
            if (!planObj) return;

            let user = db.users[currentMobile];
            if (user.wallet < planObj.price) {
                alert("Wallet me balance kam hai!");
                return;
            }

            user.wallet -= planObj.price;
            let adminMob = db.settings.adminNumber;
            if (!db.users[adminMob]) db.users[adminMob] = { wallet: 5000, subscription: null };
            db.users[adminMob].wallet += planObj.price;

            let now = new Date().getTime();
            let expiresAt = now + (30 * 24 * 3600 * 1000);
            if (planObj.durationHours) expiresAt = now + (planObj.durationHours * 3600 * 1000);
            if (planObj.durationDays) expiresAt = now + (planObj.durationDays * 24 * 3600 * 1000);

            user.subscription = { planId: planObj.id, planName: planObj.name, expiresAt: expiresAt };

            saveDB();
            updateHeader();
            renderSubscriptionStatusBox();
            closeCreatorModal();
            alert("Subscription successfully buy ho gaya!");
        }

        function openMatchModal() { closeCreatorModal(); document.getElementById('matchModal').classList.remove('hidden'); }
        function closeMatchModal() { document.getElementById('matchModal').classList.add('hidden'); }

        function openInternationalMatchModal() { document.getElementById('internationalMatchModal').classList.remove('hidden'); }
        function closeInternationalMatchModal() { document.getElementById('internationalMatchModal').classList.add('hidden'); }

        function saveMatchSchedule(isInternational) {
            let prefix = isInternational ? 'int' : 'match';
            let matchObj = {
                id: 'match_' + Date.now(),
                creator: currentMobile,
                isInternational: isInternational,
                seriesType: document.getElementById(`${prefix}SeriesType`).value,
                seriesName: document.getElementById(`${prefix}SeriesName`).value.trim(),
                team1: document.getElementById(`${prefix}Team1`).value.trim(),
                team2: document.getElementById(`${prefix}Team2`).value.trim(),
                score1: document.getElementById(`${prefix}Score1`).value.trim() || 'Yet to bat',
                score2: document.getElementById(`${prefix}Score2`).value.trim() || 'Yet to bat',
                toss: document.getElementById(`${prefix}Toss`).value,
                dateTime: document.getElementById(`${prefix}DateTime`).value.trim() || "2026/23-Sep/3:30 pm",
                venue: document.getElementById(`${prefix}Venue`).value.trim() || 'Stadium',
                price: isInternational ? (Number(document.getElementById('intPrice').value) || 0) : 0,
                limit: isInternational ? (Number(document.getElementById('intLimit').value) || 0) : 0,
                soldCount: 0,
                code6: document.getElementById(`${prefix}Code6`).value.trim(),
                resultStatus: document.getElementById(`${prefix}ResultStatus`).value
            };

            if (!matchObj.seriesName || !matchObj.team1 || !matchObj.team2 || matchObj.code6.length !== 6) {
                alert("Sabhi zaroori fields bharein (6 digit code zarouri hai)!");
                return;
            }

            db.matches.push(matchObj);
            saveDB();
            if (isInternational) closeInternationalMatchModal();
            else closeMatchModal();
            renderMatches();
            alert("Match successfully publish ho gaya!");
        }

        function verifyMatchCode() {
            let code = document.getElementById('verifyCodeInput').value.trim();
            let resDiv = document.getElementById('verifyResult');
            let match = db.matches.find(m => m.code6 === code);

            if (!match) {
                resDiv.innerHTML = `<div class="alert-box alert-error">Invalid Code!</div>`;
                return;
            }

            resDiv.innerHTML = `
                <div class="alert-box alert-success">
                    <strong>Series:</strong> ${match.seriesName}<br>
                    <strong>Match:</strong> ${match.team1} vs ${match.team2}<br>
                    <strong>Toss:</strong> ${match.toss || 'Not updated'}
                </div>
            `;
        }

        function renderMatches() {
            let intList = document.getElementById('internationalMatchesList');
            let apnaList = document.getElementById('apnaMatchesList');
            let intHTML = '', apnaHTML = '';

            db.matches.forEach(match => {
                checkAndSettleMatchResults(match);
                let priceDisplay = (match.price && match.price > 0) ? `₹${match.price}` : `<span style="color:var(--danger)">Price Not Set</span>`;
                let cardClass = match.seriesType === 'new' ? 'match-card new-series-gap' : 'match-card';

                let cardHTML = `
                    <div class="${cardClass}">
                        <div class="series-title-bar">
                            <span>${match.seriesName}</span>
                            <span style="font-size:0.75rem; background:#fff; padding:2px 6px; border-radius:4px; color:#333;">Code: ${match.code6}</span>
                        </div>
                        <div class="match-row">
                            <div class="team-box">🏏 ${match.team1}</div>
                            <div class="vs-text">vs</div>
                            <div class="team-box">${match.team2} 🏏</div>
                        </div>
                        <div style="font-size:0.85rem; color:#444; margin-bottom:8px;">
                            <strong>Toss:</strong> ${match.toss || 'Yet to happen'}
                        </div>
                        <div class="match-meta">
                            <span>💰 Ticket Price: ${priceDisplay} (Sold: ${match.soldCount}/${match.limit})</span>
                        </div>
                        <div style="margin-top: 10px; display:flex; justify-content:space-between; align-items:center;">
                            <span style="font-size:0.85rem; font-weight:bold; color:var(--success);">Status: ${match.resultStatus}</span>
                            <div>
                                ${(currentMobile === db.settings.adminNumber || currentMobile === match.creator) ? 
                                    `<button class="btn btn-danger" style="padding:6px 12px; font-size:0.85rem;" onclick="deleteMatch('${match.id}')">Delete</button>` : ''}
                            </div>
                        </div>
                    </div>
                `;

                if (match.isInternational) {
                    intHTML += cardHTML;
                } else {
                    apnaHTML += cardHTML;
                }
            });

            intList.innerHTML = intHTML || '<p>Koi International match nahi hai.</p>';
            apnaList.innerHTML = apnaHTML || '<p>Koi apna schedule create nahi kiya gaya hai.</p>';
        }

        function buyTicket(matchId) {
            let match = db.matches.find(m => m.id === matchId);
            if (!match) return;

            if (!match.price || match.price <= 0) {
                alert("Ticket ka price fix nahi hai, isliye ticket buy nahi ho sakti!");
                return;
            }

            if (match.soldCount >= match.limit) { 
                alert("Sold out!"); 
                return; 
            }

            let user = db.users[currentMobile];
            if (user.wallet < match.price) { 
                alert("Wallet balance kam hai!"); 
                return; 
            }

            user.wallet -= match.price;
            let recipientMob = match.creator || db.settings.adminNumber;
            if (!db.users[recipientMob]) db.users[recipientMob] = { wallet: 5000, subscription: null };
            db.users[recipientMob].wallet += match.price;

            match.soldCount += 1;
            db.tickets.push({
                id: 'tkt_' + Date.now(),
                matchId: match.id,
                mobile: currentMobile,
                pricePaid: match.price,
                teamPicked: null,
                sattaAmount: 0,
                status: 'Active'
            });

            saveDB();
            updateHeader();
            renderMatches();
            renderActiveTickets();
            renderMyPurchasedTickets();
            alert("Ticket successfully buy ho gayi via Zomato District!");
        }

        function renderActiveTickets() {
            let listDiv = document.getElementById('activeTicketsList');
            let userTickets = db.tickets.filter(t => t.mobile === currentMobile && t.status === 'Active');

            if (userTickets.length === 0) {
                let buyOptionsHTML = '';
                db.matches.forEach(m => {
                    if(m.price && m.price > 0) {
                        buyOptionsHTML += `
                            <div style="background:#fff; padding:10px; margin-bottom:10px; border-radius:6px; border:1px solid var(--border); display:flex; justify-content:space-between; align-items:center;">
                                <span><strong>${m.seriesName}</strong> (${m.team1} vs ${m.team2}) - ₹${m.price}</span>
                                <button class="btn btn-success" style="padding:5px 10px; font-size:0.8rem;" onclick="buyTicket('${m.id}')">Buy via Zomato District</button>
                            </div>
                        `;
                    }
                });
                listDiv.innerHTML = '<p>Koi active running ticket nahi hai. Ticket kharidne ke liye "Active Ticket Distric by Zomato" tab ke zariye available matches se book karein:</p>' + (buyOptionsHTML || '<p>Koi ticket available nahi hai.</p>');
                return;
            }

            let html = '';
            userTickets.forEach(tkt => {
                let match = db.matches.find(m => m.id === tkt.matchId);
                if (!match) return;

                html += `
                    <div class="match-card" style="border-left: 5px solid var(--success);">
                        <div class="series-title-bar"><span>Ticket ID: ${tkt.id}</span><span>${match.seriesName}</span></div>
                        <p><strong>${match.team1} vs ${match.team2}</strong></p>
                        <div style="margin-top:10px; background:#fcfcfc; padding:12px; border-radius:6px; border:1px solid var(--border);">
                            <h4 style="margin-bottom:8px;">🎲 Satta & Bet Zone</h4>
                            ${tkt.teamPicked ? 
                                `<p>Chuni gayi team: <b>${tkt.teamPicked}</b> | Lagaye gaye ₹: <b>${tkt.sattaAmount}</b></p>` :
                                `<label>Konsi team jeete gi?</label>
                                <select id="sattaTeam_${tkt.id}"><option value="${match.team1}">${match.team1}</option><option value="${match.team2}">${match.team2}</option></select>
                                <label>Bet Amount (₹):</label>
                                <input type="number" id="sattaAmt_${tkt.id}" placeholder="Amount">
                                <button class="btn btn-warning" style="width:100%;" onclick="placeSatta('${tkt.id}')">Confirm Satta</button>`
                            }
                        </div>
                    </div>
                `;
            });
            listDiv.innerHTML = html;
        }

        function renderMyPurchasedTickets() {
            let listDiv = document.getElementById('myPurchasedList');
            let userTickets = db.tickets.filter(t => t.mobile === currentMobile);

            if (userTickets.length === 0) {
                listDiv.innerHTML = '<p>Koi ticket history nahi hai.</p>';
                return;
            }

            let html = '';
            userTickets.forEach(tkt => {
                let match = db.matches.find(m => m.id === tkt.matchId);
                let matchName = match ? `${match.team1} vs ${match.team2}` : 'Expired';
                html += `
                    <div class="match-card">
                        <p><strong>Ticket ID:</strong> ${tkt.id} | Match: ${matchName}</p>
                        <p style="font-size:0.85rem; color:#666;">Price: ₹${tkt.pricePaid} | Status: ${tkt.status}</p>
                    </div>
                `;
            });
            listDiv.innerHTML = html;
        }

        function placeSatta(tktId) {
            let tkt = db.tickets.find(t => t.id === tktId);
            let match = db.matches.find(m => m.id === tkt.matchId);
            let team = document.getElementById(`sattaTeam_${tktId}`).value;
            let amt = Number(document.getElementById(`sattaAmt_${tktId}`).value);

            let user = db.users[currentMobile];
            if (amt <= 0 || user.wallet < amt) { alert("Wallet balance kam hai!"); return; }

            user.wallet -= amt;
            let recipientMob = match.creator || db.settings.adminNumber;
            if (!db.users[recipientMob]) db.users[recipientMob] = { wallet: 5000, subscription: null };
            db.users[recipientMob].wallet += amt;

            tkt.teamPicked = team;
            tkt.sattaAmount = amt;
            saveDB();
            updateHeader();
            renderActiveTickets();
            renderMyPurchasedTickets();
            alert("Satta placed successfully!");
        }

        function checkAndSettleMatchResults(match) {
            if (match.resultStatus === 'Upcoming') return;

            db.tickets.forEach(tkt => {
                if (tkt.matchId === match.id && tkt.status === 'Active' && tkt.teamPicked) {
                    let user = db.users[tkt.mobile];
                    let recipientMob = match.creator || db.settings.adminNumber;

                    if (match.resultStatus.includes('Won')) {
                        let winnerTeam = match.resultStatus.includes('Team 1') ? match.team1 : match.team2;
                        if (tkt.teamPicked === winnerTeam) {
                            let winAmt = tkt.sattaAmount * 2;
                            if (db.users[recipientMob]) db.users[recipientMob].wallet -= winAmt;
                            if (user) user.wallet += winAmt;
                            tkt.status = 'Settled (Won)';
                        } else {
                            tkt.status = 'Settled (Lost)';
                        }
                    } else if (match.resultStatus === 'Draw / Abandoned') {
                        if (user) user.wallet += tkt.sattaAmount;
                        tkt.status = 'Refunded';
                    }
                }
            });
            saveDB();
        }

        function openMasterAdminPanel() {
            if (currentMobile !== db.settings.adminNumber) return;
            renderAdminAllMatches();
            renderAdminAllTickets();
            renderAdminPlansList();
            document.getElementById('masterAdminModal').classList.remove('hidden');
        }

        function closeMasterAdminModal() { document.getElementById('masterAdminModal').classList.add('hidden'); }

        function switchAdminSubTab(tabName, evt) {
            document.querySelectorAll('.admin-sub-tab').forEach(el => el.classList.add('hidden'));
            if (tabName === 'matches') document.getElementById('adminTabMatches').classList.remove('hidden');
            if (tabName === 'tickets') document.getElementById('adminTabTickets').classList.remove('hidden');
            if (tabName === 'plans') document.getElementById('adminTabPlans').classList.remove('hidden');
            
            if(evt && evt.target) {
                let parent = evt.target.parentElement;
                parent.querySelectorAll('.tab-btn').forEach(el => el.classList.remove('active'));
                evt.target.classList.add('active');
            }
        }

        function renderAdminAllMatches() {
            let container = document.getElementById('adminAllMatchesList');
            let html = '';
            db.matches.forEach(match => {
                html += `
                    <div class="match-card">
                        <p><strong>${match.seriesName}</strong> (${match.team1} vs ${match.team2}) - ₹${match.price}</p>
                        <div style="margin-top:8px; display:flex; gap:8px;">
                            <button class="btn btn-warning" style="padding:5px 10px; font-size:0.8rem;" onclick="openEditMatchModal('${match.id}')">✏️ Edit Price & Winner</button>
                            <button class="btn btn-danger" style="padding:5px 10px; font-size:0.8rem;" onclick="adminDeleteMatch('${match.id}')">Delete</button>
                        </div>
                    </div>
                `;
            });
            container.innerHTML = html || '<p>Koi match nahi hai.</p>';
        }

        function openEditMatchModal(matchId) {
            let match = db.matches.find(m => m.id === matchId);
            if (!match) return;

            document.getElementById('editMatchId').value = match.id;
            document.getElementById('editSeriesName').value = match.seriesName;
            document.getElementById('editTeam1').value = match.team1;
            document.getElementById('editTeam2').value = match.team2;
            document.getElementById('editMatchPrice').value = match.price;
            document.getElementById('editMatchLimit').value = match.limit;
            document.getElementById('editResultStatus').value = match.resultStatus;

            document.getElementById('editSingleMatchModal').classList.remove('hidden');
        }

        function closeEditSingleMatchModal() { document.getElementById('editSingleMatchModal').classList.add('hidden'); }

        function saveEditedMatch() {
            let id = document.getElementById('editMatchId').value;
            let match = db.matches.find(m => m.id === id);
            if (!match) return;

            match.seriesName = document.getElementById('editSeriesName').value.trim();
            match.team1 = document.getElementById('editTeam1').value.trim();
            match.team2 = document.getElementById('editTeam2').value.trim();
            match.price = Number(document.getElementById('editMatchPrice').value);
            match.limit = Number(document.getElementById('editMatchLimit').value);
            match.resultStatus = document.getElementById('editResultStatus').value;

            checkAndSettleMatchResults(match);
            saveDB();
            closeEditSingleMatchModal();
            renderAdminAllMatches();
            renderMatches();
            alert("Match updated successfully!");
        }

        function adminDeleteMatch(matchId) {
            if (confirm("Delete karna chahte hain?")) {
                db.matches = db.matches.filter(m => m.id !== matchId);
                saveDB();
                renderAdminAllMatches();
                renderMatches();
            }
        }

        function renderAdminAllTickets() {
            let container = document.getElementById('adminAllTicketsList');
            let html = '';
            db.tickets.forEach(tkt => {
                html += `
                    <div class="match-card">
                        <p><strong>Ticket ID:</strong> ${tkt.id} | User: ${tkt.mobile} | Status: ${tkt.status}</p>
                    </div>
                `;
            });
            container.innerHTML = html || '<p>Koi ticket nahi hai.</p>';
        }

        function renderAdminPlansList() {
            let container = document.getElementById('adminPlansList');
            let html = '';
            db.settings.plans.plans.forEach ? db.settings.plans.forEach(plan => {
                html += `
                    <div class="match-card" style="padding:10px; margin-bottom:8px;">
                        <p><strong>${plan.name}</strong> - ₹${plan.price} (${plan.durationDays ? plan.durationDays + ' Days' : 'Hours'})</p>
                        <button class="btn btn-danger" style="padding:4px 8px; font-size:0.75rem; margin-top:5px;" onclick="deletePlan('${plan.id}')">Delete Plan</button>
                    </div>
                `;
            }) : '';
            container.innerHTML = html;
        }

        function addNewSubscriptionPlan() {
            let id = document.getElementById('newPlanId').value.trim();
            let name = document.getElementById('newPlanName').value.trim();
            let price = Number(document.getElementById('newPlanPrice').value);
            let days = Number(document.getElementById('newPlanDays').value);

            if (!id || !name || !price) { alert("Saari details bharein!"); return; }

            db.settings.plans.push({ id: id, name: name, price: price, durationDays: days || 30 });
            saveDB();
            renderSubscriptionPlans();
            renderAdminPlansList();
            alert("Naya subscription plan successfully add ho gaya!");
        }

        function deletePlan(planId) {
            db.settings.plans = db.settings.plans.filter(p => p.id !== planId);
            saveDB();
            renderSubscriptionPlans();
            renderAdminPlansList();
            alert("Plan delete ho gaya.");
        }

        function deleteMatch(matchId) {
            if (confirm("Delete karna chahte hain?")) {
                db.matches = db.matches.filter(m => m.id !== matchId);
                saveDB();
                renderMatches();
            }
        }

        function switchTab(tabName, evt) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('.tab-btn').forEach(el => el.classList.remove('active'));

            if (tabName === 'international') document.getElementById('internationalTabContent').classList.remove('hidden');
            else if (tabName === 'apna') document.getElementById('apnaTabContent').classList.remove('hidden');
            else if (tabName === 'activeTickets') {
                document.getElementById('activeTicketsTabContent').classList.remove('hidden');
                renderActiveTickets();
            }
            else if (tabName === 'myPurchased') document.getElementById('myPurchasedTabContent').classList.remove('hidden');
            
            if(evt && evt.target) {
                evt.target.classList.add('active');
            }
        }
    </script>
</body>
</html>
