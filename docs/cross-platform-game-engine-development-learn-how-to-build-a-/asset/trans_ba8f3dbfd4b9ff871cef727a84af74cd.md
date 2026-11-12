

此函数获取我们希望生成的数字所在区间的最小值和最大值，并返回生成的数字。[10]

```
engine/src/scripts/pipe_spawner.h
```

```cpp
// . . .
FUSE_LINE void on_update(float dt) {
  if(game_over) { return; }

  // find player
  auto player = find_entity("player");
  auto& p_rb = player.get_component <ecs::rigidbody_component> ();

  // check if player's rigidbody is disabled
  if(player.is_alive() && p_rb.disabled) {
    // stop ground scroll animation
    auto ground = find_entity("ground");
    auto& gd = ground.get_component <ecs::rigidbody_component> ();
    gd.disabled = true;

    // stop all pipes motion
    for(auto& pi_pipe : pipes) {
      auto& rb = pi_pipe.get_component <ecs::rigidbody_component> ();
      rb.disabled = true;
      auto& co = pi_pipe.get_component <ecs::collider_component> ();
      co.disabled = true;
    }

    game_over = true;
    return;
  }

  // update pipes
  update_pipes();

  // create pipes
  if(time > 2.5f) {
    time = 0.f;
    float space = math::random(60, 150);
    spawn_pipe(380, -space);
    spawn_pipe(380, 720/2 + space);
  }

  // update counter
  time += dt;
}
// . . .
```

我们首先检查 "game_over" 是否设置为 true。如果不是，我们检查玩家的刚体是否被禁用。只有当玩家与管道或地面碰撞时才会发生这种情况。当这种情况发生时，我们

![](img/2763810ed0a1572c2bec59ee52dd75be_205_0.png)

必须确保通过禁用其刚体来停止地面运动。我们还通过禁用管道的刚体来停止所有管道运动。

如果飞机仍在飞行，我们调用更新函数来移动我们的管道。然后我们检查是否已过去 2 秒。如果是，我们将使用 "spawn_pipe" 函数创建另一对管道。

## 图 43 幕后

图 43 展示了游戏运行时幕后发生的情况。管道是在屏幕视口之外创建的，由于刚体的存在，它们将开始向玩家移动。每次我们创建一对管道时，都会将时间值重置为零，以便在玩家存活期间重新开始循环。

如果你编译你的项目，你将能够看到管道被创建。

![](img/2763810ed0a1572c2bec59ee52dd75be_206_0.png)

### 添加得分

得分也将是一个带有文本组件的实体。以下是将得分实体添加到场景中的代码。

```
engine/src/ecs/scene.h
FUSE_INLINE void start() {
    // ...

    // score text
    auto score = add_entity("score");
    auto& s_tr = score.get_component<transform_component>();
    s_tr.translate = vec2f(120, 20);
    auto& tx = score.add_component<text_component>();
    tx.text = "Score: 0";
    tx.font = font->id;

    // start systems
    for (auto& sys : _systems) { sys->start(); }
}
```

这个实体非常简单。它只有一个变换组件和一个文本组件。如果你运行你的代码，你将能够在屏幕上看到文本。然而，它的值不会相应更新。所以，让我们来修复它。

### engine/src/scripts/pipe_spawner.h

```
// ...
FUSE_INLINE void update_pipes() {
    auto it = pipes.begin();
    while (it != pipes.end()) {
        // remove dead pipe
        auto &pipe = (*it);
        if (!pipe.is_alive()) {
            it = pipes.erase(it);
            continue;
        }

        // destroy if out of the screen and set score
        auto &tr = pipe.get_component<ecs::transform_component>();
        if (tr.translate.x < -50) {
            pipe.destroy();
            auto &tx = find_entity("score").get_component<ecs::text_component>();
            tx.text = "Score: " + std::to_string(++score);
        }

        it++;
    }
}
// ...
```

在 "update_pipes" 函数中，我们通过将当前得分的值转换为字符串来更新得分的文本。这简单地意味着当一对精灵移出视野时，得分将增加一。处理这件事有更好的方法，但那留作你的课后作业。

### engine/src/scripts/pipe_spawner.h

```cpp
// . . .
FUSE_INLINE void on_update(float dt) {
if(game_over) { return; }
// find player
auto player = find_entity("player");
auto& p_rb = player.get_component<ecs::rigidbody_component>();
// check if player's rigidbody is disabled
if(player.is_alive() && p_rb.disabled) {
// stop ground scroll animation
auto ground = find_entity("ground");
auto& gd = ground.get_component<ecs::rigidbody_component>();
gd.disabled = true;
}
// show game over text
auto scr = find_entity("score");
auto& tx = scr.get_component<ecs::text_component>();
tx.text = "GAME OVER";
// stop all pipes motion
for(auto& pipe : pipes) {
auto& rb = pipe.get_component<ecs::rigidbody_component>();
rb.disabled = true;
auto& co = pipe.get_component<ecs::collider_component>();
co.disabled = true;
}
game_over = true;
return;
}
// update pipes
update_pipes();
// create pipes
if(time > 2.5f) {
time = 0.0f;
float space = math::random(60, 150);
spawn_pipe(380, -space);
spawn_pipe(380, 720/2 + space);
}
// update counter
time += dt;
}
// . . .
```

为了在玩家死亡时显示“Game Over”，我们也在“on_update”函数中更改了得分的值。如上述代码片段所示。这就是让它运行所需做的全部内容。

![](img/2763810ed0a1572c2bec59ee52dd75be_209_0.png)

![](img/2763810ed0a1572c2bec59ee52dd75be_209_1.png)

## 添加音效

我们的引擎应该能够在被要求时播放声音，而不会干扰其他进程。只有在音频文件预先加载到引擎内存中时才有可能实现。

在被要求播放时加载音频文件效率相当低，因为加载音频文件可能需要一些时间，具体取决于格式和大小。这就是为什么我们在资产管理章节中创建了音频资产。

我们还需要实现一个加载音频文件的函数，就像我们为纹理和字体所做的那样。以下代码片段显示了资产注册表的成员函数定义，用于加载音频文件。

## 加载音频文件

流程保持不变。我们从源文件加载音频数据，检查加载是否成功，然后创建一个资产。

```
engine/src/assets/registry.h

// ...

FUSE_INLINE audio_o_asset* load_audio(const std::string& src, const std::string& name) {
    audio_o_clip audio_o;
    audio_o.data = Mix_LoadWAV(src.c_str());
    audio_o.filename = src;

    if (!audio_o.data) {
        FUSE_ERROR("%s", IMG_GetError());
        return NULL;
    }

    auto asset = new audio_o_asset();
    asset->instance = audio_o;
    asset->name = name;

    _data[type_id<audio_o_asset>()].push_back(asset);
    return asset;
}

// ...
```

请务必相应地更新你的资产注册表。如下所示，在场景的 start 函数中加载两个声音文件。

```
engine/src/ecs/scene.h

// . . .

FUSE_INLINE void start() {
    // . . .

    // load background music
    _assets.load_audio("assets/song.mp3", "music");

    // load explosion effect
    _assets.load_audio("assets/boom.wav", "boom");

    // . . .
}

// . . .
```

## 背景音乐

在游戏过程中播放背景音乐是很常见的。它为游戏增添了生机和乐趣。我们需要一个可以调用的函数来播放资产注册表中可用的任何音效。因此，将以下函数添加到“script_instance”中。

```
engine/src/scripts/script_instance.h

// . . .

FUSE_INLINE void play_audio(std::string name, int channel = -1,
    int loops = 0, int vol = 50) {
    auto& chunk = assets->get<audio_asset>(name)->instance.data;
    Mix_VolumeChunk(chunk, vol);
    Mix_PlayChannel(channel, chunk, loops);
}

// . . .
```

该函数接受四个参数。第一个参数是我们希望播放的音频资产的名称。第二个参数是我们希望播放歌曲的通道。如果你传递 "-1"，SDL 将为你选择下一个空闲通道。但你也可以指定一个特定的通道来播放声音。第三个参数是告诉 SDL 声音应该播放多少次。"-1" 表示无限循环。最后一个参数是你希望播放声音的音量。
该函数在注册表中查找声音资产，设置音量级别，

