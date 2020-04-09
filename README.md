## Team Roster

### Samuel Martinez
  
[![GitHub](github.png)](https://github.com/semartinez147)  [![LinkedIn](linkedin.png)](https://linkedin.com/in/semartinez147)

--- 
 
### Trace Decker

[![GitHub](github.png)](https://github.com/TraceDecker/)  [![LinkedIn](linkedin.png)](https://www.linkedin.com/in/trace-decker-cohort9/)

---
 
### Abby Reyes

[![GitHub](github.png)](https://github.com/mabbyreyes/)  [![LinkedIn](linkedin.png)](https://www.linkedin.com/in/maritzaareyes/)

---
  
### Jawid Mohammadi

[![GitHub](github.png)](https://github.com/Jawidmohammadi/)  [![LinkedIn](linkedin.png)](https://www.linkedin.com/in/jawid-mohammadi/)

---

---

## Description

Scavengr is an augmented reality scavenger hunt app that uses QR codes and/or NFC tags to display multimedia hints with or without wireless service.  

QR codes are simple images that phone cameras can easily identify, even from a distance, in low light, or at an angle.  NFC tags require physical contact with the phone (i.e. Apple Pay), but they are inexpensive, can be easily embedded in physical objects, and can be written/rewritten by most Android devices.  

Users in the Organizer role can set up new hunts easily and quickly with default QR templates, or expand them using NFC tags embedded in real-world objects.  

Hunter users will be able to start a hunt by using a public link or accepting a private invitation.  Scavengr will track hunt progress and publish completion times.

---

## Intended users

* Teachers with an interest in active learning.
* Youth group leaders who need new activities.
* Museum, zoo, aquarium staff developing interactive experiences for guests.
* Parents who want their kids to be familiar with technology but still physically & mentally active.

Scavengr hunts are a creative and low cost activity that can be easily tailored to any group and age.  They can facilitate active learning in museums, classrooms and other spaces, guide a night on the town, or take explorers out into the wilderness.  QR and NFC tags are inexpensive and can be set up unobtrusively in public spaces like parks, malls or urban areas.


### [User Stories](user_stories.md)

---

## Client-side functionality

### Organizer profile

The Organizer will be provided with a default list of QR codes that can be easily printed, and given the option to replace any clue with an NFC tag (BYO NFC).  They will assign a hint (any format of media, either uploaded or linked by url) to each clue, and generate a scavenger hunt link that can be shared by email, text, QR or NFC.  This can be done before or after placing the QR/NFC clues along the path of the hunt.

The Organizer will choose an access level, either open to any user with the hunt link, or closed to invited users only.

### Hunter profile

Hunters will either hunt online, passing QR and NFC info to the server and receiving hints back, or hunt offline, with all data stored on the device.  Online hunting will require wireless service but use very little storage, while offline hunting will need to store files locally but will be independent of wireless service.

When a Hunter begins a hunt, they will be presented with the first hint, and a timer will start.  When the app receives the NFC or QR data from the first clue, it will display the  hint to the second clue, and so on.  When the final clue is scanned, the Hunter will have an option to add their name and time to a leaderboard for the hunt.


## Server-side functionality

The Scavengr server will maintain hunt details including clue/hint associations, clue media files, and leaderboards.  Access will be managed by OAuth, and each hunt will be the property of its Organizer.  Private hunts will only be visible to profiles authorized (through OAuth) by the Organizer.

Hunters will have the option of downloading any hunt they have access to for offline use.

---

## Current State of the App

Scavengr's server is able to handle HTTP requests, but does not restrict user permissions. 
We were unable to successfully implement a Preload Launcher, so data is being manually added through Postman.

The client app has a local database, as well as service classes that interact with the server and 
local entities to download and upload Hunt entities.  We built our UI with a mix of static fields 
and list adapters to receive and display database objects.  The Current Clue fragment opens a camera view and 
contains QR recognition logic that triggers a webview containing the media linked to each clue 
before advancing to the next.

There are currently five default QR codes, which contain the text "scavengr-clue-1", 
"scavengr-clue-2", etc.  Scanning the code linked to a Clue loads the corresponding media Url in a 
pop up webview.  There is an error Toast if any other QR code is detected.  

Due to social isolation measures and a lack of foresight, we did not get NFC tags to experiment 
with, and so have not made an attempt at incorporating NFC read/write into the app.

#### Our goals for the future include:

* In-app QR generation.

* NFC integration.

* Server security.

* HuntDetails POJO to preview a Hunt before downloading to reduce server traffic & storage use.

* Media upload to server to enable offline play.

---

## External services/data

1. Physical NFC tags 
  * Need to be purchased by the user.
  * NFC read/write functionality is supported by existing Android libraries; [Here's a starting point](https://developer.android.com/guide/topics/connectivity/nfc/nfc).
  * NFC tags will replace QR codes optionally and won't be critical to any function of the app.
  
2. Device camera
  * Required to scan QR codes on a hunt.
  * Unless a hunt is entirely NFC-based, issues with the device's camera will make participating in a hunt impossible.

2. [Android GMS Vision](https://developers.google.com/android/reference/com/google/android/gms/vision/package-summary)
  * This is a Google API separate from the standard Android libraries.
  * Contains utilities for recognizing QR codes and other data from camera input, and interpreting their contents.
  * Along with the camera, this is required for QR functionality. 
  
3. QR codes
  * Printable QR codes will be provided to simplify user experience.
  * Additional codes can be generated and printed for free online.
  * QR codes are required for the app to work, and may need to be replaced if they are lost/damaged.
  
4. [OAuth login](https://oauth.net/2/)
  * Users will be required to authenticate through OAuth during account creation.
  * OAuth scope will be limited to generating a user token.
  * Users will still be able to modify/participate in hunts saved locally without OAuth access.
  
5. Scavengr Server 
  * Hunt data and user profiles will be stored remotely.
  * The server will manage access levels and scoreboards for hunts
  * Authorized users are able to download hunt database files.
  * Server access will be required to save/access new hunts.

---

## Design Documentation

### [Entity Relationship Diagram](erd.md)
### [Wireframe Diagram](scavenger-wireframe.md)
### [Implementation](implementation.md)
### [Data Definition Language](ddl.md)

### [Build Instructions]

+ Fork/Clone the Server and Client:
    +[Server Repository](https://github.com/staj-scavengers/server)
    +[Client Repository](https://github.com/staj-scavengers/scavengr-client)

+ Import the server as a Maven project, and the Client as a Gradle project.
+ Run the ServerLoader class to start the server app.
+ Adjust the "BASE_URL" field in the client's app-level build.gradle to match the IP of your server device, or set it to 10.0.2.2 to run on an Android emulator.
+ Preload a sample Hunt by copying the contents of server/src/main/resources/preload/preload.json to the body of a JSON POST request in Postman.
+ Use the following pre-generated QR codes:
    + [Clue 1](scavengr_qr_clue_1.png)
    + [Clue 2](scavengr_qr_clue_2.png)
    + [Clue 3](scavengr_qr_clue_3.png)
    + [Clue 4](scavengr_qr_clue_4.png)
    + [Clue 5](scavengr_qr_clue_5.png)
    + 