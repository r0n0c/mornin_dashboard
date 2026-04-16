# **🌅 Morning Launchpad (v3.0)**

A high-visibility, "lean-back" dashboard designed for a 1080p kitchen TV. The Morning Launchpad guides children through their morning routine using a dynamic countdown, weather-aware clothing advice, and daily activity reminders.  
Designed specifically for deployment via **Home Assistant** to a **Google Chromecast**.

## **🚀 Features**

* **Mission Control UI**: Massive high-contrast countdown timer and progress bars designed for legibility from across the room.  
* **Smart Weather Engine**: Integrates with the National Weather Service (NWS) API to calculate "Common Sense" gear advice (e.g., advising rain boots if it's over 40°F and raining, or a winter coat if below 32°F).  
* **Auto-Scrolling Routine**: Displays the full morning schedule. Past tasks are greyed out, and the current task is automatically centered and highlighted.  
* **Daily Specials**: A custom reminders table that changes based on the day of the week (e.g., "Library Day," "Gym Shoes Needed," etc.).  
* **Visual State Machine**:  
  * **Green/Normal**: Steady progress.  
  * **Orange/Warning**: 2 minutes remaining (Timer begins to pulse).  
  * **Red/Critical**: 30 seconds remaining (Rapid pulse to encourage speed).  
* **Success State**: A full-screen "Doorway Hub" at 07:25 with confetti, weather summaries, and final departure checks.

## **🛠️ Installation**

### **1\. Host the File**

Place the dash.html file into your Home Assistant /config/www/ directory.

### **2\. Access the Dashboard**

In Home Assistant, this folder is served under the /local/ path. You can verify it by navigating to: https://your-ha-url:8123/local/dash.html

### **3\. Deploy to Chromecast**

For the best experience on a TV (bypassing browser autoplay/security blocks), use the **DashCast** receiver or a Home Assistant Action:  
**Example Action Call:**  
action: media\_player.play\_media  
target:  
  entity\_id: media\_player.kitchen\_tv  
data:  
  media\_content\_id: "http://YOUR\_HA\_INTERNAL\_IP:8123/local/dash.html"  
  media\_content\_type: "website"

## **⚙️ Configuration**

You can easily customize the routine and reminders by editing the constant objects at the top of the \<script\> tag:

### **The Routine**

Adjust the ROUTINE array to match your family's schedule:  
const ROUTINE \= \[  
  { id: "EAT", start: "06:50", end: "07:10", title: "Breakfast", list: \["🍳 Fuel your Body"\] },  
  // ...  
\];

### **Daily Specials**

Update the DAILY\_SPECIALS object for your weekly recurring events:  
const DAILY\_SPECIALS \= {  
  1: "🎻 Anderson Orchestra", // Monday  
  3: "📚 Henny Library",       // Wednesday  
  // ...  
};

## **🧪 Debugging & Testing**

The dashboard includes a built-in simulation engine. Append URL parameters to test different times and weather conditions without waiting for the actual morning.

* **Test a specific time**: ?start=06:44  
* **Fast-forward (Simulation)**: ?accel=60 (1 real second \= 1 minute of dashboard time)  
* **Test Weather**: ?temp=28\&condition=snow

**Ultimate Test URL:** https://.../dash.html?start=06:30\&accel=60\&debug=true

## **📺 Technical Notes**

* **Overscan Protection**: The UI includes a 4vh 4vw padding buffer to ensure elements aren't cut off by physical TV bezels.  
* **Single File**: All HTML, CSS (Tailwind), and JS are contained in one file for easy management.  
* **NWS API**: Requires internet access to fetch live weather data for Monona/Madison, WI coordinates (adjustable in the script).

*Created to turn morning chaos into a mission-driven success.*
