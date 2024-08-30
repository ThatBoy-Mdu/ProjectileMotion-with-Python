## Physics

[NPHY 312.docx](https://github.com/user-attachments/files/16822679/NPHY.312.docx)

``` Python
import math
import matplotlib.pyplot as plt

# Constants
g = 9.8  # Acceleration due to gravity (m/s^2)

# Kinematics function without air resistance
def kinematics_no_air_resistance(x, y, v_init, theta, dt):
    """
    Simulate the projectile motion of a cannonball without air resistance.
    """
    
    # Convert angle to radians
    theta = math.radians(theta)
    
    # Calculate initial velocity components
    v_x = v_init * math.cos(theta)
    v_y = v_init * math.sin(theta)
    
    nmax = len(x)  # Number of points in the trajectory
    
    # The equations will be calculated over the values in range nmax
    for i in range(1, nmax):
        # Update velocities considering gravity only
        v_y -= g * dt
        
        # Update positions based on the velocities
        x[i] = x[i-1] + v_x * dt
        y[i] = y[i-1] + v_y * dt
        
        # Check if the projectile hits the ground (y <= 0)
        if y[i] <= 0:
            y[i] = 0  # Ensure the last point is exactly on the ground
            x = x[:i+1]  # Truncate the x array up to the current point
            y = y[:i+1]  # Truncate the y array up to the current point
            break
    
    return x, y

# Parameters for the simulation
dt = 0.25  # Time step (seconds)
v_init = 700  # Initial velocity (m/s)
thetas = [30, 45, 55]  # Different launch angles to simulate (degrees)

# Function to display the results
def display(x, y, label):
    """
    Plot the trajectory of the cannonball.
    
    Args:
        x (list): x-coordinates of the trajectory.
        y (list): y-coordinates of the trajectory.
        label (str): Label for the plot (usually the angle).
    """
    plt.plot(x, y, label=label)

# Loop over each angle and simulate the trajectory without air resistance
for theta in thetas:
    x = [0] * 5000  # Initialize x-coordinates array
    y = [0] * 5000  # Initialize y-coordinates array
    
    # Compute the trajectory without air resistance
    x, y = kinematics_no_air_resistance(x, y, v_init, theta, dt)
    
    # Display the results
    display(x, y, f"theta = {theta}")

# Set plot title and labels
plt.title("Canon Ball Trajectory Without Air Resistance")
plt.xlabel("x in meters")
plt.ylabel("y in meters")
plt.grid(True)
plt.legend()
plt.show()
```
![image](https://github.com/user-attachments/assets/c2eaba77-c828-4ee6-86fe-1d7289fc7ad9)
figure of different projectile angles
