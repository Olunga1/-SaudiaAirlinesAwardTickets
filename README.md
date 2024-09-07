Here's the formatted version in markdown:

# Saudia Airlines Award Ticket Availability Checker

## Overview

This project provides an automated solution to check the availability of Saudia Airlines award tickets (business and economy class) and sends email notifications when tickets become available. The solution is implemented using two approaches:

1. **Custom-Coded Solution using Python**
2. **Serverless Automation using Pipedream**

## Approach 1: Custom-Coded Solution Using Python

### 1. Prerequisites

To run the custom-coded solution, you need the following:

* Python 3.x installed on your system.
* Libraries: `selenium`, `requests`, `beautifulsoup4`, `smtplib`, `schedule`.
* WebDriver for Selenium (ChromeDriver/GeckoDriver).

### 2. Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/your-username/saudia-award-ticket-checker.git
   cd saudia-award-ticket-checker
   ```

2. **Install the required libraries:**

   ```bash
   pip install selenium requests beautifulsoup4 schedule
   ```

3. **Download the WebDriver:**
   * For Chrome, download ChromeDriver and place it in your project directory.
   * For Firefox, download GeckoDriver and place it in your project directory.

### 3. Usage

1. **Edit the `config.py` file:** Update the `FROM_LOCATION`, `TO_LOCATION`, `DATE`, `CLASS` (O for business, X for economy), and `EMAIL` fields.

2. **Run the script:**

   ```bash
   python check_availability.py
   ```

3. **Automate the process:** The script uses the `schedule` library to run the checking process every X hours. You can modify the interval in the `check_availability.py` file.

### 4. Script Details

* `check_availability.py`: This script logs into the Saudia Airlines website (handles 2FA if needed), navigates to the award ticket search page, enters the required information, scrapes the availability data, and sends an email if tickets are available.
* `config.py`: Contains all configurable parameters like login credentials, email details, flight details, and scheduling interval.

### 5. Limitations

* **Dynamic Pages**: The solution may need regular updates due to changes in the website's structure.
* **2FA Handling**: The current implementation requires manual input for 2FA codes.

### 6. Troubleshooting

* Ensure WebDriver is compatible with your browser version.
* Check network and login credentials if automation fails.

## Approach 2: Serverless Automation Using Pipedream

### 1. Prerequisites

* Pipedream account: Sign up at Pipedream.
* Saudia Airlines account credentials.
* API keys for email service (e.g., SendGrid).

### 2. Workflow Setup

1. **Create a New Workflow:**
   * Go to Pipedream and create a new workflow.

2. **Add Steps:**
   * **Step 1: HTTP Request Step to Login**
      * Use the HTTP request component to perform a POST request to the Saudia Airlines login endpoint.
      * Handle 2FA by triggering a temporary input step that waits for the 2FA code.
   * **Step 2: Check Award Availability**
      * After logging in, navigate to the award ticket search page using another HTTP request step.
      * Parse the HTML response to extract availability and cost data.
   * **Step 3: Email Notification**
      * If the desired award ticket is available, use the built-in Pipedream email component or a service like SendGrid to send a notification to your email.

3. **Set the Schedule Trigger:**
   * Set a trigger to run the workflow at your desired interval (e.g., every 6 hours).

4. **Save and Deploy:**
   * Save the workflow and deploy it to start the automation process.

### 3. Advantages of Pipedream Approach

* **Ease of Use**: No need for local setups or handling browser automation.
* **Scalable and Flexible**: Easily add more steps or integrate with other services.
* **Cost-Effective**: Only pay for what you use.

### 4. Limitations

* **Dependency on Third-Party Services**: Reliant on Pipedream's services and limits.
* **Less Custom Control**: Less control compared to custom scripts.

### 5. Troubleshooting

* Ensure your API keys and login credentials are correct.
* Check Pipedream's rate limits and adjust the frequency of requests accordingly.
