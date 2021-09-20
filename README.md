Different behavior of SW when sending using POSTMAN and via Notification composer.
Steps to replicate:
1. Add firebase@9.0.2 to app 
2. firebase-messaging-sw.js service-worker file in the public folder in our react app and add this code:

            // Scripts for firebase and firebase messaging
            importScripts('https://www.gstatic.com/firebasejs/9.0.2/firebase-app.js');
            importScripts('https://www.gstatic.com/firebasejs/9.0.2/firebase-messaging.js');

            // Initialize the Firebase app in the service worker by passing the generated config
            var firebaseConfig = {
                  apiKey: "",
                  authDomain: "",
                  projectId: "",
                  storageBucket: "",
                  messagingSenderId: "",
                  appId: "",
                  measurementId: ""
              };

              firebase.initializeApp(firebaseConfig);

              // Retrieve firebase messaging
              const messaging = firebase.messaging();

              messaging.onBackgroundMessage(function (payload) {
              console.log('Received background message ', payload);

              const notificationTitle = payload.notification.title;
              const notificationOptions = {
                  body: payload.notification.body,
              };

              self.registration.showNotification(notificationTitle,
                  notificationOptions);
              });
  
3. Send notification via POSTMAN:
 
             {
                "message": {
                  "token": "FCM TOKEN",
                  "notification": {
                    "body": "Body of Your Notification in data",
                    "title": "Title of Your Notification in data"
                  }
                }
              }


This procedure will replicate duplicate background notification.
