# larva-video-correction
Script that detects and corrects errors in a larva video recording software (PiVR) developed by Louis Lab

# Notebook Files
### Version 1
Detecting head-tail swap errors based on the *change in tail position*. If the change in tail position meets a certain threshold, 
then we can consider it an error. Through EDA, we see that there are certain peaks throughout the video which indicate potential 
error points where the head-tail coordinates swap.

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
