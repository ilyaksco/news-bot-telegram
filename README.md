# 🤖 AI News Bot for Telegram (Advanced Edition)

![Go Version](https://img.shields.io/badge/Go-1.21%2B-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

An advanced, self-managing Telegram bot that automatically fetches news from various sources, summarizes it using AI (Google Gemini), and posts it to your Telegram channel. This bot is fully configurable in real-time directly from a Telegram chat interface.

---

## ✨ Key Features

-   **Database-Driven**: All settings and news sources are stored in a persistent SQLite database, making the bot robust and stateful.
-   **Fully Interactive Management**: Configure every aspect of the bot directly from a Telegram chat using the `/settings` command. No more editing files and restarting!
-   **Dynamic Source Management**: Add, view, and delete news sources (both RSS and Scrape types) in real-time through an interactive menu.
-   **Role-Based Security**: A secure Superadmin/Admin system protects sensitive commands. The Superadmin (defined in `.env`) can grant or revoke admin privileges to other users via Telegram commands.
-   **Live Component Reloading**: Changes to the AI model, prompt, or schedule interval take effect immediately without needing a bot restart.
-   **Intelligent Scraper**: Capable of fetching news from both RSS Feeds and direct web page scraping.
-   **AI Summaries**: Leverages Google Gemini to create concise and informative news summaries.
-   **Duplicate Prevention**: Uses the database to ensure the same news article is never posted twice.
-   **Safe & User-Friendly**: Features input validation with re-prompt loops and requires confirmation for critical actions like deleting a source.

---

## 🚀 Getting Started

To get this bot running, follow these steps.

### 📋 Prerequisites

-   [Go](https://go.dev/dl/) version 1.21 or newer installed.
-   A Telegram account and your **Telegram User ID**. You can get your ID by messaging `@userinfobot`.
-   An API Key for **Google Gemini**. Get one from [Google AI Studio](https://aistudio.google.com/).
-   A **Telegram Bot** Token. Get one from [@BotFather](https://t.me/BotFather).

### 🛠️ Installation & Setup

1.  **Clone this repository:**
    ```sh
    git clone https://github.com/ilyaksco/news-bot-telegram.git
    cd your-repo-name
    ```

2.  **Create your environment file from the example:**
    ```sh
    cp .env.example .env
    ```

3.  **Fill in the Configuration**: Open the `.env` file and fill in the required variables: `TELEGRAM_BOT_TOKEN`, `TELEGRAM_CHAT_ID`, `SUPER_ADMIN_ID`, and `GEMINI_API_KEY`. The other variables can be left as default and changed later from within Telegram.

4.  **Initial News Sources**: The `sources.json` file is used **only on the very first run** to populate the database. You can edit this file to set up your initial list of news sources. After the first run, this file is no longer used.

5.  **Install Go dependencies:**
    ```sh
    go mod tidy
    ```

6.  **Run the Bot!**
    ```sh
    go run main.go
    ```
    On the first run, the bot will migrate settings from `.env` and sources from `sources.json` into its database (`newsbot.db`). On subsequent runs, it will load everything from the database.

---

## 🤖 Bot Management

Once the bot is running, all management is done through Telegram commands. You must be the Superadmin or an Admin to use these.

-   `/settings`
    This is the main entry point for all bot configuration. It will display the current settings and show buttons to edit them or manage news sources.

-   `/setadmin {user_id} {true/false}`
    (Superadmin only) Grants or revokes admin privileges for a given user ID.
    -   Example to grant admin: `/setadmin 12345678 true`
    -   Example to revoke admin: `/setadmin 12345678 false`

-   `/cancel`
    Cancels any ongoing configuration process, such as adding a new source or changing a setting.

-   `/help`
    Displays a list of available commands.

---

## 📄 License

This project is licensed under the MIT License.
