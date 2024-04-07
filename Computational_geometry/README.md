<div align="center">
📖 Computational_geometry
</div> 

# Computational Geometry 

## Geometry
* Point
* Line
* Segment
* Polyline

## Algorithms
* Bssic Operation
  * dot product - 点积
  * Cross product - 叉积
* Projection-投影
  * Projection length of point p - 点到线段的投影长度
  * Projection point of point p - 点到线段的投影点
* Distance-求距离
  * Point to Point
  * Point to Line
  * Point to Segment
  * Segment to Segment 
* Side-求相对位置关系
一个点与线段之间的位置关系, 定义一个enum来表示
```cpp
enum class Side{
    // When the segment's length is zero, it's useless to determine the side, so we use DEFAULT_NO_SIDE to show.
    DEFAULT_NO_SIDE=0,
    LEFT,
    RIGHT,
    // The three below states mean that the point is in line.
    ON_AFTER,
    ON_BEFORE,
    WITHIN
};
```
* Point to Left of the Segment. - 点在线段的左边
* Point to Right of the Segment. - 点在线段的右边
* Point on the Segment's Line - 点在线段所在的直线上
  * Point in front of the Segment - 点在线段前面
  * Point behind the Segment - 点在线段后面
  * Point indside the Segment - 点在线段内部
* Intersection-相交
Intersection of Segments - 线段与线段之间的相交
  * Determining Intersection - 判断是否相交
  * Calculating the Intersection Point - 若相交则求出相交点
* Curvature-曲率
* Obtain curvature according to p1,p2,p3. - 通过三点求曲率：
* Find closest segment-求polyline上距离给定点最近的线段
Find the given point's closest segment in polyline using linear search. - 求距离给定点最近的线段。


Bibliography: 
* <a href="https://github.com/CHH3213/Math_Geometry">Math_Geometry</a>
* <a href="https://blog.csdn.net/weixin_42301220/article/details/135439512">计算几何学 | 实用计算几何学知识c++代码实现</a>
* 

  

