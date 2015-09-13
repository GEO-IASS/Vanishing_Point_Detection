# Vanishing-Point-Detector

![](https://cloud.githubusercontent.com/assets/8938083/9835917/7c594192-5a1f-11e5-986f-5877b56e1fe6.png)
Detector on sample footage. Red colored lines were considered for estimating the vanishing point. The black circle marks the region of interest, where the center of the circle is the approximate vanishing point.


Dependencies: OpenCV and Armadillo

Average performance: 21fps

#Procedure
* The algorithm starts by computing dx and dy of the image.
Then the edge vectors are formed which encodes the direction
and magnitude at each pixel.

* This field is segmented into connected regions of pixels that
share the same vector direction up to a certain tolerance.

* The principal axis of the bounding box enclosing this region
gives a single pixel thick straight line. Then, x, y co-ordinates of
either ends are stored.

* Then the lines are converted to the ax + by = c form.

* These co-efficients (a, b, c) are stored in the matrix A, B in the
following format:

     A = [a1 b1
          a2 b2
            ..
            ..
         an bn]
  
  
  
    B = [c1 c2 ... cn ]'

* Solve for vector X in AX = B with the concept of least
square approximation of the answer. Where X = [x y] T

* For each pair of lines in the matrix A, their point of intersection
X’ = [x y] T is found. This is multiplied with the matrix A and
then B is subtracted to get the error vector E.

    E = AX’ – B

* The squared sum of error vector is computed and whichever
X’ gave the least summation of errors is chosen as the
vanishing point in the image.
