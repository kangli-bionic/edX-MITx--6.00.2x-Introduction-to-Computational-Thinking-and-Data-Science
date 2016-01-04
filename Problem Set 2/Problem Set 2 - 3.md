### PROBLEM 1: RECTANGULARROOM CLASS  (10/10 points)

You will need to design two classes to keep track of which parts of the room have been cleaned as well as the position and direction of each robot.

In ps2.py, we've provided skeletons for the following two classes, which you will fill in in Problem 1:

**RectangularRoom
**Represents the space to be cleaned and keeps track of which tiles have been cleaned.

**Robot**
Stores the position and direction of a robot.

We've also provided a complete implementation of the following class:

**Position**
Stores the x- and y-coordinates of a robot in a room.

Read ps2.py carefully before starting, so that you understand the provided code and its capabilities.

### PROBLEM 1

In this problem you will implement two classes, RectangularRoom on this page and Robot on the next.

For the RectangularRoom class, decide what fields you will use and decide how the following operations are to be performed:

Initializing the object

Marking an appropriate tile as cleaned when a robot moves to a given position (casting floats to ints - and/or the function math.floor - may be useful to you here)

- Determining if a given tile has been cleaned

- Determining how many tiles there are in the room

- Determining how many cleaned tiles there are in the room

- Getting a random position in the room

- Determining if a given position is in the room

Complete the RectangularRoom class by implementing its methods in ps2.py.

Although this problem has many parts, it should not take long once you have chosen how you wish to represent your data. For reasonable representations, a majority of the methods will require only a couple of lines of code.)

**Hint:
**During debugging, you might want to use random.seed(0) so that your results are reproducible.

Enter your code for RectangularRoom below.

```python
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
```

	Correct