### PROBLEM 4: RANDOMWALKROBOT CLASS  (10/10 points)

iRobot is testing out a new robot design. The proposed new robots differ in that they change direction randomly after every time step, rather than just when they run into walls. You have been asked to design a simulation to determine what effect, if any, this change has on room cleaning times.

Write a new class RandomWalkRobot that inherits from Robot (like StandardRobot) but implements the new movement strategy.RandomWalkRobot should have the same interface as StandardRobot.

Test out your new class. Perform a single trial with the StandardRobot implementation and watch the visualization to make sure it is doing the right thing. Once you are satisfied, you can call runSimulation again, passing RandomWalkRobot instead of StandardRobot.

Enter your code for classes Robot and RandomWalkRobot below.

```python
# Enter your code for Robot and RandomWalkRobot in this box
class Robot(object):
    """
    Represents a robot cleaning a particular room.

    At all times the robot has a particular position and direction in the room.
    The robot also has a fixed speed.

    Subclasses of Robot should provide movement strategies by implementing
    updatePositionAndClean(), which simulates a single time-step.
    """
    def __init__(self, room, speed):
        """
        Initializes a Robot with the given speed in the specified room. The
        robot initially has a random direction and a random position in the
        room. The robot cleans the tile it is on.

        room:  a RectangularRoom object.
        speed: a float (speed > 0)
        """
        self.speed = speed
        self.room = room
        self.position = room.getRandomPosition()
        self.direction = random.choice(range(360))
        room.cleanTileAtPosition(self.position)

    def getRobotPosition(self):
        """
        Return the position of the robot.

        returns: a Position object giving the robot's position.
        """
        return self.position
            
    def getRobotDirection(self):
        """
        Return the direction of the robot.

        returns: an integer d giving the direction of the robot as an angle in
        degrees, 0 <= d < 360.
        """
        return self.direction
        
    def setRobotPosition(self, position):
        """
        Set the position of the robot to POSITION.

        position: a Position object.
        """
        self.position = position

    def setRobotDirection(self, direction):
        """
        Set the direction of the robot to DIRECTION.

        direction: integer representing an angle in degrees
        """
        self.direction = direction
        
    def updatePositionAndClean(self):
        """
        Simulate the raise passage of a single time-step.

        Move the robot to a new position and mark the tile it is on as having
        been cleaned.
        """
        raise NotImplementedError # don't change this!

# ---------------------------------------------------

class RandomWalkRobot(Robot):
    """
    A RandomWalkRobot is a robot with the "random walk" movement strategy: it
    chooses a new direction at random at the end of each time-step.
    """
    def updatePositionAndClean(self):
        """
        Simulate the passage of a single time-step.

        Move the robot to a new position and mark the tile it is on as having
        been cleaned.
        """
        oldPos = self.getRobotPosition()
        self.direction = random.choice(range(360))
        newPos = oldPos.getNewPosition(self.direction, self.speed)
        while True:
            if not self.room.isPositionInRoom(newPos):
                self.direction = random.choice(range(360))
                newPos = oldPos.getNewPosition(self.direction, self.speed)
            else : 
                break  
        self.setRobotPosition(newPos) 
        self.room.cleanTileAtPosition(newPos) 

```

	Correct