For now we only have a brief recap of 2 stuff

For now we are gone work with 2D and 3D points, so $x\in \mathbf{R}^2$  and $x\in \mathbf{R}^3$ .

Points are represented with *homogeneous coordinates* where $\tilde{x}=\tilde{x},\tilde{y},\tilde{w}\in\mathbf{P^2}$ vectors differ only in scale but are considered to be equivalent. and $P^2=R^3-(0,0,0)$ called *projective space*.

A homogenous vector $\tilde{x}$ can be converted back o inhomogenous by dividiing for it's last element.
$$\tilde{x}=(\tilde{x},\tilde{y},\tilde{w})=\tilde{w}(\tilde{x},\tilde{y},1)=\tilde{w}\bar{x}$$ with $\bar{x}=(x,y,1)$ . In the case of $\tilde{w}=0$ we have *points at infinity*.

a 2D line can be represented as a set of homogenous coordinates $\tilde{I}=(a,b,c)$ with a line equation expressed as $$\tilde{x}\tilde{I}=ax+by+c=0$$
the equation can be normalized to $\mathbf{1}=(\hat{n}_x,\hat{n}_y,d)=(\tilde{\mathbf{n}},d)$ with $||\hat{\mathbf{n}}||=1$ with $\hat{\textbf{n}}$ being perpendicular to the line and $d$ the distance to the origin it can also be expressed as a function of a rotation angle $\theta$ where $\mathbf{\hat{n}}=(\hat{n}_x,\hat{n}_y)=(\cos \theta,\sin \theta)$  with a combinaton $(\theta,d)$.

For homogenous coodinates we can compute intersecion of two lines as: $$\tilde{x}=\tilde{I_1} \times \tilde{I_2}$$ with $\times$ being the cross product operator.

We can also use 2D conics expressed as $x^TQx=0$. 

3D points also havetheir homogenous counter part with a vector of coordinates the can augmented by dividing for the last element $w$.

A lined can be expressed as a linear combination of two points it comes across $r=(1-\lambda)p+\lambda q$ and if we restrict $\lambda$ to the interval $[0,1]$ we can a segment.

a lot of equations cannot represent correctly lines thus we have to use something that is not biased toward a particular orientation: the Plucker coordinates:

$$L=\tilde{p}\tilde{q}^T-\tilde{q}\tilde{p}^T$$ where p and q are two different points on the line, here we have only four degrees of freedom and L is homogenous thus $|L|=0$ which is a quadratic constraint on the coordinates.
# 2D transformations
a 2d translation $x'=x+t$ can be written as $$x'= \begin{bmatrix}I & t \end{bmatrix}\bar{x}$$ or 
$$
\bar{x}'=\begin{bmatrix} I & t \\ 0^T & 1 \end{bmatrix}\bar{x}
$$

## rotation + translation

$$x'=\begin{bmatrix} R & t \end{bmatrix}\bar{x}$$
$$R=\begin{bmatrix} \cos \theta & -\sin \theta  \\ sin \theta & \cos \theta \end{bmatrix}$$ with R being orthonormal.

## Scaled rotation 

It scales the the point it is applied to.

$$x'=\begin{bmatrix}a & -b & t_x \\ b & a & t_y\end{bmatrix}\bar{x}$$ also here angle between lines are preserved, it can also be expressed as $x'=sRx+t$ , here angles between lines are preserved plus we don't need it to be that $a^2 + b^2=1$.

## Affine

It is written as $x'=A\bar{x}$ with $A$ is a 2x3 arbitrary matrix $$x'=\begin{bmatrix}a_{00}&a_{01}&a_{0
2}\\ a_{10}&a_{11}&a_{1
2} \end{bmatrix}\bar{x}$$
parallels lines are parallel under an affine transformation. 
## Projective
It uses homogeneous coordinates.

$$\tilde{x}'=\tilde{H}\tilde{x}$$
It is called *perspective* transform and we have $\tilde{H}$ as a an arbitrary 3x3 matrix, also the matrix is homogeneous and defined only by a scale meaning that another matrix is equivalent aside from the scale.

$$x'=\frac{h_{00}x+h_{00}y+h_{02}}{h_{20}x+h_{21}y+h_{22}} \text{ and } y'=\frac{h_{10}x+h_{11}y+h_{12}}{h_{20}x+h_{21}y+h_{22}}$$ ![[Pasted image 20250211111810.png]]

This is the hierarchy in terms of degrees of freedom and it is important that they form a nestedd set of groups where they arre closed under composition and have an inverse that is member of the same group. Each group is a subgroup of a more complex one. These are known as *Lie groups* and are very used in robotics applications.

## Co-vectors
We can also transform lines expressed as equations, consider $\tilde{l}\tilde{x}=0$ we can transform it through a matrix like $\tilde{x'}=\tilde{H}\tilde{x}$ and we get that $$\tilde{l'}\tilde{x'}=\tilde{l'}^T\tilde{H}\tilde{x}=(\tilde{H}^T\tilde{l'})^T\tilde{x}=\tilde{l}\tilde{x}=0$$
## Stretch/squash

$$x'=s_xx+t_x$$ $$y'=s_yy+t_y$$
this changes the aspect ration of an image.

## Planar surface flow

$$
x'=a_0+a_1x+a_2y+a_6x^2+a_7xy 
$$
$$y'=a_3+a_4x+a_5y+a_6xy+a_7y^2$$

It estimates the motion of a planar surface.

## Bilinear interpolant

Used to interpolate deformation due to motion of four corner points of a square. 

$$
x'=a_0+a_1x+a_2y+a_6xy 
$$
$$y'=a_3+a_4x+a_5y+a_7xy$$

# 3d transformations

the transformations we have seen before are preactically identical to the 2D ones just with more degrees of freedom, see the image below.

![[Pasted image 20250211114619.png]]

The interesting parts are the 3d rotations instead.

## 3D rotations

The $R$ matrix is difficult to parametrize we can see different interpretations depending on our nneds.

### Euler angles

We express the rotation mattrix as the producvt of three rotation however it is bad since it sensible to very small changes and is dependant on the order.

### Axis/angle (exponential twist)

We have a rotation axis $\hat{n}$ and an angle $\theta$ that can be combined to a 3D vector $\omega=\theta\hat{n}$ .

We can first project a vector $v$ on the axis $\hat{n}$ and get $$v_{||}=\hat{n}(\hat{n}v)=(\hat{n}\hat{n}^T)v$$
this the part not affected by the rotation and now we can get the perpendicular residual of $v$ from $\hat{n}$ $$v_{\perp}=v-v_{||}=(I-\hat{n}\hat{n}^T)v$$
now rotate it by 90 degrees using the cross product.
$$
v_{\times}=\hat{n}\times v_{\perp}= \hat{n} \times v = [\hat{n}]_{\times}v
$$

with 
 $$[\hat{n}]_x=\begin{bmatrix}
 0 & - \hat{n}_z & \hat{n}_y \\
\hat{n}_z & 0 & -\hat{n}_x \\
\hat{n}_y & - \hat{n}_x & 0 \\
 
 \end{bmatrix}$$
also note that $v_{\times \times}=-v_{\perp}$  so now  we have that $$v_{||}=v-v_{\perp}=v+v_{\times \times}=(I+[\hat{n}
]^2_{\times})v$$
The in plane component of the rotated vector is computed as $$u_{\perp}=cos \theta v_{\perp} + \sin \theta v_{\times}=(\sin \theta [\hat{n}]_{\times}- \cos \theta [\hat{n}]^2_{\times})v$$
so now we can say that 
$$u= u_{\perp}+v_{||}=(I+\sin \theta [\hat{n}]_{\times} + (1- \cos \theta[\hat{n}]^2_{\times}))v$$
so now we finally get a rotation matrix parametrized as 
$$R(\hat{n},\theta)=I+\sin \theta [\hat{n}]_{\times} + (1- \cos \theta[\hat{n}]^2_{\times})$$
a.k.a Rodrigue's formula.

the product of axis and angle $\omega = \theta \hat{n}=(\omega_x,\omega_y,\omega_z)$ is the most minimal representation we can use however it is not  unique but it is good for small rotations especially when expressed in radiants.

$$R(\omega) \approx I+ \sin [\hat{n}]_{\times} \approx I + [\theta \hat{n}]_{\times}=\begin{bmatrix}
1 & -\omega_z & \omega_y \\
 \omega_z & 1& \omega_x \\
-\omega_y & -\omega_x &1\\

\end{bmatrix} $$

we can also do $R(\omega)v \approx v+ \omega \times v$ and can be to compute the derivative of $Rv$ w.r.t. $\omega$ $$\frac{\partial Rv}{\partial \omega^T} = - [v]_{\times}=\begin{bmatrix}
0 & z & -y \\
-z & 0 & x \\
y & -x & 0 \\
\end{bmatrix}$$ 
An alternative is the *exponential twist* where a rotation $\theta$ is obatined with $k$ rotations through $\theta / k$  in the limit $k \rightarrow \infty$  and we get that $$R(\hat{n},\theta)= \lim_{k \rightarrow \infty} (I + \frac{1}{k}[\theta \hat{n}]_{\times})^k= \exp [\omega]_{\times} $$   with some mathematical formulation we can use Taylor series and get that $$\exp [\omega]_{\times}=\dots = I + \sin \theta[\hat{n}]_{\times}+(1- \cos \theta)[\hat{n}]^2_{\times}$$ 
### unit quaternions

a quaternion is a unit $q = (q_x,q_y,q_z,q_w)$ where $||q||=1$ and $q$ and $-q$ .

![[Pasted image 20250211130054.png]]

Qauternions can be derived from the zaxis/angle representation $$q=(v,w)=(\sin \frac{\theta}{2}\hat{n},\cos \frac{\theta}{2})$$with the classical rotation and axis angles.
now we can see that $\theta = 2 \sin \frac{\theta}{2} \cos \frac{\theta}{2}$  and $(1- \cos \theta) = 2 \sin^2 \frac{\theta}{2}$ we get that $$
R(\hat{n},\theta)= I + \sin \theta[\hat{n}]_{\times}+ (1- \cos \theta)[\hat{n}]^2_{\times}=I + 2w[v]_{\times} + 2[v]_{\times}^2
$$and we get the formula for $R(q)$ and we get that 
$$
R(q)=\begin{bmatrix}
1-2(y^2+z^2) & 2(xy+zw) & 2(xz+yw) \\
2(xy+zw) & 1-2(x^2+z^2) & 2(yz+xw) \\
2(xz+yw) & 2(yz+xw) &1-2(x^2+y^2) \\
\end{bmatrix}
$$
their rotations can be composed thorugh simple algebra for two quaternions  we get a *quaternion multiply* operation $$q_2=q_oq_1=(v_0 \times v_1 + w_0v_1,w_0w_1 - v_0v_1)$$

Note that $R(q_2)=R(q_0)R(q_1)$ it is not commutative! 

The opposite of a quaternion is obtained from flip the sign of v or w but NOT BOTH.

$$
q_2= q_0 / q_1 = q_0q_1^{-1}=(v_0 \times v_1 + w_0v_1 - w_1v_0,-w_0w_1 -v_0v_1)
$$

This represents the *incremental rotation* between two rotations desired. To take the inperlation we can use the *spherical linear interpolation* which can be obtained in two ways.

$$
(1) q_2=q_r^{\alpha}q_0
$$
$$
(2)q_2=\frac{\sin (1-\alpha)}{\sin \theta}q_0 + \frac{\sin \alpha \theta}{\sin \theta}q_1

$$

where $\theta = \cos^{-1}(q_0q_1)$. The results are all comparable when using these formulas.

Now we have dealt with two ways to do the same thing, how do i compare the two methods?
- axis/angle is minimal and doesn't need constraints on the parameters
- quaternions are better for a smoothly moving camera since there are no disconuities in the representation nad it is easy to interpolate and chain transformations that are otherwise rigid we also have a simple algorithm to  implement the slerp
![[Pasted image 20250211142114.png]]
# 2D to 3D projections

we basically drop the z component from a 3d coordinate $p$ with various amtrices depending on the type coordinate $$x=[I_{2 \times2}|0]p$$ for normale coordinates while for homogenous coordiantes we write 
$$
\tilde{x}=\begin{bmatrix}
1&0&0&0\\
0&1&0&0\\
0&0&0&1\\

\end{bmatrix}\tilde{p}
$$
however for lens we need to scale the world coordinates so that they fit into a image sensor *scaled ortography* $$
x=[I_{2 \times 2}|0]p
$$
Before dealing with the various prjoections we can see visually a reprentation for them

![[Pasted image 20250211142835.png]]
in figure (b) in the image we see a representation of this first method, the scaling can be equal for all objects or different for each object as in figure (c) after the rescaling of the orthography.

In (d) we have projection to a line that is parallel to the line of sight of the object center.

## perspective

the most used one is the perspective one (e) in the figure. we project a component to an image plabne by dividing for their z component 
$$
\bar{x}=\mathbf{P}_z(p)=\begin{bmatrix}x/z \\ y/z \\ 1\end{bmatrix}
$$
in homogenous coordinates it would be $\tilde{x}=[I_{3 \times 3}|0]\tilde{p}$  basically drop the $w$ component of $p$ so now we can't recover distance after projection. in CG we have projection into normalized device coordinatres $(x,y,z)\in[-1,1]\times [-1,1] \times [0,1]$ and then rescales them into pixel coordinates using a viewport transformation. The initial perspective projection is obtained as:

$$\tilde{x}=\begin{bmatrix}
1 & 0 & 0 & 0\\
0&1&0&0\\
0&0& -z_{far}/z_{range} & z_{near}z_{far}/z_{range}\\
0&0&1&0
\end{bmatrix} \tilde{p}$$
with $z_{near}$ and $z_{far}$ being the nearest and furthest z clipping planes and $z_{range}=z_{far}-z_{near}$ we actually need only x and y but z is useful to do stuf like z-buffering. For $z_{near}=1,z_{far}=1 \rightarrow \infty$ and with the third row sign-swapped the third element becomes inverse depth which can be useful in some cases.
## camera intrinsics
As of now we only projected into a pinhole now we want to switch inside the camera, we can esttimate the situation from the figure below.
![[Pasted image 20250211151558.png]]
we use a sensor homography $M_s$ to have a mapping from 2d pixel coordinates to 3d rays. Then use a intrinsic camera matrix $K$ to map 3d camera centered points $p_c$ to pixel coordinates $\tilde{x}_s$ . an image sensor returns pixel values indexed by pixel coordinates $(x_s,y_s)$ and to convert them to 3d coordiantes we first scale the coordinate values with the pixel spacings $(s_x,s_y)$ and then describe the orientation of the sensor array relative to the camera projection center $O_c$ with origin $c_s$ and a 3D rotation $R_s$ . the combined prjoection from 2d to 3d is written as

$$
p=[R_s \text{ } C_s]\begin{bmatrix}
s_x & 0 & 0\\
0 & s_y & 0\\
0 & 0 & 0\\
0 & 0 & 1\\
\end{bmatrix}
\begin{bmatrix}
x_s \\ y_s \\ 1
\end{bmatrix}
=M_s\bar{x_s}
$$
the first two columns  of the $M_s$ matrix are the 3d vectors that correspond to the unit steps of the image pixel array along the $x_s$ and $y_s$ and the third column is the 3d image array origin $c_s$ .

$M_s$ is parametrized by 8 unkwon parameters:
- 3 to describe the rotation $R_s$ 
- 3 to descrive $c_s$ 
- 2 for the scale factors $(s_x,s_y)$ 
The 3D pixel centered points $p$ and the camara centered point $p_c$ are tied by an unknown scaling s $p=sp_c$ and now we can write the complete projection between $p_c$ and the pixel adress homogenous version $\tilde{x}_s$ $$\tilde{x}_s=\alpha M^{-1}_sp_s=Kp_c$$ with $K$ being the *calibration matrix* which describes camera intrinsics.
the camera extrinisics are the orientation in space described by $(R,t)$ which are estimated when using measurements as $$\tilde{x}=K[R \text{ }t]p_w=Pp_w$$ with $P=K[R|t]$ known as the camera matrix.

An interesting part is that K can be written as an upper triangular matrix 
$$
K=\begin{bmatrix}
f_x &s &c_x\\
0 & f_y &c_y\\
0 &0 &1\\
\end{bmatrix}
$$
- the $f$ terms are the focal lengths along teh x and y dimension
- $s$ encodes a possible skew of sensors
- $(c_x,c_y)$ denotes the image center in pixel coordinates
we could have $f_x=f_y$ and multiply $f_y$ by a parameter $a$ which is the *aspect ratio* , we can have  a more simpler form by using $a=1,s=0,f_x=f_y$  and given the $W,H=image_{weight},image_{heigth}$  we can se $(c_x,c_y)=(W/2,H/2)$  . Now we only have to use a single paramter which is the focal length $f$ with the sitatuion being represented below.

![[Pasted image 20250212114707.png]]

### focal length

If we number pixel coordinates using integer values e.g. in $[0,W)\times [0,H)$ the focal length $f$ and camera center $(c_x,c_y)$ can expressed in pixel values. The relationship with the focal length is expressed visually in the image below:
![[Pasted image 20250212120339.png]]

$$
\tan \frac{\theta_H}{2}=\frac{W}{2f} \implies f=\frac{W}{2}[\tan \frac{\theta_H}{2}]^{-1} 
$$

that is the relationship between the focal length, the wifth nad horizontal FOV $\theta_H$ .

We can make the focal length and image center indipendent of the image resolution using $[-1,1)$ along the image dimension and $[-a^{-1},a^{-1})$ with $a\ge1$  being the image ratio and such a feat can bea accomplished using the *normalized device device coordinates* 
$$
x'_s=(2x_s-W)/S \text{ and } y'_s=(2y_s-H)/S \text{ where } s=max(W,H)
$$

Now we can have simpligied unitless setting under these conditions 

$$
S=W=2,f^{-1}=\tan \frac{\theta_H}{2}
$$
we acn also convert between different focal lengths and switch to a pixel expressed one by multiplying for $W/2$ .

### camera matrix

when combining camera extrinsics and intrinsics we obtain the *camera matrix*

$$P=K[R\text{ }t]$$
alternatively we can have an invertible camera matrix obtrained without dropping the last row of P

$$
\tilde{P}=\begin{bmatrix} 
K & 0 \\
0^T & 1\\
\end{bmatrix}
\begin{bmatrix} 
R & t \\
0^T & 1\\
\end{bmatrix}=\tilde{K}E
$$
with $E$ being a rigid body transformation and $\tilde{K}$ a full rank calibration matrix in this we can map directly to the screen coordinates from the 3D world coordinates with a plus disparity 
$$
\bar{p}_w=(x_w,y_w,z_w,1) \text{ } \textbf{x}_s=(x_s,y_s,1,d) \text{ } x_s \sim \bar{P}\bar{p}_w
$$
with $\sim$ meaning "up to scale", after the multiplication by the third element we obtain the normalized form $\textbf{x}_s$.



in general $\tilde{P}$ allows us to remap the last row to what is more useful for us. 

we write the last row of $\tilde{P}$ , indicated as $p_3$ , with $p_3=s_3[\hat{n}_0|c_0]$ with $||\hat{n}_0||=1$ and we obtain the equation $$d=\frac{s_3}{z}(\hat{n}_0p_w+c_0)$$ 