
# JBCalendarDatePicker
A replacement for UIDatePicker made for Catalyst.

## Installation

To install, add the source to the top of your podfile:

`source 'https://github.com/joshbirnholz/JBPodSpecs.git'`

Then add this pod to your targets:

`pod 'JBCalendarDatePicker'`

## Use

There are two classes you can use: `JBDatePickerViewController` and `JBCalendarViewController`.

They are both similar to `UIDatePickerView`, and their `date`, `minimumDate`, `maximumDate`, `calendar`, and `locale` properties can be configured as you would with a `UIDatePickerView`. Configure them before presenting either of the view controllers.

`JBDatePickerViewController` also has a `datePickerMode` property as well, although `UIDatePicker.Mode.countDownTimer` is not support.

### JBDatePickerViewController

![enter image description here](https://i.imgur.com/OtPr5V7.png =245x)

`JBDatePickerViewController` displays labels showing its represented date and allows the user to use the keyboard to enter a date. When the user clicks on the date portion, the view controller presents its own `JBCalendarViewController`. You can allow the user to select a date, time, or both, by setting the `datePickerMode` property.

    import JBCalendarDatePicker
    
    class ViewController: UIViewController {
	    var datePicker: JBDatePickerViewController!

		override func viewDidLoad() {
			super.viewDidLoad()

			let datePicker = JBDatePickerViewController()
			view.addSubview(datePicker.view)
			addChild(datePicker)
			datePicker.didMove(toParent: self)
			self.datePicker = datePicker

			// Configure the datePicker's properties
		}
	}

### JBCalendarViewController

![enter image description here](https://i.imgur.com/NV48jUk.png =188x)

`JBCalendarViewController` is just the calendar, without the labels.

The view controller tries to present itself as a popover automatically, so be sure to set the `popoverPresentationController`'s `barButtonItem` property or the `sourceView` and `sourceRect` properties.

    @IBOutlet func buttonPressed(_ sender: UIBarButtonItem) {
        let calendarPicker = JBCalendarViewController()
        calendarPicker.popoverPresentationController?.barButtonItem = sender
        present(calendarPicker, animated: true, completion: nil)
    }
