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


