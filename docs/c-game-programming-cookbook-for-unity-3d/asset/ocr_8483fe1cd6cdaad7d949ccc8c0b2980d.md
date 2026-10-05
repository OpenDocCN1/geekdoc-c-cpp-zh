```
void Start ()
{
    // we will grab the volume from PlayerPrefs when this script
    // first starts
    volume= PlayerPrefs.GetFloat(gamePrefsName+"_MusicVol");

    // create a game object and add an AudioSource to it,
    // play music on
    source=new GameObject("Music_AudioSource");
    source=GO.AddComponent<AudioSource>();
    source.name="MusicAudioSource";n    source.playOnAwake=true;
    source.clip=music;
    source.volume=volume;

    // the script will automatically fade in if this is set
    if (shouldFadeInStart) {
        fadeState=0;
        volume=0;
    } else {
        fadeState=1;
        volume=volumeON;
    }

    // set default values
    targetFadeState=1;
    targetVolume=volumeON;
    source.volume=volume;
}

void Update ()
{
    // if the audource is not playing and it's supposed to
    // loop, play it again (Sam?)
    if (!source.isPlaying && loopMusic) {
        source.Play();
    }

    // deal with volume fade in/out
    if(fadeState!=targetFadeState) {
        if (targetFadeState==1) {
            if (volume==volumeON)
                fadeState=1;
        } else {
            if (volume==0)
                fadeState=0;
        }

        volume=Mathf.Lerp(volume, targetVolume, Time.deltaTime * fadeTime);
        source.volume=volume;
    }
}

public void FadeIn ( float fadeAmount )
{

```