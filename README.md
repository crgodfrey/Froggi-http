# Froggi API Documentation

## Overview

Froggi is a web-based scoreboard management system built with Axum (Rust). It provides endpoints for managing game scoreboards, team information, sponsors, and overlay displays.


> [!NOTE]  
> For use with bitfocus companion or any other http based program, the header uses the format of {"api-auth": "Your_api_key"_found_in_settings} (referred to as $(custom:URL)) , and the url should be the home page of froggi.


## Authentication

The system uses session-based authentication with two middleware layers:
- **auth_give_session_layer**: Provides session data to handlers
- **auth_session_layer**: Requires valid session for access

## Base URL Structure

All endpoints use the base URL: `$(custom:URL)`

---

## Downs Display Endpoints

### GET /downs/display/{type}

Displays downs information in different formats.

**Parameters:**
- `type` (required): Display format
  - `down` - Shows just downs
  - `togo` - Shows just yards to go
  - `both` - Shows both in "# & #" format (e.g., "3rd & 30")

**Example:**
```
GET $(custom:URL)/downs/display/both
```

---

## Authentication Endpoints

### GET /login
Displays the login page.

### POST /login
Authenticates user credentials.

### GET /login/create
Displays the account creation page.

### POST /login/create
Creates a new user account.

### POST /logout
Logs out the current user and destroys the session.

---

## Dashboard & Core Pages

### GET /
Main dashboard page (requires authentication).

### GET /teaminfo
Team information management page (requires authentication).

### GET /settings
Settings configuration page (requires authentication).

### GET /logs
System logs page (requires authentication).

---

## Game Clock Management

All game clock endpoints require authentication.

### POST /game-clock/ctl/{operation}
Controls game clock operations.
- `operation`: `start`, `stop`, `pause`, or `reset`

### POST /game-clock/set/{mins}/{secs}
Sets the game clock to specific time.
- `mins`: Minutes (0-99)
- `secs`: Seconds (0-59)

### POST /game-clock/set-mins/{mins}
Sets only the minutes on the game clock.

### POST /game-clock/set-secs/{secs}
Sets only the seconds on the game clock.

### POST /game-clock/update/{mins}/{secs}
Updates the game clock by adding/subtracting time.

### GET /game-clock/display/{format}
Displays the current game clock time.
- `format`: Display format option

---

## Countdown Clock Management

All countdown clock endpoints require authentication.

### POST /countdown-clock/ctl/{operation}
Controls countdown clock operations.

### POST /countdown-clock/set/{mins}/{secs}
Sets the countdown clock to specific time.

### POST /countdown-clock/set-mins/{mins}
Sets only the minutes on the countdown clock.

### POST /countdown-clock/set-secs/{secs}
Sets only the seconds on the countdown clock.

### POST /countdown-clock/update/{mins}/{secs}
Updates the countdown clock time.

### GET /countdown-clock/display/{format}
Displays the current countdown clock time.

### POST /countdown/text/set
Sets custom text for countdown display.

---

## Score Management

All score endpoints require authentication.

### Home Team Points
- **POST /home-points/update/{amount}** - Add/subtract points
- **POST /home-points/set/{amount}** - Set exact point total
- **GET /home-points/display** - Display current home team points

### Away Team Points
- **POST /away-points/update/{amount}** - Add/subtract points
- **POST /away-points/set/{amount}** - Set exact point total
- **GET /away-points/display** - Display current away team points

---

## Quarter Management

Requires authentication.

### POST /quarter/set/{quarter}
Sets the current quarter/period.
- `quarter`: Quarter number (1-4, OT, etc.)

### POST /quarter/update/{amount}
Updates the quarter by the specified amount.

### GET /quarter/display
Displays the current quarter.

---

## Downs Management

Requires authentication.

### POST /downs/set/{down}
Sets the current down.
- `down`: Down number (1-4)

### POST /downs/update/{amount}
Updates the current down by the specified amount.

### POST /downs/togo/set/{yards}
Sets the yards to go for first down.
- `yards`: Yards remaining

### POST /downs/togo/update/{amount}
Updates yards to go by the specified amount.

---

## Team Information Management

### Team Presets
- **POST /teaminfo/create** - Create new team preset (requires auth)
- **POST /teaminfo/select/{id}** - Select team preset (requires auth)
- **POST /teaminfo/remove/{id}** - Remove team preset (requires auth)
- **GET /teaminfo/download-preset/{id}** - Download team preset (requires auth)
- **POST /teaminfo/import-preset** - Import team preset (requires auth)

### Team Display
- **PUT /teaminfo/selector** - Get team preset selector
- **PUT /teaminfo/name/{team}** - Get team name display
- **PUT /teaminfo/button-css** - Get team button CSS
- **PUT /icon/{team}** - Get team icon

---

## Sponsors Management

Requires authentication.

### POST /sponsors/upload
Upload sponsor images/videos.
- Supports files up to 2GB
- Content-Type: multipart/form-data

### POST /sponsors/remove/{id}
Remove a sponsor by ID.

### PUT /sponsors/manage
Get sponsor management interface.

---

## Overlay & Display

### GET /overlay
Main overlay display page (public access).

### GET /overlay-websocket
WebSocket connection for real-time overlay updates.

### PUT /overlay/team-border-css
Get CSS for team borders on overlay.

---

## Visibility Controls

Requires authentication.

### POST /visibility/toggle/{element}
Toggle visibility of overlay elements.
- `element`: Element identifier to show/hide

### PUT /visibility/buttons
Get visibility control buttons interface.

---

## WebSocket Connections

### GET /dashboard-websocket
Real-time dashboard updates (requires authentication).

### GET /overlay-websocket
Real-time overlay updates (public access).

---

## System Management

All system management endpoints require authentication.

### POST /popup/{type}
Trigger system popups or notifications.

### POST /config-json/set
Update system configuration.

### PUT /config-json/form
Get configuration form interface.

### POST /reset
Reset system to default state.

### POST /restart
Restart the application.

### POST /shutdown
Shutdown the application.

### POST /update
Update the application.

### PUT /update/menu
Get update management interface.

---

## Static Assets

Public access endpoints for frontend resources:

- **GET /styles.css** - Main stylesheet
- **GET /htmx.js** - HTMX library
- **GET /app.js** - Main application JavaScript
- **GET /index.js** - Index page JavaScript
- **GET /overlay.js** - Overlay JavaScript
- **GET /settings.js** - Settings page JavaScript
- **GET /teaminfo.js** - Team info JavaScript
- **GET /sanitize.js** - Input sanitization library
- **GET /ws.js** - WebSocket handling
- **GET /local-asset/{directory}/{asset}** - Local asset files

---
