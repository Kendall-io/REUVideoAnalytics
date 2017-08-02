# REUVideoAnalytics
### A project by Kendall Molas, Tristan Gurtler, Lynn Wu, Charissa Miller for REU NYIT 2017
The purpose of making this program is to analyze when asterisks appeared and disappeared in our video recordings by getting the timestamps of these appearances and disappearances.<br>

The process is somewhat long due to making several .csv files and .txt files. The .csv files that are made when using this code is:
- frames.csv
    - Contains time frame data of the video
- results.csv
    - Contains the dataframe and the frames.csv into one .csv file
- relevantKeyPresses.txt
    - Contains all the relevant keypresses
- cleanedRelevantKeyPresses.txt
    - Cleans the relevantKeyPresses.txt due to whitespace and extra lines of text that does not need to be there.


## Prequisites
Python<br>Anaconda<br>Jupyter-Notebook<br>FFMPEG<br>OpenCV

## Usage
### Part 1 of VideoProcess_Part1.ipynb
Extracting the frames of a given video at a specific FPS. The only variables that need to be implemented and changed is:<br>
- startTime
	- Start video from a certain time-frame 00:00:00.000 (hours,minutes,seconds,milliseconds), user-determined
- videoFileName
- videoFileExtension
- contrastVal
	- Numerical value which changes the contrast of the extracted images of the video
- brightnessVal
	- Numerical value which changes the brightness of the extracted images of the video, used for videos that are too 'dark'
- cropImage
	- Dimensions of the extracted image. [x,y,z,w] | [x,y] is the image size, and [z,w] is the coordinate on the image where it will start creating. The specific values that was used for the REU was [55:120:1245:445]
- rotateImage
	- The specific values that was used fro the REU was '-10*PI/180'
```python
startTime = 'Insert start time here'
videoFileName = 'Enter video name here, do not include the extension'
videoFileExtension = 'Enter video extension here'
videoToBeProcessed = videoFileName + videoFileExtension
imageFileSaveArea = 'images' + videoFileName
frameFileName = 'frames' + videoFileName + '.csv'
contrastVal = 'Enter contrast value'
brightnessVal = 'Enter brightness value'
cropImage = 'Crop size and area'
rotateImage = 'How much it is being rotated'
```

## Part 2 of VideoProcess_Part2.ipynb
```python
videoFileName = 'Input video file name that was just processed here'
```
<br>

This is for debugging purposes for the user to see what the image looks like after analyzation
```python
###
# This is used for debugging purposes to see how the image is like after contours are drawn
# Usage: Input the image file name in the area below
###

# Read the image
img = cv2.imread('../' + imageFileSaveArea + '/____')
# Grayscale the read image
im_gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
# Apply the bilateral filter onto the grayscale image
bf_image = cv2.bilateralFilter(im_gray, 6, 175, 175)
# Apply the canny edge filter on the bilateral filtered image
ed_image = cv2.Canny(bf_image, lowThresh, high_thresh)

_, contours, _ = cv2.findContours(ed_image, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

contour_list = []
asterisksPresent = 0
for cnts in contours:
    approx = cv2.approxPolyDP(cnts, 0.01*cv2.arcLength(cnts,True),True)
    area = cv2.contourArea(cnts)
    if ((len(approx) > 0) & (area > 30) or ((len(cnts) > 0) & (area > 10))):
        asterisksPresent = asterisksPresent + 1
        contour_list.append(cnts)
        
print 'Asterisks present are: %d' % asterisksPresent        
cv2.drawContours(ed_image, contour_list,  -1, (255,255,0), 2)
plt.imshow(img)
plt.show()
```

## History
Update: July 28, 2017<br>
Update Code to look cleaner and act more as necessary.
<br>

Update: July 18, 2017 9:17 AM<br>
Formatting changes<br>
<br>
Update: July 17,2017 12:56 AM<br>
Added usability for the user through jupyter-notebook<br>
<br>
Uploaded: July 5, 2017 12:04 AM

## Credits

Denisolt(https://github.com/Denisolt)<br>Tristan Gurtler(https://github.com/tristangurtler)<br>
