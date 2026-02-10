# 🏏 Cricbuzz LiveStats: Real-Time Cricket Insights & SQL-Based Analytics

## Overview
Cricbuzz LiveStats is a **Streamlit-based cricket analytics dashboard** that combines:

- **Live Match Data** from the Cricbuzz API (RapidAPI)
- **Structured Cricket Data** in a MySQL database
- Interactive **SQL-driven analytics**
- Full **CRUD operations** for player data management

This project aims to provide a comprehensive tool for cricket enthusiasts and data analysts, offering both real-time updates and in-depth historical data analysis capabilities.

## Features

1.  **🏠 Home Page**: Provides an overview of the project, its features, and the technology stack used.
2.  **📺 Live / Recent Matches**:
    *   Fetches and displays live or recently concluded matches from the Cricbuzz API.
    *   Shows real-time scores, match status, venue details, and series information.
    *   Allows viewing detailed scorecards (batting and bowling figures for each innings) for individual matches.
    *   **Prioritizes API data.** If API call fails, a small set of static demo data is displayed with a warning.
3.  **📊 Top Player Statistics**:
    *   Displays top player statistics (e.g., Most Runs, Most Wickets, Best Average, etc.) across different match formats (Test, ODI, T20I).
    *   **Prioritizes API data.** If the API fails, it gracefully falls back to displaying statistics from the local MySQL database.
4.  **🔍 SQL Queries & Analytics**:
    *   A collection of 25+ predefined SQL queries ranging from Beginner to Advanced levels.
    *   Users can run these queries with a single click to extract insights from the local database.
    *   Includes a "Custom SQL Runner" for users to write and execute their own SQL queries against the database (SELECT queries recommended for safety).
5.  **🛠 CRUD Operations**:
    *   Provides a user-friendly interface for **C**reate, **R**ead, **U**pdate, and **D**elete operations on player records and their career statistics in the MySQL database.
    *   Ensures data integrity with appropriate validation and warning messages.

## Technical Stack

-   **Python**: The core programming language for the application logic.
-   **Streamlit**: Used for building the interactive and responsive web user interface.
-   **MySQL Database**: A relational database management system for storing structured cricket data (players, teams, matches, stats, etc.).
-   **REST API (RapidAPI)**: Integration with the Cricbuzz Cricket API to fetch real-time and statistical data.
-   **Pandas**: Utilized for efficient data manipulation and tabular display within Streamlit.
-   `mysql-connector-python`: Python client for MySQL database interaction.
-   `requests`: For making HTTP requests to the RapidAPI endpoint.

## Setup Instructions

**Please follow these steps carefully to set up and run the project:**

### **1. Clone or Download the Project**

Download or clone the entire `cricbuzz_livestats` project folder to your local machine.

### **2. Set Up Python Environment & Dependencies**

1.  **Install Python**: Ensure Python 3.8 or higher is installed on your system.
2.  **Create Virtual Environment (Recommended)**:
    Open your terminal or command prompt, navigate to the `cricbuzz_livestats` project directory, and run:
    ```bash
    python -m venv venv
    # For Linux/macOS:
    source venv/bin/activate
    # For Windows (Command Prompt):
    venv\Scripts\activate
    # For Windows (PowerShell):
    # venv\Scripts\Activate.ps1
    ```
3.  **Install Required Libraries**:
    With your virtual environment activated, install the necessary Python packages:
    ```bash
    pip install -r requirements.txt
    ```

### **3. MySQL Database Configuration & Initialization**

1.  **Start MySQL Server**: Ensure your MySQL database server is running.
2.  **Update Database Credentials**:
    Open `cricbuzz_livestats/utils/db_connection.py`.
    Locate the `DB_CONFIG` dictionary and **replace `"your_mysql_password_here"` with your actual MySQL `root` user password.** This step is crucial for the application to connect to your database.
    ```python
    DB_CONFIG = {
        "host": "localhost",
        "user": "root",
        "password": "YOUR_MYSQL_PASSWORD", # <--- UPDATE THIS LINE
        "database": "cricbuzz_db"
    }
    ```
3.  **Create Database Tables and Insert Sample Data**:
    From your terminal (still in the `cricbuzz_livestats` directory with the virtual environment active), run the following script:
    ```bash
    python utils/db_connection.py
    ```
    This script will:
    *   Create a database named `cricbuzz_db` if it doesn't exist.
    *   Create all necessary tables (players, teams, matches, stats, etc.).
    *   Insert a comprehensive set of sample data into these tables.
    You should see "Database and tables created successfully!" and "Sample data inserted successfully!" messages in your terminal. **Resolve any errors reported during this step before proceeding.**

### **4. API Key Configuration**

*   Your RapidAPI Key has been directly embedded into `pages/live_matches.py` and `pages/top_stats.py` as requested.
*   **SECURITY ALERT**: It is highly recommended to **regenerate your API key on the RapidAPI dashboard** for security purposes, especially if you share your code or deploy it publicly. For production, consider using environment variables or a `secrets.toml` file.

### **5. Run the Streamlit Application**

1.  After completing all the above steps successfully, ensure your virtual environment is active.
2.  Run the Streamlit application from your `cricbuzz_livestats` directory:
    ```bash
    streamlit run app.py
    ```
3.  A new tab in your web browser should automatically open, displaying the Streamlit application (typically at `http://localhost:8501`).

---

## **Troubleshooting**

*   **"Blank Page" / Page Not Loading**:
    *   **Check your terminal**: The Streamlit server terminal often shows detailed error messages (Python tracebacks) in red. This is your primary source for debugging.
    *   **Confirm file structure**: Ensure all `.py` files are in the correct `pages/` and `utils/` directories, and that `__init__.py` files exist.
    *   **Database Connection**: Verify your MySQL server is running and `utils/db_connection.py` has the correct password. An `st.error` will appear in the app if DB connection fails.
*   **API Errors (e.g., 400, 403, 429)**:
    *   **API Key**: Double-check your `RAPIDAPI_KEY` in `pages/live_matches.py` and `pages/top_stats.py` for typos.
    *   **RapidAPI Dashboard**: Log in to RapidAPI, go to your Cricbuzz Cricket API subscription.
        *   Check your **quota/usage** to ensure you haven't exceeded your daily/monthly limits.
        *   Verify the API key shown on RapidAPI matches the one in your code.
        *   Test the endpoints (`/matches/v1/recent`, `/stats/v1/player/stats`, `/mcenter/v1/{matchId}/hscard`) directly in the RapidAPI playground to see if they return data.
*   **"No data found in database"**:
    *   **Run `python utils/db_connection.py` again**: This ensures the database is created and populated.
    *   **Check MySQL**: Use a MySQL client (like MySQL Workbench or command-line client) to verify if `cricbuzz_db` exists and if tables like `players`, `career_stats` contain data.

---

