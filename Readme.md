# Camera app with location tracking -

> Researching the issue Error: Call to function 'ExponentImagePicker.launchCameraAsync' has been rejected

It seems to be related to the expo task manager too.

** I've found that the issue appears when: **

- Given you are tracking location via a task in the task manager
- When you close the app
- When you reopen the app
- When you try to pick an image
- Then the image picker will not open

## Reproduce the issue

The issue is only reproducible with a full production build or a development build using a dev client.
Here are the steps for reproducing with a dev client:

Deployment steps:

- `yarn install`
- `npx expo install`
- `eas build:configure`
- `eas build --profile development --platform android`
- install the dev client

Functional steps:

- run `npx expo start`
- open via dev client
- Press "pick an image"
- You will be able to pick an image
- Select start tracking
- After a few sec an icon will appear in you top notification bar indicating that you are being tracked
- Close the app (really close it by swiping it out of your open apps menu)
- Open app
- Press "pick an image"
- **The camera picker won't open!**

->

```
[Error: Call to function 'ExponentImagePicker.launchCameraAsync' has been rejected.
→ Caused by: java.lang.IllegalStateException: Attempting to launch an unregistered ActivityResultLauncher with contract expo.modules.imagepicker.contracts.CameraContract@5ec86f0 and input CameraContractOptions(uri=content://be.transit.camera.ImagePickerFileProvider/cached_expo_files/ImagePicker/b6cee57e-db28-4b5e-a738-8d096c043011.jpeg, options=expo.modules.imagepicker.ImagePickerOptions@472c469). You must ensure the ActivityResultLauncher is registered before calling launch()]
```
