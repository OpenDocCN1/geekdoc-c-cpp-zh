

为了安全起见，会对索引号进行检查以确保其有效性，防止因调用错误导致空引用异常。如果索引号超过了范围，将将其设置为数组中的最后一个 `AudioClip`，并在控制台中记录警告以引起注意：

```c
if (anIndexNumber>=soundObjectList.Count)
    Debug.LogWarning("BaseSoundController>Trying to do PlaySoundByIndex with invalid index number. Playing last sound in array, instead.");
    anIndexNumber = soundObjectList.Count-1;
```

会创建一个临时的 `AudioClip` 来存储所需的音频，并通过 `AudioSource.PlaySound()` 进行播放：

```c
tempSoundObj=(SoundObject)soundObjectList[anIndexNumber]
tempSoundObj.PlaySound(position);
```

在音频控制器为游戏音频提供完整解决方案之前还有一段路要走，但它可以作为一个良好且的起点。

## 8.2 音乐播放器

`MusicController.cs` 脚本用于播放音乐。它将根据 `PlayerPrefs` 值设置音量，并处理音量淡入淡出以及音频片段循环。以下是完整的脚本：

```csharp
using UnityEngine;
using System.Collections;

public class MusicController : MonoBehaviour
{
    private float volume;
    public string gamePrefsName = "DefaultGame"; // 不要忘记设置
    // 在编辑器中设置这个！！

    public AudioClip music;

    public bool loopMusic;

    private AudioSource source;
    private GameObject sourceGO;

    private int fadeState;
    private int targetFadeState;

    private float volumeON;
    private float targetVolume;

    public float fadeTime=15f;
    public bool shouldFadeInAtStart=true;

    void Start ()
    {
        // 当此脚本首次启动时，
        // 我们从 PlayerPrefs 获取音量
        volume= PlayerPrefs.GetFloat(gamePrefsName+"_MusicVol");

        // 创建一个游戏对象并为其添加 AudioSource 组件，
        // 开始播放音乐
        sourceGO=new GameObject("Music_AudioSource");
        source=sourceGO.AddComponent<AudioSource>();
        source.name="MusicAudioSource";
        source.playOnAwake=true;
        source.clip=music;
        source.volume=volume;

        // 如果设置了此项，脚本将自动淡入
        if (shouldFadeInAtStart) {
            fadeState=0;
            volume=0;
        } else {
            fadeState=1;
            volume=volumeON;
        }

        // 设置默认值
        targetFadeState=1;
        targetVolume=volumeON;
        source.volume=volume;
    }

    void Update ()
    {
        // 如果音频源没有播放且本应该
        // 循环，则重新播放 (Sam?)
        if (!source.isPlaying && loopMusic) {
            source.Play();
        }

        // 处理音量淡入/淡出
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
        volume=0;
        fadeState=0;
        targetFadeState=1;
        targetVolume=volumeON;
        fadeTime=fadeAmount;
    }

    public void FadeOut ( float fadeAmount )
    {
        volume=volumeON;
        fadeState=1;
        targetFadeState=0;
        targetVolume=0;
        fadeTime=fadeAmount;
    }
}
```

### 8.2.1 脚本解析

`MusicController.cs` 脚本应该被添加到场景中的一个空游戏对象。它派自 `MonoBehaviour` 以使用引擎调用的 `Start()` 和 `Update()` 函数：

```csharp
public class MusicController : MonoBehaviour
{}
```

`MusicController` 脚本可以在加载时自动淡入音乐，从而实现更平的场景过渡。应该在 Unity 编辑器的组件 Inspector 窗口中设置 `shouldFadeInAtStart`：

