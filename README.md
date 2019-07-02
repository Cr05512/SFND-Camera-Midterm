MP.1 Data Buffer Optimization:  
In order to keep the data buffer size constant to 2, an ```erase``` of the oldest element  
in the vector has been performed only when the dimension exceedes the preferred one.

MP.2 Keypoint Detection:  
The implementation of Harris has been taken from previous exercises, while the  
other ones (FAST, BRISK, ORB, AKAZE, and SIFT) have been added under the function  
descKeypointsModern() through an IF-ELSE selection based on the String provided.

MP.3 Keypoint Removal:  
To filter out all the points outside the given Rect, it has been performed a check  
over all the detected features and by keeping only the ones inside. The code function  
is the:  
```
vehicleRect.contains(keypoints[i].pt)
```

MP.4 Keypoint Descriptors:  
As for the detectors, the descriptors can be selected by providing the corresponding  
string in the main program and, through an IF-ELSE selection, the relative descriptor  
object is created and the keypoints descriptors are returned.  

MP.5 Descriptor Matching:  
Here the FLANN and KNN Methods have been implemented by looking at the documentation  
and by checking eventual data type (The FLANN library accepts only CV_32F data). Both  
methods can be selected by providing the right string in the main program.  
NOTE: In the BF approach a check over the descriptorName has been added in order to  
switch the norm type in the case the user forgets to select it. The SIFT descriptor  
returns non-binary values which are not suitable for Hamming Distance.  

MP.6 Descriptor Distance Ratio:  
Here the descriptor distance ratio test has been implemented with a 2-Nearest-Neighbor,  
in order to select only the best match if and only if the mentioned approach condition  
is satisfied.  

MP.7 Performance Evaluation 1:  
In order to count the total number of detected keypoints, an auxiliary variable has been used,  
namely ```totalKpts```, which contains, by the end of the main program, the sum of all the detected  
keypoints over all the frames. In the provided spreadsheet, it is possible to find the total number of  
detections for each detector. About the distribution of keypoints, it has been noticed  
that the majority of detections fall onto the contours of the car/shadows where a stronger  
discontinuity in light is present, or onto the internal seats where, as well, the intensity  
change is well marked. As expected, some keypoints fall even into the road or by near  
vehicles. One weak observation, the density of keypoints seems to grow with the preceding vehicle  
getting closer.  

MP.8 Performance Evaluation 2:  
To do this, similarly as MP.7, an auxiliary variable, namely ```totalMatches```, has been  
used to accumulate all the matches over the frames. Moreover, as suggested from the  
rubric, the ```MAT_BF``` method has been selected with a descriptor distance ratio set  
to 0.8.

MP.9 Performance Evaluation 3:  
As final point, a ```loggerTime``` table has been instantiated (in this case a 10x2 matrix)  
and with the help of two support variables, ```tDetector``` and ```tDescriptor```, the table  
elements have been filled with computed execution times for the detector algorithm (left column)  
and the descriptor one (right column). Furthemore, a mean over all the frames has been taken  
in order to provide an average time for a particular detector and descriptor. In the provided  
spreadsheet, it is possible to find all the combinations between detectors and descriptors with  
the corresponding average times, total time, total keypoints found, total matches and finally  
the ratio between matched points and found ones. Hence, as requested, a TOP 3 table has been  
built containing the best choices in terms of total time, with the FAST-BRIEF combination  
resulting as the best one. Considering the matches over keypoints ratio, a second table  
has been provided in order to suggest the best combinations in terms of the given measure.  
As personal conclusion, I would pick the FAST-BRIEF combination which resembles one of the  
fastest pair which, at the same time, keeps a decent matching ratio. On the other hand, if  
a wide computational power is available, I would pick the SHITOMASI-BRIEF coupling,  
considering that the total computation time is low and the matching ratio is really high. 

Some side notes:  
The combination SIFT-ORB breaks the program due to an out-of-memory error, might be a bug.  
The AKAZE descriptor can be used only with AKAZE keypoints, but the viceversa  
is not true; a check has been added to fix this.  
The interaction time with the OpenCV windows seems to influence (not always) a little the performances  
of detectors in terms of execution times.  
All the simulations have been done on an Intel i7-8750H processor clocked at 2.20GHz (12threads).  
The work has been done entirely on a local machine and using OpenCV-4.1.0

