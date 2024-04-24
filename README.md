# Face Morph
This project implements face morphing, which is capable of generating faces that are a blend of the inputs.

## Libraries 
* numpy
* dlib (facial landmarks)
* cv2 (image loading, resize)
* matplotlib
* scipy.spatial.Delaunay

## Implementation Outline
### Inputs
Find two faces as inputs for blending. </br>
* https://unsplash.com/photos/WNoLnJo7tS8
* https://unsplash.com/photos/d2MSDujJl2g

![image](https://github.com/XDDz123/face-morph/assets/20507222/bdcde3f8-713b-4793-a8fe-77e8cb3e78b4) </br>

### Landmarks
Use Dlib to locate facial landmarks. Additional points could be added manually if desired.</br></br>
![image](https://github.com/XDDz123/face-morph/assets/20507222/1b91d86e-f506-4439-9b98-73bfce997875)

### Meshing
Create a mesh from the generated landmarks using Delaunay triangulation from Scipy.</br></br>
![image](https://github.com/XDDz123/face-morph/assets/20507222/8694d544-eea4-48ec-9ede-a96ef4d14731)

### Transform
Define an intermediate mesh by blending vertex positions. in_between = (1 - w) * vertex_A + w * vertex_B, where A and B are the input faces. </br>
This establishes a correspondence between triangles within the blended face, face A, and face B.  </br>
Compute the affine transformation matrix from vertices of each triangle within the mesh and intermediate positions. </br>
For each pixel within each triangle in the intermediate mesh, use the matrices to locate its corresponding pixel in the face images. </br>
Then fill in the intermediate image by blending the colors of the corresponding pixels based on (1 - w) * A_pixel + w * B_pixel.</br> </br>
![image](https://github.com/XDDz123/face-morph/assets/20507222/f548a34b-b468-4371-9793-edd9b7c33aa5)

### Results
![meshed](https://github.com/XDDz123/face-morph/assets/20507222/3d5f9657-a28f-4cd9-92d7-a0b966113a28)
