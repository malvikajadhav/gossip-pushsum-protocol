# Gossip & Pushsum Protocol

<b>Course</b>: COP5615 - Distributed Operating System Principles <br>
<b>Institute</b>: Unviersity of Florida <br>
<b>Semester</b>: Fall 2021 <br>
<b>Instructor</b>: Dr. Alin Dobra <br>
<b>Team</b>: 
* Prateek Kumar Goel ([Github](https://github.com/pkgprateek))
* Malvika Ranjitsinh Jadhav ([Github](https://github.com/malvikajadhav))

## Problem Definition:
The goal of this project is to determine the convergence of such algorithms through a simulator based on actors written
in F#. Since actors in F# are fully asynchronous, the particular type of Gossip implemented is the so called Asynchronous Gossip.

<strong>Topologies:</strong> The actual network topology plays a critical role in the dissemination speed of Gossip protocols. As part of this project you have to experiment with various topologies. The topology determines who is considered a neighbor in the above algorithms.
* Full Network: Every actor is a neighbor of all other actors. That is, every actor can talk directly to any other actor.
* 3D Grid Actors form 2D Grid: The actors can only talk to the grid neighbors.
* Line: Actors are arranged in a line. Each actor has only 2 neighbors (one left and one right, unless you are the first or last actor).
* Imperfect 3D Grid: Grid arrangement but one random other neighbor is selected from the list of all actors (8+1 neighbors).

## Requirements:

### Input:
The input provided (with command line to run this code) will be of the form:
```console
foo@bar~$ dotnet fsi gossip.fsx numNodes topology algorithm
```
Where numNodes is the number of actors involved (for 3D based topologies rounded to nearest cube), topology is one of full, 3D, line, imp3D, algorithm is one of gossip, push-sum.

## Implementation

We have used the actor model to successfully implement the algorithms gossip and pushsum for the full network, line, 3D grid and Imperfect 3D grid topologies.

<b> Gossip:</b><br>
Convergence in Gossip protocol is achieved when any one node listens to the rumour ample number of times. We have set this limiting value to 10. After the network converges time required for convergence is printed. While every node sends the rumour to one of its neughbours in every call, it also sends a message to self so that this process starts all over again until convergence.

<b> Push sum:</b><br>
The push sum algorithm in our converges when for one of the actors in the network the estimate ratio (s/w) does not change more than 10<sup>-10</sup> for three consecutive rounds. After convergence we print the time required for convergence. To reduce time of convergence we make each actor send a message to self to wake up and start the computation all over again.

<b>Largest network that reached convergence:</b><br>
For our implementation we managed to reach the following sizes for network:

| Maximum nodes | Gossip | Pushsum | 
|----------------------|---------------|----------------|
|Full Network | 50000         | 150000            | 
| Line Network  | 50000          | 95000           | 
| 3D Grid      | 50000         | 100000          | 
| Imperfect 3D Grid | 50000        | 25000          | 

### Output
We have attached output of out program for each topology for both the algorithms. We have taken network size = 100 <br>
1.Full network:
![full_network](https://user-images.githubusercontent.com/20522169/148422991-7741a79b-68d8-44ef-b240-571f03ed223b.jpg)

2.Line network:
![line](https://user-images.githubusercontent.com/20522169/148423049-4886b4fe-92a3-45f3-a1d8-5cce81ecf351.jpg)

3.3-D Grid:
![3D-grid](https://user-images.githubusercontent.com/20522169/148423077-18552840-49a0-456d-a96e-6b1c0d61d6f6.jpg)

4.Imperfect 3-D:
![imperfect-3d](https://user-images.githubusercontent.com/20522169/148423117-2e5b4033-bbf7-4dc4-a700-74d1d838265a.jpg)

