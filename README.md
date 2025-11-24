# ApexPilot – AI Driving Coach for GR86 Cup Telemetry

ApexPilot is an AI-powered driving analysis tool built on real Toyota GR86 Cup Sonoma 2025 telemetry.  
It converts race data into expert driving recommendations using a sequence model, and visualizes the results interactively.

---

## 🚀 Quick Start

To use the interactive replay (`replay.html`), you **must** run a local HTTP server.  
Opening the HTML file directly will cause a **CORS (Cross-Origin Request) error** when it loads `model_output.csv`.

### ✅ Start a Local Server (Python)

Open a terminal inside the project folder and run:

```bash
python -m http.server 8000
```

Then open your browser and go to:

```
http://localhost:8000/replay.html
```

This solves all CSV loading + CORS issues.

---

## 📁 Repository Contents

```
LICENSE
ToyotaHackathon.ipynb      # Main notebook (processing → model → inference)
processed_data.csv         # Cleaned dataset (progress_dist, smoothing, corner_index)
model_output.csv           # AI predictions and diffs for every lap
replay.html                # Interactive visualization (requires local server)
README.md                  # Project documentation
```

---

## 📄 File Descriptions

### **processed_data.csv**
Contains cleaned telemetry:
- speed, steering, throttle, brake  
- timestamps, gear, RPM  
- computed progress_dist  
- auto-generated corner_index  
- smoothed control inputs

### **model_output.csv**
Contains all telemetry **plus AI predictions**:
- `pred_steer`, `pred_ath`, `pred_brk`
- `diff_steer`, `diff_ath`, `diff_brk`
- corner / sector alignment  
Used directly by `replay.html`.

### **replay.html**
Interactive lap analyzer that displays:
- Steering / Throttle / Brake comparison  
- Δ(input) visualizations  
- Corner-colored blocks  
- Sector boundaries  
- Dropdown for vehicle & lap selection  

📌 **Requires** a local HTTP server to run properly.

---

## 🧠 How It Works

The full pipeline implemented in `ToyotaHackathon.ipynb` includes:

1. Telemetry cleanup  
2. Lap detection & flying-lap filtering  
3. progress_dist reconstruction  
4. Automatic corner detection  
5. Control smoothing  
6. Mamba sequence model training  
7. Full-lap inference → writes into `model_output.csv`  
8. Visualization through `replay.html`

---

## 🔧 Serving the Visualization

Run:

```bash
python -m http.server 8000
```

Then open:

```
http://localhost:8000/replay.html
```

Alternative port:

```bash
python -m http.server 5000
```

---

## 📜 License

See `LICENSE`.

---

## 🙌 Acknowledgements

Built using data from the Toyota GR86 Cup as part of an AI-based motorsport analytics project.
