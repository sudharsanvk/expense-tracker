💰 Collaborative Trip Expense Tracker (HTML/Google Sheets)

This project provides a fully responsive, single-page web application to track and visualize group expenses for a trip (e.g., Mysore & Coorg Adventure). It uses the flexibility of Google Sheets as a data store and Google Apps Script as a serverless API endpoint, allowing for real-time logging and charting without needing a dedicated database server.

The frontend is built purely with HTML, CSS, and vanilla JavaScript, leveraging Chart.js for effective data visualization.

🚀 Setup Guide (Mandatory Steps)

This application requires two distinct components to be set up: the Google Sheet (Database) and the Google Apps Script (API/Backend).

Step 1: Prepare the Google Sheet (Data Layer)

Create Sheet: Create a new Google Sheet file (e.g., "Mysore Trip Data").

Name the Tab: Ensure the main sheet tab is named Expenses.

Set Headers: The first row (Row 1) must contain these exact headers:

A1

B1

C1

D1

E1

F1

Date

Description

Category

Amount

Payer

Participants

Step 2: Deploy the Google Apps Script (API Layer)

The provided Apps Script code acts as a bridge, allowing your HTML page to read and write data to the Google Sheet.

Open Script Editor: In your Google Sheet, go to Extensions > Apps Script.

Paste Code: Paste the Code.gs script (which contains the doGet and doPost functions) into the Code.gs file, replacing any existing content.

Review Participants: Check the PARTICIPANTS array in the Code.gs file and ensure it lists the names of all your friends (e.g., ["Anil", "Binu", "Chetan", "Dinesh"]).

Deploy as Web App:

Click the Deploy button (top right) and select New Deployment.

Select the type as Web App.

Execute as: Me.

Who has access: Anyone.

Click Deploy.

Copy the URL: Copy the resulting Web App URL. This URL is your new backend API endpoint.

Step 3: Configure the HTML Frontend

Locate the HTML File: Open the generated tracker.html file in a text editor.

Update Configuration: Find the JavaScript configuration section near the top of the <script> tag:

// !!! REPLACE THIS WITH YOUR DEPLOYED GOOGLE APPS SCRIPT URL !!!
const WEB_APP_URL = 'YOUR_GOOGLE_APPS_SCRIPT_WEB_APP_URL_HERE';


Paste the URL: Replace the placeholder string with the Web App URL you copied in Step 2.

Launch: Save the tracker.html file and open it in any web browser.

🛠️ Key Features

Responsive Design: Optimized for mobile phones for easy expense logging on the go.

Settlement Simplification: The script calculates net balances and provides a minimized list of transactions (e.g., A pays C directly, instead of A paying B and B paying C).

Real-time Charts: Uses Chart.js to render two critical visualizations immediately upon loading data:

Total Spend by Category (Pie Chart)

Total Paid by Each Person (Bar Chart)

Asynchronous Logging: Expenses are logged to the Google Sheet via the Apps Script API without refreshing the page.

💡 How the Split Logic Works

The application uses a standard double-entry accounting principle to track debts:

When an expense is logged (e.g., Anil pays ₹1,000 for 4 participants), the total amount is calculated.

Payer (Anil): Anil's balance is credited by the total amount (+₹1,000).

Participants (All 4): Each participant owes an equal share (₹250). Each of the 4 participants (including Anil) is debited their share (-₹250).

Anil's Net Balance: +₹1,000 (paid) - ₹250 (his share) = +₹750 (Anil is owed ₹750).

The final Settlement Plan takes these net balances and simplifies them to the fewest required transfers between creditors (those owed money) and debtors (those who owe money).
