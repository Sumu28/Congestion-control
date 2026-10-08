# Network Congestion Control: An OpenGL Simulation

**Watch a data packet find its way through a congested network.**

When too many packets pile into one part of a network, performance drops. This is a small interactive 3D simulation, written in C++ with OpenGL and GLUT, that shows the idea visually. A packet of legitimate data travels from an office to a server through a cloud of routers. You can then flood the network from two "hacker" nodes and watch the packet take a different route to get through.

---


## What you see

- **Office** on the left and a **Server** on the right, with a **cloud** of seven routers (R0 to R6) between them.
- A **Home** node (labelled "HACKER" in the scene) and a **Remote User** node, which act as the two sources of congestion.
- A small **blue cube** is the legitimate data packet. **Red** and **pink** cubes are the flood traffic from the two hackers.

## What happens

1. **No congestion.** The packet takes the best route: office to router R1, up through R2, across to the server.
2. **Congestion from Hacker A.** Red packets flood the path towards the server, so the data packet is sent around the busy link, via R0 and R3 on the way to R4 and the server.
3. **Congestion from Hacker B.** Pink packets flood from the remote-user side, so the data packet takes a lower route through R6 and R0 instead.
4. **Both at once.** The packet is rerouted around both problems.
5. **Removing congestion** from either hacker returns the packet to the better path.

The point it makes: congestion control is about steering traffic away from overloaded links so the network does not collapse. The "About" screen in the program also explains the difference between congestion control and flow control.

## Controls

| Input | Action |
|---|---|
| **S** | Start the simulation |
| **Q** | Quit |
| **Right-click** | Open the menu |

**Menu options:** Send Some Data · Create Congestion From Hacker A · Create Congestion From Hacker B · Remove Congestion From Hacker A · Remove Congestion From Hacker B · About · Quit

The About screen is also labelled "a/A" in the menu, but the code only responds to it through the menu, not the keyboard.

## How it is built

- **Language and libraries:** C++, OpenGL, GLUT (3D shapes such as cubes, spheres and tori, bitmap text, and a perspective camera).
- **Animation:** a global idle function moves the packets a small step each frame. Each scenario (normal, Hacker A, Hacker B, both) has its own movement rules written directly into the code.
- **Rendering:** the older fixed-function OpenGL style, with double buffering and a depth test.

## Running it

The code uses `windows.h` and a `void main`, so it is set up for **Windows with Visual Studio**.

1. Install a GLUT library such as freeglut, and link it in your project.
2. Create a C++ project, add the source file and build.
3. Run it, press **S** to start, and right-click to try the scenarios.

To run it on Linux or macOS you would need to remove `windows.h`, change `void main` to `int main`, and include GLUT for your platform.

## Limitations

- The routes are hard-coded for this one layout. It does not model real routing, queues or packet loss.
- The movement uses exact coordinate checks, so changing speeds or positions can break the animation.
- It is a teaching visualisation, not a network simulator.

## Ideas for improving it

- Show link load with colours or thickness instead of fixed rerouting
- Add real queue and packet-loss behaviour
- Let the user place routers and choose the topology
- Port it to modern OpenGL and make it cross-platform

## Tech stack

C++ · OpenGL · GLUT · Visual Studio
