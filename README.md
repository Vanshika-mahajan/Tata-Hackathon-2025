# Tata-Hackathon-2025
# Agnipath EV Nav: Intelligent Journey Planner & Green Impact Assistant

## 💡 Innovating the Future of Smart Mobility

**Agnipath EV Nav** is an intelligent, AI-powered journey planner designed to enhance the Electric Vehicle (EV) driving experience in India by providing smart routing, identifying charging infrastructure, and quantifying the positive environmental impact of choosing electric. Built for the Tata Hackathon 2025, it aims to reduce range anxiety and promote sustainable transportation by making EV trips seamless and eco-conscious.

---

## ✨ Features

* **Natural Language Understanding (NLU):** Interact with the system using everyday language (e.g., "Plan a trip from X to Y for my EV"). Powered by a local Large Language Model.
* **Smart Routing:** Calculates the shortest path between any two locations in Delhi (using OpenStreetMap data).
* **Integrated Charging Stops:** Identifies potential EV charging stations located along the planned route.
* **Green Impact Calculation:** Quantifies the CO2 emissions saved, equivalent liters of petrol/diesel saved, and trees planted compared to a traditional Internal Combustion Engine (ICE) vehicle for the same journey.
* **Natural Language Generation (NLG):** Presents trip plans and environmental benefits in a clear, friendly, and conversational summary.
* **Extensible Data Foundation:** Built on open-source geographic data and publicly available EV charging station information.

---

## 🏗️ How It Works (High-Level Architecture)

1.  **User Query (Natural Language):** The user inputs a trip request (e.g., "Plan a trip from Connaught Place to Noida Sec 62 for my Tata Punch EV.").
2.  **LLM - Natural Language Understanding (NLU):** A local **Llama 3.2** model (via Ollama) processes the query, extracting structured parameters like `origin`, `destination`, and `ev_model`.
3.  **Geocoding:** Place names are converted into precise Latitude and Longitude coordinates using `geopy`.
4.  **Road Network Alignment:** These coordinates are mapped to the nearest nodes (intersections) on a pre-downloaded, detailed road network graph of Delhi (from OpenStreetMap via OSMnx).
5.  **Routing Algorithm:** NetworkX's shortest path algorithm calculates the most efficient route.
6.  **Charging Stop Identification:** Pre-aligned EV charging station data is filtered to find stations along the calculated route.
7.  **Green Impact Calculation:** Custom Python logic quantifies the environmental benefits of the EV trip based on distance and standard emission factors.
8.  **Natural Language Generation (NLG):** A human-readable summary, including trip details and environmental impact, is dynamically generated and presented to the user.

---

## 💻 Technologies Used

* **Python:** Core programming language.
* **Ollama:** To run Large Language Models (LLMs) locally.
* **Llama 3.2:** The specific LLM model used for NLU.
* **Pandas:** For data loading, manipulation, and cleaning.
* **OSMnx:** For downloading and working with OpenStreetMap (OSM) road network data.
* **NetworkX:** For graph theory algorithms, specifically shortest path calculation.
* **Geopy:** For geocoding (converting place names to coordinates).
* **Matplotlib:** For basic visualization of routes (within Jupyter).
* **Git & GitHub:** For version control and collaboration.
* **Anaconda/Conda:** For managing Python environments and dependencies.

---

## 🚀 Setup & Run Instructions

Follow these steps to get Agnipath EV Nav up and running on your local machine.

### **Prerequisites:**

* **Git:** [Download & Install Git](https://git-scm.com/downloads)
* **Anaconda/Miniconda:** [Download & Install Anaconda (Python 3.11 version recommended)](https://www.anaconda.com/products/distribution)
* **Ollama:** [Download & Install Ollama for Windows](https://ollama.com/download)

### **Step-by-Step Setup:**

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/Vanshika-mahajan/Tata-Hackathon-2025.git](https://github.com/Vanshika-mahajan/Tata-Hackathon-2025.git)
    cd Tata-Hackathon-2025
    ```

2.  **Create and Activate Conda Environment:**
    Open your **Anaconda Prompt** (search in Windows Start Menu).
    ```bash
    conda create -n tata_ev_nav_hackathon_py311 python=3.11
    conda activate tata_ev_nav_hackathon_py311
    ```

3.  **Install Python Dependencies:**
    While in the active `(tata_ev_nav_hackathon_py311)` environment and in your project directory (`Tata-Hackathon-2025`), install all required libraries:
    ```bash
    pip install -r requirements.txt
    ```

4.  **Download LLM Model using Ollama:**
    Ensure the Ollama application is running in the background (it usually starts automatically with Windows).
    Open any terminal (Git Bash or Anaconda Prompt) and pull the Llama 3.2 model:
    ```bash
    ollama pull llama3.2:latest
    ```
    *(This will download a 2.0 GB model. If you experience "out of memory" issues during execution, you can try `ollama pull phi3:latest` (2.2 GB downloaded, but potentially different runtime memory, though if you're tight on RAM, simpler f-string NLG is used in this project as a fallback).*

5.  **Register Jupyter Kernel:**
    Still in your active `(tata_ev_nav_hackathon_py311)` environment in Anaconda Prompt:
    ```bash
    python -m ipykernel install --user --name=tata_ev_nav_hackathon_py311 --display-name "Tata EV Nav Hackathon (Python 3.11)"
    ```

6.  **Launch JupyterLab:**
    Deactivate your conda environment first:
    ```bash
    conda deactivate
    ```
    Then, from your project directory in any terminal (Anaconda Prompt or Git Bash):
    ```bash
    jupyter lab
    ```

7.  **Open and Run the Notebook:**
    * In the JupyterLab interface that opens in your browser, navigate to your project directory.
    * Open `data_exploration.ipynb` (or `Demo_Agnipath_EV_Nav.ipynb` if you've renamed it for demo).
    * **Crucially, select the "Tata EV Nav Hackathon (Python 3.11)" kernel** for the notebook (top-right dropdown menu).
    * **Run all cells from top to bottom.** (You can use `Cell > Run All` from the Jupyter menu).
        * **Important Note:** The **road network graph (`road_network_Delhi_India.graphml`)** and **OSMnx cache files (`data/cache/`)** are large generated files and are NOT committed to GitHub. Running the notebook (specifically Step 4 and subsequent loading steps) will automatically download and generate these files on your local machine. This might take 5-15 minutes the first time.

---

## ❓ Usage

Once all cells have run, an interactive prompt will appear in your Jupyter Notebook output:

`How can I help you plan your EV journey? `

Type your queries here.

**Example Queries:**

* `Plan a trip from Connaught Place, Delhi to Sector 62, Noida for my Tata Punch EV.`
* `I want to go from Dilli Haat to India Gate.`
* `Find free charging stations near South Extension market.`
* `What's the best route from Karol Bagh to Chandni Chowk?`
* `exit` (to quit the interactive session)

---

## 📊 Example Output
Road network graph loaded for full workflow.
Aligned EV stations data loaded for full workflow.

--- EV Journey Planner: Interactive Mode (Type 'exit' to quit) ---
How can I help you plan your EV journey?  Plan a trip from Connaught Place, Delhi to Sector 62, Noida for my Tata Punch EV.
--- Processing Query: 'Plan a trip from Connaught Place, Delhi to Sector 62, Noida for my Tata Punch EV.' ---
Debug: LLM Parsed Params: {'origin': 'Connaught Place, Delhi', 'destination': 'Sector 62, Noida', 'ev_model': 'Tata Punch EV', 'intent': 'plan_trip'}
Debug: Origin Str: Connaught Place, Delhi, Destination Str: Sector 62, Noida, EV Model: Tata Punch EV, Intent: plan_trip
Debug: Geocoding 'Connaught Place, Delhi'...
Geocoded 'Connaught Place, Delhi' to: (28.6314022, 77.2193791)
Debug: Geocoding 'Sector 62, Noida'...
Geocoded 'Sector 62, Noida' to: (28.6211447, 77.3643493)
Debug: Finding nearest nodes for (28.6314022, 77.2193791) and (28.6211447, 77.3643493)...
Debug: Nearest Origin Node: 1191294765, Nearest Destination Node: 9857973351
Debug: Calculating shortest path...
Debug: Route calculated. Length: 14.72 km.
Debug: Finding charging stations along route...
Debug: Found 8 charging stops on route.
Debug: Calculating Green Impact...
Debug: Green Impact results: {'co2_emitted_ice_kg': 2.27, 'co2_emitted_ev_kg': 1.81, 'co2_saved_kg': 0.46, 'liters_fuel_saved': 0.2, 'equivalent_trees_planted': 0.02}
Debug: Generating natural language summary with LLM...
Debug: NLG response received from LLM.
Debug: Raw NLG Content from LLM:
AI: Great trip planned from Connaught Place, Delhi to Sector 62, Noida!
Here's your EV journey summary:
Estimated Distance: 14.72 km
Charging Stops Found: 8 (on-route stations)
First Potential Stop: EESL Block A
Assumed EV Model: Tata Punch EV
Your EV contributes to a greener future!
Estimated CO2 Saved: 0.46 kg CO2
Equivalent Liters of Petrol Saved: 0.20 liters
Equivalent Trees Planted (annually): 0.02 trees
Enjoy your clean, efficient, and sustainable journey!

How can I help you plan your EV journey?
---

## 🌟 Alignment with Tata Hackathon Theme

Agnipath EV Nav directly addresses **"Innovating the future of smart mobility"** by:

* **Promoting EV Adoption:** By providing intelligent trip planning and reducing "range anxiety" for long journeys.
* **Enhancing User Experience:** Utilizing AI (LLM) for natural, conversational interaction, making complex planning simple.
* **Driving Sustainability:** Quantifying the environmental benefits of EV usage, encouraging eco-conscious choices in transportation.
* **Leveraging Data & AI:** Building upon open geographic data, EV charging infrastructure data, and advanced AI models for practical, impactful solutions.
* **Synergy with Tata's Vision:** Directly complements Tata Motors' push for EVs, Tata Power's expanding charging network, and Tata Technologies' focus on digital transformation in mobility.

---

## 💡 Future Enhancements

* **Real-time Charger Availability:** Integrate with APIs (e.g., Tata Power EZ Charge API, if available) for real-time charging station status (availability, queue times).
* **Optimal Charging Strategy:** Suggest ideal charging stops based on battery State-of-Charge (SoC), charger type preference (AC/DC), and charging speed, minimizing total travel time.
* **Broader Geographic Coverage:** Extend road network and charging data beyond Delhi-NCR.
* **Advanced UI:** Develop a dedicated web application (e.g., using Flask/Streamlit) with an interactive map (Folium/Leaflet) for a more user-friendly interface.
* **Customizable EV Profiles:** Allow users to define their specific EV model's battery capacity, efficiency, and charging curve.
* **Multi-modal Integration:** Incorporate public transport, micromobility, and ride-hailing into planning.

---

## 👥 Team Members

* [Vanshika Mahaja]
* [Areeza Suhail]


---

## 📄 License

This project is open-sourced under the MIT License.
