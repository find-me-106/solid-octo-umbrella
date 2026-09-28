# Wallpost setup
1. Firebase console: create project > Build > Authentication > enable Email/Password. Build > Firestore Database > create.
2. Paste your web-app config into js/config.js. Add your Cloudinary cloud name and an UNSIGNED upload preset.
3. Firestore > Rules, paste:
   rules_version = '2';
   service cloud.firestore { match /databases/{db}/documents {
     match /posts/{id} { allow read: if true;
       allow create: if request.auth != null && request.resource.data.uid == request.auth.uid;
       allow delete: if request.auth != null && resource.data.uid == request.auth.uid; }
     match /users/{uid} { allow read: if true; allow write: if request.auth != null && request.auth.uid == uid; }
   } }
4. Run from a server (modules don't work from file://): `npx serve site` or VS Code Live Server. Add your domain (localhost is included) under Authentication > Settings > Authorized domains.
