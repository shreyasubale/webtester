# MRAID WebTester Architecture

The MRAID WebTester is a web-based tool designed to test Mobile Rich Media Ad Interface Definitions (MRAID) implementations. This document outlines the architecture and core components of the system.

## Project Structure

```
webtester/
├── css/                    # Style sheets for the application
├── jquery/                 # jQuery and UI libraries
├── img/                    # Image assets
├── widgets/                # UI widget implementations
├── safari/                 # Core MRAID implementation
│   ├── main.js             # Application logic
│   └── mraidview.js        # MRAID view implementation
├── compliance/             # IAB compliance test ads
│   ├── units/              # Test ad units
│   └── docs/               # Compliance documentation
├── index.html              # Main application entry point
├── htmlproxy.php           # Proxy for HTML content
├── imageDownload.php       # Helper for image downloads
├── favicon.ico             # Site favicon
├── LICENSE                 # BSD License
└── README.md               # Project documentation
```

## Core Components

### 1. User Interface (index.html)

The UI is divided into three main tabs:

1. **Prepare**: Configure test environment properties
   - Device geometry (ad sizes, screen sizes)
   - API version selection (MRAID v1 or v2)
   - Placement type (Inline or Interstitial)
   - Off-screen option
   - Native features to emulate (sms, tel, calendar, etc.)

2. **Flight**: Input ad code for testing
   - Head script inclusion
   - HTML tag source input

3. **Test**: Run and monitor the ad
   - Console output for logging
   - Orientation controls
   - Error and info filtering

### 2. Core MRAID Implementation (safari/mraidview.js)

This is the heart of the application, providing a web-based MRAID container implementation. Key components:

- **Constants**: Defines MRAID versions, placements, states, events, and features
- **Event Handling**: System for registering and triggering event listeners
- **MRAID Bridge**: Implementation of the MRAID API specification
- **Rendering Engine**: Creates and manages the ad frame/window

The implementation follows the MRAID specification flow:
1. Initialize properties (version, supports)
2. Create ad window
3. Initialize ad frame and bridge
4. Set up event listeners
5. Signal ready state to the ad

### 3. Application Logic (safari/main.js)

Controls the application flow and user interaction:

- **Event Listeners**: For console logging and error reporting
- **Form Handling**: Processing user input from the Prepare tab
- **Rendering**: Functions to render ads from HTML or URLs
- **Utilities**: Helper functions for orientation changes, query string parsing, etc.

### 4. Compliance Testing (compliance/units/)

Contains IAB-created test ad units for validating MRAID implementations:

- Interstitial ads
- Resize functionality (with error testing)
- Two-part expand tests
- Full-page ad examples
- Video support tests

## Data Flow

1. User configures test environment in the Prepare tab
2. User inputs ad HTML/script in the Flight tab
3. System renders the ad in a popup window with MRAID container
4. MRAID events and method calls are logged to the console
5. User can manipulate the environment (e.g., orientation) to test ad behavior

## Integration Points

- **Query String Parameter**: The `adtag` parameter allows direct injection of HTML into the Flight tab
- **Console Logging**: All MRAID interactions are logged to the console for debugging

## Technical Constraints

- Project is no longer actively maintained
- Uses older versions of jQuery and related libraries
- Implementation specifically designed for MRAID v1 and v2 (not newer versions)
- Some browser security policies may affect functionality when running locally

---

This architecture document should be updated if any feature changes or enhancements are made to the system. 