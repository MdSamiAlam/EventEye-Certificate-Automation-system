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


