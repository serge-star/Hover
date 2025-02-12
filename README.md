<p align="center">
  <img height="250" src="Screenshots/Hover.png"/>
</p>

# Version 1.1

[![apm](https://img.shields.io/apm/l/vim-mode.svg)](https://github.com/onurhuseyincantay/Hover/blob/develop/License.md)[![CocoaPods compatible](https://img.shields.io/cocoapods/v/HoverKitSDK.svg)](https://cocoapods.org/pods/HoverKitSDK)
[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
[![Swift Package Manager compatible](https://img.shields.io/badge/Swift%20Package%20Manager-compatible-brightgreen.svg)](https://github.com/apple/swift-package-manager)
![Swift](https://github.com/onurhuseyincantay/Hover/workflows/Swift/badge.svg)</br>

## Currently Available
| Platform      | Version       |
| ------------- |:------------- | 
| iOS           | 12.0          |
| tvOS          | 10.0          |
| macOS         | 10.15         |
| watchOS       | 3.0           |
| macCatalyst   | 13.0          |

Hover is a Network layer which uses Apple's new framework `Combine` and provides async network calls with different kind of request functions.

## Why and When to Use
The main benefit to use Hover is to abstract the networking layer as much as possible and remove redunant code from your projects as we know `Apple` announced a new framework called `Combine` the main goal is to provide a declarative Swift API for processing values over time. These values can represent many kinds of asynchronous events, so networking calls are the most important async events, which actually needs to have a support for `Combine` to prevent and integrate Apple's native framework. Why you shouldnt use is when you dont have that much networking calls and also not so complex data flows to keep track on which means actually that you dont have states for the UI then dont use it. :) 

#### Cocoapods Installation
```swift
target 'MyApp' do
  pod 'HoverKitSDK', "~> 1.1"
end
```

#### Carthage Installation
```swift
github "onurhuseyincantay/Hover" ~> 1.1
```

#### Swift Package Manager Installation
Package            |  branch
:-------------------------:|:-------------------------:
<img height="250" src="Screenshots/package.png" />  |   <img height="250" src="Screenshots/branchInfo.png" />


# Sample Usage
#### Provide Target
```swift
 enum UserTarget {
  case login(email: String, password: String) 
 }
 
 extension UserTarget: NetworkTarget { 
    var path: String {
        switch self {
        ...
    }
    var providerType: AuthProviderType {
        ...
    }
    
    var baseURL: URL {
        ...
    }
    
    var methodType: MethodType {
        switch self {
          ...
        }
    }
    
    var contentType: ContentType? {
        switch self {
         ...
        }
    }
    
    var workType: WorkType {
        switch self {
          ...
        }
    }
    
    var headers: [String : String]? {
        ...
    }
 }
```
#### Request With Publisher
```swift
let provider = Hover()
let publisher = provider.request(
            with: UserTarget.login(email: "ohc3807@gmail.com", password: "123456"),
            scheduler: DispatchQueue.main,
            class: UserModel.self
        )
...
publisher.sink({ ... })
```

#### Request With Subscriber
```swift
let provider = Hover()
let userSubscriber = UserSubscriber()
provider.request(with: UserTarget.login(email: "ohc3807@gmail.com", password: "123456"), class: UserModel.self, subscriber: userSubscriber)
```

Tested with [JsonPlaceholder](https://jsonplaceholder.typicode.com)
Inspired By [Moya](https://github.com/Moya/Moya) Developed with 🧡

