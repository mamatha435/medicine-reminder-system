USER-CONFIGURABLE MEDICINE REMINDER SYSTEM
AIM

To design and implement a User-Configurable Medicine Reminder System using the LPC2148 ARM7 microcontroller that allows users to configure medicine timings and automatically reminds them to take medicines at the scheduled time using a Real-Time Clock (RTC), LCD display, keypad, and buzzer.

OBJECTIVES:Display the current date and time using the RTC. Allow users to set and modify medicine reminder timings.Monitor medicine schedules continuously.Generate an alert when the configured medicine time is reached.Allow the user to acknowledge the reminder.Continue monitoring after each reminder without restarting the system.



BLOCK DIAGRAM

                           +----------------------+
                           |      Power Supply    |
                           |       (3.3V/5V)      |
                           +----------+-----------+
                                      |
                                      v
                     +--------------------------------+
                     |          LPC2148 ARM7          |
                     |        Microcontroller         |
                     +--------------------------------+
                      |      |        |        |      |
          ------------       |        |        |      ------------
         |                   |        |        |                   |
         v                   v        v        v                   v
    +----------------+   +-------------+  +-------------+   +----------------+
    | 16x2 LCD       |   | RTC Module  |  | 4x4 Keypad  |   |    Buzzer      |
    | Display        |   | (Current    |  | User Input  |   | Alert Output   |
    | Time & Alerts  |   | Date & Time)|  |             |   |                |
    +----------------+   +-------------+  +-------------+   +----------------+
                                                     ^
                                                     |
                                     +---------------+---------------+
                                     |                               |
                              +--------------+                +--------------+
                              | Switch-1     |                | Switch-2     |
                              | EINT0        |                | EINT1        |
                              | Configuration|                | Acknowledge  |
                              +--------------+                +--------------+



HARDWARE REQUIREMENTS:  
LPC2148 ARM7 Microcontroller, RTC (Real-Time Clock), 16×2 LCD Display, 4×4 Matrix Keypad, Buzzer, Two Push Buttons, Switch-1 (EINT0), Switch-2 (EINT1), USB-UART, Converter / DB9 Cable, Power Supply.

SOFTWARE REQUIREMENTS:
Embedded C, Keil uVision IDE, Flash Magic, LPC2148 Header Files


<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/87804aaa-d614-482b-830b-79b8075a520f" />


ROLE OF EACH COMPONENT: LPC2148 Acts as the brain of the system.
Functions:
Reads current time from RTC., Displays time on LCD. Reads keypad inputs. Stores medicine schedules.Compares current time with stored schedules.Controls buzzer. Handles external interrupts.
RTC (Real-Time Clock) Maintains accurate date and time.
Functions:Runs continuously even after power reset (with backup battery). Provides current time to LPC2148.Used for reminder comparison.
LCD Displays: Current Time, Current Date, Configuration Menu, Medicine Time, Reminder Messages

Example:Time : 09:30 AM - Date : 18/07/2026 . Reminder:Take Medicine Now ,4×4 Matrix Keypad Used for Setting RTC Entering medicine timings Selecting menu options

Example: Medicine Time: 08:30 ->Buzzer - Provides an audible reminder.

Operation:
Time Match

↓

Buzzer ON

↓

User presses Switch-2

OR

1 minute timeout

↓

Buzzer OFF
Switch-1 (EINT0)

Purpose

Enter configuration mode.

Functions

Edit RTC
Add medicine timing
Modify medicine timing
Switch-2 (EINT1)

Purpose: Acknowledges medicine intake.
Functions:Stops buzzer immediately, Clears reminder, Returns to clock mode

WORKING PRINCIPLE
Step 1: System Initialization: After power ON,LPC2148 initializes:RTC,LCD, Keypad, Buzzer, External Interrupts, GPIOLCD displays: Medicine Reminder System

Step 2: Display Current Time. Controller continuously reads RTC. LCD displays: 18/07/2026  09:45:18

Step 3: Configuration Mode:  When Switch-1 is pressed,  Interrupt EINT0 occurs. LCD shows: 1.Edit RTC        2.Set Medicine     RTC Configuration

User enters: 1.Date     2.Month     3.Year       4.Hour    5.Minute      6.Second        RTC gets updated.         Medicine Configuration

User enters:Example: Medicine 1  -> 08:00 AM .  Medicine 2   -> 01:00 PM.          Medicine 3  ->  08:30 PM   controller stores these timings.

Step 4: Normal Monitoring   Controller repeatedly performs Read RTC-> Compare Current Time  -> Compare with all stored medicine timings  -> Match?  Yes → Alert No → Continue
Step 5: Reminder Generation:Suppose current time  08:00 AM  Stored schedule:  08:00 AM    Controller detects match.  LCD displays: Take Medicine Now ->Buzzer turns ON.

Step 6: Acknowledgment : User presses Switch-2. Interrupt EINT1 occurs. Controller Stops buzzer,Clears message,  Returns to RTC display.
Step 7: Timeout  If user does not press Switch-2,  Controller waits for  1 minute  Then  Stops buzzer automatically Clears reminder  Continues monitoring
Step 8: Continuous Operation : The controller repeats

     Read RTC

       ↓
    Compare Time

      ↓

    Reminder

      ↓

     Wait

     ↓

    Repeat

    System runs continuously.

SOFTWARE FLOW:

     Power ON
      |
    Initialize LCD
    RTC
    Keypad
    Buzzer
    Interrupts
        |
    Display Current Time
      |
    Switch-1 Pressed?
      |
    Yes -------------- No
    |                  |
    Configuration      |
    Mode               |
    |                  |
    Store Schedule     |
     |                 |
    Return             |
      |                |
    Read RTC           |
      |                |
    Compare Current Time
    with Medicine Schedule
      |
     Time Match?
      |
     No ---------- Yes
     |              |
     |         LCD Message
     |         Buzzer ON
     |              |
     |       Switch-2 Pressed?
     |              |
     |      Yes -------- No
     |       |            |
     | Stop Buzzer    Wait 1 min
     | Clear Alert         |
     |       |             |
     |       ------Timeout-|
     |              |
    Return to RTC Display
       |
    Repeat Forever

APPLICATIONS:

1.Home medicine reminder
2.Elderly patient assistance
3.Hospital patient monitoring
4.Medical clinics
5.Nursing homes
6.Healthcare automation
7.Personal healthcare devices
8.Rehabilitation centers

ADVANTAGES:

1.Easy to configure.
2.Automatic medicine reminders.
3.Accurate timing using RTC.
4.Low power consumption.
5.Simple user interface.
6.Prevents missed medication.
7.User acknowledgment feature.
8.Portable and reliable.
9.Can be modified to support multiple reminders.
10.Low-cost embedded solution.

LIMITATIONS:Limited number of medicine schedules depending on memory.  No wireless communication. No SMS or mobile notification. Manual configuration required.
Single-user system.

FUTURE ENHANCEMENTS

1.GSM module for SMS reminders.
2.Wi-Fi/IoT monitoring.
3.Mobile application integration.
4.Voice reminders.
5.Cloud data storage.
6.Fingerprint-based user identification.
7.Medicine box automation.
8.Multiple user profiles.
9.Battery backup with power-failure notification.
10.Bluetooth connectivity.

CONCLUSION

The User-Configurable Medicine Reminder System provides a reliable embedded solution for timely medication management. Using the LPC2148 microcontroller, RTC, LCD, keypad, and buzzer, the system continuously monitors real time, allows users to configure medicine schedules, and generates alerts at the appropriate time. The acknowledgment mechanism using external interrupts makes the system interactive and user-friendly, while its modular design allows future expansion with IoT, GSM, or mobile applications for enhanced healthcare support.
