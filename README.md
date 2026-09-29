# FaceCheck: Opt-in Attendance

Building AI course project

## Summary

FaceCheck is an idea for a small attendance system for classes and clubs. Members who choose to join are recognized by a webcam at the door and marked present automatically. Everything runs locally, and members can leave and delete their data at any time.

## Background

Taking attendance by hand or by passing around a sheet wastes time, and it is easy to forget or fake.

* Roll call takes 5-10 minutes of every session
* Paper sheets get lost and are hard to analyze
* QR-code check-ins can be shared with friends who aren't there

My motivation is to see how face recognition can save time while being used responsibly. Consent and privacy are part of the design from the start rather than an afterthought.

## How is it used?

1. A member joins voluntarily by giving written consent and taking a few photos.
2. When the member arrives, a webcam at the door captures the face.
3. The system compares it to the enrolled members and marks the person present.
4. The organizer sees a simple attendance list after the session.

The users are the organizer (teacher or club leader) and the members. Anyone can decline and check in manually instead, and a member can ask for their data to be deleted at any time. The camera should be clearly visible, with a sign explaining what it does.

## Data sources and AI methods

The only data is the photos that members provide themselves. No public face datasets are needed for the demo, because a pretrained model is used.

The method is face embeddings: a pretrained neural network turns each face into a list of numbers, and a new face is matched to the closest enrolled face. If the distance is too large, the person is marked "unknown" and no guess is made.

| Step | Description |
| ---- | ----------- |
| Input | Webcam image |
| Detection | Find the face in the image |
| Embedding | Convert the face into numbers |
| Matching | Compare with enrolled members |
| Output | Present / unknown |

A demo could be built in Python with an open source library such as [face_recognition](https://github.com/ageitgey/face_recognition) (check its license before use).

## Challenges

* Face recognition works worse for some skin tones, ages and lighting conditions, so some members may be missed or misidentified.
* Faces are sensitive biometric data, so photos must be stored securely, kept only as long as needed, and never shared.
* Photos of people can fool it unless liveness detection is added.
* It shouldn't be used to track people or used on anyone who hasn't given consent, and the law on biometric data varies by country (for example GDPR in the EU).
* It doesn't solve the case where someone simply doesn't want to be recognized. A manual alternative must always exist.

## What next?

* Test accuracy on a diverse group of volunteers and report the results honestly
* Add liveness detection
* Store only embeddings, not photos
* Build a simple dashboard for the organizer
* Get feedback from members and a data protection expert

## Acknowledgments

* Inspired by open source face recognition projects
* face_recognition library by Adam Geitgey (credit and license to be confirmed)
