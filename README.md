# Geometric-Applications-of-BST's  
Part of Algorithms - Part1, Princeton University.  
Geometric Application of BST's - 1d and 2d range search - Kd trees - Nearest Neighbour problem - Intersection of line segments and rectangles.  

BST's are widely used to address problems with processing geometric data. While working with geometric data, we will be working with geometric objects like points and line segments. For example, given a set of points in a 2d plane, "what subset of points lie in a given rectangle ?" or "what is the point closest to a given point ?". These are interesting problems that have lots and lots of applications, from computerated design, games and movies, Astro-Physics and also in abstractions like databases and other situations with multiple keys or multiple dimensions.  

1D Range Search - given a set of 1 dimensional keys (all keys lie on the same straight line) find the keys(or the count of keys) which lie in a given range.  
      Possible solutions : Unordered array : insertion - O(1), range count - O(n) - range search - O(n).  
                           Ordered array   : insertion - O(n), range count - O(logn) _ range search - O(R + logn) where R = number of returned points.  
                           
   Each of these solutions have a linear time factor in either insertion or in range search or in range count. However a BST can do all three operations in logarithmic time, just using the primitive BST methods - insert and search.  
   
Line Segment Intersection : Given a set of Line Segments(all parallel to the x and y axis), find all points where two or more line segments intersect.  
      Brute Force : For every Line Segment, compare it with every other line segment and see if it intersects. Time Complexity - O(n^2) where n is the number of Line Segments.
      
   A faster NlogN solution using BST's :
      Sweep Line Algorithm : Consider a Vertical Line that sweeps through the data. Every time it hits some line segment, consider it as an event. So sweeping from left to right means we consider every x coordinate as an event. The first kind of event is when we hit a the left end point of a horizontal line segment.  Insert the y coordinate into a BST.
The second kind of event is when we encounter the right endpoint of a horizontal line segment. Remove the y coordinate from the BST as we have processed the line segment completely. The third kind of event is when we encounter a vertical line segment. In this case, perform a range search on the bst for the upper and lower y coordinates of the vertical line segment.  
Time Complexity - O(NlogN).  


Working with 2 Dimensional Keys(Points on a plane) : 2d Trees - An extension of BST's that allow us to do efficient processing on sets of points in space.
In a 2d Tree, the binary search tree invariant changes every other level. For the first level, all points to the left lie on the left subtree and all points to its right lie on the right subtree. For the second Level, all points below lie on the left subtree and all points above lie on the right subtree. Levels 1, 3, 5, 7... have divide the points on "leftness" and "rightness" and levels 2, 4, 6, 8...divide the points on "topness" and "bottomness". 

A Kd - Tree is an extension of the 2d - Tree, for k dimensions. The ith level filters the search space on the (i % k)th dimension.

Applications :  
  * Ray Tracing  
  * 2d range search  
  * Flight simulators  
  * N body simulation    
  * Collision detection  
  * Astronomical Databases  
  * Nearest Neighbour search  
  * Adaptive Mesh Rendering  
  * Accelerate renderig in video games  
  * Hidden surface removal and Shadow casting  


Searching a point : see if the point lies to the right or the left of root and move to the appropriate subtree, then see if it lies to the right or to the left of the root and proceed. Each level narrows down the region of search in the 2d space. Average Time Complexity - O(Log N). 

Range Search : searching for points that lie in a rectangle :  
    * Check root lies in the rectangle  
    * if it does, recursively search in both subtrees  
    * if it doesnt, search in the left/right subtree depending on whether the root was to the left of/ right of/ above or below the rectangle.  
    
 Time Complexity - O(NlogN + R) Where R is the number of points returned.  
 
Nearest Neighbour search : also uses a similar idea where we narrow down subtrees based whether the target point lies above/ below/ left of or right of the root and updating the min distance as we search for the nearest point.    

KdTree.java - implementation of Kd Tree with Range search and nearest neighbour search.

   
