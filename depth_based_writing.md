---
title: Depth Based Writing and Tracking
parent: Proposed Solution
nav_order: 1
---
## Depth Based Writing and Tracking

The first problem that we have addressed is key-point tracking. The finger key-point has to be efficiently tracked across frames to give a smooth writing effect. Before delving into our solution to this problem, let us first look at previous approaches to the problem. The most basic approach in finger tracking was template matching. But since it was not scale and rotational invariant, additional computations were needed to make it more robust. Incorporating them would in turn, lead to a decrease in frame processing rate. Also, as the finger of every person is different, using template matching was not an universal solution.

The next solution was optical flow, particularly the Lucas-Kanade Optical Flow algorithm. This algorithm tracks a given moving point efficiently. However, it is a bit slow when applied over the entire frame. Another disadvantage of this approach is that it is highly dependent on the given reference point. There is a possibility of errors progressively increasing, and overtime the reference point might drift away from the desired location. This leads to a need for frequent re- calibration.

The final solution is the MediaPipe based key-point localization. As it detects the key-point efficiently between frames, it can be used for air writing. However, one disadvantage with this approach is that it does not have the memory of the previous point and the end output has jitters associated with it. This leads us to our solution.

We have combined the advantages of optical flow with that of MediaPipe, the result of which eradicated their standalone issues. We have used MediaPipe for calibration and optical flow for tracking purposes. This eliminates the jitter problem we had before as well as the progressive error build-up issue with optical flow. As stated previously, using the entire image frame to write is both algorithmically costly and puts strain on the user’s hands. To avoid this, we have defined a small Region of Interest (ROI) so that the user has more control and improved performance. Applying optical flow on this ROI makes it robust. But having a small ROI limits the user to write within the confined space. To remedy this, our product uses a novel “lazy move” based approach that increases the size of the board dynamically with respect to the movement of the cursor. This enables the user to utilize a larger space using the same ROI. More details regarding this will be divulged ahead.

The second part of our solution is with regards to hand removal. Now that the user is able to write efficiently on the virtual blackboard, how can he/she stop writing? The most famous solution to this problem is using two gestures, one to enable writing and the other one to stop writing. While this does the job for us, it also adds an additional overhead to the user. Frequent changes of the gestures can be confusing to the user. Our solution addresses this problem in a more efficient way.

To see how, let us go back to the concept of traditional blackboards. When the user wants to write, he would place the marker on the plane, i.e., the board and when the user wants to stop writing, he/she would remove the finger out of the plane. This is where our idea spawned. We decided to split the world space into two zones in order to mimic the traditional boards: writing zone and tracking zone. Here, the writing zone is the board, whereas the tracking zone is the space in front of the board. When the user’s hand is inside the writing zone, we implement the writing algorithm and the user can write on the board. When the user’s hand is in the tracking zone, the tracking algorithm is implemented where the index finger is now tracked continuously. This helps the user to understand where the cursor currently is with respect to the writing board.

#### Depth Based Hand Removal 
<img src="assets/flowchart1.png" width="635" height="350" alt="Depth Based Hand Removal ">&nbsp;&nbsp;

Another feature of our solution is that the user can decide where his writing zone can be. The threshold is set by the user himself. If at one point of time, the user is at a particular position he can set the writing zone to be in front of his body. If at another point of time, the user decides to move out of that position, he/she can correspondingly shift the writing zone as well. This gives additional flexibility to the user to move around.

#### Depth Based Hand Removal for the letter i
![Depth Based Hand Removal](assets/depth_based_hand_removal.gif)

To summarize, our product makes use of two deep learning models to efficiently implement the air writing algorithm:

• First, MediaPipe is used to localize the hand keypoints and the key-point of the index finger is used for calibration. This point is provided to the optical flow algorithm in the subsequent frames for smooth tracking. The reason we use a blend of MediaPipe and optical flow is because optical flow is more efficient in tracking the key point over time. As MediaPipe doesn’t have the memory of the key-point from the previous frame, using it for tracking can lead to jitters. Hence, we use MediaPipe for calibration and recalibration purposes.
• Second, we use palm detection and map it to the depth map output to detect the depth of the centre of the palm. We use the depth of the centre of the palm to determine whether the user is currently in the writing zone or tracking zone.

In addition to the above said functionalities, we have also provided a view of the user on-screen to enable him to better position himself with respect to the camera. The image of the user being displayed is inverted laterally to ensure that the movement is in accordance with that of the user.