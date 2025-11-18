# CountryDialCodePicker

## 📚 Table of Contents

- [✨ Features](#-features)  
- [🛠 Requirements](#-requirements)  
- [📦 Installation](#-installation)  
- [🚀 How to Use](#-how-to-use)  
- [⚠️ Notes](#-notes)  
- [📝 Version 1.0.0](#-version-100)  
- [👤 Author](#-author)  

## ✨ Features

`CountryDialCodePicker` is a simple and customizable SwiftUI component that allows users to select a country along with its dial code. It provides a searchable list of countries, an index bar for quick navigation, and supports various customization options to fit your app’s design and requirements.

**Note:** You can also add a **header icon** in `CountryDialCodePickerView` to enhance the UI. Here's a SwiftUI example showing how to add a leading icon next to the title in the header:

```swift
CountryDialCodePickerView(title: {
    HStack {
        Image(systemName: "globe")
            .foregroundColor(.blue)
        Text("Select Country")
            .font(.headline)
    }
}) { country in
    // handle selection
}
```

## 🛠 Requirements

- iOS 14.0 or later  
- Swift 5.3 or later  
- Xcode 12 or later  
- SwiftUI  

## 📦 Installation

You can add `CountryDialCodePicker` to your Xcode project using Swift Package Manager (SPM). Follow these beginner-friendly steps:

1. **Open your Xcode project** — Launch Xcode and open the project where you want to add the package.

2. **Open the Swift Package Manager interface** — In the menu bar, click on **File > Add Packages...**. This will open a dialog to add a new package dependency.

3. **Enter the package repository URL** — In the search bar, paste the following URL and press Enter:

   ```
   https://github.com/vishalvaghasiya-ios/CountryDialCodePicker.git
   ```

4. **Choose the version or branch** — Select the version you want to use (usually the latest release) or specify a branch if needed. Then click **Add Package**.

5. **Add the package to your project target** — Xcode will ask which targets to add the package to. Select your app target and confirm.

Once the package is added, you can start using it in your Swift files by importing the module:

```swift
import CountryDialCodePicker
```

## 🚀 How to Use

### Basic Usage Example

Here’s an updated example using the new demo-based API for presenting the country picker and handling the selected country:

```swift
import SwiftUI
import CountryDialCodePicker

struct ContentView: View {
    @State private var selectedCountry: Country?
    @State private var isPresented = false

    var body: some View {
        VStack(spacing: 20) {

            if let selectedCountry {
                HStack {
                    Text(selectedCountry.flagEmoji)
                        .font(.largeTitle)
                    Text("\(selectedCountry.name) \(selectedCountry.dialCode)")
                        .font(.title3)
                }
            } else {
                Text("No country selected")
                    .foregroundColor(.gray)
            }

            Button("Open Country Picker") {
                isPresented = true
            }
            .font(.title2)
            .padding()
        }
        .sheet(isPresented: $isPresented) {
            CountryPicker.view(
                config: CountryPickerConfig(
                    displayMode: .countryFlagAndCode,
                    showSearch: true,
                    showIndexBar: true,
                    title: "Select Country"
                ),
                onSelect: { country in
                    selectedCountry = country
                    isPresented = false
                },
                onCancel: {
                    isPresented = false
                }
            )
        }
    }
}
```

#### UIKit Example

```swift
import UIKit
import CountryDialCodePicker

class MyViewController: UIViewController, CountryPickerDelegate {
    var selectedCountry: Country?

    @IBAction func showPicker(_ sender: Any) {
        let pickerVC = CountryPickerViewController(
            config: CountryPickerConfig(
                displayMode: .countryFlagAndCode,
                showSearch: true,
                showIndexBar: true,
                title: "Select Country"
            ),
            onSelect: { [weak self] country in
                self?.selectedCountry = country
                self?.dismiss(animated: true)
            },
            onCancel: { [weak self] in
                self?.dismiss(animated: true)
            }
        )
        pickerVC.modalPresentationStyle = .formSheet
        present(pickerVC, animated: true)
    }

    // MARK: - CountryPickerDelegate
    func countryPicker(didSelect country: Country) {
        selectedCountry = country
    }

    func countryPickerDidCancel() {
        dismiss(animated: true)
    }
}
```

### Customizations

`CountryDialCodePicker` offers several ways to customize its appearance and behavior:

#### Title

You can set a custom title for the picker:

```swift
CountryDialCodePickerView(title: "Choose your country") { country in
    // handle selection
}
```

#### Index Bar

The index bar allows quick navigation through the country list. You can enable or disable it:

```swift
CountryDialCodePickerView(showIndexBar: false) { country in
    // handle selection
}
```

#### Search Bar

The search bar is enabled by default, allowing users to filter countries by name or dial code. You can disable it if needed:

```swift
CountryDialCodePickerView(showSearchBar: false) { country in
    // handle selection
}
```

#### Appearance

You can customize colors, fonts, and other UI elements by modifying the view or extending it according to your needs.

## ⚠️ Notes

### Keyboard Handling Notes

When the search bar is active, the keyboard appears automatically. The picker view is designed to handle keyboard appearance gracefully, adjusting the list height to prevent it from being obscured.

If you embed the picker in a custom view, ensure you handle keyboard dismissal appropriately, for example by adding a tap gesture to dismiss the keyboard when tapping outside the search field.

### Selection Handling

The picker returns the selected country via a closure. The `CountryDialCode` model contains relevant information such as:

- `name`: The country name (e.g., "United States")  
- `dialCode`: The dial code (e.g., "+1")  
- `code`: The ISO country code (e.g., "US")  

Use this information to update your UI or perform actions based on the user's selection.

### Highlighting Previously Selected Country

You can pass a previously selected country to the picker so that it is highlighted when the picker is opened again. This helps provide context to users and improves the selection experience.

## 📝 Version 1.0.0

Feel free to explore and customize `CountryDialCodePicker` to best fit your app’s needs. Contributions and feedback are welcome!

## 👤 Author

Vishal Vaghasiya  
GitHub: [vishal-vaghasiya](https://github.com/vishal-vaghasiya)
