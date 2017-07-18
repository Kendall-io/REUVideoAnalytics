# REUVideoAnalytics
### A project by Kendall Molas, Tristan Gurtler, Lynn Wu, Charissa Miller for REU NYIT 2017
The purpose of making this program is this analyze when asterices appeared and disappeared in our video recordings by getting the timestamps of these appearances and disappearances.<br>

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
Python<br>Anaconda<br>Jupyter-Notebook<br>FFMPEG

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
```

## History
Update: July 18, 2017 9:17 AM<br>
- Formatting changes<br>
Update: July 17,2017 12:56 AM<br>
- Added usability for the user through jupyter-notebook<br>
Uploaded: July 5, 2017 12:04 AM

## Credits

Denisolt(https://github.com/Denisolt)<br>Tristan Gurtler(https://github.com/tristangurtler)<br>
