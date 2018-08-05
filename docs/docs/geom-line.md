## Introduction

Line shape and methods, built-in methods of phaser.

- Author: Richard Davey

## Usage

### Create shape

```javascript
var line = new Phaser.Geom.Line(x1, y1, x2, y2);
```

#### Clone shape

```javascript
var line1 = Phaser.Geom.Line.Clone(line0);
```

### Draw on [graphics](graphics.md)

```javascript
graphics.strokeLineShape(line);
```

### Set properties

- All properties
    ```javascript
    line.setTo(x1, y1, x2, y2);
    ```
    or
    ```javascript
    Phaser.Geom.Line.CopyFrom(source, dest);
    ```
- Position
    ```javascript
    line.x1 = 0;
    line.y1 = 0;
    line.x2 = 0;
    line.y2 = 0;
    ```
    or
    ```javascript
    line.left = 0;    // min(x1, x2)
    line.top = 0;     // min(y1, y2)
    line.right = 0;   // max(x1, x2)
    line.bottom = 0;  // max(y1, y2)
    ```
    - Offset start, end
        ```javascript
        var line = Phaser.Geom.Line.Offset(line, dx, dy); 
        // line.x1 += dx, line.y1 += dy, line.x2 += dx, line.y2 += dy
        ``` 
    - Set center position
        ```javascript
        var line = Phaser.Geom.Line.CenterOn(line, x, y);
        ```
- Start point, angle, length
    ```javascript
    var line = Phaser.Geom.Line.SetToAngle(line, x, y, angle, length);
    ```
    - `line` : The line to set
    - `x` , `y` : start point
    - `angle` : The angle of the line in **radians**
        ```javascript
        var rad = Phaser.Math.DegToRad(deg);
        ```
    - `length` :　The length of the line
- Rotate a line around its **midpoint** by the given angle in radians
    ```javascript
    var line = Phaser.Geom.Line.Rotate(line, angle)
    ```
    - `line` : The line to set
    - `angle` : The angle of the line in **radians**
        ```javascript
        var rad = Phaser.Math.DegToRad(deg);
        ```
- Normal vector
   ```javascript
   var normal = Phaser.Geom.Line.GetNormal(line);  // normal: {x, y}
   // var normal = Phaser.Geom.Line.GetNormal(line, normal);  // modify normal
   ```

### Get properties

- Position
    ```javascript
    var x1 = line.x1;
    var y1 = line.y1;
    var x2 = line.x2;
    var y2 = line.y2;    
    var top = line.top;       // min(x1, x2)
    var left = line.left;     // min(y1, y2)
    var right = line.right;   // max(x1, x2)
    var bottom = line.bottom; // max(y1, y2)    
    ```
    - Start point
       ```javascript
       var start = line.getPointA();  // start: {x, y}
       var start = line.getPointA(start);  // modify start
       ```
    - End point
       ```javascript
       var end = line.getPointB();  // end: {x, y}
       var end = line.getPointB(end);  // modify end
       ```       
    - Middle point
        ```javascript
        var middle = Phaser.Geom.Line.GetMidPoint(line);  // middle: {x, y}
        // var middle = Phaser.Geom.Line.GetMidPoint(line, middle);
        ```
- Length
    ```javascript
    var length = Phaser.Geom.Line.Length(line);
    ```
    - Width : Abs(x1 - x2)
        ```javascript
        var width = Phaser.Geom.Line.Width(line);
        ```
    - Height : Abs(y1 - y2)
        ```javascript
        var width = Phaser.Geom.Line.Height(line);
        ```
- Slope : (y2 - y1) / (x2 - x1)
    ```javascript
    var slope = Phaser.Geom.Line.Slope(line);
    ```
- Angle
    ```javascript
    var angle = Phaser.Geom.Line.Angle(line);
    ```
    - `angle` : The angle of the line in **radians**
        ```javascript
        var deg = Phaser.Math.RadToDeg(rad);  // deg : -180 ~ 180
        ```

### Point(s) & shape

- Get a random point inside shape
    ```javascript
    var point = line.getRandomPoint();
    // var point = line.getRandomPoint(point);  // modify point
    ```
- Get point at shape's edge
    ```javascript
    var point = line.getPoint(t);  // t : 0 ~ 1. 0=start, 0.5=middle, 1=end
    // var point = line.getPoint(t, point);  // modify point
    ```
- Get points around shape's edge
    ```javascript
    var points = line.getPoints(quantity);
    // var points = line.getPoints(quantity, null, points);  // modify points
    ```
    or calculate quantity from steps
    ```javascript
    var points = line.getPoints(false, step);
    // var points = line.getPoints(false, step, points);  // modify points
    ```
    - `points` : an array of point
- Get points using *Bresenham*'s line algorithm
    ```javascript
    var points = Phaser.Geom.Line.BresenhamPoints(line, step);
    // var points = Phaser.Geom.Line.BresenhamPoints(line, step, points);  // modify points
    ```

### Equal

```javascript
var isEqual = Phaser.Geom.Line.Equals(line0, line1);
```

x1, y2, x2, y2 are equal.

### Intersection

- Line to [circle](geom-circle.md)
    ```javascript
    var result = Phaser.Geom.Intersects.LineToCircle(line, circle);
    // var result = Phaser.Geom.Intersects.LineToCircle(line, circle, nearest);  // nearest : nearest point on line
    ```
- Line to [rectangle](geom-rectangle.md)
    ```javascript
    var result = Phaser.Geom.Intersects.LineToRectangle(line, rect);
    ```
- Line to triangle
    ```javascript
    var result = Phaser.Geom.Intersects.TriangleToLine(triangle, line);
    ```
- Line to line
    ```javascript
    var result = Phaser.Geom.Intersects.LineToLine(line1, line2);
    // var result = Phaser.Geom.Intersects.LineToLine(line1, line2, out);  // out : intersected point
    ```