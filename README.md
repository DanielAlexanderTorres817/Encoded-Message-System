# Encoded Messaging System

## Project Overview

This project simulates the game **"Pass It On!"** using Adafruit Circuit Playground Classic boards. The goal of the game is to pass a specific gesture between players, and the system will recognize if the gesture has been transmitted successfully. Players attempt to replicate a pre-recorded gesture, and if detected correctly, the system provides visual and audio feedback, confirming success.

The game utilizes the Circuit Playground’s built-in accelerometer to capture gesture data, compares it against 10 pre-recorded gestures stored in flash memory, and provides feedback using the board's neopixels and buzzer.

## Features

- **Real-time Gesture Recognition**: Detects and compares player gestures to pre-recorded patterns using accelerometer data.
- **Visual Feedback via Neopixels**: The Circuit Playground’s neopixels light up with specific colors to indicate game states like success or failure.
- **Audio Feedback**: Buzzer tones indicate success or failure during gameplay.
- **Gesture Filtering**: Sliding window averaging is applied to smooth accelerometer readings and reduce noise.
- **Pre-recorded Gestures**: Ten pre-recorded gestures are stored in flash memory and used for comparison.

## Hardware Requirements

- **Adafruit Circuit Playground Classic**: Provides accelerometer data, neopixel feedback, and buzzer sounds for the game.
  
## Software Requirements

- **Arduino IDE**: Used to write, compile, and upload the code to the Circuit Playground.
- **Adafruit Circuit Playground Library**: Provides access to the accelerometer, neopixels, and buzzer.

## Project Structure

- **main.cpp**: The main source code file that controls gesture detection, game logic, and interaction with Circuit Playground hardware.
- **Adafruit_CircuitPlayground.h**: Provides functions for accessing hardware components such as the accelerometer, neopixels, and buzzer.

## Key Functions

- **`light_LED(int pixel, uint32_t color)`**: Lights up a specific neopixel with a given color for 5 seconds and turns off the LEDs afterward.
- **`print_gesture(float gesture[COUNTER][3])`**: Prints out a gesture for debugging purposes.
- **`get_gesture_value(int gesture_index, int i, int j)`**: Retrieves a specific gesture reading from the stored gestures in flash memory.
- **`find_closest_gesture(float current[COUNTER][3])`**: Compares the current gesture against the 10 pre-recorded gestures and returns the closest match, or throws an error if no match is found.
- **`averageGesture(float gesture[COUNTER][3])`**: Filters out noise from the current gesture using a sliding window technique to smooth the data.
- **`setup()`**: Initializes the Circuit Playground, setting up the accelerometer and other hardware components.
- **`loop()`**: Continuously checks for gestures, records accelerometer data, and compares it against the pre-recorded gestures to provide feedback on success or failure.

## How It Works

1. **Gesture Detection**: 
   - When the player presses the left button, the accelerometer captures 40 readings for the X, Y, and Z axes.
   - These readings are stored in a `current_gesture` array.

2. **Gesture Filtering**:
   - The `current_gesture` data is filtered using a sliding window technique to remove noise and smooth out the gesture data.

3. **Gesture Comparison**:
   - The system compares the filtered gesture with the 10 pre-recorded gestures stored in flash memory using Euclidean distance to determine the closest match.

4. **Visual and Audio Feedback**:
   - If the gesture is correctly recognized, a specific neopixel lights up, and a success tone is played via the buzzer.
   - If the gesture is not recognized, the red LED lights up, and a failure tone is played.

## How to Build and Run

1. **Clone the repository** or download the project files.
2. **Install the Adafruit Circuit Playground Library** in the Arduino IDE:
   - Go to `Sketch` > `Include Library` > `Manage Libraries`, search for "Adafruit Circuit Playground", and install it.
3. **Connect the Adafruit Circuit Playground Classic** to your computer via USB.
4. **Upload the Code**:
   - Open `main.cpp` in the Arduino IDE, select the correct board and port, and upload the code to the Circuit Playground.
5. **Play the Game**:
   - Press the left button to start recording your gesture.
   - Wait for the game to recognize your gesture, then observe the visual and audio feedback on the board.

## Customization

- **Adding New Gestures**:
   - You can modify the `gestures` array in the code to add new pre-recorded gestures. This involves replacing the existing gesture values with new accelerometer readings.
- **Error Threshold**:
   - Adjust the `error_threshold` variable to control how strictly the game matches player gestures to pre-recorded gestures. Lower values make the game more sensitive, while higher values allow for more error in the gesture.
- **Neopixel Colors**:
   - The `color_array` stores the colors for each neopixel. You can change the colors by modifying the values in this array.



## Video Demonstration
https://github.com/user-attachments/assets/c32250fa-7f2f-418b-8b1b-eb9399861ad5

