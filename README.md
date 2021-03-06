# Capacitor Native Audio Plugin

Capacitory community plugin for native audio engine.

## Maintainers

| Maintainer    | GitHub                                      | Social                     | Sponsoring Company |
| ------------- | ------------------------------------------- | -------------------------- | ------------------ |
| Priyank Patel | [priyankpat](https://github.com/priyankpat) | [N/A](https://twitter.com) | Ionic              |

Mainteinance Status: Actively Maintained

## Installation

To use npm

```bash
npm install @capacitor-community/native-audio
```

To use yarn

```bash
yarn add @capacitor-community/native-audio
```

Sync native files

```bash
npx cap sync
```

On iOS, no further steps are needed.

On Android, register the plugin in your main activity:

```java
import com.getcapacitor.community.firebasecrashlytics.FirebaseCrashlytics;

public class MainActivity extends BridgeActivity {

  @Override
  public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

    // Initializes the Bridge
    this.init(
        savedInstanceState,
        new ArrayList<Class<? extends Plugin>>() {

          {
            // Additional plugins you've installed go here
            // Ex: add(TotallyAwesomePlugin.class);
            add(FirebaseCrashlytics.class);
          }
        }
      );
  }
}
```

## Configuration

No configuration required for this plugin.

## Supported methods

| Name           | Android | iOS | Web |
| :------------- | :------ | :-- | :-- |
| configure      | ✅      | ✅  | ❌  |
| preloadSimple  | ✅      | ✅  | ❌  |
| preloadComplex | ✅      | ✅  | ❌  |
| play           | ✅      | ✅  | ❌  |
| loop           | ✅      | ✅  | ❌  |
| stop           | ✅      | ✅  | ❌  |
| unload         | ✅      | ✅  | ❌  |
| setVolume      | ✅      | ✅  | ❌  |
| getDuration    | ❌      | ✅  | ❌  |
| getCurrentTime | ❌      | ✅  | ❌  |

## Usage

```typescript

import { Plugins } from '@capacitor/core';

const { NativeAudio } = Plugins;

/**
 * This method will throw an exception triggering crashlytics to log the event.
 * @param none
 * @returns void
 */
NativeAudio.configure({
  fade: '',
});

/**
 * This method will load short duration audio file into memory.
 * @param assetPath - relative path of the file or absolute url (http://)
 *        assetId - unique identifier of the file
 * @returns void
 */
NativeAudio.preloadSimple({
  assetPath: 'audio/chime.mp3',
  assetId: 'chime_audio',
});

/**
 * This method will load more optimized audio files for background into memory.
 * @param assetPath - relative path of the file or absolute url (file://)
 *        assetId - unique identifier of the file
 *        volume - numerical value of the volume between 0.1 - 1.0
 *        audioChannelNum - number of audio channels
 *        isUrl - pass true if assetPath is a `file://` url
 * @returns void
 */
NativeAudio.preloadComplex({
  assetPath: 'audio/inception.mp3',
  assetId: 'inception_audio',
  volume: 1.0,
  audioChannelNum: 1,
  isUrl: false
});

/**
 * This method will play the loaded audio file if present in the memory.
 * @param assetId - identifier of the asset
 * @returns void
 */
NativeAudio.play({
  assetId: 'chime_audio',
});

/**
 * This method will loop the audio file for playback.
 * @param assetId - identifier of the asset
 * @returns void
 */
NativeAudio.loop({
  assetId: 'chime_audio',
});


/**
 * This method will stop the audio file if it's currently playing.
 * @param assetId - identifier of the asset
 * @returns void
 */
NativeAudio.stop({
  assetId: 'chime_audio',
});

/**
 * This method will unload the audio file from the memory.
 * @param assetId - identifier of the asset
 * @returns void
 */
NativeAudio.unload({
  assetId: 'chime_audio',
});

/**
 * This method will set the new volume for a audio file.
 * @param assetId - identifier of the asset
 *        volume - numerical value of the volume between 0.1 - 1.0
 * @returns void
 */
NativeAudio.setVolume({
  assetId: 'inception_audio',
  volume: 0.4,
});

/**
 * this method will get the duration of an audio file.
 * only works if channels == 1
 */
NativeAudio.getDuration({
  assetId: 'inception_audio'
})
.then(result => {
  console.log(result.duration);
})

/**
 * this method will get the current time of a playing audio file.
 * only works if channels == 1
 */
NativeAudio.getCurrentTime({
  assetId: 'inception_audio'
});
.then(result => {
  console.log(result.currentTime);
})
```
