Base64 PDF Signer
A powerful, browser-based tool designed to seamlessly bridge the gap between Base64-encoded PDF documents and physical hardware signature pads.

This project allows users to preview Base64 PDFs entirely in the browser, send them to a connected signature pad device, and instantly retrieve the digitally signed PDF back as a Base64 string without requiring manual file downloads or complex local setups.

✨ Features
Base64 to PDF Rendering: Instantly convert and preview raw Base64 strings as interactive PDFs.
Drag & Drop Upload: Easily drop a local .pdf file to automatically generate its Base64 equivalent.
Hardware Signature Integration: Natively communicates with local signature pad hardware via WebSockets.
Automated File Bridging: Dynamically saves temporary files to the local disk (d:\) to allow the C++ hardware service to read the PDF.
In-Memory Signed Preview: Once signed, the hardware returns the document as a Base64 string which is instantly converted to a Blob URL and previewed—skipping local disk caching.
Developer Friendly: Automatically logs the final, signed Base64 string directly to the browser console for easy extraction and debugging.
🛠️ Technologies Used
Frontend: HTML5, Vanilla CSS3, Vanilla JavaScript (ES6+).
Communication: WebSockets (ws://) for real-time, bi-directional communication with local hardware services.
Browser APIs:
FileReader API for converting local files to Data URLs.
Blob & URL.createObjectURL() for rendering binary PDF data in <iframe> elements securely.
atob() and Uint8Array for raw Base64 to binary conversion.
🚀 How It Works (Workflow)
Load Document: The user pastes a Base64 string or uploads a PDF.
Preview & Bridge: The browser renders the PDF using a Blob URL. Simultaneously, it connects to a local WebSocket (ws://localhost:1818) to silently decode and save a temporary working copy of the PDF to the local disk.
Initiate Signature: The user clicks "Sign PDF". The browser contacts the signature pad service via a second WebSocket (ws://localhost:2828), passing the temporary file path.
Hardware Interaction: The signature pad UI pops up, allowing the user to sign the document natively.
Receive & Render: Once completed, the signature service sends a BeginAfterSign JSON payload back to the browser. This payload contains the signed PDF as a Base64 string.
Final Output: The browser logs the string to the console and dynamically updates the iframe to show the final, signed document.
⚙️ System Requirements
To fully utilize the hardware signing capabilities, the host machine must be running the following local services:

Camera/File Service: Listening on ws://localhost:1818 (Handles Base64Decode commands for file bridging).
Signature Pad Service: Listening on ws://localhost:2828 (Handles TouchSign commands and returns the BeginAfterSign payload).
📄 Usage
Simply open base64_pdf_Signerr.html in any modern web browser. No external dependencies, Node.js servers, or build steps are required for the frontend interface.

html
<!-- Example of the core WebSocket initialization used in the project -->
var webSocket1 = new WebSocket('ws://localhost:1818');
var webSocket = new WebSocket('ws://localhost:2828');
📝 License
This project is proprietary and intended for integration with specific banking/fintech hardware terminals.
