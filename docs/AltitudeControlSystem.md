# Altitude Control System

## **Introduction**

This document outlines the design and implementation of the altitude control system (ACS) used in our CubeSat. The ACS is responsible for determining and controlling the CubeSat's position, altitude, and orientation in space, ensuring that the CubeSat can carry out its mission objectives, such as Earth observation, communication, or scientific measurements. This system utilizes a combination of sensors, actuators, and control algorithms to achieve precise control over the CubeSat’s movement and orientation.

## **1. System Overview**

The CubeSat's ACS is composed of several key components that work together to determine its altitude, position, and orientation, and to perform necessary maneuvers in space. These components include:

1. **Sensors** for determining the CubeSat’s orientation and position.
2. **Actuators** for adjusting the CubeSat’s attitude and performing maneuvers.
3. **Control Algorithms** that process sensor data and generate actuator commands.
4. **Onboard Processing** to coordinate the system and ensure continuous operation during the mission.

## **2. Determining Coordination, Altitude, and Orientation**

### **2.1 Sensors Employed**

We used a combination of sensors to determine the CubeSat's orientation and position:

1. **Sun Sensors**:
   - These sensors provide coarse orientation data by detecting the Sun's position relative to the CubeSat. This information is essential for initial orientation and coarse attitude control.

2. **Earth Horizon Sensors**:
   - These sensors, which use infrared or visual cameras, detect the Earth's curvature. They allow the CubeSat to determine its altitude and confirm its orientation relative to the Earth’s surface.

3. **Star Trackers**:
   - Star trackers capture images of stars and compare them with a star catalog, providing highly accurate orientation data. This is used for precise attitude control.
     ![7](https://github.com/user-attachments/assets/2911b4d7-e8d6-425e-9cd0-a294a425077b)


4. **Magnetometers**:
   - Magnetometers measure the strength and direction of the Earth's magnetic field. This helps us determine the CubeSat’s orientation in relation to the magnetic field, especially when other sensors may not provide enough precision.
     ![8](https://github.com/user-attachments/assets/38a571e1-0134-488c-a524-3ff63e3fc248)


5. **Gyroscopes and Inertial Measurement Units (IMUs)**:
   - Gyroscopes measure angular velocity, while IMUs combine this with acceleration data to track changes in orientation. These sensors provide real-time updates for fine-tuning attitude control.

6. **GNSS Receivers**:
   - Global Navigation Satellite System (GNSS) receivers, including GPS, help determine the CubeSat's position (latitude, longitude, and altitude). This information is crucial for determining orbital parameters and confirming altitude.

### **2.2 Coordination and Altitude Determination**

Using the GNSS receivers, we calculate the CubeSat’s position in orbit by triangulating signals from multiple satellites. The altitude is determined based on the orbital height data received from the GNSS system, supplemented by the Earth horizon sensors that provide an estimate of distance using the curvature of the Earth.

### **2.3 Orientation Determination**

Orientation (attitude) is determined using data from the star trackers, magnetometers, and gyroscopes. The CubeSat's attitude is represented by its roll, pitch, and yaw, which are calculated from the sensor data. This orientation data is critical for ensuring that the CubeSat’s payload, such as cameras or sensors, is properly aligned.

## **3. Maneuvering Using Motors and Magnets**

### **3.1 Actuators and Maneuvering**

To adjust the CubeSat’s position and orientation, we employed the following actuators:

1. **Reaction Wheels**:
   - We use small reaction wheels to control the CubeSat's attitude. By changing the spin rates of these wheels, we can rotate the CubeSat around any axis. This allows for precise control of orientation without expelling any mass, which is energy-efficient.

2. **Magnetorquers**:
   - Magnetorquers are electromagnetic coils that interact with the Earth's magnetic field. By applying current to these coils, we can generate torque and adjust the CubeSat’s orientation. This is a power-efficient method, though less precise than reaction wheels, and is typically used for coarse adjustments or maintaining stable orientation.

3. **Thrusters** (if equipped):
   - In case the CubeSat needs to make minor adjustments to its orbital trajectory or counteract drift, small thrusters expel gas or plasma to generate thrust, enabling orbital corrections.

### **3.2 Control Algorithms**

The onboard computer runs a suite of control algorithms to manage the ACS:

1. **PID Controllers**:
   - We implemented Proportional-Integral-Derivative (PID) controllers to regulate the CubeSat's attitude. These controllers minimize the error between the desired orientation and the current orientation by adjusting the actuator inputs accordingly.

2. **Kalman Filters**:
   - To improve the accuracy of our orientation data, we use Kalman filters to fuse information from multiple sensors (e.g., star trackers, magnetometers, and gyroscopes). This provides more accurate estimates of the CubeSat's attitude and reduces noise in the sensor data.

3. **Optimal Control**:
   - We also use optimal control algorithms to minimize energy consumption during maneuvers, especially when adjusting the CubeSat’s attitude. This ensures that power is used efficiently, which is critical for long-duration missions.

### **3.3 Maneuvering Process**

The process of maneuvering the CubeSat follows these steps:

1. **Orientation Adjustment**:
   - The CubeSat's attitude is first determined using sensor data. Based on mission requirements (e.g., pointing a sensor toward a target), the control algorithm computes the required attitude adjustments.
   - The reaction wheels adjust the CubeSat’s rotation by changing their spin rates.

2. **Magnetorquer Assistance**:
   - For coarse attitude control or to stabilize the CubeSat, the magnetorquers generate torque by interacting with Earth's magnetic field. This process does not consume fuel, making it energy-efficient for small adjustments.

3. **Position Control**:
   - In cases where the CubeSat needs to adjust its orbit or position (e.g., to counter drift or achieve a new trajectory), thrusters are fired to apply a small but necessary force to achieve the desired movement.

## **4. Challenges and Solutions**

### **4.1 Power Constraints**
- **Challenge**: CubeSats have limited power resources, and precise actuators like reaction wheels can be power-hungry.
- **Solution**: To address this, we use a combination of power-efficient actuators (magnetorquers) for routine adjustments and only activate reaction wheels or thrusters when necessary. Solar panels are also used to recharge the CubeSat's batteries.

### **4.2 Space Environment**
- **Challenge**: The harsh space environment, including radiation and extreme temperatures, can affect sensor accuracy and actuator performance.
- **Solution**: Redundant sensors and actuators are used for critical functions, and components are shielded against radiation and temperature fluctuations.

### **4.3 Size and Weight Limitations**
- **Challenge**: CubeSats have strict size and weight constraints, making it difficult to integrate large or heavy components.
- **Solution**: We optimized the design of the ACS by using compact and lightweight components, such as miniaturized reaction wheels and magnetorquers. We also optimized the placement of sensors and actuators to maximize efficiency within the limited space.

## **5. Conclusion**

The altitude control system implemented in our CubeSat successfully manages the satellite’s orientation, altitude, and maneuvers using a combination of sensors, actuators, and control algorithms. By leveraging efficient power systems, advanced control methods, and redundant components, we were able to overcome the challenges of operating in space with limited resources. This system ensures that our CubeSat can meet mission objectives with high precision and reliability.
