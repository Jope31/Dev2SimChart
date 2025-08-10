# **Composer Data Charting Tool**

A simple, self-contained HTML tool to visualize live and backtest performance for your Composer.trade symphonies. It fetches data directly from the Composer APIs and charts multiple symphonies on a single, interactive graph, making it easy to compare their performance from user-specified start dates.

✨ **Features**

⦁	Multi-Symphony Charting: Plot live and backtest data for multiple symphonies on a single graph.<br>
⦁	Clear Visual Comparison: Each symphony is assigned a unique color pair, with a dark shade for live data and a light shade for backtest data, making comparisons intuitive.<br>
⦁	Download Your Chart: Save the generated performance chart as a PNG file with a single click.<br>
⦁	Detailed Status Log: A comprehensive log provides real-time feedback on API requests, data processing, and potential errors.<br>
⦁	Custom Date Ranges: Specify a unique start date for each symphony to align backtests with your analysis needs.<br>
⦁	**Daily P&L Z-Score Ranking**: Automatically calculates and displays a z-score for each symphony's most recent daily performance, ranking them by statistical deviation from their historical backtest.<br>
⦁	Fully Self-Contained: Runs entirely in your browser from a single HTML file—no installation needed.<br>

🚀 **How It Works**

This tool is a single HTML file that uses JavaScript to call the official Composer API endpoints.<br>

⦁	Frontend: Plain HTML styled with Tailwind CSS.<br>
⦁	Charting: Uses Chart.js to render the interactive line graphs.<br>
⦁	API Communication: Makes direct fetch requests to the Composer API to get live and backtest data.<br>
⦁	CORS Handling: The Composer APIs require API requests to be made from a server, not directly from a browser. This tool bypasses this restriction by sending requests through a local CORS (Cross-Origin Resource Sharing) proxy. You will need to run your own local proxy for the tool to work.

🛠️ **Setup and Installation**

This tool requires two components to run locally: a local web server to serve the `index.html` file and a local CORS proxy to handle API requests.

1.  **Run a Local CORS Proxy:**
    The tool is hardcoded to use a proxy at `http://localhost:8080`. The recommended way to set this up is using the `cors-anywhere` package.
    - **Install Node.js:** If you don't have it, download and install it from [nodejs.org](https://nodejs.org/).
    - **Install `cors-anywhere`:** Open your terminal and run:
      ```bash
      npm install -g cors-anywhere
      ```
    - **Run the proxy:** In the same terminal, run the following command. You must keep this terminal window open while using the tool.
      ```bash
      cors-anywhere
      ```
    This will start the proxy server on port 8080.

2.  **Run a Local Web Server:**
    In a **new** terminal window, navigate to the directory where you saved `index.html`. The easiest way to serve the file is with Python's built-in server.
    - **For Python 3:**
      ```bash
      python -m http.server
      ```
    This will start a web server, usually on port 8000.

3.  **Access the Tool:**
    Open your web browser and navigate to: http://localhost:8000

# Usage Guide

1.  **Enter Your Credentials:**
    Fill in your Composer API Key, Secret Key, and Account ID. This information is sent directly to the Composer API and is not stored by the tool.

2.  **Add Your Symphonies:**
    In the text area, add the symphonies you want to chart. Use the format `Name,SymphonyID,YYYY-MM-DD`, with one symphony per line. The name can be anything you choose and will be used to label the data in the chart.

    For example:
    ```
    My Core Strategy,FTZP9wjzjvnIw21KQtIL,2025-04-15
    Experimental Algo,anotherSymphonyID,2025-06-01
    ```

3.  **Fetch and Chart Data:**
    Click the "Fetch and Chart Data" button. The status log will show the progress of the API calls. Once finished, the chart will appear below.

4.  **Download the Chart:**
    Click the "Download PNG" button to save a copy of the chart to your computer.

# Z-Score Ranking

Below the main performance chart, you will find the **Daily P&L Z-Score Ranking**. This section provides a powerful statistical snapshot of your symphonies' recent performance.

### What is a Z-Score?
A z-score measures how many standard deviations a data point is from the mean of a dataset. In this tool, it answers the question: **"How unusual was the most recent trading day's profit or loss compared to the symphony's own historical backtest?"**

### How is it Calculated?
For each symphony, the tool performs the following steps:
1.  It takes the Profit & Loss (P&L) of the most recent live trading day.
2.  It calculates the historical daily P&L for the entire duration of the backtest.
3.  It finds the mean (average) and standard deviation (a measure of volatility) of these historical P&Ls.
4.  Finally, it calculates the z-score using the formula:
    `z = (Latest Daily P&L - Historical Mean P&L) / Historical Standard Deviation`

### How to Interpret the Ranking
The symphonies are ranked by their **absolute z-score**, from lowest to highest.
- **Low Z-Score (close to 0):** The most recent day's performance was very typical and falls in line with historical norms.
- **High Positive Z-Score (e.g., > 2.0):** The symphony had a significantly better-than-average day. This is a 2-sigma event, suggesting a positive but statistically unusual outcome.
- **High Negative Z-Score (e.g., < -2.0):** The symphony had a significantly worse-than-average day. This is a negative 2-sigma event, indicating a large, unexpected loss compared to its history.

This ranking helps you quickly identify which strategies are behaving as expected and which are experiencing outlier events that may warrant further investigation.

⚠️ Disclaimer
This is an unofficial tool. It is not affiliated with, endorsed by, or supported by Composer.trade. The API keys and other sensitive information you provide are used solely for the purpose of making API calls to the Composer servers from your browser and are not stored or transmitted elsewhere. As this tool requires you to run a local web server and a CORS proxy, be aware of the security implications and only run it in a trusted environment.
