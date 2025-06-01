# ☁️ AI Weather Reporter 📧

A concise automation workflow built with n8n, Lovable Forms, WeatherAPI, and Supabase to provide users with personalized weather reports. This project showcases end-to-end data processing from form submission to email delivery.

## ✨ Features

* **Dynamic Data Capture:** Captures user details (Name, Email, City) via a custom Lovable Form.
* **Basic Data Processing:** Uses custom JavaScript for email validation and data formatting.
* **Real-time Weather Data:** Fetches current weather conditions and Air Quality Index (AQI) from WeatherAPI.com.
* **Data Persistence:** Stores all user submissions and corresponding weather data in a Supabase database.
* **Personalized Email Reports:** Sends automated, customized emails to users with their requested weather information.

## 🚀 Technologies Used

* **n8n:** Workflow automation platform
* **Lovable Forms:** Front-end form creation ([https://lovable-form-json-craft.lovable.app/](https://lovable-form-json-craft.lovable.app/))
* **WeatherAPI.com:** Weather data API
* **Supabase:** Backend-as-a-Service (Database & API)
* **SMTP:** For sending emails
* **JavaScript:** For custom logic within n8n's Code node.

## ⚙️ How It Works

1.  A user fills out and submits the [Lovable Form](https://lovable-form-json-craft.lovable.app/) (fields: `full_name`, `email`, `city`).
2.  The form submission triggers an **n8n Webhook**.
3.  An **n8n Code node** processes the incoming data, including a basic email validation check, and formats the data for downstream nodes.
4.  An **n8n HTTP Request node** calls the WeatherAPI.com to get current weather data for the specified city.
5.  The combined user and weather data is then stored in a **Supabase table** (`Weather`) via the n8n Supabase node.
6.  Finally, an **n8n Email node** sends a personalized weather report to the user's email address using SMTP.

## 🛠️ Setup and Installation

### Prerequisites

* An active **n8n** instance (self-hosted or cloud).
* A **Lovable Forms** account.
* A **WeatherAPI.com** API key.
* A **Supabase** project and database.
* **SMTP** server details or a Gmail/other email service connected to n8n for sending emails.

### Steps

1.  **Clone this Repository:**
    ```bash
    git clone [https://github.com/Muneeb20019/n8n-2.git](https://github.com/Muneeb20019/n8n-2.git)
    cd n8n-2
    ```
2.  **Import n8n Workflow:**
    * Open your n8n instance.
    * Go to 'Workflows' and click 'New'.
    * Click the 'Import from JSON' button.
    * Upload the `ai_weather_reporter_workflow.json` file from this repository.
    * **Important:** After importing, navigate to the **HTTP Request node**. In its `URL` parameter, **replace `YOUR_WEATHERAPI_KEY_HERE` with your actual WeatherAPI.com API key.** Also, configure your Supabase and SMTP credentials within n8n.
3.  **Configure Lovable Form:**
    * Go to your Lovable Form ([https://lovable-form-json-craft.lovable.app/](https://lovable-form-json-craft.lovable.app/)).
    * In the form settings, configure a webhook to point to the **"Production URL" of your n8n Webhook node**. (You can find this URL in the Webhook node's settings in n8n, under 'Webhook URLs' and selecting 'Production URL').
4.  **Setup Supabase Database:**
    * In your Supabase project, create a table named `Weather`.
    * Define the following columns with precise data types:
        * `fullName`: `text`
        * `email`: `text`
        * `city`: `text`
        * `email valid`: `boolean`
        * `temperature`: `numeric`
        * `condition`: `text`
        * `aqi`: `numeric`
        * `Timestamp`: `timestamptz`
5.  **Activate n8n Workflow:**
    * In your n8n instance, activate the workflow by toggling the "Active" switch in the top right corner. Once active, it will be ready to process data sent to its Production Webhook URL.

## 🖼️ Screenshots / Demos

*(Here, you would embed screenshots or GIFs)*
* Screenshot of the Lovable Form.
* Screenshot of the complete n8n workflow.
* Screenshot of data in your Supabase `Weather` table.
* Screenshot of an example received email.

## ✍️ Author

* **Muneeb Ali Khan** - (https://github.com/Muneeb20019)- [Your LinkedIn Profile Link]

## 📜 License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.
