# Creative-Programming-homework-2.1
色彩引力（失败作）


float locx , locy , vx , vy , ax , ay , l1 , l2 ;//定义行星位置xy，速度xy，加速度xy
float G ;//定义色彩引力常数
int r , g , b ;//定义三原色


void setup() {
  size(1280,720) ;
  background(0) ;//黑色背景
  /*translate(640,360) ;//将原点移至中央*/          //这一行我因为对translate理解不够清楚，使用这行最后得不到想要的结果，所以把这一行标注掉
  smooth(2) ;
  noStroke() ;//图形没有边线
  fill(255) ;//填充白色
  ellipse(640,360,200,200) ;//绘制恒星
  locx = random(0,1280) ;
  locy = random(0,720) ;//行星初始位置随机
  vx = 0.01 * random(-100,100) ;
  vy = 0.01 * random(-100,100) ;//初速度随机
  G = 1500 ;//色彩引力常量
  r = 255 ;
  g = 255 ;
  b = 255 ;
}


void draw(){
  fill(r,g,b) ;
  ellipse(locx,locy,50,50) ;//绘制行星
  /*ellipse(locx,locy,0.1*locx,0.1*locy) ;//绘制行星*/          //这行代码是让行星的半径也跟着发生变化，最后的图案不上面要好一点，但也不是非常漂亮，并且偏离了原本的主题，所以舍弃
  l1 = (locx-640) * (locx-640) + (locy-360) * (locy-360) ;//行星和太阳的距离1
  print(l1,"\n") ;//用于查看行星与太阳当前距离，在第一阶段
  
  if (l1 < 8000) {
    ax = 0 ;
    ay = 0 ;
  }
  else {
    ax = ((640 - locx) / l1) * (G * (r + b + g)/l1) ;//加速度在x轴上的分量
  /*if (locx > 640) {
    ax = -(G * (r + b + g)/l1) ;
  }
  else if (locx < 640) {
    ax = (G * (r + b + g)/l1) ;
  }
  else {
    ax = 0 ;
  }*///确定加速度在x方向上的方向和大小          //是第41行代码的不完全版
  
    ay = ((360 -locy) / l1) * (G * (r + b + g)/l1) ;//加速度在y轴上的分量
  /*if (locy > 360) {
    ay = -(G * (r + b + g)/l1) ;
  }
  else if (locy < 360) {
    ay = (G * (r + b + g)/l1) ;
  }
  else {
    ay = 0 ;
  }*///确定加速度在y方向上的方向和大小          //是第54行代码的不完全版
  }
  
  vx = vx + ax ;
  vy = vy + ay ;//速度随加速度而改变
  locx = locx + vx ;
  locy = locy + vy ;//位置随速度而改变
  
  l2 = (locx-640) * (locx-640) + (locy-320) * (locy-320) ;//行星和太阳的距离2
  
  
/*if (r < 255) {
    if (abs(locx-640) > 560) {
      r = r + 2 ;
    }
    if ((abs(locx-640) > 360) && (abs(locx-640) < 560)) {
      r = r + 1 ;
    }
  }
  if (r > 0) {
    if ((abs(locx-640) > 80) && (abs(locx-640) < 280)) {
      r = r - 1 ;
    }
    if (abs(locx-640) < 80) {
      r = r - 2 ;
    }
  }
  
  if (g < 255) {
    if (abs(locy-360) > 300) {
      g = g + 2 ;
    }
    if ((abs(locy-360) > 180) && (abs(locx-360) < 300)) {
      g = g + 1 ;
    }
  }
  if (g > 0) {
    if ((abs(locy-360) > 60) && (abs(locy-360) < 180)) {
      g = g - 1 ;
    }
    if (abs(locy-360) < 60) {
      g = g - 2 ;
    }
  }
      
  if ((b < 255)) {
    if (l2 > l1) {
      b = b + 1 ;
    }
  }
  if ((l2 < l1)) {
      if (vy < 0) {
        b = b - 1 ;
      }
  }*/          //颜色随位置而改变
  
/*if (r < 255) {
    if (vx * (locx - 640) > 0) {
      r = r + 1 ;
    }
  }
  if (r > 0) {
      if (vx * (locx - 640) < 0) {
        r = r - 1 ;
      }
  }//r的值与行星在x方向上的方向有关
  
  if (g < 255) {
    if (vy * (locy - 360) > 0) {
      g = g + 1 ;
    }
  }
  if (g > 0) {
      if (vy * (locy - 360) < 0) {
        g = g - 1 ;
      }
  }//g的值与行星在y方向上的方向有关
  
   if ((b < 255)) {
    if (l2 > l1) {
      b = b + 1 ;
    }
  }
  if ((l2 < l1)) {
      if (vy < 0) {
        b = b - 1 ;
      }//b的值与行星和太阳的距离有关*/          //颜色随运动状态而改变
      
  if ((b < 255)) {
    if (l2 > l1) {
      r = r + 1 ;
      g = g + 1 ;
      b = b + 1 ;
    }
  }
  if ((l2 < l1)) {
      if (vy < 0) {
        r = r - 1 ;
        g = g - 1 ;
        b = b - 1 ;
      }
  }//b的值与行星与太阳的距离有关          //这段代码行星是黑白的
  
  
  if ((locx < 0) || (locx > 1280)) {
    vx = -vx ;
  }
  if ((locy < 0) || (locy > 720)) {
    vy = -vy ;
  }//当小球碰到边框时，弹回
  
  fill(r,g,b,1) ;
  ellipse(640,360,200,200) ;//绘制恒星
  
}
