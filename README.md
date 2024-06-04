import matplotlib.pyplot as plt
import numpy as np

# Stakeholder data
stakeholders = [
    ("WA Government", 4, 4, 5),
    ("Auditor General", 3, 4, 5),
    ("EduWest consortium", 4, 4, 4),
    ("Department of Education", 4, 4, 5),
    ("Perth metropolitan Local Community", 2, 2, 3),
    ("Strategic Projects business unit in Dept. of Finance", 3, 3, 4),
    ("Corporate service managers", 3, 3, 4),
    ("Principals", 3, 3, 4),
    ("Teachers", 2, 2, 3),
    ("Support staff", 2, 2, 3),
    ("Students", 1, 1, 3),
    ("Police", 2, 3, 3)
]

# Normalize sizes for visualization
def normalize(val, min_val, max_val):
    return (val - min_val) / (max_val - min_val) * 100

# Calculate sizes and distances
sizes = [normalize((power * urgency), 1, 20) for _, proximity, power, urgency in stakeholders]
distances = [4 - proximity for _, proximity, _, _ in stakeholders]

# Plot
fig, ax = plt.subplots()
ax.set_aspect('equal')

for i, (stakeholder, proximity, power, urgency) in enumerate(stakeholders):
    size = sizes[i]
    distance = distances[i]
    angle = np.deg2rad(i * 360 / len(stakeholders))
    x = distance * np.cos(angle)
    y = distance * np.sin(angle)
    
    ax.scatter(x, y, s=size, label=stakeholder, alpha=0.5)
    ax.text(x, y, stakeholder, ha='center', va='center', fontsize=8)

# Add concentric circles
for r in range(1, 5):
    circle = plt.Circle((0, 0), r, color='black', fill=False, linestyle='dotted')
    ax.add_artist(circle)

# Legend
plt.legend(loc='upper right', bbox_to_anchor=(1.3, 1.05), fontsize=8)
plt.title('Stakeholder Circle for WA Schools PPP Project')
plt.show()
