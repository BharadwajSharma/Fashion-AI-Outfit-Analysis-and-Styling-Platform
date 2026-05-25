# Fashion+ — AI Outfit Analysis & Styling App

Upload a photo of an outfit and get instant AI-powered style analysis, color detection, harmony scoring, and personalized recommendations.

---

## Tech Stack

- **Frontend**: React + Vite + Tailwind CSS
- **Backend**: FastAPI + Python
- **CV/ML**: CLIP (zero-shot clothing detection), KMeans (color extraction), OpenCV
- **AI Styling**: Rule-based engine + Anthropic Claude for natural language explanation

---

## Project Structure

```
fashion-plus/
├── backend/
│   ├── main.py                  # FastAPI app + /analyze endpoint
│   ├── requirements.txt
│   └── modules/
│       ├── detector.py          # CLIP-based clothing detection
│       ├── color_extractor.py   # KMeans dominant color extraction
│       ├── style_engine.py      # Rule-based harmony + recommendations
│       └── llm_explainer.py     # Claude API for natural language
└── frontend/
    ├── index.html
    ├── package.json
    ├── tailwind.config.js
    └── src/
        ├── App.jsx
        ├── index.css
        └── components/
            ├── UploadZone.jsx
            ├── LoadingScreen.jsx
            ├── Results.jsx
            ├── OutfitBadge.jsx
            ├── ColorSwatch.jsx
            └── HarmonyMeter.jsx
```

---

## Setup

### 1. Backend

```bash
cd backend

# Create a virtual environment (recommended)
python -m venv venv
source venv/bin/activate      # Mac/Linux
venv\Scripts\activate         # Windows

# Install dependencies
pip install -r requirements.txt

# Set your Anthropic API key
# Mac/Linux:
export ANTHROPIC_API_KEY=your_key_here
# Windows:
set ANTHROPIC_API_KEY=your_key_here

# Start the server
uvicorn main:app --reload
```

> **Note**: The CLIP model (~350MB) downloads automatically on first run. This may take a minute depending on your connection.

Backend runs at: `http://localhost:8000`
API docs at: `http://localhost:8000/docs`

---

### 2. Frontend

```bash
cd frontend

npm install
npm run dev
```

Frontend runs at: `http://localhost:5173`

---

## Usage

1. Open `http://localhost:5173`
2. Upload a photo of an outfit (JPG or PNG, up to 10MB)
3. Click **Analyze Outfit**
4. View:
   - Detected clothing items (upper, lower, feet)
   - Dominant colors per item
   - Harmony score (0–100)
   - AI stylist explanation (powered by Claude)
   - Alternative clothing suggestions
   - Suggested color palette
   - Occasion tags

---

## API

### `POST /analyze`

**Request**: `multipart/form-data` with field `file` (image)

**Response**:
```json
{
  "detected_items": [
    { "category": "t-shirt", "region": "upper", "confidence": 0.82 }
  ],
  "colors": [
    { "item": "t-shirt", "region": "upper", "color_name": "navy blue", "hex": "#1a2f6e", "rgb": [26, 47, 110] }
  ],
  "harmony_score": 78,
  "harmony_label": "Balanced",
  "style_feedback": "The navy blue upper pairs well with the light grey lower...",
  "recommendations": {
    "alternatives": ["beige", "white", "cream"],
    "palette": ["#c87941", "#e8d5b0", "#6b5c3e", "#d4956a"],
    "palette_names": ["Camel", "Cream", "Chocolate", "Terracotta"]
  },
  "occasion_tags": ["Casual", "Weekend"],
  "llm_explanation": "Your outfit communicates a clean, put-together casual look..."
}
```

---

## Tips for Best Results

- Use photos with good lighting
- Full-body shots work best
- Solid color clothing is detected more accurately than patterns
- Traditional wear (sarees, kurtas) is supported

---

## Environment Variables

| Variable | Description |
|---|---|
| `ANTHROPIC_API_KEY` | Your Anthropic API key (required for style explanations) |

Get your key at: https://console.anthropic.com

---

## Extending the App

- **Add skin tone analysis**: Detect face region, sample skin pixels, classify as warm/cool/neutral undertone
- **Shopping integration**: Map recommended colors to product search APIs
- **Wardrobe builder**: Let users save outfits and track their palette over time
- **Seasonal palettes**: Add Spring/Summer/Autumn/Winter color theory layer
