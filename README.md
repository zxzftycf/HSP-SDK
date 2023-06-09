[TOC]



# 说明 #

​		这是游戏《人类保存计划》的SDK使用文档，详细描述了如何使用SDK为游戏制作模组，如果你不习惯阅读md文档，同级目录下有README.pdf文档也可供阅读，两者是相同的。

​		本SDK是unity插件，可能需要你有操作unity编辑器的基本知识，没有也没关系，我会在文档中一步步的引导操作。

​		该插件不需要你有任何的编程能力，一切都是可视化配置。

​		SDK的根本原理采用同名替换原则，不管是配置中的ID，或者是模型，UI等等，游戏内优先级高的资源会替代同名的优先级低的资源，所以在配置ID和资源命名时，尽量带有自我特色，以避免和其他模组冲突。

​		由于模组使用的AssetBundle实现，所有模组内容会被打包成AssetBundle。AssetBundle中不允许打包代码，所以所有的资源文件请勿包含代码。

​		如果在开发模组时遇到问题，可以打开设置中开发者设置中的日志选项，可以查看输出的日志，来判断模组是否产生了问题。

# 准备工作

1. 在unity官网下载unity hub。
2. SDK使用的编辑器版本是2021.3.6f1c1，如果hub中不包含此版本，可以按以下步骤操作：在unity hub中依次点击安装-安装编辑器-存档-下载存档-找到2021.3.6版本-从hub下载-等待下载完成。
3. 在hub中依次点击项目-新项目-所有模板-3D核心模板-输入项目名称和位置-建议启用版本管理-创建项目。
4. 打开项目，在Assets目录下点击右键-导入包-自定义包-选择HSP-SDK.unitypackage-导入-等待导入完成。
5. 看到编辑器最上方工具栏出现《青思游戏》的按钮，则导入成功。警告可以忽视。
6. 将工程目录下Assets/HSP-SDK/Templete/TagManager.asset文件拷贝到工程目录下ProjectSettings/TagManager.asset，覆盖原文件。 准备工作完成。

# 一个简单的开始示例

​		在这个示例中，我们尝试修改0号的攻击力成长率。

1. 点击青思游戏-人类保存计划-配置编辑器-新建配置方案-输入名称-创建。
2. 点击编辑配置-选择要编辑的配置-点击物体配置-导入模板配置-删除其他配置只保留0号的配置。
3. 找到0号的物体成长率一栏-点击展开列表-将攻击力一栏的数值改为100-点击保存。
4. 点击青思游戏-人类保存计划-模组编辑器-新建模组-输入名称，建议和配置方案使用同样的名称，方便管理-创建。
5. 点击编辑模组-模组元素类型选择配置方案-模组元素名称中输入刚才创建的配置方案的名称-点击新增。
6. 点击打开模组-填入模组的各项信息，也可以不填入，如果要上传至创意工坊，则必须填入。
7. 点击生成模组-选择导出目录-点击保存-导出。
8. 打开游戏-点击模组-本地模组。
9. 在工程路径一栏输入模组工程路径，即刚才的unity工程中HSPModProject文件夹的绝对路径。
10. 在模组名称栏输入刚才创建的模组的名称-点击加载模组。
11. 点击管理模组-刷新-刚才加载的本地模组就出现在了列表里-点击启用-将优先级调整到最高-关闭界面。
12. 点击确定前往加载界面重新加载模组。
13. 开始游戏-进入一张地图-查看0号的属性详情，可以看到攻击力的成长（黄色的值），已经变成了刚才配置的100。
14. 可以在管理模组界面停用次模组，再次进入一张地图查看0号的属性详情，可以看到又恢复到了原来的10。
15. 确认模组内容正确后，点击模组-本地模组-点击注册到创意工坊，将刚才的本地模组创建成创意工坊的物品-点击上传到创意工坊，将模组内容上传，然后就可以通过创意工坊页面查看和下载次模组了。
16. 也可以不将本地模组上传，做为一个本地的私人模组继续使用。

# 如何修改语言文本

​		如前示例，打开多语言配置，可以选择要配置的语言类型，修改或新增文本ID及其内容，游戏内会自动根据玩家选择的语言，显示对应文本ID的内容。

# 如何修改UI

​		这个示例中演示如何修改UI界面。UI文件是unity的prefab格式，请不要改变节点之间的父子关系，可以新增节点，但不要删除节点，可以修改节点的位置，大小，颜色，图片等等。

1. 选择一个要修改的UI界面，这里我们选择开始界面，效果最明显。
2. 点击青思游戏-人类保存计划-模组编辑器-新建模组-输入模组名称testChangeUI-创建。
3. 点击打开模组-输入模组相关信息。
4. 点击编辑模组-删除所有已存在配置。
5. 进入工程中Assets/HSP-SDK/Templete/UI目录，拷贝StartUIPrefab.prefab文件到。Assets/HSPModProject/testChangeUI/Content目录下。
6. 双击打开Assets/HSPModProject/testChangeUI/Content/StartUIPrefab.prefab文件。
7. 修改StartUIPrefab/Canvas/Image节点的位置，修改StartUIPrefab/Canvas/BtnNode节点的位置。保存修改。
8. 回到模组编辑器-点击生成模组-选择导出目录-点击保存-导出。
9. 进入游戏，如简单示例中一样，加载本地模组。
10. 关闭模组界面，前往模组加载界面重新加载模组，加载完毕后看见开始界面节点的位置已经发生了改变。

# 如何制作动画

​		游戏中的所有动画控制器（包括非人形）都继承自人形空手动画控制器，这个控制器在Assets/HSP-SDK/Templete/Animation/HumAnimations.controller目录下。

1. 如前面的示例，在模组编辑器中创建一个新的模组。
2. 将上面提到的模板目录下的动画控制器拷贝到新模组的工程目录下的Content文件夹下。
3. 重命名拷贝的动画控制器，防止覆盖游戏本身的控制器。
4. 双击打开新的动画控制器，用自己的动画片段填充到控制器中对应动作的Motion中。
5. 新建配置方案，将自己的动画控制器配置在想要修改动画的物体的配置中。
6. 导出模组，进行本地验证。

# 如何制作物体模型

​		模型格式应该是.fbx的，模型的Model界面勾选读取/写入，模型Rig界面应该具备Avatar，没有则应该从模型生成，人形模型骨骼应该符合unity标准，否则无法复用游戏自带的人形动画。

1. 将.fbx模型拖入空白场景生成节点，再将该节点拖入到Assets目录下任意位置生成预制件.prefab文件。
2. 双击打开预制件，在最顶层节点，添加Animator组件，取消勾选应用根运动，填入模型的Avatar。
3. 在最顶层节点，添加BoxCollider组件，调整改组件的大小和中心，来匹配模型大小，该组件就是物体的碰撞检测盒，决定了受击范围等。
4. 请勿调整最顶层节点的缩放、旋转、位置，如需调整，应该调整其子节点。
5. 右键最顶层节点-创建空对象，为节点添加一个子节点，重命名为attackNode。该节点表示物体的攻击节点，近战攻击范围判断，远程弹幕发射都是从此节点位置产生，所以将该节点位置调整到合适的攻击点，一般人形攻击点在胸部附近，非人形在嘴部附近。
6. 再为顶层节点添加一个子节点，重命名为hudNode。该节点时物体血条的显示位置，一般在物体的头部正上方，调整该节点到指定位置。
7. 再为顶层节点添加一个子节点，重命名为sfxNode。该节点为物体的音效节点，如果该节点下没有任何子节点，则物体没有音效表现。
8. 为sfxNode添加一个子节点，并重命名为move，为该节点添加AudioSource组件，取消勾选唤醒时播放和循环，将音效问价拖动到AudioClip一栏中，该音效做为物体移动时播放的音效。
9. 为sfxNode添加一个子节点，并重命名为attack，重复上面的操作，该音效做为物体攻击时的音效。
10. 为sfxNode添加一个子节点，并重命名为dead，重复上面的操作，该音效做为物体死亡时的音效。
11. 为sfxNode添加一个子节点，并重命名为beHit，重复上面的操作，该音效做为物体受击时的音效。
12. 保存所有修改。创建一个新的配置方案，将0号的配置中的模型一栏文件名修改为新制作的模型的文件名。
13. 创建一个新的模组，将模型的prefab文件拷贝到新模组的Content目录下，导出模组。
14. 打开游戏，加载本地模组，验证0号模型是否被修改。

# 如何使物体手持道具

​		任意模型都可以附加道具模型，不论是人形还是非人形。需要在模型骨骼节点中添加左手武器持有节点和右手武器持有节点，不论这两个节点是什么部位。

1. 对于非人形模型，在任意骨骼节点下创建子节点，假设这是左手武器持有点，在该节点点击右键，点击显示节点路径，将打印出的节点路径复制（路径中不要包含最顶层节点），将该路径填入物体配置中的左手持有点一栏，同样的创建并配置右手武器持有点。
2. 对于人形模型，左手武器持有点的节点位置应该在左手骨骼节点中心，并需要调整角度，x轴与手臂重合平行，y轴垂直于手掌心，z轴指向人物身后。
3. 右手武器持有点的节点位置应该在右手骨骼节点中心，并需要调整角度，x轴与手臂重合平行，y轴垂直于手掌心，z轴指向人物前方。
4. 同样需要将两个持有点的节点路劲配置在物体配置表中，这样人形物体就可以将第一道具显示出来了。

# 如何制作道具模型

​		这里的道具模型通常指游戏中支持的武器模型，包括双手斧，弓，弩，长枪，法杖，单手剑，双手剑。不要对根节点进行位置，缩放，旋转的更改。

1. 根节点不要有其他组件，模型的节点（包含mesh组件）做为根节点的子节点，并重命名为body。

2. 在根节点下新建子节点并重命名为sfxNode，在该节点下新建节点并重命名为attack，为attack节点添加AudioSource组件，取消勾选唤醒时播放和循环，这个节点是武器攻击时要播放的音效。

3. 双手武器需要定义一个另一只手的接触点，在根节点下新建节点，并重命名为AttachPoint，将接触点的位置调整到合适位置，角度对于每种武器是固定的。

   |        | 旋转x | 旋转y | 旋转z |
   | ------ | ----- | ----- | ----- |
   | 双手斧 | 47.7  | -75.4 | 23.7  |
   | 弩     | 84.3  | 167.4 | 329.5 |
   | 长枪   | 38.6  | -75.7 | 34.4  |
   | 双手剑 | 2.4   | 97    | 184   |

   表格中没有提到的武器，则不需要AttachPoint节点。

4. 每种武器的旋转角度也是不同的，请不要旋转根节点，应该旋转body节点。

   |        | 旋转x | 旋转y  | 旋转z  |
   | ------ | ----- | ------ | ------ |
   | 双手斧 | 270.7 | 5.5    | -185.9 |
   | 弓     | 87.3  | 97.1   | -88.4  |
   | 弩     | -81.1 | 21.4   | -181.9 |
   | 长枪   | 1.2   | -92.2  | -89.3  |
   | 法杖   | 67.5  | -107.4 | -91.7  |
   | 单手剑 | 89.9  | 0      | 0      |
   | 双手剑 | 96.1  | 3.9    | 5.2    |

# 如何制作技能和弹幕

​		技能和弹幕都是通过弹幕和触发器配置结合完成，具体可以看模板配置示例，这里主要讲弹幕模型的制作。不要对根节点进行位置，缩放，旋转的更改。

1. 弹幕的模型或粒子效果不应出现在根节点上，新建一个根节点的子节点，重命名为body。将模型和粒子效果挂在body节点上，位置，缩放，旋转的更改应该对body节点进行。
2. 新建一个根节点的子节点，重命名为sfxNode，在该节点下创建子节点collider，这个节点会在弹幕碰撞时播放音效。创建create节点，该节点会在弹幕创建时播放音效。也可以使用唤醒时播放的音效，只要不是以上两个节点名称，这样可以用来播放持续的音效。
3. 在根节点或根节点的子节点上添加BoxCollider组件，这个就是用来检测碰撞的包围盒，调整这个组件的中心和大小，来适配弹幕模型或特效。

# 如何制作地图

​		制作地图相对复杂，想要制作漂亮的地图可能需要你对unity地形工具有所了解。当然也可以进行一个简单的开始。

1. 点击青思游戏-人类保存计划-地图编辑器。
2. 新建地图，输入地图名称testMap，长度和宽度50,50（可以在后面通过修改地形的长宽来更改）。点击创建。
3. SDK会从模板场景创建一个新的场景并打开。
4. CameraNode/GameCamera节点是游戏的主摄像机，可以调整参数以适应你的地图，但是位置和旋转会根据玩家位置实时计算更新，所以更改位置和旋转是无效的。
5. CameraNode/MiniMapCamera节点是游戏的小地图摄像机，可以调整参数以适应你的地图，但是位置和旋转会根据玩家位置实时计算更新，所以更改位置和旋转是无效的。但是位置y轴是不会改变的，所以你应该调整y的高度，以避免小地图摄像机被场景中的高大物体遮挡。
6. MapNode/MapTile节点用于绘制地图格子区域，一般不需要调整，如果绘制地图区域时被场景物体遮挡，可以调整其Y轴位置。
7. MapNode/Walkable节点中包含了所有可行走的物体，如果场景中有物体玩家可以在上面行走（如桥梁，道路等等），请务必放置于此节点中，并将物体的标签更改为terrains。
8. MapNode/Walkable/Terrain节点是地图地形的主要节点，你可以通过地形工具来编辑地形或调整一些地形参数，请将地形标签设置为terrains。
9. MapNode/NotWalkable节点包含了所有的障碍物，玩家不可在上面行走的物体应该放置于此节点中。
10. MapNode/Ignore节点包含了一些忽略物体，即玩家会穿模，不和该物体产生碰撞。
11. SunNode/Directional Light节点是场景中的直射光，可以调整参数以适应你的地图，也可以新增其他光源。对于光照的更改是完全自由的。
12. Sound/BGM节点是地图的背景音乐，进入该地图时自动播放该音乐。
13. Sound/SFX/bird节点是地图的环境音效，如果地图还有其他环境音效请放置在SFX节点中。
14. 点击打开地图，填入地图名称和地图简介，可以填入多语言配置中的文本ID以支持多语言。或者直接填入你想展示的文本。
15. 专属道具ID用于在地图预览界面展示该地图的专属道具。
16. 物体激活范围填入合适的值可以减少产生不必要的物体，毕竟更新展示玩家看不见的物体可能是没有意义的。这可以使游戏运行的更流畅。当然如果地图中某些物体需要的AI需要保持激活状态，也可以将此范围调大，但避免穿件太多物体，游戏可能会卡顿。
17. 同步地形高度功能可以将地形的高度与场景中某个静态模型同步，因为游戏生成物体是依赖二维区域格子地图，生成位置高度会读取地形高度，所以这个功能很实用，比如一个斜坡物体。
18. 点击地图区域，添加一些自定义区域，将当前绘制区域ID切换为玩家，切换到场景界面，点击键盘左alt键进入绘制模式。
19. 点击键盘k键绘制玩家出生点，再在地图编辑器中切换到其他自定义区域，切换到场景中绘制自定义区域。
20. 点击键盘左alt键退出绘制模式。
21. 点击地图编辑器-地图物体，新增要出现在地图中的物体（不包括玩家），刚刚绘制的区域中应该包含该物体配置中的生成区域，否则物体无法生成在地图上。
22. 如果在配置中存在任务，则在地图任务中配置任务的ID。
23. 点击地图编辑器-保存，点击导航图-生成导航图，导航图是物体的可行走区域，点击显示导航图，查看是否和预想的有出入。
24. 进入目录Assets/HSPMapProject/testMap，制作一张地图的预览图片并拖入此目录，将图片纹理类型改变为Sprite，点击应用，删除目录下testMap-Thumbnail.png，并将新拖入的图片重命名为testMap-Thumbnail.png。
25. 点击青思游戏-人类保存计划-配置编辑器，新建配置方案testMap。
26. 点击编辑配置，选择地图展示配置，输入刚才创建的地图名称testMap，点击新增。点击保存。
27. 点击青思游戏-人类保存计划-模组编辑器，新建模组testMap。
28. 点击编辑模组，新增模组元素地图testMap和模组元素配置方案testMap。
29. 点击生成模组，选择导出目录，点击保存，点击导出。
30. 打开游戏，按照简单示例的方法加载该本地模组。
31. 验证地图是否正确显示，是否可以游玩。
