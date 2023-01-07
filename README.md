# larva-video-correction
Script that detects and corrects errors in a larva video recording software (PiVR) developed by Louis Lab

# Notebook Files
### Version 1
Detecting head-tail swap errors based on the *change in tail position*. If the change in tail position meets a certain threshold, 
then we can consider it an error. In the chart below detailing the change in tail position over video frames, we see that there are certain peaks throughout the video which indicate potential error points where the head-tail coordinates swap.

<img width="295" alt="Screen Shot 2023-01-07 at 2 06 06 PM" src="https://user-images.githubusercontent.com/89556961/211172146-91e4eab0-0d7b-451e-b29b-1efe38180fef.png">

### Version 2/2.5
Fixing minor errors in the subfunctions written from V1. Realizing that using change in tail position as a marker for HT errors 
is not accurate. After manually lining up the actual video with our EDA plots from V1, there were many cases where a HT swap occurs 
but the change in tail position was below our defined threshold.

While I was manually watching videos of larva, I noticed that everytime an error occured it was always before the larva "blinks." 
In this case, a "blink" is when the head, tail, and centroid coordinates all converge into the centroid position. However, not ALL 
"blinks" indicate an error. To check if an error occured at the blink, I took the angle between the vector formed before and after 
the blink as a threshold of whether it is an error. 

Also found that the video files for unprocessed and processed data are very different. Processed data will smooth the larva movements 
and remove instances when the larva "blinks." With this realization, it is important for lab members to first run the error correction 
script with unprocessed data THEN run the processing script to smoothen movements. 

![IMG_61F7087703F3-1](https://user-images.githubusercontent.com/89556961/211171830-7f8bd346-f1a5-433c-b6d2-fe680aaf5ae5.jpeg)

### Version 3
Using the new method, the script was able to catch and fix about 81% of errors that occured. Another member of the coding team developed 
a filter to process the data in a manner that the `ht_correction` function could more easily digest. When running the script after the filter, 
it could catch about 90% of errors that occured.

### Sample Output
Orange = tail of larva

Blue = head of larva

In the left picture, the video software indicates that the tail of the larva is shifting a lot which is not characteristic of larva behavior. Typically, 
only the head of the larva is shifting to scope out the environment while the tail simply follows. Thus, it is clear that an error occurred in the 
video's detection of head and tail. After applying the script, the orange line is smoother which means the errors were identified and corrected.

<img width="367" alt="Screen Shot 2023-01-07 at 2 04 56 PM" src="https://user-images.githubusercontent.com/89556961/211172117-fda02c32-696e-4431-bffd-9918d45793b4.png">

