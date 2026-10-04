
```java
bmOptions.inJustDecodeBounds = false;
bmOptions.inSampleSize = scaleFactor;
bmOptions.inPurgable = true;

try {
  Thread.sleep(500); // 延迟半秒以允许图片处理
} catch (InterruptedException ie) {
}

Bitmap bitmap = BitmapFactory.decodeFile(Environment.getExternalStorageDirectory() + "/DCIM/Camera/" + picfilename + ".jpg", bmOptions);
return bitmap;

public void onClose() {
  if (camera != null) {
    camera.release();
    camera = null;
  }
  PhotoCapture.this.finish();
}
```
