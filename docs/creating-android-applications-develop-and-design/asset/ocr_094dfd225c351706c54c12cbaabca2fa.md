```
```java
private final IBinder mBinder = new MusicServiceStub(this);
@Override
public IBinder onBind(Intent intent) {
    return mBinder;
}
static class MusicServiceStub extends IMusicService.Stub {
    WeakReference<MusicService> mService;
    MusicServiceStub(MusicService service) {
        mService = new WeakReference<MusicService>(service);
    }
    public void pause(){
        mService.get().pause();
    }
    public void play(){
        mService.get().play();
    }
    public void setDataSource(long id){
        mService.get().setDataSource(id);
    }
    public String getSongTitle(){
        return mService.get().getSongTitle();
    }
}
```
```