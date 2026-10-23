```
```
 raf.seek(pos)
 pos = raf.readLong()
 i += 1
}
reader(raf)
}

def clear() {
 raf.seek(ltail)
 raf.writeLong(localFirstFree)
 localFirstFree = lhead
 lhead = -1
 ltail = -1
 length = 0
}

def insertAll(n:Int, elems:Traversable[A]) {
 if(n>length) throw new IllegalArgumentException("Insert at index "+
 " of "+length)
 var i = 0
 var (prev,next) = if(n==0) (-1L,lhead) else {
 var (pp,nn) = (lhead,-1L)
 while(i<n) {
 raf.seek(pp)
 if(i<n-1) pp = raf.readLong()
 else nn = raf.readLong()
 i += 1
}
 (pp,nn)
}
 if(prev != -1L) raf.seek(prev)
 for(elem <- elems) {
 val npos = newNodeePosition
 if(prev == -1L) {
 lhead = npos
 prev = npos
 } else raf.writeLong(npos)
 raf.seek(npos+8)
 writer(raf,elem)
 raf.seek(npos)
}
 if(next == -1L) ltail = raf.getFilePointer()
 raf.writeLong(next)
 length += elems.size
}

def iterator = new Iterator[A] {
 var pos = lhead
 def hasNext = lhead > -1L
 def next = {
 raf.seek(pos)
 pos = raf.readLong()
 reader(raf)
}
}
```
```