# Truck Transportation Management with Google Sheets & Google Maps 🚚

This project optimizes truck logistics using Google Sheets, Google Maps, and OpenWeather APIs. It integrates advanced scripting and data analysis to improve transportation management.

## Features
- **Travel Time Estimation**: Utilizes Google Maps API to estimate travel and return times for each route.
- **Driver Management**: Displays driver availability and schedules trips efficiently.
- **Route Optimization**: Plans routes considering driver's working hours and travel distances.
- **Comprehensive Tracking**: Records driving time and total kilometers for each driver and truck.
- **Weather Integration**: Incorporates OpenWeather API for real-time weather updates.
- **Automated Data Analysis**: Provides actionable insights for decision-making.

## Demo Video 🎥
[Watch the Demo](https://1drv.ms/v/c/A9927BE78AA24F21/ESFPoorne5IggKl0BQAAAAAB5LuCJUfI3rJ84CEhI6-EHQ?e=iWKIfw)

## Repository Structure
- `/scripts`: Contains Apps Script files and examples.
- `/docs`: Documentation for the project.
- `/data`: Sample data files.
- `/media`: Screenshots and other media files.

## Requirements
- Google Sheets
- Google Maps API
- OpenWeather API
- Google Apps Script enabled in Google Workspace



---

## Requirements
- Google Sheets
- Google Maps API
- OpenWeather API
- Google Apps Script enabled in Google Workspace

---

## Code Explanations

### `/src/GOOGLEMAPS.js`
This function calculates the distance or travel time between two addresses using the Google Maps API.
```javascript
/**
 * Get Distance between 2 different addresses using Google Maps API.
 * 
 * @param {string} start_address - Starting address.
 * @param {string} end_address - Ending address.
 * @param {string} return_type - Return type: "miles", "kilometers", "minutes", "hours".
 * @return {number|string} - The calculated distance or duration, or an error message.
 */
function GOOGLEMAPS(start_address, end_address, return_type) {
  var mapObj = Maps.newDirectionFinder();
  mapObj.setOrigin(start_address);
  mapObj.setDestination(end_address);
  var directions = mapObj.getDirections();
  var getTheLeg = directions["routes"][0]["legs"][0];
  var meters = getTheLeg["distance"]["value"];

  switch (return_type) {
    case "miles":
      return meters * 0.000621371;
    case "minutes":
      return getTheLeg["duration"]["value"] / 60;
    case "hours":
      return getTheLeg["duration"]["value"] / 60 / 60;
    case "kilometers":
      return meters / 1000;
    default:
      return "Error: Wrong Unit Type";
  }
}

