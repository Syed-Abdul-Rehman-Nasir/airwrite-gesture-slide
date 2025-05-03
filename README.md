# Virtual Painter 
AirWrite is a Python-based project that allows users to write in the air using hand gestures detected through OpenCV and MediaPipe. The system tracks hand movements in real-time to enable touchless text input.

Main Idea
*Detect hands using MediaPipe
*Track the index and middle fingers to recognize gestures
*Track fingertip locations in real-time
*Draw text on a black canvas when only the index finger is up
*Make a selection (e.g., change drawing tool or color) when both index and middle fingers are up
*Mask the drawing with the live webcam frame to create a seamless interaction

Installation
There are some prerequisites that need to be installed to run this project.

Install the required libraries by running the following command in the project directory:
pip install -r requirements.txt

Now you can run the project directly from your terminal:
python main.py
If everything is set up correctly, a window will pop up and the module is ready to use.

