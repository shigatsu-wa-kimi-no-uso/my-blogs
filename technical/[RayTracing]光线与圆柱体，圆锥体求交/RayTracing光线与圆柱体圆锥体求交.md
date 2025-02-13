# [RayTracing]光线与圆柱体，圆锥体求交

光线与圆球、三角形求交是很容易的，但是对于稍微更复杂的圆柱体、圆锥体如何求交呢？

先回想下对于不规则图形的常见处理措施，比如求函数图像为不规则曲线的积分，要么用数值法，要么用解析式法。

如果曲线非常不规则，解析式方法往往失效，但是对于某些曲线它实际上是多个函数的分段罢了，这时候分段进行积分即可。

对于图形也一样，圆柱体、圆锥体，本质上就是某个范围，是范围也就是集合，就能求交、并、补等。

我没有系统学过图形和立体几何上的求交求并，但直觉告诉我这么做没问题。

### 光线与圆柱体求交  
下面加粗的均为三维向量，下标 $x,y,z$ 表示对应向量的 $x,y,z$ 分量。

对于圆柱体，在直角坐标系下，假设圆柱的底面与 $xOy$ 平面平行，高与 $z$ 轴平行，高度为 $h$ ， 圆柱底面半径为 $r$ ，那么实际上就是这么一个方程：

$(\bold R_{xy}- \bold C_{xy})^2=r^2, \bold R_z \in [\bold C_z,\bold C_z +h] $ 

其中光线 $\bold R=\bold S+t\bold d$ ， $\bold C$ 为圆心。

所以对于光线与圆柱体求交，实际上就是光线的 $x,y$ 分量与圆柱底面的圆求交，光线的 $z$ 分量与区间$ [\bold C_z,\bold C_z +h]$ 的求交。

换句话说，圆柱体即“无限高但有限半径”的圆柱与“有限高但无限半径”的圆柱的两者的交集，与圆柱体求交，自然也就是求光线进入代表“无限高但有限半径”的圆，与进入代表“有限高但无限半径”的区间的交集。

因此求解过程就是

①计算光线进出“无限高但有限半径”的圆柱的时间，得到 $[t1_{in},t1_{out}]$ ，也就是解方程 $(\bold R_{xy}- \bold C_{xy})^2=r^2$ 

②计算光线进出“有限高但无限半径”的圆柱的时间，也就是光线的 $z$ 分量进出区间 $[\bold C_z,\bold C_z +h] $ 的时间 $[t2_{in},t2_{out}]$ 

③求交得到光线进出圆柱体的时间 $[t_{in},t_{out}]$ （假设所有的 $t$ 都是正值） $[t1_{in},t1_{out}] \cap[t2_{in},t2_{out}]=[t_{in},t_{out}]$ 

### 光线与圆锥体求交  
圆柱体的表示更加复杂些，但沿用上面的思路，圆锥体可以看作是“底面随高度变化”的圆柱，与某个区间相交。

在直角坐标系下，假设圆锥的底面与 $xOy$ 平面平行，高与 $z$ 轴平行，圆锥的“尖”朝向 $z$ 轴正方向，高度为 $h$ ， 圆柱底面半径为 $r$ ，可以得到方程：

$(\bold R_{xy}- \bold C_{xy})^2=[k(\bold A_z-\bold R_z)]^2, \bold R_z \in [\bold C_z,\bold A_z]$ 

其中光线 $\bold R=\bold S+t\bold d$ ， $\bold C$ 为圆心， $\bold A$ 为圆锥的顶点， $k=\tan\frac{\theta}{2}$ , $\theta $ 为圆锥的顶角。

代入光线的方程，展开，整理，可以得到

$ [(\bold d_{xy})^2 - (k\bold d_z)^2]t^2 + 2[\bold d_{xy} \cdot (\bold S_{xy}-\bold C_{xy})+\bold d_z \cdot (\bold A_z-\bold S_z)k^2]t + (\bold S_{xy} - \bold C_{xy})^2 - k^2 (\bold A_z-\bold S_z)^2 = 0$ 

可以看到这是个关于 $t$ 的一元二次方程，求根公式可以派上用场了！

沿用上面的思路，计算光线与圆锥体求交的过程如下：

①计算光线进出“无限高”的圆锥体的时间，得到 $[t1_{in},t1_{out}]$ ，也就是解方程 $(\bold R_{xy}- \bold C_{xy})^2=[k(\bold A_z-\bold R_z)]^2$ 

②计算光线进出“圆锥体的高度区间”的时间，也就是光线的 $z$ 分量进出区间 $[\bold C_z,\bold A_z]$ 的时间 $[t2_{in},t2_{out}]$ 

③求交得到光线进出圆柱体的时间 $[t_{in},t_{out}]$ （假设所有的 $t$ 都是正值） $[t1_{in},t1_{out}] \cap[t2_{in},t2_{out}]=[t_{in},t_{out}]$ 

