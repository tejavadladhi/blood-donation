<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>LifeLink Pro - Advanced Edition</title>
    <script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
    <style>
      :root {
        --brand: #d9534f;
        --success: #28a745;
        --dark: #2c3e50;
        --bg: #f4f7f6;
        --accent: #f39c12;
      }
      body {
        font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
        background: var(--bg);
        margin: 0;
        padding: 10px;
      }
      .app-container {
        max-width: 500px;
        margin: auto;
        background: white;
        border-radius: 25px;
        box-shadow: 0 15px 35px rgba(0, 0, 0, 0.15);
        min-height: 95vh;
        display: flex;
        flex-direction: column;
        overflow: hidden;
      }
      .header {
        background: var(--dark);
        color: white;
        padding: 20px;
        display: flex;
        justify-content: space-between;
        align-items: center;
      }
      .nav-bar {
        display: flex;
        background: #34495e;
      }
      .nav-item {
        flex: 1;
        padding: 15px;
        color: #a0aec0;
        text-align: center;
        cursor: pointer;
        font-size: 13px;
        font-weight: bold;
      }
      .nav-item.active {
        color: white;
        border-bottom: 4px solid var(--brand);
        background: rgba(255, 255, 255, 0.05);
      }
      .pane {
        padding: 25px;
        overflow-y: auto;
        flex-grow: 1;
        display: none;
      }
      .pane.active {
        display: block;
      }
      input,
      select {
        width: 100%;
        padding: 12px;
        margin-bottom: 15px;
        border: 1px solid #ddd;
        border-radius: 10px;
        box-sizing: border-box;
      }
      .password-wrapper {
        position: relative;
        display: flex;
        align-items: center;
        margin-bottom: 15px;
      }
      .password-wrapper input {
        margin-bottom: 0;
        padding-right: 45px;
      }
      .toggle-password {
        position: absolute;
        right: 12px;
        background: none;
        border: none;
        cursor: pointer;
        font-size: 18px;
        padding: 5px;
        color: #666;
        transition: opacity 0.3s ease;
      }
      .toggle-password:hover {
        opacity: 0.7;
      }
      .forgot-password-link {
        text-align: center;
        margin-top: 10px;
      }
      .forgot-password-link a {
        color: var(--brand);
        text-decoration: none;
        font-size: 12px;
        cursor: pointer;
        font-weight: 500;
      }
      .forgot-password-link a:hover {
        text-decoration: underline;
      }
      .modal {
        display: none;
        position: fixed;
        z-index: 1000;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.4);
      }
      .modal.active {
        display: flex;
        align-items: center;
        justify-content: center;
      }
      .modal-content {
        background-color: #fefefe;
        padding: 30px;
        border-radius: 15px;
        width: 100%;
        max-width: 400px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      }
      .modal-close {
        color: #aaa;
        float: right;
        font-size: 28px;
        font-weight: bold;
        cursor: pointer;
      }
      .modal-close:hover {
        color: #000;
      }
      .modal-title {
        margin-top: 0;
        color: var(--dark);
      }
      .btn {
        width: 100%;
        padding: 14px;
        border: none;
        border-radius: 12px;
        color: white;
        font-weight: bold;
        cursor: pointer;
      }

      /* Reward Badges */
      .badge {
        display: inline-block;
        padding: 4px 10px;
        border-radius: 20px;
        font-size: 10px;
        font-weight: bold;
        text-transform: uppercase;
        margin-top: 5px;
      }
      .bronze {
        background: #cd7f32;
        color: white;
      }
      .silver {
        background: #c0c0c0;
        color: #333;
      }
      .gold {
        background: #ffd700;
        color: #333;
      }
      .platinum {
        background: #e5e4e2;
        color: #333;
        border: 1px solid #999;
      }

      /* Stock Table */
      .stock-table {
        width: 100%;
        border-collapse: collapse;
        font-size: 12px;
        margin: 10px 0;
      }
      .stock-table td {
        padding: 8px;
        border: 1px solid #eee;
      }
      .stock-input {
        width: 50px;
        padding: 4px;
        margin: 0;
        text-align: center;
      }

      .chart-container {
        background: #fff;
        padding: 15px;
        border-radius: 15px;
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
        margin-bottom: 20px;
      }
      .bar-wrapper {
        display: flex;
        align-items: flex-end;
        height: 100px;
        gap: 5px;
        justify-content: space-around;
        padding-top: 20px;
      }
      .bar {
        width: 18px;
        background: var(--brand);
        border-radius: 3px;
        position: relative;
      }
      .bar span {
        position: absolute;
        top: -18px;
        left: 50%;
        transform: translateX(-50%);
        font-size: 9px;
      }

      .card {
        border: 1px solid #eee;
        padding: 15px;
        margin-bottom: 10px;
        border-radius: 15px;
        position: relative;
      }
      .dist-tag {
        position: absolute;
        top: 10px;
        right: 10px;
        font-size: 10px;
        color: #666;
        font-weight: bold;
      }
      .admin-table {
        width: 100%;
        border-collapse: collapse;
        font-size: 11px;
        margin-top: 10px;
      }
      .admin-table th,
      .admin-table td {
        border: 1px solid #f0f0f0;
        padding: 10px;
        text-align: left;
      }

      #logDisplayArea {
        background: #fff;
        padding: 15px;
        border-radius: 15px;
        border: 2px solid #eee;
        display: none;
        margin-top: 10px;
      }
      @media print {
        body * {
          visibility: hidden;
        }
        #logDisplayArea,
        #logDisplayArea * {
          visibility: visible;
        }
        #logDisplayArea {
          position: absolute;
          left: 0;
          top: 0;
          width: 100%;
        }
      }
    </style>
  </head>
  <body>
    <div class="app-container">
      <div class="header">
        <div style="font-weight: 900; letter-spacing: 1.5px">LIFELINK PRO</div>
        <div
          onclick="handleProfileClick()"
          style="cursor: pointer; font-size: 20px"
        >
          👤
        </div>
      </div>

      <div class="nav-bar">
        <div
          class="nav-item active"
          id="btn-hosp-tab"
          onclick="switchPane('hosp-pane')"
        >
          HOSPITAL
        </div>
        <div class="nav-item" id="btn-reg-tab" onclick="switchPane('reg-pane')">
          REGISTRATION
        </div>
      </div>

      <div id="hosp-pane" class="pane active">
        <h3>Find Ready Donors</h3>
        <input
          type="text"
          id="hospSearchName"
          placeholder="Your Registered Hospital Name"
        />
        <select id="searchGroup">
          <option value="A+">A+</option>
          <option value="B+">B+</option>
          <option value="O+">O+</option>
          <option value="AB+">AB+</option>
          <option value="A-">A-</option>
          <option value="B-">B-</option>
          <option value="O-">O-</option>
          <option value="AB-">AB-</option>
        </select>
        <button
          class="btn"
          style="background: var(--brand)"
          onclick="performSearch()"
        >
          Search Database
        </button>
        <div id="searchResults" style="margin-top: 20px"></div>
      </div>

      <div id="reg-pane" class="pane">
        <div
          id="reg-type-selection"
          style="text-align: center; padding-top: 20px"
        >
          <button
            class="btn"
            style="background: var(--brand); margin-bottom: 15px"
            onclick="toggleRegType('donor')"
          >
            🩸 REGISTER AS DONOR
          </button>
          <button
            class="btn"
            style="background: var(--dark)"
            onclick="toggleRegType('hosp')"
          >
            🏥 REGISTER AS HOSPITAL
          </button>
        </div>
        <div id="donor-reg-form" style="display: none">
          <button
            onclick="toggleRegType('back')"
            style="
              border: none;
              background: none;
              color: var(--brand);
              cursor: pointer;
              font-weight: bold;
              margin-bottom: 10px;
            "
          >
            ← Back
          </button>
          <h3>Donor Sign Up</h3>
          <input type="text" id="regName" placeholder="Full Name" />
          <input type="email" id="regEmail" placeholder="Email Address" />
          <div class="password-wrapper">
            <input type="password" id="regPass" placeholder="Password" />
            <button type="button" class="toggle-password" onclick="togglePasswordVisibility('regPass')">👁️</button>
          </div>
          <input type="text" id="regAddress" placeholder="Address" />
          <input type="tel" id="regPhone" placeholder="Phone" />
          <select id="regGender">
            <option value="Male">Male</option>
            <option value="Female">Female</option>
          </select>
          <select id="regGroup">
            <option value="A+">A+</option>
            <option value="B+">B+</option>
            <option value="O+">O+</option>
            <option value="AB+">AB+</option>
            <option value="A-">A-</option>
            <option value="B-">B-</option>
            <option value="O-">O-</option>
            <option value="AB-">AB-</option>
          </select>
          <button
            class="btn"
            style="background: var(--success)"
            onclick="handleRegistration('donor')"
          >
            Register
          </button>
        </div>
        <div id="hosp-reg-form" style="display: none">
          <button
            onclick="toggleRegType('back')"
            style="
              border: none;
              background: none;
              color: var(--brand);
              cursor: pointer;
              font-weight: bold;
              margin-bottom: 10px;
            "
          >
            ← Back
          </button>
          <h3>Hospital Sign Up</h3>
          <input type="text" id="hospRegName" placeholder="Hospital Name" />
          <input type="email" id="hospRegEmail" placeholder="Email Address" />
          <div class="password-wrapper">
            <input type="password" id="hospRegPass" placeholder="Password" />
            <button type="button" class="toggle-password" onclick="togglePasswordVisibility('hospRegPass')">👁️</button>
          </div>
          <input type="text" id="hospRegLoc" placeholder="City" />
          <button
            class="btn"
            style="background: var(--dark)"
            onclick="handleRegistration('hosp')"
          >
            Register Hospital
          </button>
        </div>
      </div>

      <div id="login-pane" class="pane">
        <h3>Sign In</h3>
        <input type="text" id="loginUser" placeholder="Username/Hospital" />
        <div class="password-wrapper">
          <input type="password" id="loginPass" placeholder="Password" />
          <button type="button" class="toggle-password" onclick="togglePasswordVisibility('loginPass')">👁️</button>
        </div>
        <button
          class="btn"
          style="background: var(--dark)"
          onclick="handleLogin()"
        >
          Login
        </button>
        <div class="forgot-password-link">
          <a onclick="openForgotPasswordModal()">Forgot Password?</a>
        </div>
      </div>

      <div id="forgotPasswordModal" class="modal">
        <div class="modal-content">
          <span class="modal-close" onclick="closeForgotPasswordModal()">&times;</span>
          <h2 class="modal-title">Reset Password</h2>
          <input type="email" id="forgotEmail" placeholder="Enter your email address" />
          <button class="btn" style="background: var(--success); padding: 10px;" onclick="sendPasswordReset()">Send Password</button>
          <button class="btn" style="background: #999; padding: 10px; margin-top: 10px;" onclick="closeForgotPasswordModal()">Cancel</button>
        </div>
      </div>

      <div id="profile-pane" class="pane">
        <div id="profileHeader"></div>

        <button
          onclick="toggleEditArea()"
          style="
            background: #eee;
            border: none;
            padding: 8px 12px;
            border-radius: 8px;
            font-size: 11px;
            cursor: pointer;
            margin-top: 10px;
          "
        >
          ✏️ Edit Profile
        </button>
        <div
          id="editArea"
          class="edit-area"
          style="
            display: none;
            background: #f9f9f9;
            padding: 10px;
            border-radius: 10px;
            margin-top: 10px;
          "
        >
          <div class="password-wrapper">
            <input type="password" id="editPass" placeholder="New Password" />
            <button type="button" class="toggle-password" onclick="togglePasswordVisibility('editPass')">👁️</button>
          </div>
          <input type="text" id="editAddress" placeholder="New Location" />
          <button
            class="btn"
            style="background: var(--dark); padding: 8px"
            onclick="saveProfileChanges()"
          >
            Update
          </button>
        </div>

        <div id="user-view">
          <div id="donorOnlyContent">
            <div
              id="donationStatsCard"
              style="
                background: var(--dark);
                color: white;
                padding: 20px;
                border-radius: 15px;
                text-align: center;
                margin-top: 15px;
              "
            >
              <div id="donorBadgeArea"></div>
              <div style="font-size: 11px; opacity: 0.7">TOTAL DONATIONS</div>
              <div
                id="donationCount"
                style="font-size: 32px; font-weight: bold"
              >
                0
              </div>
              <div
                id="cooldownTimer"
                style="font-size: 10px; color: #ff7675"
              ></div>
            </div>
          </div>

          <div id="hospOnlyContent" style="display: none">
            <h4 style="margin: 20px 0 5px">📦 Blood Stock Manager (Units)</h4>
            <div id="stockGrid"></div>
            <button
              class="btn"
              style="background: var(--success); padding: 8px; font-size: 12px"
              onclick="updateHospStock()"
            >
              Save Stock Changes
            </button>
          </div>

          <h4
            style="
              border-left: 4px solid var(--brand);
              padding-left: 10px;
              margin-top: 25px;
            "
          >
            📋 ACTIVITY LOGS
          </h4>
          <div id="logContent"></div>

          <h4
            style="
              border-left: 4px solid var(--brand);
              padding-left: 10px;
              margin-top: 25px;
            "
          >
            🔔 NOTIFICATIONS
          </h4>
          <div id="notificationsContainer"></div>
        </div>

        <div id="admin-view" style="display: none">
          <div class="chart-container">
            <div
              style="font-size: 11px; font-weight: bold; margin-bottom: 10px"
            >
              DONOR DATABASE GRAPH
            </div>
            <div id="barGraph" class="bar-wrapper"></div>
          </div>

          <h4>🏥 HOSPITAL LOGS</h4>
          <div
            id="hospitalButtons"
            style="display: grid; grid-template-columns: 1fr 1fr; gap: 8px"
          ></div>

          <div id="logDisplayArea">
            <div
              style="
                display: flex;
                justify-content: space-between;
                align-items: center;
                margin-bottom: 10px;
              "
            >
              <h4 id="logTitle" style="margin: 0; font-size: 13px">Logs</h4>
              <div>
                <button
                  class="btn"
                  style="
                    width: auto;
                    padding: 5px 10px;
                    font-size: 10px;
                    background: var(--success);
                  "
                  onclick="window.print()"
                >
                  PDF
                </button>
                <button
                  class="btn"
                  style="
                    width: auto;
                    padding: 5px 10px;
                    font-size: 10px;
                    background: var(--brand);
                  "
                  onclick="toggleLogArea(false)"
                >
                  X
                </button>
              </div>
            </div>
            <div id="adminLogTable"></div>
          </div>

          <h4 style="margin-top: 20px">👥 DONOR LIST</h4>
          <div id="adminDonorList"></div>
        </div>

        <button
          class="btn"
          style="background: #eee; color: #333; margin-top: 30px"
          onclick="handleLogout()"
        >
          Logout
        </button>
      </div>
    </div>

    <script>
      const ADMIN_PROFILES = [
        { id: "S.Durgaprasad", pwd: "prasad271" },
        { id: "U.pavankumar", pwd: "pavan310" },
        { id: "Sk.nagulshareef", pwd: "shareef277" },
        { id: "V.teja", pwd: "teja313" },
        { id: "V.trinadh", pwd: "trinadh301" },
        { id: "V.neeraj", pwd: "neeraj316" },
      ];
      const BLOOD_GROUPS = ["A+", "A-", "B+", "B-", "O+", "O-", "AB+", "AB-"];
      const COMPATIBILITY = {
        "A+": ["A+", "A-", "O+", "O-"],
        "B+": ["B+", "B-", "O+", "O-"],
        "AB+": ["A+", "A-", "B+", "B-", "O+", "O-", "AB+", "AB-"],
        "O+": ["O+", "O-"],
        "A-": ["A-", "O-"],
        "B-": ["B-", "O-"],
        "AB-": ["A-", "B-", "O-", "AB-"],
        "O-": ["O-"],
      };

      let storage = JSON.parse(localStorage.getItem("lifelink_global_v15")) || {
        donors: [],
        hospitals: [],
        activeSessionId: null,
      };

      function saveData() {
        localStorage.setItem("lifelink_global_v15", JSON.stringify(storage));
      }

      function switchPane(id) {
        document
          .querySelectorAll(".pane")
          .forEach((p) => p.classList.remove("active"));
        document
          .querySelectorAll(".nav-item")
          .forEach((n) => n.classList.remove("active"));
        document.getElementById(id).classList.add("active");
        if (id === "hosp-pane")
          document.getElementById("btn-hosp-tab").classList.add("active");
        if (id === "reg-pane")
          document.getElementById("btn-reg-tab").classList.add("active");
        if (id === "profile-pane") loadDashboard();
      }

      function toggleRegType(type) {
        document.getElementById("reg-type-selection").style.display =
          type === "back" ? "block" : "none";
        document.getElementById("donor-reg-form").style.display =
          type === "donor" ? "block" : "none";
        document.getElementById("hosp-reg-form").style.display =
          type === "hosp" ? "block" : "none";
      }

      function toggleEditArea() {
        const area = document.getElementById("editArea");
        area.style.display = area.style.display === "block" ? "none" : "block";
      }
      function toggleLogArea(show) {
        document.getElementById("logDisplayArea").style.display = show
          ? "block"
          : "none";
      }

      function performSearch() {
        const hName = document.getElementById("hospSearchName").value;
        const group = document.getElementById("searchGroup").value;
        const hosp = storage.hospitals.find(
          (h) => h.name.toLowerCase() === hName.toLowerCase()
        );
        if (!hosp) {
          alert("Please login as a hospital first.");
          return;
        }

        const results = storage.donors.filter(
          (d) =>
            COMPATIBILITY[group].includes(d.group) &&
            getCooldownInfo(d).eligible
        );
        const container = document.getElementById("searchResults");
        container.innerHTML = results.length
          ? `<p>Found ${results.length} donors for ${group}</p>`
          : "No eligible donors.";

        results.forEach((d) => {
          const dist = (Math.random() * 10 + 1).toFixed(1); // Simulation
          container.innerHTML += `<div class="card">
                <span class="dist-tag">📍 ${dist} km away</span>
                <strong>${d.name} (${d.group})</strong><br><small>${d.address}</small><br>
                <a href="tel:${d.phone}" style="color:green; text-decoration:none; font-weight:bold; font-size:12px;">📞 CALL DONOR</a><br>
                <button class="btn" style="padding:6px; font-size:10px; background:var(--dark); margin-top:8px;" onclick="sendAlert('${d.id}', '${hosp.name}', '${group}')">SEND ALERT</button>
            </div>`;
        });
      }

      function sendAlert(donorId, hospName, group) {
        const donor = storage.donors.find((d) => d.id == donorId);
        donor.notifications.unshift({
          id: Date.now(),
          hosp: hospName,
          msg: `${hospName} urgently needs ${group}.`,
          status: "pending",
        });
        saveData();
        alert("Alert Dispatched!");
      }

      function togglePasswordVisibility(fieldId) {
        const input = document.getElementById(fieldId);
        if (input.type === "password") {
          input.type = "text";
        } else {
          input.type = "password";
        }
      }

      function handleLogin() {
        const u = document.getElementById("loginUser").value,
          p = document.getElementById("loginPass").value;
        const admin = ADMIN_PROFILES.find((a) => a.id === u && a.pwd === p);
        const donor = storage.donors.find((d) => d.name === u && d.pass === p);
        const hosp = storage.hospitals.find(
          (h) => h.name === u && h.pass === p
        );
        if (admin || donor || hosp) {
          storage.activeSessionId = admin
            ? admin.id
            : donor
            ? donor.id
            : hosp.id;
          saveData();
          switchPane("profile-pane");
        } else {
          alert("Invalid credentials.");
        }
      }

      function loadDashboard() {
        const id = storage.activeSessionId;
        const admin = ADMIN_PROFILES.find((a) => a.id === id);
        const donor = storage.donors.find((d) => d.id == id);
        const hosp = storage.hospitals.find((h) => h.id == id);

        if (admin) {
          document.getElementById("user-view").style.display = "none";
          document.getElementById("admin-view").style.display = "block";
          renderAdminView();
        } else if (donor) {
          document.getElementById("user-view").style.display = "block";
          document.getElementById("admin-view").style.display = "none";
          document.getElementById("donorOnlyContent").style.display = "block";
          document.getElementById("hospOnlyContent").style.display = "none";
          renderDonorUI(donor);
        } else if (hosp) {
          document.getElementById("user-view").style.display = "block";
          document.getElementById("admin-view").style.display = "none";
          document.getElementById("donorOnlyContent").style.display = "none";
          document.getElementById("hospOnlyContent").style.display = "block";
          renderHospUI(hosp);
        }
      }

      function renderAdminView() {
        const counts = BLOOD_GROUPS.map(
          (g) => storage.donors.filter((d) => d.group === g).length
        );
        const max = Math.max(...counts) || 1;
        document.getElementById("barGraph").innerHTML = BLOOD_GROUPS.map(
          (g, i) => `
            <div style="text-align:center">
                <div class="bar" style="height:${
                  (counts[i] / max) * 80
                }px"><span>${counts[i]}</span></div>
                <div style="font-size:8px;">${g}</div>
            </div>`
        ).join("");

        document.getElementById("hospitalButtons").innerHTML = storage.hospitals
          .map(
            (h) =>
              `<button style="padding:10px; border-radius:10px; border:1px solid #ddd;" onclick="showAdminLogs('${h.name}')">🏥 ${h.name}</button>`
          )
          .join("");

        let html = `<table class="admin-table"><tr><th>Name</th><th>Group</th><th>History</th></tr>`;
        storage.donors.forEach(
          (d) =>
            (html += `<tr><td>${d.name}</td><td>${d.group}</td><td>${d.history.length} Times</td></tr>`)
        );
        document.getElementById("adminDonorList").innerHTML = html + `</table>`;
      }

      function showAdminLogs(hName) {
        toggleLogArea(true);
        document.getElementById("logTitle").innerText = `Logs: ${hName}`;
        let logs = [];
        storage.donors.forEach((d) =>
          d.history.forEach((h) => {
            if (h.hospital === hName)
              logs.push({ n: d.name, g: d.group, d: h.date });
          })
        );
        let html = `<table class="admin-table"><tr><th>Hospital</th><th>Donor</th><th>Group</th><th>Date</th></tr>`;
        logs.forEach(
          (l) =>
            (html += `<tr><td>${hName}</td><td>${l.n}</td><td>${l.g}</td><td>${l.d}</td></tr>`)
        );
        document.getElementById("adminLogTable").innerHTML = logs.length
          ? html + `</table>`
          : "No records.";
      }

      function renderDonorUI(d) {
        document.getElementById(
          "profileHeader"
        ).innerHTML = `<h3>Welcome, ${d.name}</h3>`;
        document.getElementById("donationCount").innerText = d.history.length;

        // Badges Logic
        let badge =
          d.history.length >= 10
            ? "platinum"
            : d.history.length >= 5
            ? "gold"
            : d.history.length >= 2
            ? "silver"
            : "bronze";
        document.getElementById(
          "donorBadgeArea"
        ).innerHTML = `<span class="badge ${badge}">${badge} Hero</span>`;

        const cool = getCooldownInfo(d);
        document.getElementById("cooldownTimer").innerText = cool.eligible
          ? "Eligible to Donate"
          : `Next: ${cool.daysLeft} days`;

        let logHtml = `<table class="admin-table"><tr><th>Hospital</th><th>Date</th></tr>`;
        d.history.forEach(
          (h) =>
            (logHtml += `<tr><td>${h.hospital}</td><td>${h.date}</td></tr>`)
        );
        document.getElementById("logContent").innerHTML = d.history.length
          ? logHtml + "</table>"
          : "No history.";

        document.getElementById("notificationsContainer").innerHTML =
          d.notifications
            .map(
              (n) => `
            <div style="background:#fff3cd; padding:10px; border-radius:10px; margin-bottom:10px; font-size:12px;">${
              n.msg
            }<br>
            ${
              n.status === "pending"
                ? `<button onclick="confirmReq(${n.id})">Confirm</button>`
                : `<b style='color:green'>Done</b>`
            }</div>`
            )
            .join("") || "No alerts.";
      }

      function renderHospUI(h) {
        document.getElementById(
          "profileHeader"
        ).innerHTML = `<h3>Hospital Dashboard: ${h.name}</h3>`;

        // Blood Stock Manager
        if (!h.stock)
          h.stock = {
            "A+": 0,
            "A-": 0,
            "B+": 0,
            "B-": 0,
            "O+": 0,
            "O-": 0,
            "AB+": 0,
            "AB-": 0,
          };
        let stockHtml = `<table class="stock-table">`;
        BLOOD_GROUPS.forEach((g) => {
          stockHtml += `<tr><td>${g}</td><td><input type="number" class="stock-input" id="stock-${g}" value="${h.stock[g]}"> Bags</td></tr>`;
        });
        document.getElementById("stockGrid").innerHTML = stockHtml + `</table>`;

        let logs = [];
        storage.donors.forEach((d) =>
          d.history.forEach((hist) => {
            if (hist.hospital === h.name)
              logs.push({ n: d.name, g: d.group, d: hist.date });
          })
        );
        let logHtml = `<table class="admin-table"><tr><th>Donor Name</th><th>Group</th><th>Date</th></tr>`;
        logs.forEach(
          (l) =>
            (logHtml += `<tr><td>${l.n}</td><td>${l.g}</td><td>${l.d}</td></tr>`)
        );
        document.getElementById("logContent").innerHTML = logs.length
          ? logHtml + "</table>"
          : "No received donations.";

        document.getElementById("notificationsContainer").innerHTML =
          h.notifications
            .map(
              (n) => `
            <div style="background:#e8f4fd; padding:10px; border-radius:10px; margin-bottom:10px; font-size:12px;">${
              n.msg
            }<br>
            ${
              n.status === "confirmed"
                ? `<button onclick="completeDonation(${n.id})">Mark Donated</button>`
                : `<b>Complete</b>`
            }</div>`
            )
            .join("") || "No confirmations.";
      }

      function updateHospStock() {
        const id = storage.activeSessionId;
        const hosp = storage.hospitals.find((h) => h.id == id);
        BLOOD_GROUPS.forEach((g) => {
          hosp.stock[g] = document.getElementById(`stock-${g}`).value;
        });
        saveData();
        alert("Inventory Updated!");
      }

      function confirmReq(nid) {
        const d = storage.donors.find((d) => d.id == storage.activeSessionId);
        const n = d.notifications.find((n) => n.id == nid);
        n.status = "confirmed";
        const h = storage.hospitals.find((h) => h.name === n.hosp);
        if (h)
          h.notifications.unshift({
            id: Date.now(),
            donorId: d.id,
            msg: `Donor ${d.name} confirmed for today.`,
            status: "confirmed",
          });
        saveData();
        loadDashboard();
      }

      function completeDonation(nid) {
        const h = storage.hospitals.find(
          (h) => h.id == storage.activeSessionId
        );
        const n = h.notifications.find((n) => n.id == nid);
        const d = storage.donors.find((d) => d.id == n.donorId);
        d.history.unshift({
          date: new Date().toLocaleDateString(),
          hospital: h.name,
        });
        n.status = "completed";
        saveData();
        loadDashboard();
      }

      function saveProfileChanges() {
        const id = storage.activeSessionId;
        const d = storage.donors.find((d) => d.id == id),
          h = storage.hospitals.find((h) => h.id == id);
        const p = document.getElementById("editPass").value,
          a = document.getElementById("editAddress").value;
        if (d) {
          if (p) d.pass = p;
          if (a) d.address = a;
        } else if (h) {
          if (p) h.pass = p;
          if (a) h.location = a;
        }
        saveData();
        alert("Saved!");
        toggleEditArea();
        loadDashboard();
      }

      function getCooldownInfo(d) {
        if (!d.history.length) return { eligible: true, daysLeft: 0 };
        const diff = Math.floor(
          Math.abs(new Date() - new Date(d.history[0].date)) / 86400000
        );
        const limit = d.gender === "Female" ? 120 : 90;
        return { eligible: diff >= limit, daysLeft: Math.max(0, limit - diff) };
      }

      function handleRegistration(type) {
        if (type === "donor")
          storage.donors.push({
            id: Date.now(),
            name: document.getElementById("regName").value,
            email: document.getElementById("regEmail").value,
            pass: document.getElementById("regPass").value,
            group: document.getElementById("regGroup").value,
            gender: document.getElementById("regGender").value,
            address: document.getElementById("regAddress").value,
            phone: document.getElementById("regPhone").value,
            history: [],
            notifications: [],
          });
        else
          storage.hospitals.push({
            id: Date.now(),
            name: document.getElementById("hospRegName").value,
            email: document.getElementById("hospRegEmail").value,
            pass: document.getElementById("hospRegPass").value,
            location: document.getElementById("hospRegLoc").value,
            stock: {},
            notifications: [],
          });
        saveData();
        alert("Registered!");
        switchPane("login-pane");
      }

      function openForgotPasswordModal() {
        document.getElementById("forgotPasswordModal").classList.add("active");
        document.getElementById("forgotEmail").value = "";
      }

      function closeForgotPasswordModal() {
        document.getElementById("forgotPasswordModal").classList.remove("active");
      }

      function sendPasswordReset() {
        const email = document.getElementById("forgotEmail").value.trim();
        
        if (!email) {
          alert("Please enter your email address.");
          return;
        }

        const donor = storage.donors.find((d) => d.email === email);
        const hospital = storage.hospitals.find((h) => h.email === email);

        if (!donor && !hospital) {
          alert("No account found with this email address.");
          return;
        }

        const user = donor || hospital;
        const subject = "Password Reset - LifeLink Pro";
        const message = `Hello ${user.name},\n\nYour password for LifeLink Pro is: ${user.pass}\n\nPlease keep it safe and do not share with anyone.\n\nBest regards,\nLifeLink Pro Team`;

        // Using EmailJS - You need to set up EmailJS account first
        // For demo, we'll use a backend simulation
        console.log("Password reset email would be sent to:", email);
        console.log("Message:", message);

        // Simulate email sending
        alert(`Password has been sent to ${email}. Please check your inbox.`);
        closeForgotPasswordModal();
      }

      function handleLogout() {
        storage.activeSessionId = null;
        saveData();
        location.reload();
      }
      function handleProfileClick() {
        storage.activeSessionId
          ? switchPane("profile-pane")
          : switchPane("login-pane");
      }
    </script>
  </body>
</html>
