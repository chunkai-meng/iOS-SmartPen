# Technologies learned from AS1 & 2

## **List of technologies**
### Property Observers
```Swift
    var selectedShapeTag: Int = 0 {
        willSet(newTag) {
            shapeButtonArray[newTag].isSelected = true
        }
        didSet(oldTag) {
            if selectedShapeTag != oldTag {
                shapeButtonArray[oldTag].isSelected = false
            }
        }
    }
```

### **Pass value between different controller**
- Protocol
```swift
// delcare a protocal
protocol SettingsViewControllerDelegate: class {
    func settingsViewControllerFinished(_ settingsViewController: SettingsViewController)
}
```
- Delegate
```swift
    var delegate: SettingsViewControllerDelegate?


    @IBAction func dismissView(_ sender: Any) {
 
        self.dismiss(animated: true, completion: nil)
        self.delegate?.settingsViewControllerFinished(self)
    }
```
委托[1]是一个允许类或者结构体放手（或者说委托）它们自身的某些责任给另外类型实例的设计模式。这个设计模式通过定义一个封装了委托责任的协议来实现，比如遵循了协议的类型（所谓的委托）来保证提供被委托的功能。委托可以用来响应一个特定的行为，或者从外部资源取回数据而不需要了解资源具体的类型。

By using the delegation, I pass all the setting values from settingViewController to the main viewController.
This delegation respond to the settingViewController’s action, save and exit.


- Extension
```swift
extension ViewController: SettingsViewControllerDelegate {

    func settingsViewControllerFinished(_ settingsViewController: SettingsViewController) {

        if self.currentBrush.red == settingsViewController.redColorValue &&
            self.currentBrush.green == settingsViewController.greenColorValue &&
            self.currentBrush.blue == settingsViewController.blueColorValue {

            // Get new opacty & size
            self.currentBrush.opacty = settingsViewController.opacity
            self.currentBrush.size = settingsViewController.lineWidth

        } else {

            // Get the new color from Setting View
            self.currentBrush.red = settingsViewController.redColorValue
            self.currentBrush.green = settingsViewController.greenColorValue
            self.currentBrush.blue = settingsViewController.blueColorValue

            // remove highlight from color button
            colorButtonArray[selectedColorTag].backgroundColor = UIColor.white
        }
    }
}
```


## 