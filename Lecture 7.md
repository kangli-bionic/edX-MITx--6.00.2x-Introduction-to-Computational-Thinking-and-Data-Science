# Lecture 7 - Curve Fitting

Our goal in this lecture is to study how computation can help us understand our experimental data and process it to help reveal the underlying truths.

#### A common pattern in Science and Engineering

1. develop a hypothesis

2. design an experiment, take measurements

3. use computation to

	a. evaluate hypothesis
	b. determine values of unknown 
	c. predict consequences

Let's see how this might work in practice.

Assume that we designed an experiment to test Hook’s law for springs ( F= - KX )

Here is our measurements :

    Distance (m) Mass (kg)
    0.0865		0.1
    0.1015		0.15
    0.1106		0.2
    0.1279		0.25
    0.1892		0.3
    0.2695		0.35
    0.2888		0.4
    0.2425		0.45
    0.3465		0.5
    0.3225		0.55
    0.3764		0.6
    0.4263		0.65
    0.4562		0.7
    0.4502		0.75
    0.4499		0.8
    0.4534		0.85
    0.4416		0.9
    0.4304		0.95
    0.4370		1.0
    

A good first step whenever we're trying to figure out what's up with our data is to plot it, to look at it visually.

Here's a couple Python procedures to help us do that.

```python
import pylab, random

# read the data in from a text file where we've entered the data.
def getData(fileName):
    dataFile = open(fileName, 'r')
    distances = []
    masses = []
    discardHeader = dataFile.readline()
	# Reads the first line of the file which is heared and discard it.
	# Each line comes in as a string. 
	# we're going to take that string and split it into substrings that correspond to the non blank portions of the line.

    for line in dataFile:
        d, m = line.split()
		# d: Distance Measurement
		# m: Mass Measurement
		distances.append(float(d))
        masses.append(float(m))
    dataFile.close()
    return (masses, distances)
```
```python
def plotData(fileName):
    xVals, yVals = getData(fileName)
	
	# convert data into the pylab array data type, a very handy data type for doing numerical manipulation.
    xVals = pylab.array(xVals)
    yVals = pylab.array(yVals)
    
	xVals = xVals*9.81 # convert mass to force (F = mg)
    pylab.plot(xVals, yVals, 'bo', label = 'Measured displacements')
    pylab.title('Measured Displacement of Spring')
    pylab.xlabel('Force (Newtons)')
    pylab.ylabel('Distance (meters)')

plotData('springData.txt')
pylab.show()
```
Here's the results:

![](./img/figure_1.png)


