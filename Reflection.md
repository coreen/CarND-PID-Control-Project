# Reflection

## Effect of each component

### P = Proportional

The proportional component causes the vehicle to drive with relation to the CTE, or cross track error. This value is the difference between the vehicle's current position and the reference trajectory, which for the simulator scenario is the lane lines of the road. Raising this value causes the vehicle to steer more strongly to the right and left based on how close the vehicle is to the edge of the road. This works well for straight line trajectories, but less so for turns of the track.

### D = Differential

To handle the increasing oscillation of the vehicle as it navigates around a turn in the track, the differential component is used to reduce this back and forth. This component is calculated by taking the difference from the previous measurement and subtracting from the proportional component. By doing so, the steering angle is decreased between each time delta, which in turn reduces the strength of the vehicle's oscillation.

### I = Integral

When the differential component nears zero, the CTE value becomes larger which in turn causes the vehicle to have oscillations again. To reduce the likelihood this will occur, the integral component takes the sum of the past proportional components into consideration. As the vehicle continues to move, the summation grows and in turn reduces the steering angle.

## Hyperparameter selection

To begin with all P, D, and I components were set to 0. This resulted in the vehicle driving off the course right away when the reference trajectory started to curve. Then the P component was tuned first. I began with modifying by 1 until the vehicle drove in a straight line, but during curves the oscillations would begin and increased in strength as the turn became more steep.

To address the oscillations, the D component was added. At first, this value was arbitrarily selected as 1 and dropped by 0.1 each time to see if that would help improve the oscillations. While that method did work for a bit, during more sharp turns the car would still have difficultly. This may have been from the vehicle moving too fast so the trajectory of the vehicle was slowed from 0.3 to 0.1.

After slowing the vehicle, it was easier to see where the vehicle could use improvement. Particularly, there is a sharp left turn towards the end of a lap around the track. During this time, the car would oscillate strongly to the point where it was really close to hitting the edge of the track. To reduce this oscillation, I decided to increase the D component by a factor of 1 instead of reduce by 0.1. This helped reduce the oscillations, but the P component was still causing the vehicle to react a bit too strongly for that sharp turn. As a result, the P component was reduced dramatically by starting from 0 and working up by 0.1 until the car could safely navigate the sharp left turn.

The final hyperparameters are [0.3, 0, 7]. The I component wasn't used, since increasing it's value produces similar impact to increasing the D component. Since in this case the D component is quite large, the CTE values produced were quite small and therefore the I component wasn't needed.
