# HOLUS SDK
![version](https://img.shields.io/badge/version-v1.0.0-blue)

The Holus SDK comes with a video recording screen to capture the identity document at different angles to check for the presence or absence of holograms in the ID. Available for limited countries only.

# Table Of Content

- [Prerequisite](#prerequisite)
- [Requirements](#requirements)
- [Permissions](#permissions)
- [Installation](#installation)
- [Holus Error Codes](#holus-error-codes)
- [Help](#help)

## Prerequisite

***NOTE : Encryption of CAPTUS SDK Result is under development***

You will need a valid license and Netrc credentials to use the Holus SDK, which can be obtained by contacting `support@frslabs.com` . 

Depending on the license - offline or online - you have opted for, the ping functionality to billing servers will be disabled or enabled. For instance, if you have opted for the offline SDK model, then there will be no server ping needed to our billing server to bill you. However, if you have chosen a transaction based pricing, then after each transaction, a ping request will be made to our billing server. This cannot be overrided by the App. A point to note is that if the ping transaction fails for any reason, the whole transaction will be void without any results from the SDK.

Once you have the license , follow the below instructions for a successful integration of Holus SDK onto your iOS Application.

## Requirements

- Swift 5.0
- iOS 12.0+

## Permissions

In Info.plist file add following code to allow your application to access iPhone's camera:
``<key>NSCameraUsageDescription</key>
<string>Allow access to camera</string>``

## Installation

### Cocoapods

You can use [CocoaPods](http://cocoapods.org/) to install `holus` by adding it to your `Podfile`:

```ruby
source 'https://gitlab.com/frslabs-public/ios/holus.git'
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '12.0'
target '<Your Target Name>' do
use_frameworks!
pod 'Holus', '1.0.0'
pod 'TensorFlowLiteSwift'
pod 'Alamofire', '~> 4.9.1'
end
```

###### Save/Edit Netrc settings to install custom pod

You will need a valid netrc credentials to install holus from maven, which can be obtained by contacting `support@frslabs.com`. 

1. Create or edit .netrc file under current user's home directory
2. Write the below lines into that file, replace <YOUR_USERNAME> and <YOUR_PASSWORD> with your credentials which is shared through email and save the file.
```ruby
machine holus-ios.repo.frslabs.space
login <YOUR_USERNAME>
password <YOUR_PASSOWRD>
```
3. In terminal enter below command to install the pod
pod install or pod update.

4. Connect with physical device to build and run holus, It will not build/run in simulator due to camera dependency.

To get the full benefits import `holus` wherever you import UIKit

``` swift
import UIKit
import Holus
```

## Getting Started

### Swift

1. Initialize the input parameters and import delegate OCRDelegate

```swift
class ViewController: UIViewController,HolusDelegate {
    func holusSuccessResponse(controller: RecordingNavigationViewController, didFinishOcrWithResult results: HolusResults) {
        let isDocumentSpoofed = results.isDocumentSpoofed
        let videoPath =  results.videoPath
        let videoReferenceID = results.videoReferenceId
    }
    func holusFailureResponse(controller: RecordingNavigationViewController, didFailWithError error: String) {
        let error = error
    }
    override func viewDidLoad() {
        super.viewDidLoad()
  
}
```

2. Invoke Holus SDK

```swift
    // ...
    
    override func viewDidAppear(_ animated: Bool) {
         let recordingVC = RecordingNavigationViewController(delegate: self)
            recordingVC.licenceKey = "LICENSE_KEY"
            recordingVC.baseURL = BASE_URL
            recordingVC.referenceID = "REFERENCE_ID"
            recordingVC.serverHeader = "HEADER"
            present(recordingVC, animated: true)
    }
    
    // ...    
```
## Holus Error Codes

Following error codes will be returned on the `onHolusFailure` method of the callback

| CODE | DESCRIPTION                  |
| ---- | ---------------------------- |
| 803  | Camera permission denied    |
| 804  | Capture interrupted            |
| 805  | Holus SDK License has expired             |
| 806  | Holus SDK License is invalid             |
| 802  | Sdk Interrupted           |
| 814  | Video upload failed             |
| 813  | Error parsing result             |
| 801  | Video reocording interupt             |
| 819  | Timeout             |
| 901  | No internet             |

 Sets the Holus SDK apiCredentials. Obtain the appropriate api credentials through a REST API call , for details about the REST API, contact `support@frslabs.com`
  
 
## Help
For any queries/feedback , contact us at `support@frslabs.com` 
