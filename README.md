![pod](https://img.shields.io/cocoapods/v/myinterview-sdk.svg) [![License](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](https://github.com/myInterviewSDK/myinterview-sdk-ios/blob/master/LICENSE) ![Platform](https://img.shields.io/badge/platform-iOS-lightgrey.svg)

# MyInterview iOS SDK
Integrate video into your recruitment solution and enhance the decision making process for employers.
To obtain required credentials please visit [myInterview.com].

## Installation
Open **Terminal**. If you don't have **cocoapods** installed on your machine type:
```
sudo gem install cocoapods
```
For more details visit [CocoaPods Getting Started]  
Then in **Terminal** cd to "your XCode project root directory"  
(where your .xcodeproj file resides) and type:
```
pod init
```
Then open your project's podfile by typing in terminal:
```
open -a Xcode Podfile
```
In your **Podfile** type:
```
pod 'myinterview-sdk'
```
Uncomment **platform :ios, '9.0'**. Uncomment **use_frameworks!** if you're using Swift.
When you are done editing the podfile, save it and close XCode. 
Then install pods into your project by typing in terminal:
```
pod install
``` 
Don't forget to provide descriptions for **NSCameraUsageDescription** and **NSMicrophoneUsageDescription** keys in your app's **Info.plist**

## Initialization & Showing
```swift
let config = MIConfig.init("apiKey")
let question = MIQuestion.init("Tell us about yourself")
let vc = MIWidget.getInterview(config, questions: [question]) { (finished, interviewId) in
    //Callback if video interview was closed. Need to dismiss VC here.
}
```
**apiKey**: your own myInterviewKey

**vc**: ViewController that you can present in your app in any way

**finished**: Boolean flag. True if interview was finished and uploaded. False otherwise.

**interviewId**: id of created interview

## Configuration

### MIConfig
```swift
let config = MIConfig.init("apiKey")
config.preparationTime = 20
config.hideQuestions = true
```
**preparationTime**: Time that user can spend on preparation if hideQuestion == true. Default is 30

**hideQuestions**: If hideQuiestions == true user won't see questions before push Start Record button. Default is false

### MIQuestion
```swift
let question = MIQuestion.init("Tell us about yourself")
question.partDuration = 30
question.numOfRetakes = 4
```
**partDuration**: the duration of this part of the interview in seconds, default is 30

**numOfRetakes**: the number of retakes the user may take for a single part, default is 0. Could be 0..9


## Example:
```swift
let config = MIConfig.init("apiKey")
config.preparationTime = 20
config.hideQuestions = true
let question1 = MIQuestion.init("Tell us about yourself")
question1.partDuration = 30
question1.numOfRetakes = 4
let questions = [
     question1,
     MIQuestion.init("This is second question"),
     MIQuestion.init("This is third question"),
];

let vc = MIWidget.getInterview(config, questions: questions) { (finished, videoId) in
    self.dismiss(animated: true, completion: nil)
}

if let safeVc = vc {
    self.present(safeVc, animated: true, completion: nil)
}
```

## License
```
Copyright 2018 Myinterview Solutions Pty Ltd.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

[myInterview.com]: https://myinterview.com
[Amazon SDK]: <https://github.com/aws/aws-sdk-ios>
[CocoaPods Getting Started]: <https://guides.cocoapods.org/using/getting-started.html>
