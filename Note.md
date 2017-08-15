这个文档是用来记录 三消游戏 Match 3 Jewel Full 298 Levels ， 模仿的一些笔记，顺便练习下写markdown
=======

> made by [Unity](http://www.unity.com) 5.5.1f


Contents:
======

第一天主要看下目录结构，以及LoginScene的逻辑
-------
[day1](#day1)

[day2](#day2)

[day3](#day3)

[day4](#day4)

--------
<span id = "day1">day1</span>
------

    目录结构： {
        Animation
        Audio
        Fonts
        GoogleMobileAds - ignore
        Graphics
        Plugins 
        Prefabs
        Resources
        Scenes
        Scripts
        Note.doc
        ReadMe.doc
    }


> 有部分资源是不在`Resources`下的，就意味着，这些资源，一般是用`鼠标去拖动`的，
  不能去使用代码加载。`LoadingScene.unity`这个UI背景居然是带着`processbar`的背景的，醉了

<img src="https://raw.githubusercontent.com/koake/Match-3-Jewel-Full-298-Levels---TemplateProject/master/Assets/Graphics/Load/background_loading.png" width = "300" alt="background" />

## Script/Home/LoadWaiting.cs
这是游戏启动的地方，这里的进度条是假的，只是看上去正在加载而已。

Q1: 在i=0的时候，`Application.LoadLevel("HomeScene")`;会执行吗？

A1: [click to jump](#answer1)
``` csharp
IEnumerator Start()
{
    for (int i = 0; i < 120; i++)
    {
        loadbar.fillAmount += 1 / 120f;
        yield return new WaitForEndOfFrame();
    }
    Application.LoadLevel("HomeScene");
}
```























### <span id = "answer1">Answer1</span>
---
不会执行，因为`Application.LoadLevel("HomeScene");`也在协程中，必须上面走完了，才会走下面

> 那下面的语句呢？如果想不出来就`动手试试`
```csharp
void Start()
{
    StartCoroutine(test());
    Debug.Log("im last stagment");
}

IEnumerator test()
{
    yield return new WaitForSeconds(5);
    Debug.Log("im in ");
}
```

