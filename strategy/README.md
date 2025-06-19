
## Strategy

This section details our algorithms, sensor logic, and overall problem-solving approach for both the **Open Challenge** and **Obstacle Challenge** rounds. Visual flowcharts and diagrams (see `/docs/` or `video/`) further illustrate our strategy.

---

### Open Challenge Strategy

The Open Challenge field’s unique feature is the **randomized size and placement of the interior wall**, changing with every round. To address this, our robot employs **multiple IR distance sensors** (front, rear, and angled sides) to continuously measure its proximity to both interior and exterior walls. By analyzing these real-time distance readings, the robot adjusts its trajectory and steering to stay equidistant from boundaries, minimizing the risk of collision. This feedback loop ensures the robot maintains a parallel orientation and adapts dynamically to new wall configurations, regardless of changes between rounds.

**Lap Counting & Turning:**  
At each corner of the field, colored lines are placed (typically blue or orange). The robot uses a **TCS34725 RGB color sensor** facing downward to detect these lines. Each time a color line is detected, the robot:
- Updates its internal lap/corner count.
- Executes a precise turn (left or right) based on which color is detected first (see flowchart below: blue = counterclockwise, orange = clockwise).
- Checks if three laps are completed, stopping in the correct sector.

**Summary:**  
- **Wall following** and **parallel driving** using IR sensor feedback.
- **Color-based lap tracking** and **direction decision**.
- **Stop** in starting sector after three laps.

---

### Obstacle Challenge Strategy

Obstacle rounds introduce randomly-placed colored blocks (red, green) as obstacles, plus purple-walled parallel parking zones. Our approach leverages both computer vision and distance sensing for robust avoidance and precise parking.

**Obstacle Detection:**  
- **HuskyLens AI Camera** identifies obstacles (by color or shape ID).
- **IR and ultrasonic sensors** cross-verify obstacle proximity, enhancing reliability.

We developed and tested two navigation strategies for this challenge:

#### **Strategy 1: Reactive Obstacle Avoidance (P-Control)**

- The robot continually scans for the **closest colored object** (block) using the HuskyLens.
- It calculates the x-coordinate offset of the object and adjusts the steering via a **proportional control loop** to keep the object at a desired position (usually just off-center).
- If the block is detected directly ahead (within a certain threshold), the robot slows and gently steers away, then realigns to the track after passing.
- **Turning and stopping logic** mirrors the open challenge: lap count and line color determine direction and finish.

This strategy is robust, simple, and highly adaptive, especially when obstacles are distributed randomly.

#### **Strategy 2: Path Planning & Trajectory Tracking**

- The robot divides the mat into logical sections.
- Using both its current heading and position (from sensors and odometry), and the HuskyLens’ map of obstacles, the robot **plans a smooth polynomial curve** (trajectory) that avoids all detected blocks in a given section.
- The robot computes and updates a series of target waypoints along this trajectory.
- Real-time steering adjustments are made to follow the curve, constantly updating based on new sensor input.
- This method allows for **anticipatory avoidance** and optimizes for speed and minimal path deviation.
- The strategy is repeated for each lap, recalculating as new obstacle positions are observed.

Both strategies are tested and tuned during development. The final choice is based on which yields more consistent, high-scoring performance under competition conditions.

---

### Parallel Parking Strategy

**Overview:**  
After completing three laps (either in open or obstacle mode), the robot must perform an **autonomous parallel parking maneuver** in the designated zone marked by purple walls.

**Process:**
1. **Zone Entry:**  
   - The robot detects the parking zone using the **HuskyLens** (color recognition of purple) and confirms location with floor markers (using the RGB sensor).
   - It approaches slowly, using **ultrasonic sensors** to measure side and rear distances, ensuring it will fit between the two parking walls.

2. **Alignment:**  
   - The robot makes small steering corrections with the servo to become parallel to the parking walls.
   - IR and ultrasonic readings are fused to check that the wheels are never closer than 2 cm to the wall (as per rules).

3. **Parking Maneuver:**  
   - Once aligned, the robot executes a precise forward or reverse maneuver to enter the parking slot without touching any walls.
   - The IMU (gyro) is used to ensure the robot maintains correct orientation during parking, correcting any angle deviation in real time.

4. **Completion:**  
   - The robot stops fully inside the parking zone, parallel to the walls, with its wheels at a safe and legal distance.
   - A final check ensures it does not cross or touch boundaries. Optionally, an LED indicator can signal that parking is complete.

---

**Note:**  
All strategies prioritize **collision avoidance**: the robot never touches any wall or obstacle. Sensor fusion (combining data from multiple sensors) is used throughout to maximize reliability, regardless of lighting, wall color, or mat layout.

---

### Flowchart Reference

For a visual representation, see the attached `/docs/strategy_flowchart.png` or `/video/strategy_explainer.mp4`.  
The key logic sequence (as per our code):

- Detect lap start color (blue = counterclockwise/left; orange = clockwise/right).
- Use wall-following and color detection for navigation and lap tracking.
- When an obstacle is detected, trigger avoidance routine (strategy 1 or 2).
- After three laps, initiate parallel parking sequence.

---

For any questions on our navigation logic or for sample code, see `/src/` or contact the team directly.
