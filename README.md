# Creative-Coding-11.18-Homework
创意编程第二讲作业

作品目标：随机生成不同颜色、大小的正方形，并将这些正方形叠加形成较为丰富的图形。
         这些叠加正方形可以沿画布竖直方向向下滑动。
         在一组正方形到达底端时，下一组正方形会随机生成并向下滑落，如此循环往复，具有序列性。

设计思路：1. 定义并存储正方形大小、颜色、数量、坐标、移动路线
         2. 创建画布并定义其背景色
         3. 绘制正方形并记录&更新其路径
         4. 更新正方形的位置，使其沿竖直方向滑动且循环往复，并定义其滑动速度

代码：
int numRects = 20; // 定义正方形的数量
float[] x = new float[numRects]; // 存储正方形中心的x坐标
float[] y = new float[numRects]; // 存储正方形中心的y坐标
float[] size = new float[numRects]; // 存储正方形的大小
color[] colors = new color[numRects]; // 存储正方形的颜色

// 定义一个记录正方形移动路线的数组
float[][] path = new float[numRects][100];
int pathIndex = 0;

void setup(){
  size(800, 600);
  noStroke();
}

void draw(){
  background(255); // 设置背景色为白色

  // 绘制正方形，并记录其路径
  for(int i = 0; i < numRects; i++){
    fill(colors[i]); // 设置填充颜色
    rect(x[i], y[i], size[i], size[i]); // 绘制正方形
    path[i][pathIndex] = y[i]; // 记录正方形的路径
    pathIndex = (pathIndex + 1) % 100; // 更新路径索引，使路径不会无限增长
  }

  // 更新正方形的位置，使其沿竖直方向滑动
  for(int i = 0; i < numRects; i++){
    y[i] += 1; // 正方形每帧向下移动1个像素
    if(y[i] > height){ // 当正方形移动到屏幕底部时，重新设置其位置到屏幕顶部，并改变其颜色和大小
      y[i] = 0;
      colors[i] = color(random(255), random(255), random(255)); // 随机生成颜色
      size[i] = random(200, 800); // 随机生成大小
      path = new float[numRects][100]; // 重置路径数组
      pathIndex = 0;
    }
  }
}

