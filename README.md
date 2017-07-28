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
### More information can be found in documentation
```python
startTime = '[Insert start time here]'
videoFileName = '[Enter video name here, do not include the extension]'
videoFileExtension = '[Enter video extension here]'
videoToBeProcessed = videoFileName + videoFileExtension
imageFileSaveArea = 'images' + videoFileName
frameFileName = 'frames' + videoFileName + '.csv'
contrastVal = '[Enter contrast value]'
brightnessVal = '[Enter brightness value]'
cropImage = '[Crop size and area]'
rotateImage = '[How much it is being rotated]'
```

## In part2.ipynb
This is for debugging purposes for the user to see what the image being analyzed, looks like.
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
