roto.rb
========

Simple 2D/3D point rotation module written in pure ruby. 

This is a port of the original python module jimijimi/rotor.py 

Installation
------------

No installation required. Copy the module to the working directory.

Dependencies
------------

None

License
-------

The project has been released under the MIT license

Author
------

Jaime Ortiz ( jimijimi ) email: jim2o at hotmail.com

Detailed description
--------------------

roto.rb is a collection of functions. There are four main functions. The first three: ```rotateX( point, angle )```, ```rotateY( point, angle )```, ```rotateZ( point, angle )``` are used to rotate a given point around any of the cartesian coordinate axes. The last function is ```rotate( point, angle, vector )``` this allows the rotation around any arbitrary axis represented by vector.

A point is a list of three elements. ```[ x, y, z ]```
A vector is a list of three real numbers of the form ```[ vx, vy, vz ]```. The vector can be normalized or unnormalized.
An angle is specified in degrees.

Additionally the script contains functions handling vectors and quaternions. However roto.rb shuldn't be seen as a vector/quartenion library. 

Example: 

Rotate an arbitrary point around the z axys:
```Ruby

  require "./roto.rb"
  
  p0 = [ 1, 0, 0 ]
  angle = 90
  p1 = Roto.rotateZ( p0, angle )

  printf( "%.3f %.3f %.3f " % ( p0[0], p0[1], p0[2] ) )
  printf( "%.3f %.3f %.3f " % ( p1[0], p1[1], p1[2] ) )
```

Output:
```
  1.000 0.000 0.000
  0.000 1.000 0.000
```

![Picture](https://raw.github.com/jimijimi/rotorb/master/images/001_rotateZ.jpg)

The red square is the origin. The black square over the x axys is the initial position. The black square over the y axys is the final position. The background mesh is not to scale.

Example: 

Rotate an arbitrary point around the axys defined by the vector v = [ 1, 1, 1 ]:

```Ruby

  require "./roto.rb"
  
  p0 = [ 1, 0, 0 ]
  angle = 90
  v = [ 1, 1, 1 ]
  p1 = Roto.rotate( p0, angle, v )

  printf( "%.3f %.3f %.3f ", p0[0], p0[1], p0[2] )
  printf( "%.3f %.3f %.3f ", p1[0], p1[1], p1[2] )
```

Output:
```
  1.000 0.000 0.000
  0.333 0.911 -0.244
```
Example: 

Create 8 points over the circuference defined around the vector v = [ 1, 1, 1 ] and starting at point p0 = [ 1, 0, 0 ]

```Ruby
  require "./roto.rb"

  p0 = [ 1, 0, 0 ]
  v = [ 1, 1, 1 ]
  
  ( 0..360 ).step( 45 ) do | angle |
	  p1 = Roto.rotate( p0, angle, v )
	  printf( "%.3f,%.3f,%.3f ", p1[0], p1[1], p1[2] )
   end
```

Output:
```
  1.000,0.000,0.000      #0 deg ( initial point )
  0.805,0.506,-0.311     #45 deg
  0.333,0.911,-0.244     #90 deg
  -0.138,0.977,0.161
  -0.333,0.667,0.667
  -0.138,0.161,0.977
  0.333,-0.244,0.911
  0.805,-0.311,0.506     #315 deg
```

API
---
info - shows module description

vectorCrossProduct( u, v ) - Returns ( u x v )

vectorDotProduct( u, v ) - Returns ( u dot v )

vectorSum( u, v ) - Returns ( u + v )

vectorScaling( scale, v ) - Returns ( scale * v )

vectorMagnitude( v ) - Returns vector magnitude.

vectorNormalized( v ) - Returns the unit vector equivalent to v.

angleBetween2VectorsRad( u, v ) - Returns the angle in radians between u and v.

angleBetween2VectorsDeg( u, v ) - Returns the angle in degrees between u and v.

quaternionDotProduct( q0, q1 ) - Returns the dot product between q0 and q1. This is a scalar.

quaternionProduct( q0, q1 ) - Returns the quaternion obtained from the product between q0 and q1.

quaternionMagnitude( q ) - Returns the magnitude of the quaternion q0.

quaternionInverse( q ) - Returns the inverse of a unit quaternion.

quaternionRotor( v, phi ) - Returns the quaternion representing the axys of rotation v and the rotation angle phi.

deg2rad( angle_deg ) - converts the angle from degrees to radians.

rotate( p0, angle, v ) - Rotates an arbitrary point p0 around an arbitrary axis v by an angle expessed in degrees.

rotateX, rotateY, rotateZ - Rotates an arbitrary point p0 around any of the coordinate axes by an angle expressed in degrees.














