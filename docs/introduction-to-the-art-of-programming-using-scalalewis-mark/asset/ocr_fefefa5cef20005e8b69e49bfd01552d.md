```
def drawWire(i:Int) {
    val PositionAndState(x,y,s) = posAndState(i)
    g.setPaint(if(s) Color.green else Color.black)
    g.fill(new Ellipse2D.Double(x-3,y-3,6,6))
    if(comps(i)==hoverComp) {
        g.setPaint(Color.red)
        g.fill(new Ellipse2D.Double(x-2,y-2,4,4))
    }
}

def drawSwitch(sw:Switch,i:Int) {
    val PositionAndState(x,y,s) = posAndState(i)
    g.setPaint(if(s) Color.green else Color.black)
    g.fill(new Rectangle2D.Double(x-4,y-4,8,8))
    if(sw==hoverComp) {
        g.setPaint(Color.red)
        g.fill(new Rectangle2D.Double(x-3,y-3,6,6))
    }
    val wIndex = comps.indexOf(sw.out)
    g.setPaint(if(posAndState(wIndex).state) Color.green else Color.black)
    g.draw(new Line2D.Double(posAndState(wIndex).x, posAndState(wIndex).y, x, y))
}

for((comp,i) <- comps.zipWithIndex) comp match {
    case g:Gate => drawGate(g)
    case w:Wire => drawWire(i)
    case s:Switch => drawSwitch(s,i)
}

def propertiesPanel() : Component = {
    if(propPanel == null) {
        import BorderPanel.Position._
        propPanel = new BorderPanel {
            val radioButtons = Seq(
                new RadioButton { action = Action("Add Switch") {
                    clickAction = (e,x,y) => e match {
                        case mc:MouseClicked =>
                            val sw = new Switch(false,x,y)
                            comps += sw
                            sw.start
                        case _ =>
                    }
                } },
                new RadioButton { action = Action("Add And Gate") {
                    clickAction = (e,x,y) => e match {
                        case mc:MouseClicked =>
                            val and = new AndGate(x,y)
                            comps += and
                            and.start
                        case _ =>
                    }
                } },
                new RadioButton { action = Action("Add Or Gate") {
```