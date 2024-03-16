<h1 align="center">Document Scanner with ML Kit on Android
</h1>

<p align="center">
  <a href="https://opensource.org/licenses/Apache-2.0"><img alt="License" ![mode_base](https://github.com/shubhanshu24510/CameraX/assets/100926922/7d2a2479-41ed-4b73-b92d-486275f5c4f9)
src="https://img.shields.io/badge/License-Apache%202.0-blue.svg"/></a>
  <a href="https://android-arsenal.com/api?level=21"><img alt="API" src="https://img.shields.io/badge/API-21%2B-brightgreen.svg?style=flat"/></a>
</p>

<p align="center">  
Integrate the ML Kit document scanner API into  Android app to effortlessly add a document scanning feature. This guide provides details on implementation, usage, and customization options for the document scanner.
</p>
</br>

### Preview

![Untitled design (1)](https://github.com/shubhanshu24510/CameraX/assets/100926922/8c2bcf8b-00fa-43a1-984f-2d8e422656b8)

### Examplae Result

![Screenshot (257)](https://github.com/shubhanshu24510/CameraX/assets/100926922/1da7df99-49d7-4780-9089-6d44e3f55a48)
![Screenshot (260)](https://github.com/shubhanshu24510/CameraX/assets/100926922/79feaca2-7cb8-446d-a976-9d1031c81d3a)
![Screenshot (259)](https://github.com/shubhanshu24510/CameraX/assets/100926922/2659d5a4-b966-49e0-8f2f-5a9c22938b2e)
![Screenshot (258)](https://github.com/shubhanshu24510/CameraX/assets/100926922/daea3d9a-9a5b-4ba3-a4b3-ad65a1dc63e8)

### Feature Details
SDK Name: play-services-mlkit-document-scanner
Implementation: Models, scanning logic, and UI flow are dynamically downloaded by Google Play services.
App Size Impact: Approximately 300KB download size increase.
Initialization Time: Users may experience a brief delay as models, logic, and UI flow are downloaded before first use.

### Tech stack & Open-source libraries
Before You Begin
Ensure that your Android app meets the following requirements:

- Minimum SDK Version: Android API level 21 or above.
- In your project-level build.gradle file, include Google's Maven repository in both buildscript and allprojects sections.

### Installation
Add the dependency for the ML Kit document scanner library to your module's app-level build.gradle file:
```cmd
dependencies {
    // ...
    implementation 'com.google.android.gms:play-services-mlkit-document-scanner:16.0.0-beta1'
}

```
### Document Scanner Configuration
Customize the document scanner user flow according to your app's requirements. The provided viewfinder and preview screen support various controls such as:

- Importing from the photo gallery
- Setting a limit to the number of pages scanned
- Scanner mode (to control feature sets in the flow)
- Instantiate GmsDocumentScannerOptions to configure the scanner options:
  
```cmd
 val options = GmsDocumentScannerOptions.Builder()
    .setGalleryImportAllowed(false)
    .setPageLimit(2)
    .setResultFormats(RESULT_FORMAT_JPEG, RESULT_FORMAT_PDF)
    .setScannerMode(SCANNER_MODE_FULL)
    .build()

```

### Scan Documents
After configuring your GmsDocumentScannerOptions, obtain an instance of GmsDocumentScanner. You can then start the scanner activity following AndroidX Activity Result APIs.

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


### Architecture Overview

 ![figure1](https://github.com/shubhanshu24510/CameraX/assets/100926922/e51a219d-cb16-4a5b-8eb4-f01cc80fbdbd)
 
- Each layer follows [unidirectional event/data flow](https://developer.android.com/topic/architecture/ui-layer#udf); the UI layer emits user events to the data layer, and the data layer exposes data as a stream to other layers.
- The data layer is designed to work independently from other layers and must be pure, which means it doesn't have any dependencies on the other layers.

With this loosely coupled architecture, you can increase the reusability of components and scalability of your app.

### UI Layer

![architecture](figure/figure2.![figure2](https://github.com/shubhanshu24510/CameraX/assets/100926922/8a92c457-bdfd-4e95-857f-59cb0dce98b9)
png)

The UI layer consists of UI elements to configure screens that could interact with users and [ViewModel](https://developer.android.com/topic/libraries/architecture/viewmodel) that holds app states and restores data when configuration changes.
- UI elements observe the data flow via [DataBinding](https://developer.android.com/topic/libraries/data-binding), which is the most essential part of the MVVM architecture. 
- With [Bindables](https://github.com/skydoves/bindables), which is an Android DataBinding kit for notifying data changes, you can implement two-way binding, and data observation in XML very clean.

### Data Layer
![figure3](https://github.com/shubhanshu24510/CameraX/assets/100926922/a8bcbac0-18eb-403a-8d03-bb5ae2847d1e)

The data Layer consists of repositories, which include business logic, such as querying data from the local database and requesting remote data from the network. It is implemented as an offline-first source of business logic and follows the [single source of truth](https://en.wikipedia.org/wiki/Single_source_of_truth) principle.<br>

### Conclusion
Integrating the ML Kit document scanner API enhances your app's functionality by providing users with a seamless document scanning experience. Experiment with the provided features and customize the scanner to meet your app's specific needs.


This README content is based on the provided documentation for integrating the ML Kit document scanner API on Android. Adjustments can be made based on specific project requirements and preferences.

## MAD Score
![summary](https://user-images.githubusercontent.com/24237865/102366914-84f6b000-3ffc-11eb-8d49-b20694239782.png)
![kotlin](https://user-images.githubusercontent.com/24237865/102366932-8a53fa80-3ffc-11eb-8131-fd6745a6f079.png)


## Find this repository useful? :heart:
Support it by joining __([(https://github.com/shubhanshu24510/CameraX])__ for this repository. :star: <br>
Also, __[follow me]__([https://github.com/shubhanshu24510])__ on GitHub for my next creations! 🤩
