```
for(i <- 0 until n) rover = rover.next
rover.data
}

def clear() {
  hd = null
  tl = null
  num = 0
}

def insertAll(n: Int, elems: Traversable[A]) {
  if(n<0 || n>=num+1) throw new IndexOutOfBoundsException(n+" of "+num)
  if(elems.nonEmpty) {
    val first = new Node(elems.head,null)
    var last = first
    num += 1
    for(e <- elems.tail) {
      last.next = new Node(e,null)
      last = last.next
      num += 1
    }
    if(n==0) {
      last.next = hd
      hd = first
      if(tl==null) tl=last
    } else {
      var rover = hd
      for(i <- 1 until n) rover = rover.next
      last.next = rover.next
      rover.next = first
      if(last.next==null) tl = last
    }
  }
}

def iterator = new Iterator[A] {
  var rover = hd
  def hasNext = rover!=null
  def next:A = {
    val ret = rover.data
    rover = rover.next
    ret
  }
}

def length : Int = num

def remove(n: Int): A = {
  if(n<0 || n>=num) throw new IndexOutOfBoundsException(n+" of "+num)
  num -= 1
  if(n==0) {
    val ret = hd.data
    hd = hd.next
    if(hd==null) tl = null
    ret
```