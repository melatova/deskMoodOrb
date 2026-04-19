![Status](https://img.shields.io/badge/Status-Active-blue)
![Platform](https://img.shields.io/badge/Platform-Photon%202-lightgrey)
[![Dashboard](https://img.shields.io/badge/Cloud-Dashboard-orange)](https://alicevortex.com/dashboard)


# 🌈 Mood Desk Orb
<div align="center">
<pre>
                             __      ____                    __          _____          __        
 /'\_/`\                    /\ \    /\  _`\                 /\ \        /\  __`\       /\ \       
/\      \    ___     ___    \_\ \   \ \ \/\ \     __    ____\ \ \/'\    \ \ \/\ \  _ __\ \ \____  
\ \ \__\ \  / __`\  / __`\  /'_` \   \ \ \ \ \  /'__`\ /',__\\ \ , <     \ \ \ \ \/\`'__\ \ '__`\ 
 \ \ \_/\ \/\ \L\ \/\ \L\ \/\ \L\ \   \ \ \_\ \/\  __//\__, `\\ \ \\`\    \ \ \_\ \ \ \/ \ \ \L\ \
  \ \_\\ \_\ \____/\ \____/\ \___,_\   \ \____/\ \____\/\____/ \ \_\ \_\   \ \_____\ \_\  \ \_,__/
   \/_/ \/_/\/___/  \/___/  \/__,_ /    \/___/  \/____/\/___/   \/_/\/_/    \/_____/\/_/   \/___/ 
</pre>                                                
</div>                                                  
                                                                                                  

## Overview
The Mood Desk Orb is a small, glowing companion designed to help bridge the gap in emotional communication.

It listens to the environment — CO₂, light, sound, temperature, and even micro‑fidgeting — and translates those signals into a color state.

Ambient, expressive, and a vibe‑translator for humans who sometimes miss the obvious cues.

A synergy of **IoT**, **sensor fusion**, **behavioral inference**, and **organic design**.
- - - - - - - 
- - - - - - - - - - - - - - - - - - - -
## Highlights
> **To help bridge the gap in emotional communication by translating mood into a color glow.**  
> **Dashboard is currently at: https://alicevortex.com/dashboard**

---

## Why this exists
**Problem:** Emotional dysregulation and “room‑reading” challenges in work/school/group settings.  
**Solution:** A sensor‑fused ambient indicator that translates physiological and environmental data into non‑verbal social cues — a gentle, non‑intrusive visual signal to help people connect more thoughtfully.


::: mermaid
graph LR;
  A[Sensors] --> B[Photon 2 Engine];
  B --> C[AI Mood Inference / Behavioral Inference Model];
  C --> D[NeoPixel Visual Output];
:::

## Hardware 
- **Particle Photon 2** (microcontroller + cloud bridge)  
- **SCD41** — CO₂, humidity, temperature (I²C)  
- **MLX90614** — IR skin temperature (I²C)  
- **HLK‑LD2410C** — mmWave presence / fidget radar (UART)  
- **VEML7700** — ambient light (I²C)  
- **MP34DT01** — PDM microphone (A0/A1)  
- **MPU6050** — accelerometer (I²C) for movement/thump detection  
- **16‑LED NeoPixel ring** (visual output)  
- **SN74AHCT125N** logic level shifter (NeoPixel data)  
- **5V 3A USB‑C PSU** (main power)  
- **OLED 128×32** (status + messages)  
- **Momentary button** (theme cycle / sleep)  
- 3D printed enclosure (transparent / matte PLA with "light tunnels" to diffuse LEDS)

---

## Firmware (summary)
- **Language / Platform**: Particle (Photon 2) C++  
- **Key features implemented**
  - Sensor drivers: SCD41, VEML7700, MLX90614, MP34DT01, LD2410C, MPU6050.  
  - NeoPixel animation + color themes.  
  - Local decision tree mood classifier (fallback when cloud unavailable).  
  - Particle Cloud publish of sensor payload (`orb_sensors`) and subscription to AI webhook responses
  - OLED messages, theme cycling button, session tracking, and non‑blocking main loop.  

---

## Mood Logic (high level)
- **Primary signals**: presence (radar), fidget average, sound density, CO₂ levels, skin temp delta, stability (vibration).  
- **Local decision tree** (fallback): uses presence + strongest indicators (thump → Anger, displaced → Surprise, high fidget+sound → Frustration, CO₂ thresholds → Fatigue/Boredom, skin temp delta → Fear/Contentment).  
- **Cloud mode**: publishes JSON payload to Particle Cloud; webhook forwards to OpenAI (gpt‑4o‑mini) which returns a mood JSON; Photon maps AI mood → animation and re‑publishes result for dashboard.

---

## Dashboard & Cloud
- **Live dashboard**: https://alicevortex.com/dashboard/  
- **Features**: real‑time sensor feeds, manual color/theme control, auto‑mode toggle, and webhook integration for AI mood analysis.  
- **Webhook**: Particle Console webhook posts `orb_sensors` JSON to endpoint; OpenAI integration returns a JSON mood object (mood, color, reason, confidence).

---

## Wiring Diagram
![Fritzing](moodOrb_bb.png)
![Schematic](moodOrb_schem.png)
---

## Resources


| 📂 Directory	 | 	📝 Description |
| -------- | -------- |
| /docs   | Datasheets   |
| /img    | Pictures and Video   |
| /testing    | Code for testing sensors   |
| /mech    | Build files (.stl etc)  |

---

## Hackster
- [publishing after provisional filed]

---
Thank you to all the wonderful people of CNM Ingenuity IoT Deep Dive for introducing me to the world of IoT!

---
Thank you for visiting the Mood Desk Orb project  
May your vibes be bright and your sensors calibrated  ( ^‿^ )
