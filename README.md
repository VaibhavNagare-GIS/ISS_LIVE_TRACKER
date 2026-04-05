# ISS Live Tracker

Real-time tracking of the International Space Station with an interactive satellite map.

**Live Demo:** https://vaibhavnagare-gis.github.io/ISS_LIVE_TRACKER/

## About

This web application tracks the ISS in real-time, showing its current position, speed, altitude, and orbital path on a satellite map. I built this initially as a personal project to learn about web mapping and APIs. Later, it became part of my WebGIS coursework at Bharati Vidyapeeth's Institute of Environment Education and Research, Pune.

## Features

The tracker displays:
- Current ISS position (latitude, longitude, altitude, velocity)
- Live ground track showing where the ISS has been
- Predicted trajectory showing where it's heading
- Current crew members aboard the station
- Visibility status (daylight or eclipse)
- Auto-follow mode to keep the ISS centered

You can toggle the ground track, trajectory line, and following mode using the buttons above the map.

## Technologies

Built with HTML, CSS, and JavaScript. Uses Leaflet.js for the interactive map, WhereTheISS.at API for real-time position data, and Open Notify API for crew information. The satellite imagery comes from Esri.

## How to Use

Just open the live link above in any web browser. The tracker updates every 3 seconds automatically. Click on the ISS marker to see detailed information in a popup.

## UN SDG Alignment

This project supports four UN Sustainable Development Goals:

**SDG 4 (Quality Education)** - Makes space science and orbital mechanics accessible through visual learning

**SDG 9 (Industry and Innovation)** - Demonstrates real-time geospatial technology using open-source tools

**SDG 13 (Climate Action)** - Highlights the ISS role in monitoring Earth's climate and environment

**SDG 17 (Partnerships)** - Shows international cooperation through the ISS partnership between NASA, ESA, JAXA, CSA, and Roscosmos

## Academic Context

**Program:** M.Sc. Geoinformatics (2nd Semester)  
**Institution:** Bharati Vidyapeeth's Institute of Environment Education and Research, Pune  
**Student:** Vaibhav Shivaji Nagare

## Data Sources

ISS position data from WhereTheISS.at API (https://wheretheiss.at)  
Current crew information from ISS People in Space API by corquaid (https://github.com/corquaid/international-space-station-APIs)  
Satellite imagery from Esri World Imagery service

## Known Issues

The crew API sometimes doesn't load due to server timeouts. The trajectory prediction uses simple linear projection rather than actual orbital mechanics, so it's an approximation. Internet connection is required for real-time updates.

## License

CC0 1.0 Universal

## Contact

Vaibhav Shivaji Nagare  
Email: vaibhavnagare20@gmail.com  
GitHub: [@vaibhavnagare-gis](https://github.com/vaibhavnagare-gis)  
LinkedIn: [@vaibhav-nagare-gis](https://www.linkedin.com/in/vaibhav-nagare-gis/)

## Acknowledgments

Thanks to NASA for ISS data and mission information. The WhereTheISS.at team for their reliable real-time position API. Special thanks to corquaid for maintaining the ISS People in Space API with current Expedition 74 crew data. The Leaflet.js community for excellent mapping tools. Esri for providing satellite imagery tiles. My professors at Bharati Vidyapeeth Institute of Environment Education and Research, Pune for valuable feedback on this project.
