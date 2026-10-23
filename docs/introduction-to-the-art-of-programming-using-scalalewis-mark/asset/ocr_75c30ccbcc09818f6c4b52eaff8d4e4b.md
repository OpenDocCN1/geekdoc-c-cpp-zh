```
```
        }
    } },
new RadioButton { action = Action("Flip Switch") {
    clickAction = (e,x,y) => e match {
        case mp:MouseClicked =>
            if (hoverComp != null) {
                hoverComp match {
                    case s:Switch => hoverComp ! FlipSwitch
                    case _ =>
                }
            }
            case _ =>
        }
    } }
) 

val group = new ButtonGroup(radioButtons:_*)
layout += new GridPanel(radioButtons.length+1,1) {
    radioButtons.foreach(rb => contents += rb)
    speedField = new TextField(speedMult.toString) {
        listenTo(this)
        reactions += {
            case ed:EditDone => speedMult = text.toInt
        }
    }
    contents += speedField
} -> North
}
)
propPanel
}

override def toString() = "Circuit"

def toXML : xml.Node = {
    <drawCircuit speed={speedMult.toString}>
        {comps.map(_.toXML)}
    </drawCircuit>
}

def react(evt:Event,cx:Double,cy:Double) {
evt match {
    case me:MouseEvent =>
        hoverComp = null
        var lastDist = 1e100
        for(comp <- comps) {
            val (ccx,ccy) = comp ?? GetPos match {
                case (x:Double,y:Double) => (x,y)
            }
            val (dx,dy) = (cx-ccx, cy-ccy)
            val dist = math.sqrt(dx*dx+dy*dy)
            if (dist<15 && dist<lastDist) {
                hoverComp = comp
                lastDist = dist
            }
        }
}
```
```