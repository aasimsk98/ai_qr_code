# AI Embedded QR Code Generator & Decoder
### Project Demonstration

This project's execution is demonstrated in the video link below. Please note that clicking this link will open a new browser tab to Google Drive.

[Watch the AI QR Code Demo](https://drive.google.com/file/d/15KHvETasldRZKeida2b3uT-B8t9WD5w4)

---
This project delivers a unique solution for QR code creation, blending standard QR generation with advanced **Stable Diffusion (SD)** and **ControlNet** image synthesis. It allows users to generate fully scannable QR codes embedded within high-fidelity, artistic backgrounds dictated by a text prompt.

---

## Tech Stack

* Python
* Streamlit (for the interactive web UI and deployment)
* Stable Diffusion WebUI API (as the core AI backend service)
* ControlNet (for maintaining QR structure during image generation)
* qrcode (for standard QR code generation)
* pyzbar (for decoding QR codes from images)
* Pillow (PIL) (for image handling and manipulation)
* requests (for communicating with the local AI API endpoint)

---

## Repository Structure

* `app.py`: The main **Streamlit** application. It handles the UI, standard QR generation/decoding, and orchestrates the AI generation workflow.
* `controlnet.py`: The **AI API Wrapper**. It defines the class responsible for building the **JSON payload**, Base64-encoding the QR image, and communicating with the Stable Diffusion WebUI API.
* `utils.py`: The **Parameter Utility**. Contains the logic to generate all possible **permutations** of user-input parameters, which accelerates ML model testing.
* `requirements.txt`: A list of all necessary Python libraries (Streamlit, qrcode, pyzbar, requests, etc.) required to run the project.
* `.gitignore`: Instructs Git to ignore local output files (`/images`) and large model files (`*.safetensors`, `*.ckpt`) which are external dependencies.
* `README.md`: This documentation file, containing the project overview, setup guide, and technical details.
---

## Project Structure and Dependencies

The project is split into two main components that run concurrently:

1.  **AI Backend (External):** Stable Diffusion WebUI (Automatic1111) — hosts the ControlNet model and handles image synthesis.
2.  **Web App (This Repository):** Contains the Streamlit frontend, Python logic (`app.py`), and the custom API wrapper (`controlnet.py`).

### Step 1: Clone the Application Repository

Start by cloning this repository, which contains the Streamlit frontend and custom Python logic:

```bash
git clone https://github.com/aasimsk98/ai_qr_code
cd ai_qr_code
```
### Step 2: Install Python DependenciesInstall the required libraries for the Streamlit application:
```Bash
pip install -r requirements.txt
```
### Step 3: Set Up the AI Backend (Automatic1111)This project requires a pre-installed Stable Diffusion WebUI (Automatic1111) running on your local machine.

**A. Install the ControlNet Extension**
1. Open your Stable Diffusion WebUI in your browser.
2. Navigate to the Extensions tab -> Install from URL.
3. Paste the following GitHub URL and click Install:
    
    ControlNet URL: https://github.com/Mikubill/sd-webui-controlnet

4. Go to the Installed tab and click Apply and restart UI.

**B. Download and Install Required AI Models**

You need two model files to enable the artistic QR code feature. Place them in the correct directories within your Automatic1111 installation (`[sd.webui]`).

| Model Type | Download Source | Placement Path |
| :--- | :--- | :--- |
| **ControlNet QR** | [monster-labs/control\_v1p\_sd15\_qrcode\_monster](https://huggingface.co/monster-labs/control-v1p-sd15-qrcode-monster/tree/main) (Download `.safetensors` and `.yaml` files) | `[sd.webui]/extensions/sd-webui-controlnet/models/` |
| **SD Checkpoint** | [ICBINP Mid 2024](https://civitai.com/models/193213/icbinp-i-cant-believe-its-not-photography-mid-2024) | `[sd.webui]/models/Stable-diffusion/` |

### Step 4: Run the AI API Backend
The WebUI must be launched with the API enabled. Ensure the --api argument is set in your webui-user.bat file (as configured), and then execute the run script:
1. Navigate to your [sd.webui] folder.
2. Execute your local run script:
```Bash
run.bat
```
Wait for the API to initialize successfully, confirming it is running on http://127.0.0.1:7860.
### Step 5: Run the Streamlit Application
In a separate terminal (leave the WebUI running), navigate back to the ai_qr_code/ directory and launch the frontend:
```Bash
streamlit run app.py
```
 The application will open in your browser.