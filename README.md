# Arduino Vibe Coder

A web-based development environment that connects AI assistants (Claude AI or local LLMs via LMStudio) with Arduino CLI for seamless embedded development. Perfect for rapid prototyping with ESP32, Teensy, and SAMD21 boards.

## Features

- **Web-based chat interface** - Talk to AI about Arduino projects
- **Dual AI Support** - Choose between Claude AI (cloud) or LMStudio (local LLM)
- **Automatic Arduino integration** - Uses your existing Arduino IDE configuration and installed boards
- **Dynamic board detection** - Shows only the boards you have cores installed for
- **Sketch management** - Load existing sketches, save new ones, with automatic context awareness
- **Project context** - AI understands your current sketch, selected board, and can suggest improvements or modifications
- **New Chat** - Start fresh conversations with complete context clearing
- **Sketchbook integration** - Can save sketches to your Arduino sketchbook folder
- **Direct compilation** - Compile sketches with one click
- **Automatic upload** - Upload to your boards without leaving the browser  
- **Serial monitoring** - View output in real-time
- **Multi-board support** - Any boards you have installed (ESP32, Arduino, Teensy, etc.)
- **Error feedback** - Compilation errors automatically sent back to AI for fixes

## Quick Start

### Option A: Using Claude AI (Cloud)
1. **Get a Claude API key** from https://console.anthropic.com/
2. **Download/Clone this repository**
3. **Download `arduino-cli.exe`** and put it in the same folder
4. **Double-click `start.bat`** 
5. **When you see "Server running"**, open browser to http://localhost:3000
6. **Select "Claude AI"** and enter your API key
7. **Start coding with AI assistance!**

### Option B: Using LMStudio (Local LLM)
1. **Install and setup LMStudio** (see LMStudio Setup section below)
2. **Download/Clone this repository**
3. **Download `arduino-cli.exe`** and put it in the same folder
4. **Double-click `start.bat`**
5. **When you see "Server running"**, open browser to http://localhost:3000
6. **Select "LMStudio (Local)"** and click Connect
7. **Start coding with your local AI!**

## Prerequisites

### 1. AI Assistant Setup

#### Option A: Claude AI Setup
**Get your API key from Anthropic:**
1. Visit https://console.anthropic.com/
2. Sign up or log in to your account
3. Go to "API Keys" in your account settings
4. Create a new API key
5. Copy the key (it starts with `sk-ant-`)

**Note:** Claude API usage is pay-per-use. Check Anthropic's pricing for current rates.

#### Option B: LMStudio Setup
**Download and Install LMStudio:**
1. Visit https://lmstudio.ai/
2. Download LMStudio for your operating system
3. Install and run LMStudio

**Configure LMStudio:**
1. **Download a Model:**
   - In LMStudio, go to the "Search" tab
   - Search for Arduino/coding-capable models like:
     - `microsoft/DialoGPT-medium` (lightweight, good for basic tasks)
     - `codellama/CodeLlama-7b-Instruct-GGUF` (excellent for code generation)
     - `TheBloke/deepseek-coder-6.7b-instruct-GGUF` (specialized for coding)
     - `microsoft/WizardCoder-Python-7B-V1.0-GGUF` (good for code)
   - Download your preferred model (7B models work well on most systems)

2. **Load the Model:**
   - Go to "Local Server" tab in LMStudio
   - Select your downloaded model
   - Click "Load Model"
   - Wait for the model to load (you'll see memory usage)

3. **Start the Server:**
   - In the "Local Server" tab, make sure these settings are configured:
     - **Server Port:** `1234` (default)
     - **Cross-Origin-Requests:** Enabled
     - **Apply chat template:** Enabled (for instruct models)
   - Click "Start Server"
   - You should see "Server running on http://localhost:1234"

4. **Test the Connection:**
   - The status should show "Server online"
   - You can test the API at http://localhost:1234/v1/models

**Arduino Vibe Coder automatically maintains conversation context for LMStudio**, so the AI will remember your code and previous questions throughout your session. It also includes your currently selected board in the context for better pin and feature recommendations.

**Recommended Models for Arduino Development:**
- **CodeLlama-7b-Instruct:** Best overall for code generation
- **DeepSeek-Coder:** Specialized for coding tasks
- **WizardCoder:** Good balance of performance and size
- **Larger models (13B+):** Better quality but require more RAM

**Model Requirements:**
- **7B models:** ~8GB RAM minimum
- **13B models:** ~16GB RAM minimum  
- **34B models:** ~32GB RAM minimum
- GPU acceleration available if you have compatible GPU

### 2. Install Node.js

**Download:** https://nodejs.org/
- Choose the LTS version (recommended for most users)
- Run the installer with default settings
- Verify installation: Open Command Prompt and type `node --version`

### 3. Install Arduino CLI

**Easy Method (Recommended):**
1. Download `arduino-cli.exe` from: https://arduino.github.io/arduino-cli/installation/
2. **Put `arduino-cli.exe` directly in your project folder** (same folder as `start.bat`)
3. That's it! No PATH configuration needed.

**Alternative Method:**
1. Download the Windows zip file and extract somewhere (e.g., `C:\arduino-cli\`)
2. Add the folder to your PATH (see Environment Variables in Windows)

**Verify installation:** 
- If using local method: Double-click `arduino-cli.exe` (should show help)
- If using PATH method: Open Command Prompt and type `arduino-cli version`

### 4. Configure Arduino CLI for Your Boards

**The Vibe Coder will automatically detect boards from your existing Arduino IDE installation.** If you need additional boards:

**ESP32 Setup:**
```bash
arduino-cli core update-index --additional-urls https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
arduino-cli core install esp32:esp32
```

**Teensy Setup:**
```bash
arduino-cli core update-index --additional-urls https://www.pjrc.com/teensy/package_teensy_index.json
arduino-cli core install teensy:avr
```

**Additional Arduino Boards:**
```bash
arduino-cli core update-index
arduino-cli core install arduino:samd    # For MKR boards, Nano 33 IoT, etc.
arduino-cli core install arduino:mbed_nano  # For Nano 33 BLE
```

*Note: The web interface will automatically show all boards from your installed cores.*

## Installation

### Option 1: Use the Startup Script (Recommended)

1. Clone or download this repository
2. Double-click `start.bat`
3. The script will:
   - Check prerequisites
   - Install Node.js dependencies
   - Start the server
   - Show you the next steps

### Option 2: Manual Installation

```bash
# Clone the repository
git clone [your-repo-url]
cd arduino-vibe-coder

# Install dependencies
npm install

# Start the server
npm start
```

## Usage

### 1. Starting the System

- **Easy way:** Double-click `start.bat`
- **Manual way:** Run `npm start` in the project folder
- Browser should open automatically to http://localhost:3000

### 2. Choosing Your AI Assistant

**For Claude AI:**
1. Select "Claude AI" from the dropdown
2. Enter your API key and click "Connect"
3. Your key is saved for future sessions

**For LMStudio:**
1. Make sure LMStudio is running with a model loaded
2. Select "LMStudio (Local)" from the dropdown  
3. Click "Connect" (no API key needed)
4. The system will connect to localhost:1234

### 3. Basic Workflow

1. **Select AI Provider:** Choose Claude or LMStudio and connect
2. **Load existing sketch (optional):** Use the sketch dropdown to load an existing project, or start fresh
3. **Ask AI for code:** "Write code for ESP32 to blink an LED" - AI will see your current sketch context
4. **Save your work:** Click "Save" to save your sketch to your sketchbook or local folder
5. **Select your board:** Choose from the dropdown (ESP32, Teensy, etc.)
6. **Select your port:** Refresh ports and choose your connected device
7. **Compile:** Click "Compile" - errors automatically go back to AI
8. **Upload:** Click "Upload" to program your board
9. **Monitor:** Serial output appears automatically

**AI Settings Management:** Use the "⚙️ AI Settings" dropdown in the header to switch providers or update API keys.

**New Chat:** Click the "🗨️ New Chat" button or use **Ctrl+Shift+N** (Cmd+Shift+N on Mac) to start a completely fresh conversation with cleared context.

**Sketch Management:** 
- 📁 Icon = Arduino sketchbook folder
- 💾 Icon = Local project folder
- AI automatically understands your current project context

### 4. Example Conversations

**Starting a new project:**
```
You: "Write code for ESP32 that blinks an LED on pin 2 with a 1-second interval"

AI: "Here's code for blinking an LED..."
[Code appears in chat and is ready for compilation]

[Click Save] → [Click Compile] → [Click Upload] → [LED starts blinking]
```

**Working with existing sketches:**
```
[Load existing sketch from dropdown]

You: "Add a button on pin 4 that changes the blink speed when pressed"

AI: "I can see your current LED blink code. Here's how to add button control..."
[Modified code appears, understanding your existing project]

[Click Save] → [Click Compile] → [Click Upload] → [Enhanced functionality]
```

### 5. Advanced Features

**New Chat Functionality:**
- **🗨️ New Chat button**: Completely clears all conversation history and current code context
- **Fresh Start**: AI forgets all previous interactions and current project
- **Keyboard Shortcut**: **Ctrl+Shift+N** (Windows/Linux) or **Cmd+Shift+N** (Mac)
- **Confirmation**: Asks before clearing to prevent accidental resets
- **Works with both**: Claude and LMStudio providers

**Context Management:**
- **Clear History** (LMStudio only): Clears conversation history but keeps current code context
- **New Chat**: Clears everything for a completely fresh start
- **Code Loading**: Automatically clears LMStudio history when loading new sketch files

**Library Management:**
- AI can suggest libraries needed for your project
- Install libraries through the interface

**Multiple Sketches:**
- Change the sketch name before compiling
- Organize different projects and experiments

**Serial Monitoring:**
- Auto-refreshes every 3 seconds
- Click "Read Serial" for immediate update
- Useful for debugging and monitoring sensor data

## Supported Boards

**The Vibe Coder automatically detects and displays all boards from your Arduino installation.** Common boards include:

**ESP32 Family:**
- ESP32 Dev Module, ESP32-S2, ESP32-S3, ESP32-C3, etc.

**Arduino Family:**
- Arduino Uno, Nano, Mega, Leonardo
- Arduino MKR series (MKR1000, MKR WiFi 1010, etc.)
- Arduino Nano 33 IoT, Nano 33 BLE

**Teensy Family:**
- Teensy 3.x, 4.0, 4.1, LC

**Other Boards:**
- Any board supported by Arduino CLI cores you have installed

*The board dropdown will show only the boards you have cores installed for, making selection easier and preventing configuration errors.*

## Development Applications

This tool is particularly useful for:

**Iterative Development:**
- Load existing sketches and ask AI to add new features
- AI understands your current code and suggests contextual improvements
- Seamlessly evolve projects from simple prototypes to complex systems
- Get help debugging specific parts of your existing code

**Sensor Integration:**
- Rapid prototyping of accelerometers, pressure sensors, temperature sensors
- Testing sensor fusion and data processing with context-aware suggestions
- Calibrating and testing environmental sensors
- Adding new sensors to existing projects

**Hardware Controllers:**
- Programming multiple microcontrollers for synchronized operation
- High-speed servo and motor control systems with iterative refinement
- Precise timing applications and real-time control
- Upgrading existing control systems with new functionality

**Learning and Development:**
- Learn embedded programming with AI assistance that understands your progress
- Get contextual explanations of your existing code
- Receive suggestions for best practices specific to your current project
- Build confidence through iterative improvement of working code

## API Endpoints

The Vibe Coder server provides these endpoints:

- `GET /api/health` - Check Arduino CLI status
- `GET /api/config` - Get Arduino configuration and sketchbook location
- `GET /api/boards` - List connected boards/ports
- `GET /api/boards/available` - List all available boards from installed cores
- `GET /api/sketches` - List available sketches from local and sketchbook folders
- `GET /api/sketches/:name` - Load a specific sketch
- `POST /api/sketch` - Save Arduino sketch (can save to sketchbook folder)
- `POST /api/compile` - Compile Arduino sketch
- `POST /api/upload` - Upload sketch to board
- `GET /api/monitor/:port` - Read serial output
- `GET /api/libraries` - List installed libraries
- `POST /api/library/install` - Install library
- `POST /api/claude` - Claude AI API proxy
- `POST /api/lmstudio` - LMStudio local LLM proxy
- `GET /api/lmstudio/health` - Test LMStudio connection

## Troubleshooting

### "Arduino CLI not found"
- **If using local method:** Make sure `arduino-cli.exe` is in the same folder as `start.bat`
- **If using PATH method:** Make sure Arduino CLI is installed and in your PATH
- Try double-clicking `arduino-cli.exe` directly to test it
- Restart Command Prompt after PATH changes
- For local method: Right-click `arduino-cli.exe` → Properties → Unblock if downloaded from internet

### "Claude API key issues"
- Make sure your API key starts with `sk-ant-`
- Check that your API key is valid at https://console.anthropic.com/
- Ensure you have sufficient credits in your Anthropic account
- API keys are automatically saved - you only need to enter once
- Use the "Clear" button if you need to enter a new key
- Check browser console for detailed error messages

### "Cannot connect to LMStudio" 
- Make sure LMStudio is running and shows "Server online"
- Verify LMStudio server is on port 1234 (default)
- Check that "Cross-Origin-Requests" is enabled in LMStudio
- Ensure a model is loaded in LMStudio (you should see memory usage)
- Try restarting LMStudio if connection fails
- Check Windows Firewall isn't blocking localhost connections
- **Debug steps**: Open browser console (F12) and look for error messages when sending messages

### "LMStudio not sending messages"
- **Check browser console (F12)**: Look for debug messages starting with 🤖, 📤, 📨, ✅, or ❌
- Verify LMStudio shows incoming requests in its log
- Make sure the model is loaded and responding in LMStudio
- Try sending a simple test message first: "Hello"
- Check that LMStudio isn't overloaded or out of memory
- **Arduino Vibe Coder automatically includes**: current code context, board selection, and conversation history in LMStudio prompts
- Make sure you have enough RAM for the model size
- 7B models need ~8GB RAM, 13B models need ~16GB RAM
- Try a smaller model if you're running out of memory
- Enable GPU acceleration in LMStudio if you have a compatible GPU
- Some models work better than others for code generation
- **Arduino Vibe Coder automatically maintains conversation history for LMStudio** - the AI will remember your previous code and questions
- If the AI seems to lose context, try asking more specific questions or referencing the current code explicitly

### "API request failed" errors
- **Claude:** 401 error = Invalid API key, 429 error = Rate limit exceeded
- **LMStudio:** 503 error = LMStudio not running or model not loaded
- Network errors: Check your internet connection (Claude) or LMStudio status
- If switching between providers, try refreshing the page

### "No boards detected"
- Check USB cable connection
- Install proper drivers for your board
- Click "Refresh Ports" button
- For ESP32: Install CP210x or CH340 drivers

### "No boards in dropdown" or "Loading boards..."
- Make sure you have Arduino cores installed: `arduino-cli core list`
- Install cores for your boards (see configuration section above)
- Check the browser console for error messages
- The dropdown will show "Loading boards..." until it gets a response from Arduino CLI

### "Compilation failed"
- Check that the correct core is installed
- Ask AI to fix the code based on error messages
- Verify board selection matches your hardware

### "Upload failed"
- Ensure correct port is selected
- Check that board is not running other serial programs
- Try pressing reset button during upload
- For ESP32: Hold BOOT button during upload if needed

### "Can't connect to localhost:3000"
- Make sure the server is actually running (you should see "Server running on http://localhost:3000")
- Check for error messages when running `start.bat`
- Try running `node server.js` directly to see detailed error messages
- Make sure port 3000 isn't being used by another program
- Check Windows Firewall isn't blocking the connection

## Development

### Adding New Boards

Edit `public/index.html` and add options to the board-select dropdown:

```html
<option value="your:board:fqbn">Your Board Name</option>
```

### Customizing the Interface

- **Colors/Styling:** Edit the CSS in `public/index.html`
- **Board Presets:** Modify the board dropdown options
- **Serial Settings:** Adjust baud rates and timeouts in the JavaScript

### AI Integration

The system supports both Claude and LMStudio APIs:

**Claude Integration:**
- Uses Anthropic's Claude API via the `/api/claude` endpoint
- Requires valid API key from console.anthropic.com
- Supports streaming responses and context awareness

**LMStudio Integration:**
- Uses OpenAI-compatible API format via the `/api/lmstudio` endpoint  
- Connects to localhost:1234 by default
- No API key required for local access
- Supports any model loaded in LMStudio

## File Structure

```
arduino-vibe-coder/
├── arduino-cli.exe       # Arduino CLI executable (download separately)
├── server.js            # Main server with AI integration
├── package.json         # Dependencies and project info
├── start.bat           # Start the server
├── public/
│   └── index.html      # Web frontend with dual AI support
├── sketches/           # Generated Arduino sketches
└── README.md          # This file
```

## Security Notes

**API Key Handling:**
- Claude API keys are saved to your browser's localStorage for convenience
- Keys persist between sessions (no need to re-enter each time)
- Use the "Clear" button to remove your saved key when needed
- The input field is password-masked for security
- Keys are stored locally on your machine only
- Never share your API key with others

**LMStudio Security:**
- LMStudio runs completely locally on your machine
- No data is sent to external servers when using LMStudio
- Models and conversations stay on your local machine
- No internet connection required for LMStudio operation

**Network Security:**
- Claude API calls use HTTPS encryption
- The Vibe Coder server runs locally on your machine
- No data is sent to third-party servers except when using Claude API
- Your code and projects remain on your local machine

## Safety Notes

**For Embedded Development:**
- Always test code in safe environments before deploying to production
- Use proper isolation and protection for high-voltage or high-current applications
- Follow standard electrical safety practices and component ratings
- This tool is for development and prototyping - production systems should have additional safety layers and testing
- Be mindful of proper power supply design and thermal considerations

**For AI-Generated Code:**
- Always review AI-generated code before uploading to hardware
- Test in safe conditions before connecting to real-world systems
- AI can make mistakes - use your engineering judgment
- Consider safety implications of AI suggestions
- Both Claude and local LLMs can generate imperfect code

## License

MIT License - See LICENSE file for details

## Contributing

This is an open-source tool designed for Arduino developers of all kinds. Feel free to fork, contribute improvements, and adapt for your specific needs!

Potential areas for contribution:
- Additional AI provider support
- Improved UI/UX
- Library management features
- Serial plotter functionality
- Model optimization for LMStudio
- Better error handling and recovery

## Support

For issues with this tool, check the troubleshooting section above. For Arduino CLI issues, see the official Arduino CLI documentation. For LMStudio issues, check the LMStudio documentation at https://lmstudio.ai/.

**Community:**
- Report bugs and request features via GitHub issues
- Share your Arduino projects and AI experiences
- Help improve the tool for the maker community
