# 👁️ EventEye: Bulk Certificate Automation System

## 🚀 Project Overview

**EventEye** is a functional frontend prototype for a certificate automation platform designed to solve the critical challenge of quickly, accurately, and trackably distributing thousands of personalized certificates to event participants.

Developed for a hackathon, this project focuses on demonstrating the seamless user experience (UX) and the power of **bulk processing simulation** using pure HTML, CSS, and vanilla JavaScript.

## ✨ Core Features Demonstrated

| Feature | Description | Implementation |
| :--- | :--- | :--- |
| **Live Automation Demo** | Visually demonstrates the system working by cycling through participant names on a mock certificate template in real-time. | JavaScript `setInterval()` dynamically updates a name overlay on the static image in `dashboard.html`. |
| **Bulk Delivery Tracking** | After the simulation, the dashboard instantly updates global metrics (**Total Sent**, **Delivery Rate**, **Bounced**) and logs the final batch status. | **`setTimeout()`** simulates the bulk server-side generation and delivery process for 10 candidates. |
| **Persistent Mock Login** | The first user to sign in *sets* their own email and password. Subsequent sign-ins must match those credentials. | **Browser Local Storage** is used to save and verify tokens. |
| **User Experience** | Modern dark theme, clear data visualization, and an interactive landing page (animated eyes). | Pure HTML/CSS/JavaScript with Font Awesome icons. |

## 🛠️ Setup and Demo Instructions

1.  **Clone the Repository:** Download the project files.
2.  **Run:** Open `index.html` in any modern web browser.
3.  **Login (Registration):** Click **"Sign In"** or **"Explore Now"** to go to `login.html`.
    * **First Time:** Enter *any* valid email and password. This action registers your credentials.
    * **Second Time:** You must use the exact credentials you set the first time.
4.  **Start Automation (Dashboard):**
    * On `dashboard.html`, click the **"Generate New Certificates"** button.
    * Click **"Start Generation & Distribution"**.
5.  **Observe the Output:** The **Live Certificate Automation** panel will appear, cycling through the 10 participant names before instantly updating the dashboard stats with the final, successful delivery status.

---

## 2. `index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>EventEye - Home</title>
  <style>
    /* Global Styles for Navigation Consistency */
    body {
      margin: 0;
      padding: 0;
      background: black;
      color: #fff;
      font-family: Arial, sans-serif;
      height: 100vh;
      overflow: hidden;
    }
    :root {
      --primary-color: #0ee6e2;
    }

    /* ===== Navbar CSS ===== */
    nav {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1rem 3rem;
      background: transparent;
      position: fixed;
      width: 100%;
      top: 0;
      z-index: 10;
      box-sizing: border-box;
    }

    .logo {
      font-size: 1.5rem;
      font-weight: bold;
      color: #fff;
    }

    .nav-links {
      display: flex;
      gap: 2rem;
    }

    .nav-links a {
      text-decoration: none;
      color: #ddd;
      font-weight: 500;
      transition: color 0.3s;
    }

    .nav-links a:hover {
      color: var(--primary-color);
    }

    .signin-btn {
      background: #fff;
      color: #000;
      border: none;
      padding: 0.5rem 1rem;
      border-radius: 6px;
      font-weight: bold;
      cursor: pointer;
      margin-right: 100px;
      /* Link to the login page */
      text-decoration: none; 
      display: inline-block;
    }
    
    /* ===== Landing Page Layout & Eye CSS ===== */
    #landing-content {
      display: flex;
      align-items: center;
      justify-content: space-between;
      height: 100%;
    }

    .eye-container {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 40%;
      height: 100%;
      background: radial-gradient(circle at center, #222, #000);
    }

    .eye {
      width: 120px;
      height: 120px;
      background: #fff;
      border-radius: 30%;
      margin: 0 20px;
      position: relative;
      overflow: hidden;
      display: flex;
      justify-content: center;
      align-items: center;
      box-shadow: inset -10px -10px 20px rgba(0,0,0,0.4);
    }

    .pupil {
      width: 50px;
      height: 50px;
      background: black;
      border-radius: 50%;
      position: absolute;
      transition: transform 0.05s linear;
    }

    .content {
      width: 60%;
      padding: 100px 40px 40px 40px; 
      color: #fff;
    }

    .highlight {
      color: var(--primary-color);
      font-weight: bold;
    }

    h1 {
      font-size: 2.5rem;
      line-height: 1.2;
    }

    .btn {
      margin-top: 20px;
      background: var(--primary-color);
      color: #030303;
      padding: 12px 25px;
      border-radius: 8px;
      border: none;
      cursor: pointer;
      font-size: 1rem;
      text-decoration: none; 
      display: inline-block;
    }

    .btn:hover {
      background: #0ac1d1;
    }
  </style>
</head>
<body>
  <nav>
    <div class="logo">👁️ EventEye</div>
    <div class="nav-links">
      <a href="index.html">Home</a>
      <a href="#">Explore</a>
      <a href="#">Guide</a>
      <a href="#">Contacts</a>
      <a href="#">FAQs</a>
    </div>
    <a href="login.html" class="signin-btn">Sign In</a>
  </nav>

  <div id="landing-content">
    <div class="eye-container">
      <div class="eye">
        <div class="pupil"></div>
      </div>
      <div class="eye">
        <div class="pupil"></div>
      </div>
    </div>

    <div class="content">
      <h1>Create. Personalize. Deliver — All in One Go —  <span class="highlight">Unforgettable</span> Experiences!</h1>
      <p>Bulk certificate generation powered by <span class="highlight">automation</span> — customizable, trackable, and ready to share <span class="highlight">instantly</span></p>
      <a href="login.html" class="btn">Explore Now</a>
    </div>
  </div>

  <script>
    const pupils = document.querySelectorAll('.pupil');
    const eyes = document.querySelectorAll('.eye');

    document.addEventListener('mousemove', (e) => {
      eyes.forEach((eye, index) => {
        const rect = eye.getBoundingClientRect();
        const eyeCenterX = rect.left + rect.width / 2;
        const eyeCenterY = rect.top + rect.height / 2;

        const angle = Math.atan2(e.pageY - eyeCenterY, e.pageX - eyeCenterX);
        const pupil = pupils[index];

        const maxMovement = 30; 
        const x = Math.cos(angle) * maxMovement;
        const y = Math.sin(angle) * maxMovement;

        pupil.style.transform = `translate(${x}px, ${y}px)`;
      });
    });
  </script>
</body>
</html>

3. login.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EventEye - Sign In</title>
    <link rel="stylesheet" href="[https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css](https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css)">
    
    <style>
        :root {
            --primary-color: #0ee6e2;
            --dark-bg: #121212;
            --card-bg: #1e1e1e;
            --secondary-text: #a0a0a0;
            --border-color: #333333;
            --text-color: #e0e0e0;
            --danger-color: #ef4444; 
        }

        body {
            margin: 0;
            padding: 0;
            background-color: var(--dark-bg);
            color: var(--text-color);
            font-family: Arial, sans-serif;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }
        
        /* ===== Navbar CSS (Minimal for Login Page) ===== */
        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 3rem;
            background: transparent;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 100;
            box-sizing: border-box;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: bold;
            color: #fff;
        }

        .nav-links {
            display: none; 
        }

        .signin-btn {
            background: #fff;
            color: #000;
            border: none;
            padding: 0.5rem 1rem;
            border-radius: 6px;
            font-weight: bold;
            cursor: pointer;
            margin-right: 100px;
            text-decoration: none;
            display: inline-block;
        }

        /* ===== LOGIN FORM STYLES ===== */
        .login-box {
            background-color: var(--card-bg);
            padding: 40px;
            border-radius: 10px;
            width: 350px;
            box-shadow: 0 8px 30px rgba(0, 0, 0, 0.5);
            text-align: center;
            margin-top: 60px;
        }

        .login-box h2 {
            color: var(--primary-color);
            margin-bottom: 30px;
            font-size: 1.8rem;
        }

        .input-group {
            margin-bottom: 20px;
            text-align: left;
            position: relative; /* Needed for positioning the eye icon */
        }

        .input-group label {
            display: block;
            margin-bottom: 8px;
            font-size: 0.9rem;
            color: var(--secondary-text);
        }

        .input-group input {
            width: 100%;
            padding: 12px;
            border: 1px solid var(--border-color);
            border-radius: 6px;
            background-color: #2a2a2a;
            color: var(--text-color);
            box-sizing: border-box;
            padding-right: 40px; /* Space for the icon */
        }
        
        /* Show/Hide Icon Styling */
        .toggle-password {
            position: absolute;
            right: 10px;
            top: 40px; 
            color: var(--secondary-text);
            cursor: pointer;
            z-index: 5;
        }
        
        /* Standard Login Button */
        .btn-login {
            width: 100%;
            padding: 12px;
            background-color: var(--primary-color);
            color: var(--dark-bg);
            border: none;
            border-radius: 6px;
            font-weight: bold;
            cursor: pointer;
            font-size: 1.1rem;
            margin-top: 20px;
            transition: background-color 0.3s;
            display: block;
            text-align: center;
        }

        .btn-login:hover {
            background-color: #0ac1d1;
        }
        
        /* Error Message Style */
        #error-message {
            color: var(--danger-color);
            margin-top: 15px;
            font-size: 0.9rem;
            text-align: center;
            display: none; 
        }

        /* Helper Text Style */
        #helper-text {
            color: var(--secondary-text);
            font-size: 0.85rem;
            margin-top: 5px;
            text-align: center;
        }
    </style>
</head>
<body>
    <nav>
        <div class="logo">👁️ EventEye</div>
        <div class="nav-links">
            </div>
        <a href="index.html" class="signin-btn">Back to Home</a>
    </nav>
    
    <div class="login-box">
        <h2><i class="fas fa-lock"></i> Organizer Login</h2>
        
        <form id="login-form">
            <div class="input-group">
                <label for="email"><i class="fas fa-envelope"></i> Email / User ID</label>
                <input type="email" id="email-input" name="email" placeholder="Enter your email" required>
            </div>
            <div class="input-group">
                <label for="password"><i class="fas fa-key"></i> Password</label>
                <input type="password" id="password-input" name="password" placeholder="Enter your password" required>
                
                <span class="toggle-password" id="toggle-password">
                    <i class="fas fa-eye-slash"></i>
                </span>
            </div>
            <button type="submit" class="btn-login">Sign In to Dashboard</button>
        </form>
        
        <div id="error-message"></div>
        <div id="helper-text"></div>
    </div>
    
    <script>
        const loginForm = document.getElementById('login-form');
        const emailInput = document.getElementById('email-input');
        const passwordInput = document.getElementById('password-input');
        const errorMessage = document.getElementById('error-message');
        const helperText = document.getElementById('helper-text');
        const togglePassword = document.getElementById('toggle-password');
        
        // --- Password Toggle Logic ---
        togglePassword.addEventListener('click', function() {
            const type = passwordInput.getAttribute('type') === 'password' ? 'text' : 'password';
            passwordInput.setAttribute('type', type);
            
            const icon = this.querySelector('i');
            icon.classList.toggle('fa-eye');
            icon.classList.toggle('fa-eye-slash');
        });


        // --- Mock Credential Management using Local Storage ---
        const SAVED_EMAIL_KEY = 'eventeye_user_email';
        const SAVED_PASSWORD_KEY = 'eventeye_user_password';

        function updateHelperText() {
            if (!localStorage.getItem(SAVED_EMAIL_KEY)) {
                helperText.textContent = "First sign-in will set your credentials for this browser.";
            } else {
                helperText.textContent = `Login: Use your saved credentials.`;
            }
        }
        updateHelperText();


        loginForm.addEventListener('submit', function(e) {
            e.preventDefault(); 

            const enteredEmail = emailInput.value.trim();
            const enteredPassword = passwordInput.value.trim();

            if (enteredEmail === "" || enteredPassword === "") {
                 errorMessage.textContent = "Please fill in both the email and password fields.";
                 errorMessage.style.display = 'block';
                 return;
            }

            const currentSavedEmail = localStorage.getItem(SAVED_EMAIL_KEY);
            const currentSavedPassword = localStorage.getItem(SAVED_PASSWORD_KEY);
            
            // Scenario 1: No credentials saved (First Time Registration/Login)
            if (!currentSavedEmail) {
                // Save the new credentials to Local Storage
                localStorage.setItem(SAVED_EMAIL_KEY, enteredEmail);
                localStorage.setItem(SAVED_PASSWORD_KEY, enteredPassword);
                
                errorMessage.style.display = 'none';
                helperText.textContent = "Registration successful! Redirecting to Dashboard...";
                
                // Redirect
                setTimeout(() => {
                    window.location.href = 'dashboard.html'; 
                }, 500); 

            } 
            // Scenario 2: Credentials already saved (Subsequent Login)
            else {
                if (enteredEmail === currentSavedEmail && enteredPassword === currentSavedPassword) {
                    // Successful Login
                    errorMessage.style.display = 'none';
                    helperText.textContent = "Login successful! Redirecting to Dashboard...";
                    
                    // Redirect
                    setTimeout(() => {
                        window.location.href = 'dashboard.html'; 
                    }, 500); 
                } else {
                    // Failed Login (Wrong details entered)
                    errorMessage.textContent = "Invalid credentials. Please use the email and password you first registered with.";
                    errorMessage.style.display = 'block';
                    passwordInput.value = ''; 
                }
            }
        });
    </script>
</body>
</html>

4. dashboard.html (Live Automation Demo)

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EventEye - Organizer Dashboard (Live)</title>
    <link rel="stylesheet" href="[https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css](https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css)">
    <style>
        
        :root {
            --dark-bg: #121212;
            --card-bg: #1e1e1e;
            --sidebar-bg: #1a1a1a;
            --primary-color: #0ee6e2; 
            --text-color: #e0e0e0;
            --secondary-text: #a0a0a0;
            --success-color: #10b981;
            --warning-color: #fbbf24;
            --danger-color: #ef4444;
            --border-color: #333333;
        }

        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: var(--dark-bg);
            color: var(--text-color);
            min-height: 100vh;
            display: flex;
        }
        
        /* ===== Navbar & Sidebar Styles (Standard) ===== */
        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 3rem;
            background: var(--dark-bg); 
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 100; 
            box-sizing: border-box;
            border-bottom: 1px solid #2a2a2a;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: bold;
            color: #fff;
        }

        .nav-links {
            display: flex;
            gap: 2rem;
            margin-left: 200px; 
        }

        .nav-links a {
            text-decoration: none;
            color: #ddd;
            font-weight: 500;
            transition: color 0.3s;
        }
        
        .nav-links .active {
            color: var(--primary-color);
            font-weight: bold;
        }

        .signin-btn {
            background: var(--primary-color);
            color: var(--dark-bg);
            border: none;
            padding: 0.5rem 1rem;
            border-radius: 6px;
            font-weight: bold;
            cursor: pointer;
            margin-right: 40px;
            text-decoration: none;
            display: inline-block;
        }
        
        .sidebar {
            width: 250px;
            background-color: var(--sidebar-bg);
            padding: 20px 0;
            display: flex;
            flex-direction: column;
            box-shadow: 2px 0 5px rgba(0, 0, 0, 0.5);
            position: fixed;
            height: 100%;
            z-index: 90;
        }

        .sidebar-logo {
            font-size: 1.8rem;
            font-weight: bold;
            color: var(--primary-color);
            text-align: center;
            margin-bottom: 40px;
            padding: 0 20px;
        }

        .sidebar-nav a {
            display: flex;
            align-items: center;
            padding: 15px 30px;
            text-decoration: none;
            color: var(--secondary-text);
            transition: background-color 0.3s, color 0.3s;
        }

        .sidebar-nav a:hover, .sidebar-nav a.active {
            background-color: #2a2a2a;
            color: var(--text-color);
            border-left: 4px solid var(--primary-color);
            padding-left: 26px; 
        }

        .main-content {
            margin-left: 250px; 
            flex-grow: 1;
            padding: 40px;
            padding-top: 100px; 
            width: calc(100% - 250px);
        }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 40px;
        }

        .header h1 {
            font-size: 2.5rem;
            color: var(--text-color);
        }

        .btn-generate {
            background-color: var(--primary-color);
            color: var(--dark-bg);
            padding: 12px 25px;
            border: none;
            border-radius: 8px;
            font-weight: bold;
            cursor: pointer;
            font-size: 1rem;
            transition: background-color 0.3s;
        }

        .btn-generate:hover {
            background-color: #0ac1d1;
        }

        /* Stats Grid Styles */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 30px;
            margin-bottom: 40px;
        }

        .stat-card {
            background-color: var(--card-bg);
            padding: 25px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
            border-left: 5px solid var(--primary-color); 
        }

        .stat-card h3 {
            margin-top: 0;
            color: var(--secondary-text);
            font-size: 0.9rem;
            font-weight: 500;
        }

        .stat-value {
            font-size: 2.5rem;
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .stat-trend {
            font-size: 0.9rem;
            color: var(--success-color);
        }

        /* Table Styles */
        .status-section {
            background-color: var(--card-bg);
            padding: 25px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
        }

        .status-section h2 {
            margin-top: 0;
            color: var(--text-color);
            font-size: 1.5rem;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 15px;
            margin-bottom: 20px;
        }
        
        .data-table {
            width: 100%;
            border-collapse: collapse;
        }

        .data-table th, .data-table td {
            padding: 15px; 
            text-align: left;
            border-bottom: 1px solid var(--border-color); 
        }

        .data-table th {
            color: var(--secondary-text);
            font-weight: 600;
            text-transform: uppercase;
            font-size: 0.8rem;
        }

        .data-table tr:hover {
            background-color: #252525; 
        }

        /* Badges */
        .badge {
            padding: 5px 10px;
            border-radius: 5px;
            font-weight: bold;
            font-size: 0.85rem;
            display: inline-block;
        }

        .badge-delivered {
            background-color: var(--success-color);
            color: var(--dark-bg);
        }

        .badge-bounced {
            background-color: var(--danger-color);
            color: var(--dark-bg);
        }

        .badge-pending {
            background-color: var(--warning-color);
            color: var(--dark-bg);
        }

        /* ===== UPLOAD MODAL STYLES (Standard) ===== */
        .modal-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            z-index: 200; 
            justify-content: center;
            align-items: center;
        }

        .upload-modal {
            background-color: var(--card-bg);
            padding: 30px;
            border-radius: 12px;
            width: 500px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.5);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 15px;
            margin-bottom: 20px;
        }

        .modal-header h3 {
            margin: 0;
            color: var(--primary-color);
            font-size: 1.5rem;
        }
        
        .close-btn {
            background: none;
            border: none;
            color: var(--secondary-text);
            font-size: 1.5rem;
            cursor: pointer;
            transition: color 0.2s;
        }
        
        .close-btn:hover {
            color: var(--text-color);
        }
        
        .modal-step {
            margin-bottom: 25px;
            padding: 15px;
            border: 1px dashed var(--border-color);
            border-radius: 8px;
        }
        
        .modal-step h4 {
            margin-top: 0;
            color: var(--text-color);
            font-size: 1.1rem;
        }
        
        .modal-step input[type="file"], .modal-step input[type="text"] {
            margin-top: 5px;
            padding: 10px;
            display: block;
            width: 100%;
            background: #252525;
            border: 1px solid #3a3a3a;
            border-radius: 4px;
            box-sizing: border-box;
            color: var(--text-color);
        }

        .btn-start {
            width: 100%;
            padding: 15px;
            background-color: var(--success-color);
            color: var(--dark-bg);
            border: none;
            border-radius: 8px;
            font-weight: bold;
            cursor: pointer;
            font-size: 1.1rem;
            margin-top: 20px;
            transition: background-color 0.3s;
        }
        
        .btn-start:hover {
            background-color: #0d9471;
        }

        /* ===== LIVE AUTOMATION PANEL STYLES (NEW) ===== */
        .processing-message-text {
             color: var(--primary-color); 
             margin-top: 20px;
             font-size: 1.1rem;
             display: flex;
             align-items: center;
             justify-content: center;
        }

        #live-automation-panel {
            display: none; 
            background-color: var(--card-bg);
            padding: 25px;
            border-radius: 10px;
            margin-bottom: 30px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
            border-left: 5px solid var(--primary-color);
        }
        
        #live-automation-panel h2 {
            margin-top: 0;
            color: var(--text-color);
            font-size: 1.5rem;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 15px;
            margin-bottom: 20px;
        }

        .live-status {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .progress-bar {
            height: 10px;
            background-color: #333;
            border-radius: 5px;
            width: 70%;
        }

        #progress-fill {
            height: 100%;
            width: 0%;
            background-color: var(--success-color);
            border-radius: 5px;
            transition: width 0.5s ease-out;
        }
        
        /* Certificate Preview Styles */
        #certificate-preview-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin: 20px auto 0;
            border: 1px solid var(--border-color);
        }

        #certificate-template {
            width: 100%;
            height: auto;
            opacity: 0.7; 
        }

        #participant-name-overlay {
            position: absolute;
            top: 50%; 
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 2.5em; 
            font-weight: bold;
            color: #d4af37; 
            font-style: italic;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.6);
            white-space: nowrap;
            transition: all 0.5s ease-in-out;
            font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        }

    </style>
</head>
<body>
    <nav>
        <div class="logo">👁️ EventEye</div>
        <div class="nav-links">
            <a href="dashboard.html" class="active">Dashboard</a>
            <a href="#">Explore</a>
            <a href="#">Guide</a>
            <a href="#">Contacts</a>
            <a href="#">FAQs</a>
        </div>
        <a href="index.html" class="signin-btn">Organizer</a>
    </nav>

    <div class="sidebar">
        <div class="sidebar-logo">👁️ EventEye</div>
        <div class="sidebar-nav">
            <a href="dashboard.html" class="active"><i class="fas fa-chart-line"></i> Dashboard</a>
            <a href="#"><i class="fas fa-certificate"></i> Certificates</a>
            <a href="#"><i class="fas fa-layer-group"></i> Templates</a>
            <a href="#"><i class="fas fa-cog"></i> Settings</a>
            <a href="index.html"><i class="fas fa-sign-out-alt"></i> Sign Out</a>
        </div>
    </div>

    <div class="main-content">
        
        <div class="header">
            <h1>Organizer Dashboard</h1>
            <button class="btn-generate" id="open-upload-modal">
                <i class="fas fa-upload"></i> Generate New Certificates
            </button>
        </div>
        
        <div id="live-automation-panel" style="display: none;">
            <h2><i class="fas fa-magic fa-pulse"></i> Live Certificate Automation</h2>
            
            <div class="live-status">
                <p>Generating <span id="cert-count-processed">0</span> of <span id="cert-count-total">0</span> Certificates...</p>
                <div class="progress-bar">
                    <div id="progress-fill"></div>
                </div>
                <span id="progress-percentage">0%</span>
            </div>
            
            <div id="certificate-preview-container">
                <img id="certificate-template" src="WhatsApp Image 2025-10-04 at 2.07.37 AM.jpeg" alt="Certificate Template">
                <div id="participant-name-overlay">Loading...</div>
            </div>
        </div>
        <div class="stats-grid" id="stats-grid">
            
            <div class="stat-card" style="border-left-color: var(--success-color);">
                <h3>Total Certificates Sent</h3>
                <div class="stat-value" id="stat-sent">12,504</div>
                <div class="stat-trend"><i class="fas fa-arrow-up"></i> 4.5% last month</div>
            </div>

            <div class="stat-card" style="border-left-color: var(--primary-color);">
                <h3>Successful Delivery Rate</h3>
                <div class="stat-value" id="stat-rate">98.2%</div>
                <div class="stat-trend">Excellent performance</div>
            </div>

            <div class="stat-card" style="border-left-color: var(--danger-color);">
                <h3>Bounced / Errors</h3>
                <div class="stat-value" id="stat-bounced">226</div>
                <div class="stat-trend" style="color: var(--danger-color);"><i class="fas fa-arrow-up"></i> +1.1% (Action needed)</div>
            </div>

            <div class="stat-card" style="border-left-color: var(--warning-color);">
                <h3>Total Participants</h3>
                <div class="stat-value" id="stat-total-participants">15,900</div>
                <div class="stat-trend">Across all events</div>
            </div>
            
        </div>

        <div class="status-section">
            <h2>Recent Automation Batches</h2>
            <table class="data-table">
                <thead>
                    <tr>
                        <th>Batch ID</th>
                        <th>Event Name</th>
                        <th>Total Participants</th>
                        <th>Certificates Processed</th>
                        <th>Delivery Status</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody id="batch-tracking-body">
                    <tr>
                        <td>#B00145</td>
                        <td>Web Dev Masterclass 2025</td>
                        <td>450</td>
                        <td>450</td>
                        <td><span class="badge badge-delivered">Delivered</span></td>
                        <td><a href="#" style="color: var(--primary-color); text-decoration: none;">View Details</a></td>
                    </tr>
                    <tr>
                        <td>#B00144</td>
                        <td>Blockchain Summit</td>
                        <td>1200</td>
                        <td>1200</td>
                        <td><span class="badge badge-bounced">Bounced (22)</span></td>
                        <td><a href="#" style="color: var(--danger-color); text-decoration: none;">Review Bounces</a></td>
                    </tr>
                    <tr>
                        <td>#B00143</td>
                        <td>Product Design Workshop</td>
                        <td>880</td>
                        <td>880</td>
                        <td><span class="badge badge-delivered">Delivered</span></td>
                        <td><a href="#" style="color: var(--primary-color); text-decoration: none;">View Details</a></td>
                    </tr>
                </tbody>
            </table>
        </div>

    </div>
    
    <div class="modal-overlay" id="upload-modal-overlay">
        <div class="upload-modal">
            <div class="modal-header">
                <h3 id="modal-title"><i class="fas fa-plus-circle"></i> New Certificate Batch</h3>
                <button class="close-btn" id="close-modal-btn">&times;</button>
            </div>
            
            <form id="generation-form">
                
                <div class="modal-step">
                    <h4>1. Event Details</h4>
                    <label for="event-name">Event Name</label>
                    <input type="text" id="event-name" value="Hackathon Winners 2025" required>
                </div>
                
                <div class="modal-step">
                    <h4>2. Participants List (.xlsx / .csv)</h4>
                    <label for="excel-file">Upload Excel/CSV File</label>
                    <input type="file" id="excel-file" accept=".csv, .xlsx" required>
                    <small style="color: var(--secondary-text); display: block; margin-top: 5px;">(Simulated list contains 10 participants).</small>
                </div>
                
                <div class="modal-step">
                    <h4>3. Certificate Template (.docx / .pdf)</h4>
                    <label for="template-file">Upload Certificate Template</label>
                    <input type="file" id="template-file" accept=".docx, .pdf" required>
                    <small style="color: var(--secondary-text); display: block; margin-top: 5px;">Automation engine will render data on the live template.</small>
                </div>
                
                <button type="submit" class="btn-start" id="start-generation-btn">
                    <i class="fas fa-rocket"></i> Start Generation & Distribution
                </button>
            </form>
            
            <p id="processing-message" class="processing-message-text" style="display: none;">
                <i class="fas fa-spinner fa-spin" style="margin-right: 10px;"></i> Generating & Sending Certificates...
            </p>
        </div>
    </div>


    <script>
        // *** Placing all script logic inside DOMContentLoaded ensures elements are loaded ***
        document.addEventListener('DOMContentLoaded', () => {
            // --- 1. MOCK DATA SOURCE (Your Participants) ---
            const MOCK_PARTICIPANTS = [
                { name: "Md Sami Alam", email: "MdSamiAlam@gmail.com", status: 'Delivered' },
                { name: "Sifat Ayesha", email: "SifatAyesha@gmail.com", status: 'Delivered' },
                { name: "Aliza Khan", email: "aliza.khan@event.com", status: 'Delivered' },
                { name: "Mayra Maryam", email: "mayra.maryam@event.com", status: 'Delivered' },
                { name: "Alvi Khan", email: "alvi.khan@event.com", status: 'Delivered' },
                { name: "Md Salman Alam", email: "md.salman.alam@event.com", status: 'Delivered' },
                { name: "Aashna Shamsad", email: "aashna.shamsad@event.com", status: 'Delivered' },
                { name: "Sana Shamsad", email: "sana.shamsad@event.com", status: 'Delivered' },
                { name: "Kumujaheed Hussain", email: "kumujaheed.h@event.com", status: 'Bounced' }, // Simulating one bounced
                { name: "Ghulam Ali Khan", email: "ghulam.ali.khan@event.com", status: 'Delivered' },
            ];
            
            // --- 2. Element References ---
            const openModalBtn = document.getElementById('open-upload-modal');
            const closeModalBtn = document.getElementById('close-modal-btn');
            const modalOverlay = document.getElementById('upload-modal-overlay');
            const generationForm = document.getElementById('generation-form');
            const processingMessage = document.getElementById('processing-message');
            const batchTrackingBody = document.getElementById('batch-tracking-body');
            const livePanel = document.getElementById('live-automation-panel');
            const nameOverlay = document.getElementById('participant-name-overlay');
            const progressFill = document.getElementById('progress-fill');
            const progressPercentage = document.getElementById('progress-percentage');
            const certCountProcessed = document.getElementById('cert-count-processed');
            const certCountTotal = document.getElementById('cert-count-total');
            
            // --- 3. Stats Elements ---
            const statSent = document.getElementById('stat-sent');
            const statRate = document.getElementById('stat-rate');
            const statBounced = document.getElementById('stat-bounced');
            const statTotalParticipants = document.getElementById('stat-total-participants');

            // --- Mock Data Counters ---
            let totalSent = 12504;
            let totalParticipants = 15900;
            let totalBounced = 226;
            let nextBatchID = 146;

            // --- 4. Modal Open Listener (Primary Fix) ---
            if (openModalBtn) {
                openModalBtn.addEventListener('click', () => {
                    generationForm.style.display = 'block';
                    processingMessage.style.display = 'none';
                    livePanel.style.display = 'none'; // Ensure live panel is hidden initially
                    document.getElementById('modal-title').innerHTML = '<i class="fas fa-plus-circle"></i> New Certificate Batch';
                    modalOverlay.style.display = 'flex';
                });
            }
            
            // --- 5. Modal Close Listeners ---
            if (closeModalBtn) {
                closeModalBtn.addEventListener('click', () => {
                    modalOverlay.style.display = 'none';
                });
            }

            if (modalOverlay) {
                modalOverlay.addEventListener('click', (e) => {
                    if (e.target.id === 'upload-modal-overlay') {
                        modalOverlay.style.display = 'none';
                    }
                });
            }

            // --- 6. Generation Form Submission (Starts Live Automation) ---
            if (generationForm) {
                generationForm.addEventListener('submit', function(e) {
                    e.preventDefault();
                    
                    // Setup Batch Details
                    const eventName = document.getElementById('event-name').value || "New Automation Batch";
                    const currentParticipants = MOCK_PARTICIPANTS.length;
                    const newBatchID = `#B00${nextBatchID++}`;
                    
                    // --- UI Transition: Start Processing ---
                    modalOverlay.style.display = 'none'; // Close modal
                    livePanel.style.display = 'block'; // Show Live Panel
                    
                    // Reset Live Panel Status
                    certCountTotal.textContent = currentParticipants;
                    certCountProcessed.textContent = 0;
                    progressFill.style.width = '0%';
                    progressPercentage.textContent = '0%';
                    nameOverlay.textContent = 'Initializing...';


                    // Add initial entry to the tracking table (Status: PROCESSING)
                    const newRow = batchTrackingBody.insertRow(0);
                    newRow.id = newBatchID.replace('#', '');
                    newRow.innerHTML = `
                        <td>${newBatchID}</td>
                        <td>${eventName}</td>
                        <td id="total-${newBatchID}">${currentParticipants}</td>
                        <td id="processed-${newBatchID}">0</td>
                        <td><span class="badge badge-pending" id="status-${newBatchID}">Generating & Sending...</span></td>
                        <td><a href="#" style="color: var(--warning-color); text-decoration: none;">Monitor</a></td>
                    `;
                    
                    // --- Start the step-by-step visual generation ---
                    simulateLiveGeneration(newBatchID, currentParticipants, MOCK_PARTICIPANTS, eventName);
                });
            }

            // --- 7. Live Generation Function (Visual Loop) ---
            function simulateLiveGeneration(batchID, total, participants) {
                let i = 0;
                
                const interval = setInterval(() => {
                    if (i < total) {
                        const participant = participants[i];
                        
                        // Core Visual Automation: Change Name on Template
                        nameOverlay.textContent = participant.name;
                        
                        // Update progress bar
                        const percentage = Math.round(((i + 1) / total) * 100);
                        progressFill.style.width = `${percentage}%`;
                        progressPercentage.textContent = `${percentage}%`;
                        certCountProcessed.textContent = i + 1;
                        
                        i++;
                    } else {
                        // Generation complete, start delivery phase
                        clearInterval(interval);
                        nameOverlay.textContent = 'Generation Complete! Distributing...';
                        
                        setTimeout(() => {
                            simulateDeliveryPhase(batchID, total, participants);
                        }, 1000); 
                    }
                }, 400); // 400ms delay per certificate
            }


            // --- 8. Delivery Phase Simulation (Final Update) ---
            function simulateDeliveryPhase(batchID, total, participants) {
                const statusElement = document.getElementById(`status-${batchID}`);
                const processedElement = document.getElementById(`processed-${batchID}`);
                const actionElement = document.getElementById(batchID.replace('#', '')).querySelector('td:last-child a');
                
                // Update Dashboard Status for Sending
                statusElement.textContent = 'Sending Emails...';
                statusElement.className = 'badge badge-warning';

                // Final Delivery Update (after a delay)
                setTimeout(() => {
                    const deliveredCount = participants.filter(p => p.status === 'Delivered').length;
                    const bouncedCount = participants.filter(p => p.status === 'Bounced').length;
                    
                    // Update Global Stats
                    totalParticipants += total;
                    totalSent += deliveredCount;
                    totalBounced += bouncedCount;
                    
                    statTotalParticipants.textContent = totalParticipants.toLocaleString();
                    statSent.textContent = totalSent.toLocaleString(); 
                    statBounced.textContent = totalBounced.toLocaleString();
                    statRate.textContent = ((totalSent / totalParticipants) * 100).toFixed(1) + '%';
                    
                    // Final Tracking Table Update
                    processedElement.textContent = total;
                    
                    if (bouncedCount > 0) {
                        statusElement.textContent = `Bounced (${bouncedCount})`;
                        statusElement.className = 'badge badge-bounced';
                        actionElement.innerHTML = 'Review Bounces';
                        actionElement.style.color = 'var(--danger-color)';
                    } else {
                        statusElement.textContent = 'Delivered';
                        statusElement.className = 'badge badge-delivered';
                        actionElement.innerHTML = 'View Details';
                        actionElement.style.color = 'var(--success-color)';
                    }
                    
                    // Finalize Live Panel
                    nameOverlay.textContent = 'Batch Complete!';
                    livePanel.style.display = 'none'; // Hide the visual panel when done
                    
                }, 3000); // 3 seconds for the "delivery" phase
            }
        });
    </script>
</body>
</html>
