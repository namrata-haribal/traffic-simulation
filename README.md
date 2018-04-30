# Traffic simulation

In this paper, I implemented cellular automaton models of traffic flow described by Nagel and
Schrekenberg. Some assumptions of their model are that cars travel only in one direction and the model
has periodic boundaries such that a car at the ‘end’ of the road loops around and comes back in the
front. Given these assumptions, Nagel and Screkenberg describe four key rules for their single-lane
traffic simulation. Every car on the road will increase its speed by 1 if the distance between itself and the
car in front is more than the car’s velocity and decrease its speed if not. The car will also decrement its
speed by 1 based on a random probability as long as the velocity of the car is not 0. 

The two-lane model has a slight addition to this. In the case that the distance between itself and the car
in front, a car would look to the other lane to see if changing to the other lane would prevent it from
slowing down. To do this, the car looks at the spot adjacent to it is empty. If it is, then it will look to ensure
two things: no car is approaching from behind and there is space to move in front. To do the former, it
calculates the distance between the position it wants to occupy and the closest car behind it. If this
distance is greater than the maximum speed, then it will look to satisfy the latter condition. To do so, it 
calculates the distance between the position it wants to occupy and the car in front of it. If this distance is 
1 more than its own velocity, the car will switch to the other lane as all three conditions are met. 

To implement this in python, the next positions are first computed based on the current positions, after
which the lane is updated with the new positions of the car. In the two lane model, the same principle is
implemented with a consideration for lane changes. This means that first, the model determines the cars
eligible for lane change based on the conditions described above. Then, it switches the lanes of the
eligible cars. Once these lane switches are performed, the aforementioned process for updating a one-
lane model is applied to two-lane models. 
