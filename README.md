# AirWrite & Gesture Slide
This project uses OpenCV and MediaPipe libraries to utilize the web camera for real-time gesture-based interaction. It includes two main modules:

# Virtual Painter module
*Detect hands using MediaPipe 
*Detect whether the index and middle fingers are up 
*Detect fingers' tip location 
*Draw a line when only the index finger is up and make a selection when both index and middle fingers are up 
*Draw on a black canvas and then mask it with the actual frame

# Gesture Slide module 
*Detect hand gestures using MediaPipe 
*Use swipe gestures (left/right) to navigate between slides 
*Enable touchless slide control during presentations

Installation There are some prerequisites that need to be installed to run this project.

Install the required libraries by running the following command in the project directory: 
pip install -r requirements.txt

Now you can run the project directly from your terminal: python main.py If everything is set up correctly, a window will pop up and the module is ready to use.


