# Classroom Manager — Google Drive / PC / Mobile Setup

This package keeps the existing Classroom Manager features and adds:

- Google Drive cloud storage for the app's JSON data file
- Google OAuth authorization in the browser
- Manual Pull / Push synchronization
- IndexedDB local storage for offline work
- PWA installation support for Windows/Android/iPhone-compatible browsers
- Existing JSON/CSV backup and restore features

## 1. Create a Google Cloud project

Open Google Cloud Console and create/select a project.

Enable:
- Google Drive API

Open Google Auth Platform / Clients and create an **OAuth 2.0 Client ID** with application type **Web application**.

Add your final HTTPS website origin under **Authorized JavaScript origins**, for example:

`https://your-site.example`

Do not put a client secret in this HTML app. Web OAuth uses the client ID; the secret is not used in the browser.

## 2. Publish the app over HTTPS

Do not use `file://` for Google Drive synchronization. Host this folder on an HTTPS web host.

The folder should contain:

- index.html
- manifest.json
- sw.js
- icon-192.png
- icon-512.png

## 3. Connect Google Drive

1. Open the published Classroom Manager.
2. In **Google Drive Sync**, paste the OAuth Web Client ID.
3. Click **Save Client ID**.
4. Click **Connect**.
5. Approve Google Drive access.
6. Click **Push** to create `ClassroomManager_Data.json` in your Google Drive.

The app requests the `drive.file` scope, which limits access to files created/used by this app rather than your entire Drive.

## 4. Use on another device

Open the same HTTPS URL on the second device.

1. Enter the same OAuth Client ID if needed.
2. Click Connect.
3. Click **Pull**.
4. The classroom data from Google Drive will be loaded into that device's local cache.

After making changes, click **Push** to upload the current copy. On the other device, click **Pull** to receive it.

## 5. Offline use

The app keeps a local IndexedDB copy. Attendance and other records can continue to be entered when temporarily offline. Push/Pull requires an internet connection.

## Important synchronization rule

This first cloud version uses explicit **Push** and **Pull** rather than silently overwriting Drive on every keystroke. This is intentional: it reduces accidental overwrites when the app is open on both PC and mobile.

Before replacing device data with Drive data, the app asks for confirmation.

## Google documentation

- Drive API JavaScript quickstart: https://developers.google.com/workspace/drive/api/quickstart/js
- Drive API scopes: https://developers.google.com/workspace/drive/api/guides/api-specific-auth
- OAuth scopes: https://developers.google.com/identity/protocols/oauth2/scopes
