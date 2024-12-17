<p align="center">   
    <a href="https://pub.dev/packages/payfast"><img src="https://img.shields.io/pub/v/payfast?logo=dart&logoColor=white" alt="Pub Version"></a>
    <a href="https://pub.dev/packages/payfast"><img src="https://badgen.net/pub/points/payfast" alt="Pub points"></a>
    <a href="https://pub.dev/packages/payfast"><img src="https://badgen.net/pub/likes/payfast" alt="Pub Likes"></a>
    <a href="https://pub.dev/packages/payfast"><img src="https://badgen.net/pub/popularity/payfast" alt="Pub popularity"></a>
    <br> 
    <a href="https://github.com/youngcet/payfast"><img src="https://img.shields.io/github/stars/youngcet/payfast?style=social" alt="Repo stars"></a>
    <a href="https://github.com/youngcet/payfast/commits/main"><img src="https://img.shields.io/github/last-commit/youngcet/payfast/main?logo=git" alt="Last Commit"></a>
    <a href="https://github.com/youngcet/payfast/pulls"><img src="https://img.shields.io/github/issues-pr/youngcet/payfast" alt="Repo PRs"></a>
    <a href="https://github.com/youngcet/payfast/issues?q=is%3Aissue+is%3Aopen"><img src="https://img.shields.io/github/issues/youngcet/payfast" alt="Repo issues"></a>
    <a href="https://github.com/youngcet/payfast/graphs/contributors"><img src="https://badgen.net/github/contributors/youngcet/payfast" alt="Contributors"></a>
    <a href="https://github.com/youngcet/payfast/blob/main/LICENSE"><img src="https://badgen.net/github/license/youngcet/payfast" alt="License"></a>
    <br>       
    <a href="https://app.codecov.io/gh/youngcet/payfast"><img src="https://img.shields.io/codecov/c/github/youngcet/payfast?logo=codecov&logoColor=white" alt="Coverage Status"></a>
</p>

# PayFast Flutter Package

A Flutter package to integrate PayFast payments into your app.

- [Getting Started](#getting-started)
  * [Usage](#usage)
  * [Payfast Onsite Activation Script](#payfast-onsite-activation-script)
  * [Android & IOS Setup](#android-and-ios-setup)
- [Features](#features)
  * [Onsite Payments](#onsite-payments)
  * [Sandbox or Live Environment integration](#sandbox-or-live-environment-integration)
  * [Customizable Payment Completion & Cancellation Callbacks](#customizable-payment-completion-and-cancellation-callbacks)
  * [Customizable Payment Summary Widget](#customizable-payment-summary-widget)
  * [Customizable Payment Button](#customizable-payment-button)
  * [Customizable Waiting Overlay Widget](#customizable-waiting-overlay-widget)
- [Properties](#properties)


### Demo

[Watch the demo video](https://permanentlink.co.za/payment/demo.mp4)


## Getting Started

This package uses Payfast's Onsite Payments integration, therefore, you need to host their onsite activiation script. Copy the `html` file below and host it on a secure server:

## Payfast Onsite Activation Script
```html
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="https://sandbox.payfast.co.za/onsite/engine.js"></script>
    <style>
        .lds-roller,
        .lds-roller div,
        .lds-roller div:after {
            box-sizing: border-box;
        }

        .lds-roller {
            /* margin: 0px auto; */
            width: 80%;
            /* height: 80px; */
            height: 100%; 
            display: flex; 
            justify-content: center; 
            align-items: center; 
            margin: 0; 
        }

        .lds-roller div {
            animation: lds-roller 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
            transform-origin: 40px 40px;
        }

        .lds-roller div:after {
            content: " ";
            display: block;
            position: absolute;
            width: 7.2px;
            height: 7.2px;
            border-radius: 50%;
            background: currentColor;
            margin: -3.6px 0 0 -3.6px;
        }

        .lds-roller div:nth-child(1) {
            animation-delay: -0.036s;
        }

        .lds-roller div:nth-child(1):after {
            top: 62.62742px;
            left: 62.62742px;
        }

        .lds-roller div:nth-child(2) {
            animation-delay: -0.072s;
        }

        .lds-roller div:nth-child(2):after {
            top: 67.71281px;
            left: 56px;
        }

        .lds-roller div:nth-child(3) {
            animation-delay: -0.108s;
        }

        .lds-roller div:nth-child(3):after {
            top: 70.90963px;
            left: 48.28221px;
        }

        .lds-roller div:nth-child(4) {
            animation-delay: -0.144s;
        }

        .lds-roller div:nth-child(4):after {
            top: 72px;
            left: 40px;
        }

        .lds-roller div:nth-child(5) {
            animation-delay: -0.18s;
        }

        .lds-roller div:nth-child(5):after {
            top: 70.90963px;
            left: 31.71779px;
        }

        .lds-roller div:nth-child(6) {
            animation-delay: -0.216s;
        }

        .lds-roller div:nth-child(6):after {
            top: 67.71281px;
            left: 24px;
        }

        .lds-roller div:nth-child(7) {
            animation-delay: -0.252s;
        }

        .lds-roller div:nth-child(7):after {
            top: 62.62742px;
            left: 17.37258px;
        }

        .lds-roller div:nth-child(8) {
            animation-delay: -0.288s;
        }

        .lds-roller div:nth-child(8):after {
            top: 56px;
            left: 12.28719px;
        }

        @keyframes lds-roller {
            0% {
                transform: rotate(0deg);
            }

            100% {
                transform: rotate(360deg);
            }
        }
    </style>
</head>
<body>
    <div class="lds-roller"><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div></div>
    <script>
            // retrieve the uuid that is passed to this file and send it to payfast onsite engine
            const queryString = window.location.search;
            const urlParams = new URLSearchParams(queryString);
            const uuid = urlParams.get('uuid');
            
            window.payfast_do_onsite_payment({"uuid":uuid}, function (result) {
                if (result === true) {
                    // Payment Completed
                    location.href = 'completed'; // triggers payment completed widget on app
                }
                else {
                    // Payment Window Closed
                    location.href = 'closed'; // triggers payment cancelled widget on app
                }
            }); 
        </script>
</body>

</html>
```

Alternatively, you can create your own `html` file but make sure to include the tags below (**do not modify the code**):

**Sandbox script location**
```html
<script src="https://sandbox.payfast.co.za/onsite/engine.js"></script> 
<script>
    // retrieve the uuid that is passed to this file and send it to payfast onsite engine
    const queryString = window.location.search;
    const urlParams = new URLSearchParams(queryString);
    const uuid = urlParams.get('uuid');
    
    window.payfast_do_onsite_payment({"uuid":uuid}, function (result) {
        if (result === true) {
            // Payment Completed
            location.href = 'completed'; // triggers payment completed widget on app
        }
        else {
            // Payment Window Closed
            location.href = 'closed'; // triggers payment cancelled widget on app
        }
    }); 
</script>
```

To point to a live server, simply change `<script src="https://sandbox.payfast.co.za/onsite/engine.js"></script>` tag to `<script src="https://www.payfast.co.za/onsite/engine.js"></script>`. Take note of the url where the `html` file is hosted, you're going pass it along in the Payfast package. 

We have to host the file because for security reasons 'Onsite Payments' requires that your application be served over HTTPS. For more detailed documentation, please refer to the official [PayFast Onsite Payments documentation](https://developers.payfast.co.za/docs#onsite_payments). 

## Usage

Install the library to your project by running: 

```bash
flutter pub add payfast
```

or add the following dependency in your `pubspec.yaml` (replace `^latest_version` with the latest version):


```yaml
dependencies:
  payfast: ^latest_version
```

### Android And IOS Setup


|             | Android | iOS   | macOS  |
|-------------|---------|-------|--------|
| **Support** | SDK 21+ | 12.0+ | 10.14+ |



**Android Setup**

Set the correct `minSdkVersion` in `android/app/build.gradle` if it was previously lower than 19:

```groovy
android {
    defaultConfig {
        minSdkVersion 19
    }
}
```

Add `<uses-permission android:name="android.permission.INTERNET" />` permission in `android/app/src/main/AndroidManifest.xml`.

**IOS Setup**

Add the key below in `ios/Runner/Info.plist`

```groovy
<key>io.flutter.embedded_views_preview</key>
<string>YES</string>
```

**Import the package and create a Payfast Widget**

```dart
import 'dart:math';

import 'package:flutter/material.dart';
import 'package:payfast/payfast.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key, required this.title, this.processPayment});

  final String title;
  final Function? processPayment;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;
  
  @override
  void initState() {
    super.initState();

  }

  String _randomId(){
    var rng = Random();
    var code = rng.nextInt(900000) + 100000;

    return '$code';
  }

  void paymentCompleted(){
    print('payment completed');
  }

  void paymentCancelled(){
    print('payment cancelled');
  }

  @override
  Widget build(BuildContext context) {
    return Material(
      child: Scaffold(
        body: Center(
          child: PayFast(
            // all the data fields are required
            data: {
                'merchant_id': '0000000', // Your payfast merchant id
                'merchant_key': '000000', // Your payfast merchant key
                'name_first': 'Yung', // customer first name
                'name_last': 'Cet',   // customer last name
                'email_address': 'domain@gmail.com', // email address
                'm_payment_id': '7663668635664', // payment id
                'amount': '50', // amount
                'item_name': '#0000002', // item name
            }, 
            passPhrase: 'xxxxxxxxxxxxxxx',  // Your payfast passphrase
            useSandBox: true, // true to use Payfast sandbox, false to use their live server
            onsiteActivationScriptUrl: 'https://somedomain.com', // url to the html file above
            onPaymentCancelled: () => paymentCompleted(), // callback function for successful payment
            onPaymentCompleted: () => paymentCancelled(), // callback function for cancelled payment
        ),)
      ),
    );
  }
}
```

The code above will show you the screen below:

<img src="https://github.com/youngcet/payfast/blob/main/doc/basic_app_screenshot.png?raw=true" alt="Basic App Screenshot" width="280"/>

A live example:

<img src="https://github.com/youngcet/payfast/blob/main/doc/live.png?raw=true" alt="Live Screenshot" width="280"/>

## Features

### Onsite Payments

Integrate Payfast's secure payment engine directly into the checkout page. Important: Please note that this is currently in Beta according to Payfast's documentation, however, it works fine.

### Sandbox or Live Environment integration

Configure whether to use PayFast's sandbox or live server. When you choose to use the sandbox or live server, ensure that the hosted `html` file also points to the server's onsite activation script (`<script src="https://sandbox.payfast.co.za/onsite/engine.js"></script>`) and the Payfast merchant id and key corresponds to the appropiate server.

```dart
PayFast(
    ...
    useSandBox: true, // true to use Payfast sandbox, false to use their live server
) 
```

### Customizable Payment Completion And Cancellation Callbacks

Use the `onPaymentCompleted` and `onPaymentCancelled` properties to handle custom actions after a successful or cancelled payment.

```dart
PayFast(
    ...
    onPaymentCancelled: () {
        // payment cancelled
    },
    onPaymentCompleted: () {
        // payment completed
    },
) 
```

<img src="https://github.com/youngcet/payfast/blob/main/doc/payment_completed.png?raw=true" alt="Payment Completed" width="280"/>
<img src="https://github.com/youngcet/payfast/blob/main/doc/payment_cancelled.png?raw=true" alt="Payment Cancelled" width="280"/>


You can change the default text of the default widgets using `onPaymentCompletedText` and `onPaymentCancelledText` properties, respectively:

```dart
PayFast(
    ...
    onPaymentCompletedText: // add your text here,
    onPaymentCancelledText: // add your text here ,
) 
```

Alternatively, you can override the widgets with your own widget:

**Payment Completed Widget:** Customize the post-payment experience with the `paymentCompletedWidget` property. You can display a custom widget when the payment is successfully completed.

**Payment Cancelled Widget:** Similarly, the `paymentCancelledWidget` allows you to display a custom widget when the payment is cancelled, providing users with clear feedback.

```dart
PayFast(
    ...
    paymentCompletedWidget: // add your widget here,
    paymentCancelledWidget: // add your widget here ,
) 
```

### Customizable Payment Summary Widget

Provide a custom widget for displaying the payment summary with the `paymentSumarryWidget` property. This allows for full customization of the payment details display.

<img src="https://github.com/youngcet/payfast/blob/main/doc/basic_app_screenshot.png?raw=true" alt="Payment Summary" width="280"/>


Or modify the default widget using the properties below:

**Payment Summary Title & Icon:** Use the `paymentSummaryTitle` and `defaultPaymentSummaryIcon` properties to customize the title and icon of the payment summary section, ensuring it matches your app's theme.

```dart
PayFast(
    ...
    paymentSummaryTitle: // add text here,
    defaultPaymentSummaryIcon: // add icon here ,
) 
```


### Customizable Payment Button

The `payButtonStyle` and `payButtonText` properties allow you to style the "Pay Now" button and change its text and styling, ensuring that it fits seamlessly with your app's design.

```dart
PayFast(
    ...
    payButtonText: // add text here,
    payButtonStyle: // add styling here ,
) 
```

### Customizable Waiting Overlay Widget

Show a custom loading spinner during the payment process with the `waitingOverlayWidget` property, helping users understand that a process is ongoing.

```dart
PayFast(
    ...
    waitingOverlayWidget: // add your widget here,
) 
```

<img src="https://github.com/youngcet/payfast/blob/main/doc/waitingoverlay.png?raw=true" alt="Waiting Overlay Widget" width="280"/>


## Properties

- **`passPhrase`**:  
  The passphrase provided by PayFast for security.

- **`useSandBox`**:  
  A boolean flag to choose between sandbox or live environment.

- **`data`**:  
  A `Map<String, dynamic>` containing the required payment data. This includes keys like:
  - `merchant_id`
  - `merchant_key`
  - `name_first`
  - `name_last`
  - `amount`
  - `item_name`
  - `m_payment_id`

- **`onsiteActivationScriptUrl`**:  
  The PayFast URL used for onsite payment activation.

- **`onPaymentCompleted`**:  
  A callback function to handle payment completion.

- **`onPaymentCancelled`**:  
  A callback function to handle payment cancellation.

- **`paymentSumarryWidget`**:  
  A custom widget to display the payment summary before the user proceeds with the payment.

- **`payButtonStyle`**:  
  The style of the "Pay Now" button.

- **`payButtonText`**:  
  The text displayed on the "Pay Now" button.

- **`paymentCompletedWidget`**:  
  A custom widget to show after the payment is successfully completed.

- **`paymentCancelledWidget`**:  
  A custom widget to show if the payment is cancelled.

- **`waitingOverlayWidget`**:  
  A custom widget to show a loading spinner during payment processing.


## Contributing

If you have ideas or improvements for this package, we welcome contributions. Please open an issue or create a pull request on our [GitHub repository](https://github.com/youngcet/payfast).

## License

This package is available under the [MIT License](https://github.com/youngcet/payfast/blob/main/LICENSE).