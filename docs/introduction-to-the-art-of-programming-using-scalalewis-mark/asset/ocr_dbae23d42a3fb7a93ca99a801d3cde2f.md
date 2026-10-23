```
private class BallBallColl(val time:Double,val b1:Int,val b2:Int) extends

\ \ \ \ CollEvent {

\ \ \ \ def handle {

\ \ \ \ \ \ \ val ball1 = workCopy(b1).advanceTo(time)

\ \ \ \ \ \ \ val ball2 = workCopy(b2).advanceTo(time)

\ \ \ \ \ \ \ val m1 = ball1.size*ball1.size*ball1.size

\ \ \ \ \ \ \ val m2 = ball2.size*ball2.size*ball2.size

\ \ \ \ \ \ \ val cmvx = (ball1.vx*m1+ball2.vx*m2)/(m1+m2)

\ \ \ \ \ \ \ val cmvy = (ball1.vy*m1+ball2.vy*m2)/(m1+m2)

\ \ \ \ \ \ \ val dx = ball1.x-ball2.x

\ \ \ \ \ \ \ val dy = ball1.y-ball2.y

\ \ \ \ \ \ \ val dist = math.sqrt(dx*dx+dy*dy)

\ \ \ \ \ \ \ if(dist>1.01*(ball1.size+ball2.size)) {

\ \ \ \ \ \ \ \ \ \ println("Warning: collision with big separation. "+b1+" "+b2+" "+dist)

\ \ \ \ \ \ \ }

\ \ \ \ \ \ \ if(dist<0.99*(ball1.size+ball2.size)) {

\ \ \ \ \ \ \ \ \ \ println("Warning: collision with little separation. "+b1+" "+b2+" "+dist)

\ \ \ \ \ \ \ }

\ \ \ \ \ \ \ val vx1 = ball1.vx-cmvx

\ \ \ \ \ \ \ val vy1 = ball1.vy-cmvy

\ \ \ \ \ \ \ val nx = dx/dist

\ \ \ \ \ \ \ val ny = dy/dist

\ \ \ \ \ \ \ val mag = nx*vx1+ny*vy1

\ \ \ \ \ \ \ workCopy(b1) = ball1.copy(vx = ball1.vx-1.9*mag*nx, vy = ball1.vy-1.9*mag*ny)

\ \ \ \ \ \ \ workCopy(b2) = ball2.copy(vx = ball2.vx+1.9*mag*nx*m1/m2, vy =

\ \ \ \ ball2.vy+1.9*mag*ny*m1/m2)

\ \ \ \ pq.removeMatchcs{

\ \ \ \ \ \ \ case bbc:BallBallColl => bbc.b1==b1 || bbc.b2==b1 || bbc.b1==b2 ||

\ \ \ \ \ \ \ \ \ \ bbc.b2==b2

\ \ \ \ \ \ \ case bwc:BallWallColl => bwc.b==b1 || bwc.b==b2

\ \ \ \ \ \ \ case \_ => false

\ \ \ \ }

\ \ \ \ val others = workCopy.indices.filter(b => b!=b1 && b!=b2)

\ \ \ \ findEventsFor(b1,others,time)

\ \ \ \ findEventsFor(b2,others,time)

\ \ }

}

private class BallWallColl(val time:Double,val b:Int,val

newDir:(Double,Double,Double,Double) => (Double,Double)) extends CollEvent {

def handle {

\ \ \ val ball = workCopy(b)

\ \ \ val nx = ball.x+(time-ball.time)*ball.vx

\ \ \ val ny = ball.y+(time-ball.time)*ball.vy

\ \ \ val (nxv,nyv) = newDir(ball.x,ball.y,ball.vx,ball.vy)

\ \ \ workCopy(b) = DrawBouncingBalls.Ball(nx,ny,nxv,nyv,ball.size,time)

\ \ \ pq.removeMatchcs{

\ \ \ \ \ \ \ case bbc:BallBallColl => bbc.b1==b || bbc.b2==b

\ \ \ \ \ \ \ case bwc:BallWallColl => bwc.b==b

\ \ \ \ \ \ \ case \_ => false

\ \ }

\ \ findEventsFor(b,workCopy.indices.filter(!=b),time)

}

}
```