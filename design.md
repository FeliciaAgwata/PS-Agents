# Practical Exercise 3: Designing a Searching Agent

---

## 1. PEAS Design

### PEAS Summary

| PEAS Part | Details |
| :--- | :--- |
| **Performance Measure** | Safe trip meaning no accidents, spills or fires, all fuel delivered, on time,short distance, low fuel use, follows traffic rules |
| **Environment** | Roads, traffic, other vehicles, people, animals, weather, fuel depots, control office |
| **Actuators** | Steering, accelerator, brakes, gears, indicators, lights, horn, tank shut-off valve, alarm |
| **Sensors** | Cameras, GPS, radar, speedometer, fuel level sensor, leak detector, tyre pressure sensor, keyboard for the destination |

### Type of Environment

| Property | Answer | Reason |
| :--- | :--- | :--- |
| **Observable** | Partially observable | The truck cannot see blind spots, potholes or what other drivers will do. |
| **Deterministic or stochastic** | Stochastic | Traffic, weather and breakdowns are unpredictable. |
| **Episodic or sequential** | Sequential | Earlier actions, like speed and braking, affect later ones. |
| **Static or dynamic** | Dynamic | Traffic and road conditions keep changing while the truck drives. |
| **Single or multi-agent** | Multi-agent | Other drivers, pedestrians and the control office also act. |

---

## 2. Directed Graph and Search Tree

### Problem Definition

| Part | Definition |
| :--- | :--- |
| **Initial State** | The truck is in Nairobi |
| **State Space** | All the towns on the chosen roads. Each town is a node and each road between towns is an arrow. |
| **Actions** | Drive from one town to the next town it connects to |
| **Goal Test** | Is the truck's current town Kisumu? |
| **Path Cost** | Add up the distances of the roads used, in kilometres |

### Abstraction

Abstraction is used here to ignore details that do not matter and keeping only what helps solve the problem.

---

### Directed Graph

> **Key:** Circle = town (state), arrow = driving from one town to another (action), number = distance in km (cost). **Nairobi** is where we start and **Kisumu** is where we want to reach.

| Road (From to To) | Distance (km) |
| :--- | :--- |
| Nairobi to Nakuru | 161 |
| Nakuru to Kericho | 117 |
| Nakuru to Eldoret | 156 |
| Nakuru to Kisumu | 178 |
| Kericho to Kisumu | 84 |
| Kericho to Kisii | 104 |
| Kisii to Kisumu | 136 |
| Eldoret to Kisumu | 138 |
| Eldoret to Kakamega | 106 |
| Kakamega to Kisumu | 81 |
<img width="1854" height="769" alt="graph" src="https://github.com/user-attachments/assets/7a5ee291-ed23-4d70-83f9-e42ea05c4016" />


```
```

---

### Search Tree

 g(n) is the total distance from Nairobi to that node. Kisumu shows up many times because each one is a different way of reaching it.
<img width="1680" height="1012" alt="tree" src="https://github.com/user-attachments/assets/41b6d824-c5e3-47ad-af69-247bea5b8721" />


```

```

---

## 3. Best Path

| Route | Working | Total (km) |
| :--- | :--- | :--- |
| **Nairobi - Nakuru - Kisumu** | 161 + 178 | **339** |
| Nairobi - Nakuru - Kericho - Kisumu | 161 + 117 + 84 | 362 |
| Nairobi - Nakuru - Eldoret - Kisumu | 161 + 156 + 138 | 455 |
| Nairobi - Nakuru - Eldoret - Kakamega - Kisumu | 161 + 156 + 106 + 81 | 504 |
| Nairobi - Nakuru - Kericho - Kisii - Kisumu | 161 + 117 + 104 + 136 | 518 |

### Answer

The best route is **Nairobi - Nakuru - Kisumu**. It costs 161 + 178 = 339 km, which is the smallest total. The next best is the route through Kericho at 362 km, which is 23 km longer. All the other routes are even longer.

So the truck drives from Nairobi to Nakuru, then from Nakuru straight to Kisumu. At each stop it checks that it is in the right town before moving on. Towns like Naivasha are left out of the graph because we only compare the main towns when choosing a route.
