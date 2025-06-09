import numpy as np
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation

# Sabitler
G = 6.67430e-11  # Evrensel çekim sabiti (m^3/kg/s^2)
M_sun = 1.989e30  # Güneş'in kütlesi (kg)
AU = 1.496e11  # 1 Astronomik Birim (m)

# Yörünge yarıçapı ve periyot
r = 1 * AU  # 1 AU'da dairesel yörünge
T = 2 * np.pi * np.sqrt(r**3 / (G * M_sun))  # Periyot (s)

# Zaman dizisi
num_frames = 300
times = np.linspace(0, T, num_frames)

# Yörünge üzerindeki konumlar
theta = 2 * np.pi * times / T
x = r * np.cos(theta)
y = r * np.sin(theta)

# Grafik hazırlığı
fig, ax = plt.subplots(figsize=(6, 6))
ax.set_xlim(-1.2 * r, 1.2 * r)
ax.set_ylim(-1.2 * r, 1.2 * r)
ax.set_aspect('equal')
ax.set_title("Dairesel Yörünge Simülasyonu (1 AU)")
planet, = ax.plot([], [], 'bo', label="Gezegen")
sun = ax.plot(0, 0, 'yo', markersize=12, label="Güneş")

# Başlangıç fonksiyonu
def init():
    planet.set_data([], [])
    return planet,

# Güncelleme fonksiyonu
def update(frame):
    planet.set_data(x[frame], y[frame])
    return planet,

# Animasyon oluşturma
ani = FuncAnimation(fig, update, frames=num_frames, init_func=init, blit=True)

plt.legend()
plt.show()
