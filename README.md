## Team Roster

  ### Samuel Martinez
  
  GitHub [![GitHub](github.png)](https://github.com/semartinez147) | LinkedIn [![LinkedIn](linkedin.png)](https://linkedin.com/in/semartinez147)

--- 
 
  ### Trace Decker

  GitHub [![GitHub](github.png)](https://github.com/TraceDecker/) | LinkedIn [![LinkedIn](linkedin.png)](https://www.linkedin.com/in/trace-decker-cohort9/)

---
 
  ### Abby Reyes

  GitHub [![GitHub](github.png)](https://github.com/mabbyreyes/) | LinkedIn [![LinkedIn](linkedin.png)](https://www.linkedin.com/in/maritzaareyes/)

---
  
  ### Jawid Mohammadi

  GitHub [![GitHub](github.png)](https://github.com/Jawidmohammadi/) | LinkedIn [![LinkedIn](linkedin.png)](https://www.linkedin.com/in/jawid-mohammadi/)

---

---

## Description

Scavengr is an augmented reality scavenger hunt app that uses QR codes and/or NFC tags to display multimedia hints with or without wireless service.  

QR codes are simple images that phone cameras can easily identify, even from a distance, in low light, or at an angle.  NFC tags require physical contact with the phone (i.e. Apple Pay), but they are inexpensive, can be easily embedded in physical objects, and can be written/rewritten by most Android devices.  

Users in the Organizer role can set up new hunts easily and quickly with default QR templates, or expand them using NFC tags embedded in real-world objects.  

Hunter users will be able to start a hunt by using a public link or accepting a private invitation.  Scavengr will track hunt progress and publish completion times.

---

## Intended users

* Teachers
* Parents
* Museum, zoo, aquarium
* Youth group/activity leaders

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

## External services/data

1. Physical NFC tags 
  * Need to be purchased by the user.
  * NFC read/write functionality is supported by existing Android libraries; [Here's a starting point](https://developer.android.com/guide/topics/connectivity/nfc/nfc).
  * NFC tags will replace QR codes optionally and won't be critical to any function of the app.
  
2. Device camera
  * Required to scan QR codes on a hunt.
  * Unless a hunt is entirely NFC-based, issues with the device's camera will make participating in a hunt impossible.
  
3. QR codes
  * Printable QR codes will be provided to simplify user experience.
  * Additional codes can be generated and printed for free online.
  * QR codes are required for the app to work, and may need to be replaced.
  
4. [OAuth login](https://oauth.net/2/)
  * Users will be required to authenticate through OAuth during account creation.
  * OAuth scope will be limited to generating a user token.
  * Users will still be able to modify/participate in hunts saved locally without OAuth access.
  
5. Scavengr Server 
  * Hunt data and user profiles will be stored remotely.
  * The server will manage access levels and scoreboards for hunts
  * Authorized users will be able to download a hunt database file to play offline.
  * Server access will be required to save/access new hunts.

---

## Design Documentation

### [Entity Relationship Diagram](erd.md)

#### Entity Classes

* [Clue](https://github.com/staj-scavengers/server/blob/master/src/main/java/io/github/stajscavengers/scavenger/model/entity/Clue.java)
* [Hunt](https://github.com/staj-scavengers/server/blob/master/src/main/java/io/github/stajscavengers/scavenger/model/entity/Hunt.java)
* [HuntActivity](https://github.com/staj-scavengers/server/blob/master/src/main/java/io/github/stajscavengers/scavenger/model/entity/HuntActivity.java)
* [Organizer](https://github.com/staj-scavengers/server/blob/master/src/main/java/io/github/stajscavengers/scavenger/model/entity/Organizer.java)
* [User](https://github.com/staj-scavengers/server/blob/master/src/main/java/io/github/stajscavengers/scavenger/model/entity/User.java)

#### Flat Interfaces

* [FlatClue](https://github.com/staj-scavengers/server/blob/master/src/main/java/io/github/stajscavengers/scavenger/view/FlatClue.java)
* [FlatHunt](https://github.com/staj-scavengers/server/blob/master/src/main/java/io/github/stajscavengers/scavenger/view/FlatHunt.java)
* [FlatHuntActivity](https://github.com/staj-scavengers/server/blob/master/src/main/java/io/github/stajscavengers/scavenger/view/FlatHuntActivity.java)
* [FlatOrganizer](https://github.com/staj-scavengers/server/blob/master/src/main/java/io/github/stajscavengers/scavenger/view/FlatOrganizer.java)
* [FlatUser](https://github.com/staj-scavengers/server/blob/master/src/main/java/io/github/stajscavengers/scavenger/view/FlatUser.java)


###  Wire Frame
(In progress)
