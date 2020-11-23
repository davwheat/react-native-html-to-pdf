# react-native-convert-html-to-pdf

[**Original library by christopherdro**](https://github.com/christopherdro/react-native-html-to-pdf)

This library is a modified copy of their repo with bug fixes.

Easily convert HTML strings to PDF documents in your React Native app, and save them on your device.

## Installation

Install the libaray

```
npm i react-native-convert-html-to-pdf

yarn add react-native-convert-html-to-pdf
```

### Option 1: Automatic

#### React Native >= 0.6.0

You don't need to do anything! Just rebuild you app - React Native will do the rest for you.

#### React Native < 0.6.0

Run `react-native link react-native-convert-html-to-pdf`

### Option 2: Manual

<details>
   <summary>Instructions</summary>

#### iOS

2. Open your project in XCode, right click on "Libraries" and select "Add Files to 'Your Project Name'".
3. Add `libRNHTMLtoPDF.a` to `Build Phases -> Link Binary With Libraries`

#### Android
- Edit `android/settings.gradle` to included

```java
include ':react-native-convert-html-to-pdf'
project(':react-nativeconvert--html-to-pdf').projectDir = new File(rootProject.projectDir,'../node_modules/react-native-convert-html-to-pdf/android')
```

- Edit `android/app/build.gradle` file to include

```java
dependencies {
  ....
  compile project(':react-native-convert-html-to-pdf')
}
```

- Edit `MainApplication.java` to include

```java
// import the package
import dev.davwheat.htmltopdf.ConvertHtmlToPdfPackage;

// include package
new MainReactPackage(),
new ConvertHtmlToPdfPackage()
```

</details>

## Permissions

### Android

1. Add the following `WRITE_EXTERNAL_STORAGE` permission to `AndroidManifest.xml`

```xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```

> **NOTE:** Starting from Android 6 (Marshmallow), users need to be prompted for permission dynamically. Follow [this](https://facebook.github.io/react-native/docs/permissionsandroid) link for more details on how to do that.


## Usage
```javascript

import React, { Component } from 'react';

import {
  Text,
  TouchableHighlight,
  View,
} from 'react-native';

import HtmlToPdf from 'react-native-convert-html-to-pdf';

export default class Example extends Component {
  async GeneratePDF() {
    let file = await HtmlToPdf.convert({
      html: '<h1>PDF TEST</h1>',
      fileName: 'test',
      directory: 'Documents',
    })

    return file.filePath;
  }

  render() {
    return(
      <View>
        <TouchableHighlight onPress={this.GeneratePDF}>
          <Text>Create PDF</Text>
        </TouchableHighlight>
      </View>
    )
  }
}
```

## Options

| Param | Type | Default | Note |
|---|---|---|---|
| `html` | `string` |  | HTML string to be converted
| `fileName` | `string` | Random  | Custom Filename excluding .pdf extension
| `base64` | `boolean` | false  | return base64 string of pdf file (not recommended)
| `directory` | `string` |default cache directory| Directory where the file will be created (`Documents` folder in example above). Please note, on iOS `Documents` is the only custom value that is accepted.
| `height` | `number` | 792  | Set document height (points)
| `width` | `number` | 612  | Set document width (points)


#### iOS Only

| Param | Type | Default | Note |
|---|---|---|---|
| `paddingLeft` | number | 10  | Outer left padding (points)
| `paddingRight` | number | 10  | Outer right padding (points)
| `paddingTop` | number | 10  | Outer top padding (points)
| `paddingBottom` | number | 10  | Outer bottom padding (points)
| `padding` | number | 10 | Outer padding for any side (points), overrides any padding listed before
| `bgColor` | string | #F6F5F0 | Background color in Hexadecimal


#### Android Only

| Param | Type | Default | Note |
|---|---|---|---|
| `fonts` | Array | `[]` | Allow custom fonts `['/fonts/TimesNewRoman.ttf', '/fonts/Verdana.ttf']` |
