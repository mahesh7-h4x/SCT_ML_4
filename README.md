Hand Gesture Recognition with MediaPipe
A real-time hand gesture recognition system using MediaPipe and OpenCV that detects various hand gestures through webcam input.

🎯 Features
Real-time hand gesture recognition using webcam

Support for 6 different gestures:

✋ Halo - All fingers extended

👌 OK - Thumb and index finger forming a circle

🤟 I Love You - Thumb, index, and pinky fingers extended

✌️ Peace - Index and middle fingers extended

✊ Fist - All fingers closed

👍 Sip/Thumbs Up - Thumb extended, other fingers closed

Real-time visual feedback with hand landmarks

Cross-platform compatibility

🚀 Installation
Prerequisites
Python 3.7 or higher

Webcam

Install Dependencies
bash
pip install opencv-python mediapipe
📁 Project Structure
text
hand-gesture-recognition/
├── gesture_recognition.py    # Main application file
├── requirements.txt          # Dependencies
└── README.md                # This file
🎮 Usage
Run the application:

bash
python gesture_recognition.py
Perform gestures in front of your webcam:

Make sure your hand is clearly visible

The system will detect and display the recognized gesture

Hand landmarks will be drawn in real-time

Controls:

Press Q to quit the application

✋ Supported Gestures
1. Halo ✋
Description: All five fingers extended upward

Use Case: General greeting, selection mode

2. OK 👌
Description: Thumb and index finger forming a circle, middle finger extended upward

Use Case: Confirmation, approval

3. I Love You 🤟
Description: Thumb, index, and pinky fingers extended; middle and ring fingers closed

Use Case: Expression, special command

4. Peace ✌️
Description: Index and middle fingers extended upward; other fingers closed

Use Case: Victory, two-finger selection

5. Fist ✊
Description: All fingers closed into a fist

Use Case: Cancel, grab, selection

6. Sip/Thumbs Up 👍
Description: Thumb extended upward; other fingers closed

Use Case: Approval, positive feedback

🔧 Technical Details
Detection Logic
The system uses MediaPipe Hand Landmarks to track 21 key points on the hand. Gesture recognition is based on:

Finger State Detection: Compares Y-coordinates of finger tips and PIP joints

Proximity Checks: Measures distance between thumb and index finger for "OK" gesture

Multi-finger Patterns: Checks specific combinations of extended/folded fingers

Key Components
MediaPipe Hands: Provides real-time hand tracking

OpenCV: Handles video capture and display

Landmark Analysis: Processes hand landmarks for gesture classification

🎯 How It Works
Hand Detection: MediaPipe detects hands in the video frame

Landmark Extraction: 21 hand landmarks are extracted for each detected hand

Gesture Analysis: Landmark positions are analyzed to determine finger states

Classification: Predefined rules match landmark patterns to gestures

Visual Feedback: Results are displayed with landmarks and gesture labels

⚙️ Customization
Adding New Gestures
You can extend the system by adding new gesture detection rules:

python
# Example: Adding a "Pointing" gesture
index_up = y(lm, mp_hands.HandLandmark.INDEX_FINGER_TIP) < y(lm, mp_hands.HandLandmark.INDEX_FINGER_PIP)
others_down = all(
    y(lm, tip) > y(lm, pip) for tip, pip in [
        (mp_hands.HandLandmark.MIDDLE_FINGER_TIP, mp_hands.HandLandmark.MIDDLE_FINGER_PIP),
        (mp_hands.HandLandmark.RING_FINGER_TIP, mp_hands.HandLandmark.RING_FINGER_PIP),
        (mp_hands.HandLandmark.PINKY_TIP, mp_hands.HandLandmark.PINKY_PIP),
    ]
)
if index_up and others_down:
    gesture = "Pointing"
Adjusting Detection Sensitivity
Modify the confidence thresholds in the MediaPipe setup:

python
hands = mp_hands.Hands(
    static_image_mode=False,
    max_num_hands=1,
    min_detection_confidence=0.7,  # Increase for stricter detection
    min_tracking_confidence=0.5    # Increase for more stable tracking
)
🐛 Troubleshooting
Common Issues
No Hand Detection

Ensure good lighting

Keep hand clearly visible

Check webcam permissions

Incorrect Gesture Recognition

Make clear, distinct gestures

Keep hand steady

Adjust camera distance

Performance Issues

Close other applications using the camera

Reduce background clutter

📝 Requirements File
Create a requirements.txt file:

txt
opencv-python==4.8.1.78
mediapipe==0.10.0
Install with:

bash
pip install -r requirements.txt
🎯 Future Enhancements
Add gesture-based control for applications

Support for two-hand gestures

Gesture sequence recognition

Machine learning-based classification

Integration with desktop applications

Custom gesture training

🤝 Contributing
Feel free to contribute by:

Adding new gestures

Improving detection accuracy

Enhancing performance

Adding new features

📄 License
This project is open source and available under the MIT License.
