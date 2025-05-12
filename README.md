<h1 align="center">📄 Document Scanner with ML Kit on Android</h1>

<p align="center">
  <a href="https://opensource.org/licenses/Apache-2.0">
    <img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-blue.svg"/>
  </a>
  <a href="https://android-arsenal.com/api?level=21">
    <img alt="API" src="https://img.shields.io/badge/API-21%2B-brightgreen.svg"/>
  </a>
</p>

<p align="center">  
Easily integrate Google's ML Kit Document Scanner API into your Android app. This project offers a clean implementation, usage guide, and customization options for a seamless document scanning experience.
</p>

---

## ✨ Preview

<p align="center">
  <img src="https://github.com/shubhanshu24510/CameraX/assets/100926922/8c2bcf8b-00fa-43a1-984f-2d8e422656b8" height="600"/>
</p>

---

## 🧪 Example Results

<p align="center">
  <img src="https://github.com/shubhanshu24510/CameraX/assets/100926922/1da7df99-49d7-4780-9089-6d44e3f55a48" height="500"/>
  <img src="https://github.com/shubhanshu24510/CameraX/assets/100926922/79feaca2-7cb8-446d-a976-9d1031c81d3a" height="500"/>
  <img src="https://github.com/shubhanshu24510/CameraX/assets/100926922/2659d5a4-b966-49e0-8f2f-5a9c22938b2e" height="500"/>
  <img src="https://github.com/shubhanshu24510/CameraX/assets/100926922/daea3d9a-9a5b-4ba3-a4b3-ad65a1dc63e8" height="500"/>
</p>

---

## 🔍 Feature Overview

| Feature | Description |
|--------|-------------|
| 📦 SDK | `play-services-mlkit-document-scanner` |
| 📥 Download Size | ~300KB |
| ⚡ Initialization | Slight delay on first use (models/UI are downloaded) |
| 🔧 Customization | Gallery import, page limits, scanner modes |

---

## 🧰 Tech Stack & Requirements

- **Minimum SDK**: 21+
- **Dependencies**:
  - Google Maven repository required in `build.gradle`
  - Kotlin + AndroidX + ML Kit Scanner

---

### 📦Installation
Add the dependency for the ML Kit document scanner library to your module's app-level build.gradle file:
```cmd
dependencies {
    // ...
    implementation 'com.google.android.gms:play-services-mlkit-document-scanner:16.0.0-beta1'
}

```
### ⚙️Configuration
Customize the document scanner options:
  
```cmd
 val options = GmsDocumentScannerOptions.Builder()
    .setGalleryImportAllowed(false)
    .setPageLimit(2)
    .setResultFormats(RESULT_FORMAT_JPEG, RESULT_FORMAT_PDF)
    .setScannerMode(SCANNER_MODE_FULL)
    .build()

```

### 📸 Start Scanning

```cmd
val scanner = GmsDocumentScanning.getClient(options)
val scannerLauncher = registerForActivityResult(StartIntentSenderForResult()) { result ->
    if (result.resultCode == RESULT_OK) {
        val result = GmsDocumentScanningResult.fromActivityResultIntent(result.data)
        result.getPages()?.let { pages ->
            for (page in pages) {
                val imageUri = pages.get(0).getImageUri()
            }
        }
        result.getPdf()?.let { pdf ->
            val pdfUri = pdf.getUri()
            val pageCount = pdf.getPageCount()
        }
    }
}

scanner.getStartScanIntent(activity)
    .addOnSuccessListener { intentSender ->
        scannerLauncher.launch(IntentSenderRequest.Builder(intentSender).build())
    }
    .addOnFailureListener { exception ->
        // Handle failure
    }

```

## 🧱 Architecture Overview

- Clean MVVM architecture with unidirectional data flow.
- Loosely coupled layers for easy testing and scalability.
- UI communicates with ViewModel → ViewModel fetches data via Repository.

### 🧩 UI Layer
![UI Layer](https://github.com/user-attachments/assets/80d123e6-e72b-4ca8-998b-a9edec78ae19)

- ViewModel + DataBinding
- Uses Bindables for two-way data binding.
- Configuration changes are gracefully handled.

### 🔄 Data Layer
![Data Layer](https://github.com/user-attachments/assets/0bdebc42-69a1-41a2-ad8f-d57d3cbf9124)

- Offline-first using Room
- Repository pattern ensures single source of truth
- Clean separation between local and external sources
- Repositories handle business logic and act as single source of truth.
- Offline-first design using local caching and potential future cloud integration.

### 📐 Architecture Diagram
![Overall Architecture](https://github.com/user-attachments/assets/29f555f6-2339-40dc-899c-79835b0c7fb7)

More on modularization: [Google Guide](https://developer.android.com/topic/modularization)
---

### ✅ MAD Score
<p align="center"> <img src="https://user-images.githubusercontent.com/24237865/102366914-84f6b000-3ffc-11eb-8d49-b20694239782.png" height="300"/> <img src="https://user-images.githubusercontent.com/24237865/102366932-8a53fa80-3ffc-11eb-8131-fd6745a6f079.png" height="300"/> </p>

### 🧾 Conclusion
By integrating ML Kit's Document Scanner, your app gains a seamless, native scanning experience powered by Google Play services. With flexible configuration and minimal setup, you can deliver high-quality scanning to your users.

---

## 🤝 Support

If you like this project, please consider ⭐ starring the repo and following me for more cool Android projects!

☕ You can also support my work by buying me a coffee:

<p align="left">
  <a href="https://buymeacoffee.com/shubhanshu24510" target="_blank">
    <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" height="60" width="217">
  </a>
</p>

---

👨‍💻 Follow @shubhanshu24510 for more cool projects
Copyright 2025 Shubhanshu Singh

### 📄 License

Licensed under the Apache License, Version 2.0
http://www.apache.org/licenses/LICENSE-2.0

