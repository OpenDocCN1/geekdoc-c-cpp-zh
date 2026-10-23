```
@transient private var startComp:CircuitComponent = null
@transient private var (dx,dy) = (0.0, 0.0)
@transient private var (sx,sy) = (0.0, 0.0)

def draw(g:Graphics2D) {
  val posAndState = comps.map(_ !? GetPosAndState match {
    case pas@PositionAndState(x,y,S) => pas
  })

def drawGate(gate:Gate) = {
  val (gx,gy) = gate !? GetPos match {
    case (x:Double,y:Double) => (x,y)
  }

g.setPaint(if(gate==hoverComp) Color.red else Color.black)
gate match {
  case og:OrGate =>
    val orPath = new GeneralPath()
    orPath.moveTo(-15+gx,-10+gy)
    orPath.quadTo(5+gx,-10+gy,15+gx,0+gy)
    orPath.quadTo(5+gx,10+gy,-15+gx,10+gy)
    orPath.quadTo(0+gx,0+gy,-15+gx,-10+gy)
    orPath.closePath()
    g.fill(orPath)
  case ag:AndGate =>
    g.fill(new Rectangle2D.Double(gx-15,gy-10,20,20))
    g.fill(new Arc2D.Double(gx-5,gy-10,20,20,-90,180,Arc2D.PIE))
  case ng:NotGate =>
    val triangle = new GeneralPath()
    triangle.moveTo(-15+gx,-10+gy)
    triangle.lineTo(10+gx,0+gy)
    triangle.lineTo(-15+gx,10+gy)
    triangle.closePath()
    g.fill(triangle)
    g.fill(new Ellipse2D.Double(gx+10,gy-2.5,5,5))
}
val (ins,outs) = gate !? GetWires match {
  case (i:List[Wire],o:List[Wire]) => (i,o)
}
for((iw,i) <- ins.zipWithIndex; if iw!=null) {
  val index = comps.indexOf(iw)
  g.setPaint(if(posAndState(index).state) Color.green else Color.black)
  g.draw(new Line2D.Double(posAndState(index).x, posAndState(index).y,
    gx-15, gy+20*i-10))
}
for((ow,i) <- outs.zipWithIndex) {
  val index = comps.indexOf(ow)
  g.setPaint(if(posAndState(index).state) Color.green else Color.black)
  g.draw(new Line2D.Double(posAndState(index).x, posAndState(index).y,
    gx+15, gy+20*i))
}
if(startComp!=null) {
  g.setPaint(Color.black)
  g.draw(new Line2D.Double(sx,sy,dx,dy))
}
```