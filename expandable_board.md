---
title: Expandable Grid
parent: Proposed Solution
nav_order: 2
---
## Expandable Grid

The area captured by an input camera is fixed and limited. This area is not expandable. Hence applying the tracking algorithm on this limited area will restrict the user to that confined space. As this area is small, it would prove inadequate to write from the user’s perspective.

In order to mitigate this problem, a possible solution is to allow the user an option to stitch new frames in all the four directions and toggle between them. The user can select the direction where the expansion has to happen. These expansion buttons can be strategically placed and dynamically selected with the use of the index finger. However, this would create an additional overhead as the user has to now move back his finger to the original position where the writing had stopped in order to ensure continuity. A solution to this problem can be to use pre-defined gestures to expand this grid. All these viable solutions demand extra effort from the user’s perspective, when compared to the real-life writing scenarios. As such these won't be suitable when factors such as ease of use and adoption are considered. Therefore, any implemented solution should run automatically based on the user’s movements and without requiring any additional input from the user. To address this, we have proposed and implemented a novel solution as given below.

In a real-life scenario, a person adds the notes on the blackboard and physically moves oneself to write on a different section of the board. In other words, the blackboard is stationary and the user navigates around it.

![Expandable Board](assets/expandable_board.gif)

In our proposed solution of “Lazy Move”, the user remains stationary and the blackboard (our canvas) is shifted according to the user’s action. The board is divided into two areas called the stationary area and the expandable area. When the user navigates in the expandable area, the canvas moves in the opposite direction of the user's movement, thereby creating additional space for writing.

The board is separated into four zones representing the directions where the expansion can happen. This includes any combination of the four which enables the user to move diagonally as well. When the user moves to the right, the grid will automatically move in the left direction thereby creating new space for writing on the right. This is similar to the original analogy of the user physically moving across the blackboard. The advantage of this approach is that the user need not move away from his position to create new space. Moreover, the user need not perform any action to move the grid. Instead, the user can continue to concentrate on the writing and the grid can be displaced automatically based on the same. The user would still be able to return to the original location. The expandable grid system with lazy move would ensure that the user can navigate throughout the entire canvas.