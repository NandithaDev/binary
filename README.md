# binary

import cv2
import os
from cvzone.HandTrackingModule import HandDetector


#variable
width,height = 1200,720
folderPath = "picture"



#camera setup
cap = cv2.VideoCapture(0)
cap.set(3,width)
cap.set(4,height)

#Presentation List(add more later)
pathImages = sorted(os.listdir(folderPath),key = len)
print(pathImages)

#variables
imgNumber = 3
scale = 2
hs,ws = int(120*scale),int(213*scale)
gestureThreshold = 250
flag = False
flag_count = 0
flag_delay = 30


#HAnd detector
detector = HandDetector(detectionCon = 0.8, maxHands =1)

while True:
    #Importing images
    succes, img = cap.read()
    img = cv2.flip(img,1)
    pathFullImages = os.path.join(folderPath,pathImages[imgNumber])
    imgCurrent = cv2.imread(pathFullImages)
    imgCurrent=cv2.resize(imgCurrent,(780,540))


    #hand dtector code
    hands, img = detector.findHands(img)
    cv2.line(img, (0, gestureThreshold),(width,gestureThreshold),(0,255,0),10)

    if hands and flag is False:
        hand = hands[0]
        fingers = detector.fingersUp(hand)
        cx, cy = hand["center"]
        # print(fingers)

        if cy <= gestureThreshold:

            #gesture1 --> left
            if fingers == [1,0,0,0,0]:
                print("left")
                flag = True
                imgNumber -= 1
                imgNumber = max(0,imgNumber)
            #gesture1 --> right
            if fingers == [0,0,0,0,1]:
                flag = True
                imgNumber += 1
                imgNumber = min(imgNumber,len(pathImages)-1)
                print("right")
    if flag:  
        flag_count += 1
        if flag_count > flag_delay:
            flag = False
            flag_count =0
    
    #adding webcam images on the slide
    imgSmall = cv2.resize(img,(ws,hs))
    h , w,_ = imgCurrent.shape
    imgCurrent[0:hs,w-ws:w] = imgSmall
    
    #cv2.imshow("Image",img)
    cv2.imshow("slides",imgCurrent)
    key = cv2.waitKey(1)
    if key == ord("q"):
        break




