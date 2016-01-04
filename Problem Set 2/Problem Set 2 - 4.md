### PROBLEM 1: ROBOT CLASS  (10/10 points)

For the Robot class, decide what fields you will use and decide how the following operations are to be performed:

- Initializing the object

- Accessing the robot's position

- Accessing the robot's direction

- Setting the robot's position

- Setting the robot's direction

Complete the Robot class by implementing its methods in ps2.py.

**Note**: When a Robot is initialized, it should clean the first tile it is initialized on. Generally the model these Robots will follow is that after a robot lands on a given tile, we will mark the entire tile as clean. This might not make sense if you're thinking about really large tiles, but as we make the size of the tiles smaller and smaller, this does actually become a pretty good approximation.

Although this problem has many parts, it should not take long once you have chosen how you wish to represent your data. For reasonable representations, a majority of the methods will require only a couple of lines of code.)

**Note:
**The Robot class is an abstract class, which means that we will never make an instance of it. Read up on the Python docs on abstract classes at [this lin](http://docs.python.org/2/library/abc.html "this lin")k and if you want more examples on abstract classes, follow [this link](http://julien.danjou.info/blog/2013/guide-python-static-class-abstract-methods "this link"). If you took edX course 6.00.1x already, you've seen an abstract class - the Trigger class from the final problem set!

In the final implementation of Robot, not all methods will be implemented. Not to worry -- its subclass(es) will implement the method updatePositionAndClean() (this is similar to the evaluate method of the Trigger class from 6.00.1x ).

Enter your code for classes RectangularRoom (from the previous problem) and Robot below.

```python
# Enter your code for RectangularRoom (from the previous problem)
#  and Robot in this box
# Enter your code for RectangularRoom in this box
class RectangularRoom(object):
    """
    A RectangularRoom represents a rectangular region containing clean or dirty
    tiles.

    A room has a width and a height and contains (width * height) tiles. At any
    particular time, each of these tiles is either clean or dirty.
    """
    def __init__(self, width, height):
        """
        Initializes a rectangular room with the specified width and height.

        Initially, no tiles in the room have been cleaned.

        width: an integer > 0
        height: an integer > 0
        """
        self.width = width
        self.height = height
        self.cleanTiles = []
        
        #raise NotImplementedError
        
    def isTileCleaned(self, m, n):
        """
        Return True if the tile (m, n) has been cleaned.

        Assumes that (m, n) represents a valid tile inside the room.

        m: an integer
        n: an integer
        returns: True if (m, n) is cleaned, False otherwise
        """
        CT = self.cleanTiles
        for pos in CT:
            if pos.getX() == m and pos.getY() == n:
                return True
        return False
                
        #raise NotImplementedError
        
    def cleanTileAtPosition(self, pos):
        """
        Mark the tile under the position POS as cleaned.

        Assumes that POS represents a valid position inside this room.

        pos: a Position
        """
        x = int(pos.getX())
        y = int(pos.getY())
        if not self.isTileCleaned(x, y):         
            self.cleanTiles.append(Position(x,y))        
        #raise NotImplementedError


    
    def getNumTiles(self):
        """
        Return the total number of tiles in the room.

        returns: an integer
        """
        return self.width * self.height
        
        #raise NotImplementedError

    def getNumCleanedTiles(self):
        """
        Return the total number of clean tiles in the room.

        returns: an integer
        """
        return len(self.cleanTiles)
        
        #raise NotImplementedError

    def getRandomPosition(self):
        """
        Return a random position inside the room.

        returns: a Position object.
        """
        m = range(self.width)
        n = range(self.height)
        pos = Position(random.choice(m), random.choice(n))
        return pos
        
        #raise NotImplementedError

    def isPositionInRoom(self, pos):
        """
        Return True if pos is inside the room.

        pos: a Position object.
        returns: True if pos is in the room, False otherwise.
        """
        x = pos.getX()
        y = pos.getY()
        if x < 0 or y < 0:
            return False
        elif x < self.width and y < self.height:
            return True
        else:
            return False
                
        #raise NotImplementedError
        
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

        

```

	Correct