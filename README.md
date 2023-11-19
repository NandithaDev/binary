# to run this file 
install openCV, cv.zone and (mediapipe , if issue persist)
run the py file "hand ppt" inside of the "HAND gesture ppt" folder

# Gesture Controls
Raise one finger (thumb) to go to the previous image (left gesture).
Raise the pinky finger to go to the next image (right gesture).



# Code Explanation
The script initializes the camera and sets up the dimensions for the window.

Images for the slideshow are loaded from the "picture" folder. Images are named in a way that they can be sorted for sequential presentation.

The hand tracking module detects the user's hand and tracks its position.

Hand gestures are recognized based on finger positions, and corresponding actions are triggered to navigate through the images.

The slideshow is displayed with a live webcam feed in the corner.

To exit the slideshow, press 'q'.

Further modifications like adjusting the brightness, zooming into the picture, pointer option and ink(drawing) option could be implemented. The total control of the presentation could be controlled by hand gestures.


