# **Composer Live vs. Backtest Charting Tool**

A simple, self-contained HTML-based tool for visualizing and comparing the performance of Composer.trade symphonies. It charts the live performance data against the historical backtest data on a single graph, allowing for easy analysis of multiple symphonies at once.

✨ **Features**

⦁	Live vs. Backtest Comparison: Directly overlays live performance (blue line) against backtest performance (orange line).
⦁	Multiple Symphonies: Chart as many symphonies as you need on a single graph.
⦁	Dynamic Date Ranges: Specify a unique start date for each symphony.
⦁	No Installation Needed: Runs entirely in your web browser from a single index.html file.
⦁	Interactive Charts: Hover over data points to see specific return percentages.

🚀 **How It Works**

This tool is a single HTML file that uses JavaScript to call the official Composer API endpoints.
⦁	Frontend: Plain HTML styled with Tailwind CSS.
⦁	Charting: Uses Chart.js to render the interactive line graphs.
⦁	API Communication: Makes direct fetch requests to the Composer API to get live and backtest data.
⦁	CORS Handling: Uses a public CORS proxy (cors-anywhere.herokuapp.com) to bypass browser security restrictions during local development. This is necessary because the Composer backtest API does not currently allow requests directly from a browser.

🛠️ **Setup and Installation**

Because this tool makes API calls from your browser, you cannot simply open the index.html file from your file system. You must serve it from a local web server.

1.	Download the File:  
Save the code for the tool as index.html.

2.	Run a Local Web Server:  
The easiest way to do this is with Python. Open your terminal or command prompt, navigate to the folder where you saved index.html, and run the following command:  
⦁	For Python 3  
python -m http.server
This will start a web server, usually on port 8000.

3.	Access the Tool:  
Open your web browser and navigate to: http://localhost:8000

# Usage Guide

1.	Activate the CORS Proxy:  
This is a critical first step. Before fetching data, open a new browser tab and go to https://cors-anywhere.herokuapp.com/. Click the button that says "Request temporary access to the demo server". You may need to do this periodically if the tool stops working.

2.	Enter Your Credentials:  
Fill in your Composer API Key, Secret Key, and Account ID. This information is only used for the API requests and is not stored anywhere.

3.	Add Your Symphonies:  
In the text area, add the symphonies you want to chart. Use the format SymphonyID,YYYY-MM-DD, with one symphony per line. For example:  
FTZP9wjzjvnIw21KQtIL,2025-04-15  
anotherSymphonyID,2025-06-01

4.	Fetch and Chart Data:  
Click the "Fetch and Chart Data" button. The status log will show the progress, and the chart will appear below once the data has been fetched and processed.

⚠️ Disclaimer
This tool relies on a free, public CORS proxy for demonstration purposes. This proxy may be slow or require frequent reactivation. For a more stable and permanent solution, you should consider running your own CORS proxy locally.
