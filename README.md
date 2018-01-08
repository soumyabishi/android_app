
# L'amour - Love calculator

A hybrid android app made using [Cordova](https://cordova.apache.org/), [Vuejs2](https://vuejs.org/), [Framework7](framework7.io) and [Webpack](https://webpack.js.org/).

App landing - [http://soumyabishi.github.io/Lamour](http://soumyabishi.github.io/Lamour)

![Alt Text](https://media.giphy.com/media/l49JPKkeibEuWeFPi/giphy.gif)




## Getting Started


### Prerequisites

To build and run this app, you need to install Android SDK. Alternatively, if you are using browser for development you can use browser platform which does not require any platform SDKs.
To check if you satisfy requirements for building the platform:

```
$ cordova requirements
Requirements check results for android:
Java JDK: installed .
Android SDK: installed
Android target: installed android-19,android-21,android-22,android-23,Google Inc.:Google APIs:19,Google Inc.:Google APIs (x86 System Image):19,Google Inc.:Google APIs:23
Gradle: installed
```

### Installing

Clone this repo to your local directory 
```
$ git clone https://github.com/soumyabishi/android_app.git
```

Install dependencies

```
$ npm install 
```

Usage: you can use every cordova commands. You just have one more command option: -- --lr. It starts live reload.

```
$ cordova run android -- --lr
$ cordova run browser -- --live-reload
```

### Build the App
Run the following command to iteratively build the project:

```
$ npm run build
$ cordova build ios
```


## Todo
1. Recent search results
2. Animated splash screen


## Acknowledgments

Shoutout to [@ankitakumar04](https://github.com/ankitakumar04/) for helping me in landing page frontend development. 


