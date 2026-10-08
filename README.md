# 🎵 Concert Price & Availability Tracker

An end-to-end data engineering and analytics project that collects concert event and ticket pricing data, tracks price changes over time, detects unusual price movements, and helps fans explore potential ticket-buying opportunities.

## 🚀 Features

* **Automated Data Ingestion:** Fetches concert event details, ticket price ranges, venues, and availability status from the Ticketmaster Discovery API.
* **Data Pipeline Orchestration:** Uses Dagster to orchestrate ingestion workflows and track pipeline execution.
* **Historical Price Tracking:** Stores daily event snapshots in DuckDB to support longitudinal price analysis.
* **Analytics with dbt:** Transforms raw data into analytical models for price trends, sell-out velocity, price anomalies, and potential buying windows.
* **Interactive Dashboard:** Uses Streamlit and Plotly to explore events, compare pricing trends, and visualize insights.
* **Price Anomaly Detection:** Applies z-score analysis to flag unusual price drops and spikes.
* **Email Alerts:** Supports configurable price alerts and email notifications through SendGrid.
* **Workflow Automation:** Uses GitHub Actions to run scheduled ingestion, transformations, and alert checks.

## 🏗️ Architecture

```text
Ticketmaster Discovery API
           |
           v
Python Ingestion Client
           |
           v
Dagster Orchestration
           |
           v
DuckDB — Daily Event Snapshots
           |
           v
dbt Transformations
           |
           v
Analytical Models
           |
           +-------------------+
           |                   |
           v                   v
   Streamlit Dashboard   Price Alert Engine
                               |
                               v
                       SendGrid Email Alerts
```

## 🛠️ Tech Stack

| Component      | Technologies                          |
| -------------- | ------------------------------------- |
| Programming    | Python, SQL                           |
| Data Source    | Ticketmaster Discovery API            |
| Orchestration  | Dagster                               |
| Storage        | DuckDB                                |
| Transformation | dbt Core                              |
| Visualization  | Streamlit, Plotly                     |
| Data Analysis  | Pandas, statistical anomaly detection |
| Notifications  | SendGrid                              |
| Automation     | GitHub Actions                        |
| Testing        | Pytest                                |

## 📊 Analytics and Insights

The project produces several analytical views:

* **Price Curves:** Examine how listed ticket prices change as event dates approach.
* **Price Anomalies:** Flag unusually large price movements using a rolling mean and standard deviation.
* **Sell-Out Velocity:** Analyze event availability and sell-out patterns across genres, venues, and days of the week.
* **Potential Buying Windows:** Identify dates or periods that may offer more favorable listed prices based on observed trends.
* **Event Exploration:** Search and filter events to compare venues, artists, dates, and prices.

The analysis becomes more informative as historical daily snapshots accumulate. Buying-window insights are estimates based on observed data, not guaranteed predictions of future prices.

## ⚙️ Getting Started

### Prerequisites

* Python 3.11 or later
* A Ticketmaster Discovery API key
* Git

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/concert-price-tracker.git
cd concert-price-tracker
```

Replace `YOUR_USERNAME` with your GitHub username.

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it:

**macOS/Linux**

```bash
source .venv/bin/activate
```

**Windows**

```powershell
.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
pip install -r requirements-dev.txt
```

### 4. Configure environment variables

Copy the example environment file:

**macOS/Linux**

```bash
cp .env.example .env
```

**Windows PowerShell**

```powershell
Copy-Item .env.example .env
```

Add your API key to `.env`:

```env
TICKETMASTER_API_KEY=your_ticketmaster_api_key
DUCKDB_PATH=data/concert_tracker.duckdb

# Optional: Email notifications
SENDGRID_API_KEY=your_sendgrid_api_key
ALERT_EMAIL=your_email@example.com
ALERT_FROM_EMAIL=alerts@yourdomain.com
```

Keep `.env` and your API credentials private. Never commit real secrets to GitHub.

### 5. Run data ingestion

```bash
python scripts/run_ingestion.py
```

The pipeline retrieves event data for the configured city and stores daily snapshots in DuckDB.

### 6. Run dbt transformations

```bash
cd transform
dbt run --profiles-dir .
cd ..
```

### 7. Launch the dashboard

```bash
streamlit run dashboard/app.py
```

Open the local URL shown in your terminal by Streamlit.

### 8. Run tests

```bash
pytest
```

## 🔔 Price Alerts

The project includes a command-line interface for managing price alerts.

Add an artist price alert:

```bash
python -m alerts.manage add --artist "Radiohead" --price 80
```

List active alerts:

```bash
python -m alerts.manage list
```

Remove an alert:

```bash
python -m alerts.manage remove --index 0
```

Run an alert check without sending notifications:

```bash
python -m alerts.check_alerts --dry-run
```

Configure SendGrid credentials to enable email delivery.

## 🔄 Automated Pipeline

The GitHub Actions workflow supports scheduled and manually triggered execution. It runs the ingestion script, executes dbt transformations, checks price alerts, and commits updated database snapshots.

To enable the workflow in your own repository, configure the following GitHub Actions secrets:

* `TICKETMASTER_API_KEY`
* `SENDGRID_API_KEY` (optional)
* `ALERT_EMAIL` (optional)

Review the workflow permissions and database commit strategy before enabling automated writes to your repository.


```

## 🔮 Future Improvements

* Expand ingestion to additional cities and event categories.
* Add more robust price forecasting and backtesting.
* Track historical prediction accuracy and alert precision.
* Introduce additional data-quality checks and pipeline observability.
* Improve dashboard filtering and personalized event alerts.

## ⚠️ Disclaimer

This project is intended for educational and analytical purposes. Ticket prices and availability can change frequently, and observed trends do not guarantee future price movements. Data collection is subject to Ticketmaster API terms, rate limits, and availability.

## 👤 Author

**Lokesh Ram**

