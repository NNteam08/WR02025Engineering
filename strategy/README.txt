
## **Strategy**

This section provides a detailed explanation and visual diagrams outlining our approach for both the **open** and **obstacle** rounds.

---

### **Open Challenge Strategy**

In the **open challenge**, the primary variation in the field is the changing size of the interior walls. To adapt to these changes, our robot utilizes **IR distance sensors** to continuously measure the distance from the walls. With multiple sensors placed at strategic positions, the robot can accurately determine its relative position and orientation to the surrounding walls. These readings allow the robot to make real-time adjustments, ensuring it remains parallel to the walls throughout its navigation.

For detecting when to make turns, the robot uses an **RGB color sensor**, which identifies the colored lines placed at the corners of the field. This mechanism not only triggers the robot to turn but also helps track the number of laps completed, ensuring the robot stops at the appropriate time. Below, you will find diagrams and flowcharts that illustrate this process in detail.Вот перефразированная и немного улучшенная версия текста:

---

### **Obstacle Challenge Strategy**

For the obstacle challenge, we have developed two distinct strategies. The first focuses solely on reacting to the nearest obstacle, while the second involves planning an entire path for one side of the mat and following it throughout the round. We are actively working with both strategies in parallel, testing and comparing their effectiveness to identify the optimal approach. Obstacle detection is performed using the **PixyCam 2.1**, which provides a list of detected objects to the **Arduino Nano** for processing.

---

### **Strategy 1**

The first strategy is designed to maintain the closest colored object on the corresponding side of the robot. This is achieved by monitoring the **x-coordinate** of the object detected by the camera and adjusting the steering accordingly to keep the object on the desired side. The robot’s turning and stopping behavior in this mode follows the same principles as in the **open challenge**. To determine the necessary steering adjustments when an object is detected, we utilize a **proportional control loop (P-control)**, ensuring precise and efficient movements.Вот немного **улучшенная и перефразированная версия** твоего текста:

---

**Strategy 2**

In this approach, we tackle the obstacle challenge by dividing the mat into sections and creating a planned trajectory for each one. Using the robot's current position and heading along with the target position and heading, we generate a polynomial curve that smoothly links these parameters. By setting multiple target points along the path, we map a continuous route that circumvents obstacles. The robot constantly updates its heading, steering toward the next point along this path. This method allows for dynamic adjustment and ensures obstacle avoidance while accurately following the planned trajectory. We repeat this process for all three rounds of the challenge.
