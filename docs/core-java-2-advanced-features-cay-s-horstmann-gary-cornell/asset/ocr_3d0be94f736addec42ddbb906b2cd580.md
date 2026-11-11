# Listing 11.1  *(Continued)*

```
```java
201  public RectangleMaker()
202  {
203      super(2);
204  }
205
206  public Shape makeShape(Point2D[] p)
207  {
208      Rectangle2D s = new Rectangle2D.Double();
209      s.setFrameFromDiagonal(p[0], p[1]);
210      return s;
211  }
212 }
213
214 /**
215  * Makes a round rectangle that joins two given corner points.
216  */
217 class RoundRectangleMaker extends ShapeMaker
218 {
219     public RoundRectangleMaker()
220     {
221         super(2);
222     }
223
224     public Shape makeShape(Point2D[] p)
225     {
226         RoundRectangle2D s = new RoundRectangle2D.Double(0, 0, 0, 20, 20);
227         s.setFrameFromDiagonal(p[0], p[1]);
228         return s;
229     }
230 }
231
232 /**
233  * Makes an ellipse contained in a bounding box with two given corner points.
234  */
235 class EllipseMaker extends ShapeMaker
236 {
237     public EllipseMaker()
238     {
239         super(2);
240     }
241
242     public Shape makeShape(Point2D[] p)
243     {
244         Ellipse2D s = new Ellipse2D.Double();
245         s.setFrameFromDiagonal(p[0], p[1]);
246         return s;
247     }
248 } 
```
```