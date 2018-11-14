# MyInterview iOS SDK
Integrate video into your recruitment solution and enhance the decision making process for employers.

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
```
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
```
let config = MIConfig.init("apiKey")
config.preparationTime = 20
config.hideQuestions = true
```
**preparationTime**: Time that user can spend on preparation if hideQuestion == true. Default is 30

**hideQuestions**: If hideQuiestions == true user won't see questions before push Start Record button. Default is false

### MIQuestion
```
let question = MIQuestion.init("Tell us about yourself")
question.partDuration = 30
question.numOfRetakes = 4
```
**partDuration**: the duration of this part of the interview in seconds, default is 30

**numOfRetakes**: the number of retakes the user may take for a single part, default is 0. Could be 0..9


## Example ([Example Link]):
```
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

[Amazon SDK]: <https://github.com/aws/aws-sdk-ios>
[Example Link]: <https://github.com>
[CocoaPods Getting Started]: <https://guides.cocoapods.org/using/getting-started.html>
