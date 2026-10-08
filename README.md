
# 📖 ЧитајЛесно | ReadEasy

### AI-Powered Reading Assistance for Children with Dyslexia

**ЧитајЛесно (ReadEasy)** is a Flutter-based mobile application designed to support children with dyslexia when reading and understanding texts in the Macedonian language.

The application combines accessibility-focused reading tools, Optical Character Recognition (OCR), Text-to-Speech (TTS), artificial intelligence, and cloud-based user data management.

Its main objective is to provide multiple ways of interacting with written content, allowing users to read, listen to, scan, simplify, and organize texts according to their individual needs.

The project also incorporates research into automatic text simplification using Large Language Models (LLMs), with a particular focus on processing Macedonian-language educational content.

---

## ✨ Key Features

### 📷 Optical Character Recognition (OCR)

The application integrates **Tesseract OCR** to extract digital text from images and documents.

- Capture text using the device camera.
- Select images from the device.
- Extract text from supported documents.
- Recognize Macedonian Cyrillic text.
- Review and edit recognized text.
- Use extracted content with other reading tools.

OCR enables users to work with printed educational materials without manually retyping their contents.

Recognition accuracy depends on image quality, lighting, document layout, and text clarity.

### 🔊 Text-to-Speech (TTS)

The application integrates **Microsoft Azure AI Speech** to convert written Macedonian text into spoken audio.

Main capabilities include:

- Audio playback of written text.
- Adjustable reading speed.
- Playback controls.
- Auditory support alongside visual reading.
- Speech generation using Azure Speech services.

TTS provides an additional way to access written information and can be combined with visual reading assistance.

### 🤖 AI-Powered Text Simplification

ЧитајЛесно includes an AI-powered text simplification feature designed to transform complex Macedonian text into a more accessible form.

The system aims to:

- Replace difficult vocabulary with simpler alternatives.
- Simplify complex sentence structures.
- Divide long sentences when appropriate.
- Preserve essential information.
- Maintain the original meaning.
- Produce natural and grammatically appropriate Macedonian text.

The simplification service is implemented using a **Python FastAPI backend** and the **Domestic-Yak-8B-Instruct** language model.

The application sends text to the backend, which processes the request and returns a simplified version.

AI-generated content should be reviewed when accuracy is important. Automatic simplification does not guarantee that every detail will be preserved correctly.

### 🎨 Reading Accessibility Tools

The application provides customizable reading settings, including:

- Adjustable text size.
- Font selection.
- Alternative visual themes.
- Reading ruler for following lines of text.
- Customizable reading presentation.
- Personalized reading preferences.

These options allow users to adapt the reading experience to their individual preferences.

No single font, color scheme, or visual setting is assumed to work equally well for every person with dyslexia.

### 👤 User Authentication and Profiles

Firebase Authentication is used to manage user accounts and authentication.

The application supports user-specific reading activity and preferences.

### 📚 Saved Texts

Users can save previously accessed texts and return to them later.

Saved content is associated with the authenticated user and synchronized using Firebase Cloud Firestore.

### 📈 Reading Activity and Progress

The application includes functionality for monitoring reading-related activity.

It provides an interface for viewing progress, daily reading goals, and achievements.

This feature is intended to encourage regular engagement with reading materials.

---

## 🛠️ Technology Stack

### Mobile Application

**Flutter & Dart**

Flutter is the primary framework used to develop the mobile application.

It handles:

- User interface rendering.
- Screen navigation.
- User interaction.
- Reading customization.
- Application state.
- Integration with external services.

The Dart programming language is used for the application logic.

### Backend

**Python & FastAPI**

FastAPI provides the REST API used for automatic text simplification.

The backend handles:

- Incoming HTTP requests.
- Request validation.
- Optional API authentication.
- Language model initialization.
- Text simplification inference.
- Structured JSON responses.
- Error handling.

### Artificial Intelligence

**Domestic-Yak-8B-Instruct**

The AI simplification component uses:

`LVSTCK/domestic-yak-8B-instruct`

Domestic-Yak is a language model developed with a particular focus on Macedonian-language processing.

The implementation uses Hugging Face Transformers and supports 4-bit model quantization with BitsAndBytes.

### Optical Character Recognition

**Tesseract OCR**

Tesseract is used for extracting digital text from images.

The application includes OCR language resources for Macedonian Cyrillic recognition.

### Speech Synthesis

**Microsoft Azure AI Speech**

Azure Text-to-Speech is integrated for generating spoken audio from written text.

The application uses HTTP communication and an audio playback component.

### Firebase Services

**Firebase Authentication**

Provides account authentication and user identity management.

**Cloud Firestore**

Stores and synchronizes user-related data.

**Firestore Security Rules**

Define access restrictions for user data.

### Additional Libraries

The Flutter project also uses packages including:

- `provider` — application state management.
- `http` — HTTP communication.
- `audioplayers` — audio playback.
- `flutter_dotenv` — local configuration loading.
- `image_picker` — image selection and capture.
- `file_picker` — document selection.
- `hive_flutter` — local storage support.
- `shared_preferences` — local preferences.
- `sqflite` — SQLite database support.
- `syncfusion_flutter_pdf` — PDF processing support.
- `tesseract_ocr` — OCR integration.

For the exact package versions, refer to `pubspec.yaml` and `pubspec.lock`.

---

## 🏗️ System Architecture

The application is organized around a Flutter frontend, Firebase cloud services, OCR and speech-processing components, and a separate AI simplification backend.

### High-Level Architecture

```text
                  USER
                   |
                   v
          FLUTTER MOBILE APP
                   |
       +-----------+-----------+
       |           |           |
       v           v           v
   Tesseract     Azure      Firebase
     OCR          TTS        Services
       |           |           |
       v           v           v
  Extracted      Audio     Authentication
    Text        Playback   and Firestore
       |
       v
   Reading Interface
       |
       v
  Simplify Text Request
       |
       v
   Python FastAPI Backend
       |
       v
   Domestic-Yak-8B-Instruct
       |
       v
  Simplified Macedonian Text
       |
       v
   Flutter Application
```

### Architectural Responsibilities

**Flutter frontend**

Responsible for user interaction, reading tools, text display, and communication with external services.

**Firebase**

Responsible for authentication and cloud-based user data storage.

**OCR processing**

Converts text from images into editable digital text.

**Azure TTS**

Provides speech synthesis for the application's listening functionality.

**FastAPI backend**

Receives simplification requests and communicates with the language model.

**Domestic-Yak**

Generates simplified Macedonian-language text.

The architecture separates the mobile user interface from the computationally demanding AI inference process.

---

## 🔄 Text Processing Workflow

### Step 1 — Text Input

Users provide text by typing, pasting, scanning, or selecting supported content.

### Step 2 — OCR Processing

When an image is selected, Tesseract OCR processes it and extracts recognizable text.

The extracted text is displayed for review.

### Step 3 — Reading Interface

The text is displayed in the reading interface.

Users can customize visual settings and access additional reading tools.

### Step 4 — Speech Synthesis

When the listening function is activated, the application uses Azure Speech to generate audio from the text.

The generated audio is played through the application.

### Step 5 — AI Simplification

When text simplification is requested, the Flutter application sends an HTTP request to the FastAPI backend.

The backend validates the request and invokes Domestic-Yak.

The generated result is returned in JSON format.

### Step 6 — Result Display

The application displays the simplified text, allowing the user to continue reading or interacting with the content.

---

## 🤖 AI Text Simplification Backend

The backend is located in:

`backend/`

It is implemented using Python and FastAPI.

### Simplification Endpoint

```http
POST /v1/simplify
```

The endpoint receives text and the parameters required for simplification.

The backend communicates with Domestic-Yak and returns a JSON response containing the generated text.

### Example Successful Response

```json
{
  "simplified_text": "..."
}
```

### Model Configuration

The backend is designed to load the following model:

`LVSTCK/domestic-yak-8B-instruct`

The implementation uses:

- Hugging Face Transformers.
- PyTorch.
- BitsAndBytes.
- 4-bit NF4 quantization.
- FP16 computation.
- Double quantization.

Model weights are loaded when the service starts and retained in memory for subsequent requests.

### Model Execution Requirements

Actual model inference requires a compatible NVIDIA CUDA GPU environment.

Approximately 8–10 GB of GPU memory may be needed for the quantized model, with additional capacity recommended.

The API supports a model-disabled mode for validation testing.

**Important:** Successful real-model inference and complete end-to-end operation must be verified on the target GPU deployment environment. Passing API validation tests alone does not establish that the model is production-ready.

For complete backend documentation, see:

[Backend README](backend/README.md)

---

## 🔊 Azure Text-to-Speech Configuration

The application uses Microsoft Azure AI Speech for text-to-speech functionality.

Azure configuration is required to enable speech generation.

### 1. Create an Azure Speech Resource

1. Visit the [Microsoft Azure Portal](https://portal.azure.com/).
2. Sign in with a Microsoft account.
3. Create an Azure AI Speech resource.
4. Select the appropriate subscription and resource group.
5. Choose an available Azure region.
6. Configure the resource according to your requirements.
7. Complete resource creation.

Azure usage may be subject to service quotas and billing.

### 2. Obtain Speech Credentials

Open the created Speech resource in Azure Portal.

Find the resource's keys and region information.

The Flutter application currently expects the following configuration variables:

```env
AZURE_TTS_API_KEY=
AZURE_TTS_REGION=
```

Use the values associated with your own Azure Speech resource.

Never place real credentials in a public repository.

### 3. Configure Local Environment

In the root directory of the Flutter project, copy:

`.env.example`

to:

`.env`

On Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Then configure your local values:

```env
AZURE_TTS_API_KEY=YOUR_AZURE_SPEECH_KEY
AZURE_TTS_REGION=YOUR_AZURE_REGION
```

Replace the placeholders with credentials from your Azure resource.

### 4. How Azure TTS Works

The Flutter application uses its TTS implementation to communicate with Azure Speech.

The general process is:

1. The user opens text in the application.
2. The user activates the listening function.
3. The application prepares the text for speech synthesis.
4. The Azure Speech service processes the request.
5. The resulting audio is received by the application.
6. The audio playback component reproduces the generated speech.

The application provides reading-speed adjustments through its TTS functionality.

### 5. Important Security Limitation

**The current Azure TTS integration is intended for controlled development and testing, not secure distribution with an embedded production key.**

The Flutter configuration currently includes `.env` as an application asset in `pubspec.yaml`.

This means that `.env` values are included in the compiled application package.

A person with access to an APK may be able to extract the Azure API key.

Therefore:

- Never commit your real Azure API key.
- Never publish an APK containing a real Azure key.
- Use temporary, limited, and replaceable credentials for local development.
- Rotate credentials if exposure is suspected.
- Monitor Azure resource usage.

Ignoring `.env` in Git protects it from accidental source-code commits, but does not protect credentials embedded in a compiled mobile application.

### Recommended Production Architecture

For production deployment, Azure credentials should remain on a secure server.

The recommended architecture is:

```text
Flutter Application
        |
        v
Authenticated Backend API
        |
        v
Azure Speech Service
        |
        v
Generated Audio
        |
        v
Flutter Audio Playback
```

In this architecture, the backend communicates with Azure, and the mobile application does not directly store the Azure Speech subscription key.

**This is a recommended future security improvement, not a description of the current implementation.**

More information:

[Azure AI Speech Documentation](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/)

---

## 🔥 Firebase Configuration

Firebase provides authentication and cloud-based data management.

The project includes:

```text
lib/firebase_options.dart
android/app/google-services.json
firestore.rules
firestore.indexes.json
firebase.json
```

### Firebase Authentication

Firebase Authentication handles user identity and authenticated access.

### Cloud Firestore

Firestore is used for synchronizing user-related application data.

The application includes account-specific data access controls.

### Firebase Security

Firebase client configuration files identify the Firebase project and are not equivalent to private administrative credentials.

However, Firebase access must be correctly restricted through authentication, authorization, and Firestore security rules.

Never commit:

- Firebase service-account private keys.
- Administrative credentials.
- Private signing keystores.
- `key.properties` containing signing secrets.

### Firestore Rules

Security rules are maintained in:

`firestore.rules`

Database indexes are defined in:

`firestore.indexes.json`

---

## 🚀 Installation and Local Setup

### Prerequisites

Before starting, install:

- Flutter SDK.
- Dart SDK compatible with `^3.9.2`.
- Android Studio or another supported Flutter development environment.
- Android SDK.
- A physical Android device or Android emulator.
- Git.

For AI backend execution, additional Python and GPU dependencies are required.

### 1. Clone the Repository

```bash
git clone https://github.com/spasenoskamarija/dyslexia_app_v2.git
cd dyslexia_app_v2
```

### 2. Install Flutter Dependencies

```bash
flutter pub get
```

### 3. Configure Environment Variables

Copy the environment configuration template.

Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Configure the variables:

```env
# Azure Speech
AZURE_TTS_API_KEY=YOUR_AZURE_KEY
AZURE_TTS_REGION=YOUR_AZURE_REGION

# AI Simplification Backend
TEXT_SIMPLIFY_BASE_URL=http://YOUR_BACKEND_HOST:8000
TEXT_SIMPLIFY_API_KEY=
TEXT_SIMPLIFY_USE_MOCK=false
```

The application must be configured to connect to the appropriate backend environment.

When using a physical phone, the backend hostname must be reachable from that device.

Do not use `localhost` to refer to a backend running on a different computer.

### 4. Verify Flutter Installation

```bash
flutter doctor
```

Resolve any required platform setup issues.

### 5. Run the Application

```bash
flutter run
```

Select a configured device when prompted.

The availability of cloud-based features depends on valid configuration, network connectivity, and the associated external services.

---

## 🐍 Running the FastAPI Backend

The simplification backend is located in:

`backend/`

### Prerequisites

- Python 3.10 or newer.
- Python virtual environment.
- Required Python dependencies.
- CUDA-compatible GPU for real Domestic-Yak inference.

### 1. Open the Backend Directory

```bash
cd backend
```

### 2. Create a Virtual Environment

```bash
python -m venv .venv
```

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Linux/macOS:

```bash
source .venv/bin/activate
```

### 3. Install Dependencies

For a compatible CUDA GPU, install an appropriate PyTorch build following the official PyTorch installation instructions.

Then run:

```bash
pip install -r requirements.txt
```

### 4. Configure Backend Environment

Copy:

`backend/.env.example`

to:

`backend/.env`

Important environment variables include:

```env
HF_TOKEN=
SIMPLIFY_API_KEY=
SIMPLIFY_MODEL_ID=LVSTCK/domestic-yak-8B-instruct
SIMPLIFY_SKIP_MODEL_LOAD=false
```

Additional host and port settings are documented in the backend configuration template.

Environment variables must be loaded into the backend process before startup.

### 5. Start the API

From the `backend/` directory:

```bash
uvicorn app.main:app --host 0.0.0.0 --port 8000
```

### 6. Health Check

The backend exposes:

```http
GET /health
```

Local endpoint:

```text
http://localhost:8000/health
```

### 7. Connect Flutter to FastAPI

In the root Flutter `.env`:

```env
TEXT_SIMPLIFY_BASE_URL=http://YOUR_BACKEND_HOST:8000
TEXT_SIMPLIFY_API_KEY=
TEXT_SIMPLIFY_USE_MOCK=false
```

The base URL should not include `/v1/simplify`.

The application appends the endpoint path when making requests.

If backend authentication is enabled, the Flutter configuration must supply the corresponding value.

**Security note:** A static API key placed in Flutter `.env` is also extractable from a distributed application. It should not be treated as secure client authentication for a public production deployment.

For additional backend-specific configuration, see:

[backend/README.md](backend/README.md)

---

## 📁 Project Structure

```text
dyslexia_app_v2/
|
|-- android/
|   Android platform configuration
|
|-- ios/
|   iOS platform configuration
|
|-- assets/
|   Application assets, fonts and OCR resources
|
|-- backend/
|   Python FastAPI simplification backend
|
|-- firestore_tests/
|   Firebase emulator security-rule tests
|
|-- lib/
|   Flutter application source code
|
|-- test/
|   Flutter tests
|
|-- .env.example
|   Environment configuration template
|
|-- .gitignore
|   Git exclusion rules
|
|-- pubspec.yaml
|   Flutter dependencies and assets
|
|-- pubspec.lock
|   Resolved dependency versions
|
|-- firestore.rules
|   Firestore access-control rules
|
|-- firestore.indexes.json
|   Firestore index configuration
|
|-- firebase.json
|   Firebase project tooling configuration
|
|-- README.md
|   Project documentation
```

---

## 🧪 Testing and Code Quality

The repository includes Flutter tests, backend validation tests, and Firebase security-rule tests.

### Flutter Static Analysis

```bash
flutter analyze
```

### Flutter Tests

```bash
flutter test
```

### Firebase Emulator Tests

The repository includes Firestore security-rule tests.

Node.js and Java are required for the documented emulator workflow.

Install test dependencies:

```bash
npm --prefix firestore_tests install
```

Execute the emulator tests:

```bash
npx firebase-tools@14.27.0 emulators:exec --only "auth,firestore" --project demo-chitajlesno "npm --prefix firestore_tests test"
```

### Backend Validation Tests

Backend tests can run in API-only mode without loading the full AI model.

See `backend/README.md` for the required setup.

These tests validate API behavior and error handling.

They do not replace real GPU inference testing.

---

## ☁️ Firestore Deployment

Firestore rules and indexes are deployed independently from the Flutter application.

The project configuration currently references the following Firebase project:

`dyslexia-app-mk-2026`

Deployment command:

```bash
npx firebase-tools@14.27.0 deploy --only "firestore:rules,firestore:indexes" --project dyslexia-app-mk-2026
```

**Warning:** This command changes cloud database configuration. Use it only if you have the appropriate permissions and intend to deploy the repository's current rules and indexes to that project.

---

## 🔐 Security Considerations

The project interacts with cloud-based authentication, AI processing, speech generation, and user-related data.

Important considerations include:

**Credential management**

Secrets must not be committed to Git or included in published documentation.

**Mobile application secrets**

Flutter assets and client-side application configuration must not be treated as secure secret storage.

**Firebase authorization**

Firestore security rules should restrict access to data according to authenticated user permissions.

**Backend security**

A publicly accessible backend requires appropriate authentication, rate limiting, secure transport, and operational safeguards.

**User privacy**

Text submitted to external services may be processed outside the device.

Production deployment should include suitable privacy disclosures, data-handling safeguards, and consideration of the application's intended use by children.

**AI reliability**

Generated simplifications may contain errors, omissions, or changes in meaning. Important content should be reviewed.

---

## 📊 Research Background

The AI simplification component is based on academic research into automatic text simplification for Macedonian.

The research compared three instruction-tuned language models:

1. Qwen3-4B-Instruct-2507
2. Gemma-3-4B-IT
3. Domestic-Yak-8B-Instruct

The experimental dataset consisted of 40 Macedonian texts divided into four categories of complexity.

Each model processed the complete dataset, producing 120 simplified outputs.

Evaluation considered:

- Structural simplification.
- Semantic similarity.
- Human-rated simplicity.
- Meaning preservation.
- Linguistic naturalness.

The evaluation indicated different strengths across the models.

Domestic-Yak was selected for integration because of its overall balance between meaning preservation, linguistic naturalness, and human evaluation results.

This selection refers to the comparative research results, not a claim that the current backend deployment has passed production readiness testing.

---

## ⚠️ Known Limitations

The application and its integrations have several limitations that should be considered:

- OCR accuracy depends on input image quality and document formatting.
- Azure TTS requires correctly configured credentials and access to the service.
- The current direct Azure integration exposes client-side credential risks in distributed builds.
- Real Domestic-Yak inference requires an appropriately configured GPU environment.
- Language model output may not always preserve every detail of the original text.
- Cloud-based functionality depends on network availability and correct service configuration.
- Cross-platform behavior, including iOS-specific OCR and build compatibility, requires independent validation.

The application is intended as an assistive reading tool, not as a diagnostic or medical system.

---

## 🔮 Future Improvements

Potential areas for further development include:

- Moving Azure TTS requests to a secure backend.
- Production deployment of the AI simplification service.
- Improved OCR accuracy for complex documents.
- Broader compatibility and device testing.
- Performance optimization.
- Additional accessibility customization.
- More extensive usability testing with intended users.
- Stronger production authentication and monitoring.
- Improved offline functionality.

These are future development directions and should not be interpreted as already implemented features.

---

## 🎓 Academic Context

ЧитајЛесно was initially developed as a collaborative student project and subsequently extended through academic research focused on automatic Macedonian text simplification using large language models.

The project brings together mobile application development, natural language processing, accessibility-focused design, and cloud-based services.

The main research objective is to investigate how large language models can assist in making complex Macedonian text easier to read while preserving meaning.

---

## 📚 References and Documentation

- [Flutter Documentation](https://docs.flutter.dev/)
- [Dart Documentation](https://dart.dev/)
- [Firebase Documentation](https://firebase.google.com/docs)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [Tesseract OCR](https://github.com/tesseract-ocr/tesseract)
- [Microsoft Azure AI Speech](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/)
- [Hugging Face Transformers](https://huggingface.co/docs/transformers/)
- [Domestic-Yak Model](https://huggingface.co/LVSTCK/domestic-yak-8B-instruct)
- [International Dyslexia Association](https://dyslexiaida.org/)

---

**ЧитајЛесно — Making Macedonian text more accessible through technology.**
