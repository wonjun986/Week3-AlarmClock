# Week3-AlarmClock
week3 practice
//게임공학전공 허원준

import UIKit

class ViewController: UIViewController {
    
    let timeSelector: Selector = #selector(ViewController.updateTime)
    
    let interval = 1.0
    
    var alarmTime: Date?
    
    var count = 0
    
    @IBOutlet var lblCurrentTime: UILabel!
    @IBOutlet var lblPickerTime: UILabel!
    @IBOutlet var datePicker: UIDatePicker!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        Timer.scheduledTimer(timeInterval: interval, target: self, selector: timeSelector, userInfo: nil, repeats: true)
        
        updateTime()
    }

    @objc func updateTime() {
        let currentDate = Date()
        
        let formatter = DateFormatter()
        formatter.dateFormat = "yyyy-MM-dd HH:mm:ss EEE"
        let currentTimeString = formatter.string(from: currentDate)
        
        lblCurrentTime.text = currentTimeString
        
        if let alarmTime = alarmTime, currentDate >= alarmTime {
            view.backgroundColor = UIColor.red
        } else {
            view.backgroundColor = UIColor.white
        }
    }
    
    @IBAction func changeDatePicker(_ sender: UIDatePicker) {
        let selectedTime = sender.date
        
        let formatter = DateFormatter()
        formatter.dateFormat = "yyyy-MM-dd HH:mm:ss EEE"
        lblPickerTime.text = "선택된 알람 시간: " + formatter.string(from: selectedTime)
        
        alarmTime = selectedTime
    }
}
