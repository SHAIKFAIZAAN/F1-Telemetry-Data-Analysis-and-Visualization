# F1-Telemetry-Data-Analysis-and-Visualization
# Developed a data analysis project using Python and the FastF1 library to visualize telemetry data from Formula 1 races. Analyzed key performance metrics such as speed, RPM, gear shifts, throttle, and braking across various circuits. Created detailed plots that illustrate the relationship between car performance metrics and track positions.
import fastf1 as ff1
import matplotlib.pyplot as plt
import numpy as np

session = ff1.get_session(2023, 'Australia', 'R')
session.load()
laps = session.laps.pick_driver('HAM')
lap = laps.pick_fastest()
telemetry = lap.get_telemetry()
speed = telemetry['Speed'].values
rpm = telemetry['RPM'].values
gear = telemetry['nGear'].values
throttle = telemetry['Throttle'].values
brake = telemetry['Brake'].values
distance = telemetry['Distance'].values
print("Sample distance data:", distance[:25])
print("Sample speed data:", speed[:25])
print("Sample RPM data:", rpm[:25])
print("Sample Gear data:", gear[:25])

# Australia GP 
turn_positions = {
    'Turn 1 - Turn 1': 0,              # Start of the circuit
    'Turn 2 - Turn 2': 300,
    'Turn 3 - Turn 3': 550,
    'Turn 4 - Turn 4': 800,
    'Turn 5 - Turn 5': 1050,
    'Turn 6 - Turn 6': 1300,
    'Turn 7 - Turn 7': 1550,
    'Turn 8 - Turn 8': 1850,
    'Turn 9 - Turn 9': 2100,
    'Turn 10 - Turn 10': 2400,
    'Turn 11 - Turn 11': 2700,
    'Turn 12 - Turn 12': 3000,
    'Turn 13 - Turn 13': 3300,
    'Turn 14 - Turn 14': 3600,
}


# Speed
plt.figure(figsize=(10, 6))
plt.plot(distance, speed, color='red', label='Speed')
for turn, pos in turn_positions.items():
    plt.axvline(x=pos, color='black', linestyle='--', alpha=0.4)  # Reduced opacity
    if turn in ['Turn 1 - Turns 1-2', 'Turn 2 - Turn 6']:  # Highlight specific turns if needed
        plt.text(pos, max(speed), turn, rotation=90, verticalalignment='bottom', horizontalalignment='right', fontsize=9)
plt.xlabel('Distance (meters)')
plt.ylabel('Speed (km/h)')
plt.title('Speed vs. Distance')
plt.grid(True)
plt.legend()
plt.show()

# RPM 
plt.figure(figsize=(10, 6))
plt.plot(distance, rpm, color='blue', label='RPM')
for turn, pos in turn_positions.items():
    plt.axvline(x=pos, color='black', linestyle='--', alpha=0.4)  
    if turn in ['Turn 1 - Turns 1-2', 'Turn 2 - Turn 6']:  
        plt.text(pos, max(rpm), turn, rotation=90, verticalalignment='bottom', horizontalalignment='right', fontsize=9)
plt.xlabel('Distance (meters)')
plt.ylabel('RPM')
plt.title('RPM vs. Distance')
plt.grid(True)
plt.legend()
plt.show()

# Gear 
plt.figure(figsize=(10, 6))
plt.step(distance, gear, color='green', where='post', label='Gear')
for turn, pos in turn_positions.items():
    plt.axvline(x=pos, color='black', linestyle='--', alpha=0.4) 
    if turn in ['Turn 1 - Turns 1-2', 'Turn 2 - Turn 6']: 
        plt.text(pos, max(gear), turn, rotation=90, verticalalignment='bottom', horizontalalignment='right', fontsize=9)
plt.xlabel('Distance (meters)')
plt.ylabel('Gear')
plt.title('Gear vs. Distance')
plt.grid(True)
plt.legend()
plt.show()

# Throttle
plt.figure(figsize=(10, 6))
plt.plot(distance, throttle, color='orange', label='Throttle')
for turn, pos in turn_positions.items():
    plt.axvline(x=pos, color='black', linestyle='--', alpha=0.4) 
    if turn in ['Turn 1 - Turns 1-2', 'Turn 2 - Turn 6']:  
        plt.text(pos, max(throttle), turn, rotation=90, verticalalignment='bottom', horizontalalignment='right', fontsize=9)
plt.xlabel('Distance (meters)')
plt.ylabel('Throttle (%)')
plt.title('Throttle vs. Distance')
plt.grid(True)
plt.legend()
plt.show()

# Brake
plt.figure(figsize=(10, 6))
plt.plot(distance, brake, color='purple', label='Brake')
for turn, pos in turn_positions.items():
    plt.axvline(x=pos, color='black', linestyle='--', alpha=0.4) 
    if turn in ['Turn 1 - Turns 1-2', 'Turn 2 - Turn 6']:  
        plt.text(pos, max(brake), turn, rotation=90, verticalalignment='bottom', horizontalalignment='right', fontsize=9)
plt.xlabel('Distance (meters)')
plt.ylabel('Brake (%)')
plt.title('Brake vs. Distance')
plt.grid(True)
plt.legend()
plt.show()
