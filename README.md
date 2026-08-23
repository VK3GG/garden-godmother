cat > ~/garden-godmother/README.md << 'README'
# 🌿 Aus Garden Goddess

A fork of [Garden Godmother](https://github.com/rancur/garden-godmother) by rancur, adapted for Australian gardeners with a focus on Melbourne's temperate climate.

> **Branch:** `australian-climate` | **Original:** [rancur/garden-godmother](https://github.com/rancur/garden-godmother)

---

## What's Changed from the Original

### 🌏 Australian Localisation
- **Seasons** replaced with Southern Hemisphere equivalents: Summer (Dec-Feb), Autumn (Mar-May), Winter (Jun-Aug), Spring (Sep-Nov)
- **Planting dates** shifted 6 months for the Southern Hemisphere
- **USDA hardiness zones** replaced with Australian climate zones (Temperate, Cool Temperate, Subtropical, Tropical, Semi-Arid, Arid, Mediterranean)
- **Temperatures** converted to Celsius throughout
- **Measurements** converted to metres
- **Frost thresholds** converted to Celsius (4°C instead of 40°F)
- **Weather API** switched to metric units (mm, km/h, °C)
- **Rebranded** to "Aus Garden Goddess"

### 🌿 Australian Plant Database (46 plants added)

**Native Bush Foods**
Warrigal Greens, Lemon Myrtle, Lilly Pilly, Davidson's Plum, Kakadu Plum, Quandong, Wattleseed, Mountain Pepper, Aniseed Myrtle, Native Mint, Saltbush, Midyim Berry, Riberry, Native Lemongrass, Bush Tomato, Macadamia, Native Violet, Murnong (Yam Daisy), Native Sea Celery, Chocolate Lily

**Common Australian Vegetables**
Silverbeet, Broad Bean, Rocket, Capsicum, Sweet Corn, Pumpkin, Beetroot, Leek, Coriander, Rhubarb, Snow Pea, Kohlrabi, Swede, Globe Artichoke, Cavolo Nero, Choko, Climbing Bean, Cherry Tomato, Zucchini

**Australian Fruit**
Cumquat, Feijoa, Tamarillo

**Asian Herbs** (popular in Australian multicultural gardens)
Vietnamese Mint, Galangal

**Edible Flowers**
Borage, Calendula

### 🔍 OpenPlantBook Enhancements
- Search by Australian common names (e.g. "warrigal greens" automatically searches for *Tetragonia tetragonioides*)
- Searches both public and user plant databases
- Import button to add plants directly from OpenPlantBook into your library
- Rate limit error messages with helpful guidance
- Common name lookup table for 70+ Australian plants

---

## Installation

### Prerequisites
- Docker and Docker Compose
- A server, NAS, or PC running Linux (tested on OpenMediaVault)
- Optional: [Home Assistant](https://www.home-assistant.io) for weather station and sensor integration
- Optional: [OpenPlantBook](https://open.plantbook.io) account (free) for plant data enrichment
- Optional: OpenAI API key for AI-powered features

### Quick Start

**1. Clone the Australian branch:**
```bash
git clone -b australian-climate https://github.com/VK3GG/garden-godmother.git
cd garden-godmother
```

**2. Create your environment file:**
```bash
nano .env
```

Add your settings:
```env
NEXT_PUBLIC_API_URL=http://YOUR_SERVER_IP:3402
OPENAI_API_KEY=your_openai_key_here
HA_TOKEN=your_home_assistant_long_lived_token
HA_URL=http://YOUR_HA_IP:8123
CORS_ORIGINS=http://YOUR_SERVER_IP:3400
COOKIE_DOMAIN=YOUR_SERVER_IP
```

**3. Build and start:**
```bash
sudo docker compose up -d --build
```

**4. Access the app:**
Open `http://YOUR_SERVER_IP:3400` in your browser.

On first run, check the logs for your admin password:
```bash
sudo docker logs garden-api | grep -i password
```

---

### Running on OpenMediaVault with Dockhand

1. In Dockhand, create a new stack using **Deploy from Git**
2. Repository URL: `https://github.com/VK3GG/garden-godmother.git`
3. Branch: `australian-climate`
4. Add your environment variables in the Dockhand UI
5. Deploy

---

## Post-Installation Setup

### 1. Set Your Location
Go to **Settings → Property** and enter your address to auto-detect your climate zone and frost dates.

### 2. Connect Home Assistant (optional)
Go to **Settings → Integrations → Home Assistant** and enter your HA URL and long-lived access token. Then map your weather station sensors in **Monitor → Sensors → Entity Mappings**.

### 3. Connect OpenPlantBook (optional)
1. Register for a free account at [open.plantbook.io](https://open.plantbook.io)
2. Generate an API token under **API Keys**
3. Add it in **Settings → Integrations → OpenPlantBook**
4. Enrich your plant database (run once, wait 24hrs if rate limited):
```bash
curl -X POST -b cookies.txt http://YOUR_SERVER_IP:3402/api/plants/enrich-all
```

> **Note:** OpenPlantBook rate limits to approximately 1 request per 4 minutes. The enrich-all endpoint runs with a 2-second delay between requests and skips already-enriched plants on subsequent runs.

### 4. Add Your Garden
Go to **Garden → Beds** and create your beds, then start tracking plantings.

---

## Searching for Australian Plants

The OpenPlantBook search understands Australian common names. Try searching for:
- "warrigal greens" → finds *Tetragonia tetragonioides*
- "lemon myrtle" → finds *Backhousia citriodora*
- "finger lime" → finds *Citrus australasica*
- "mountain pepper" → finds *Tasmannia lanceolata*
- "feijoa" → finds *Acca sellowiana*

If a plant isn't in OpenPlantBook, it may already be in the local database — check the Plant Library first.

---

## Credits

- **Original project:** [Garden Godmother](https://github.com/rancur/garden-godmother) by [rancur](https://github.com/rancur) — all core functionality, architecture and design
- **Australian plant data** sourced from [CERES Nursery](https://ceres.org.au), [Leaf Root Fruit](https://www.leafrootfruit.com.au), [Bunnings](https://www.bunnings.com.au), [Bush to Bowl](https://bushtobowl.com) and [Australian Plants Society](https://austplants.com.au)
- **Melbourne planting calendar** based on temperate climate zone data from [Gardenate](https://gardenate.com) and [Plant Planner](https://plantplanner.com.au)

---

## Contributing

If you'd like to add more Australian plants, improve the localisation, or fix bugs, please open a pull request on the `australian-climate` branch of [VK3GG/garden-godmother](https://github.com/VK3GG/garden-godmother).
README

cd ~/garden-godmother
git add README.md
git commit -m "Add comprehensive Australian localisation README"
git push origin australian-climate
