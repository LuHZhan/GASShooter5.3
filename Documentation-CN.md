# GASShooter

## 简介

GASShooter 是一个针对 Unreal Engine 5 的 **GameplayAbilitySystem (GAS)** 插件的高级 FPS/TPS 示例项目。它是 [GASDocumentation](https://github.com/tranek/GASDocumentation) 的姊妹项目，关于此处演示的技术将在该 README 中详细讨论。

这不是生产就绪代码，而是一个用于评估与武器相关的 GAS 技术的起点。特别是 TargetActors（具有持久性击中结果）和 ReticleActors（准星）在 `Tick()` 中有大量代码。

此项目中的资源来自 Epic Games 的 **ShooterGame** 学习项目、Epic Games 的 **Infinity Blade** 资产，或者是我自己制作的。

| 快捷键   | 操作                         |
| -------- | ---------------------------- |
| T        | 切换第一人称和第三人称视角。 |
| 左键     | 激活武器的主能力，确认目标。 |
| 中键     | 激活武器的替代能力。         |
| 右键     | 激活武器的次要能力。         |
| 滚轮向上 | 切换到下一个武器。           |
| 滚轮向下 | 切换到上一个武器。           |
| R        | 重新加载武器。               |
| 左Ctrl   | 取消目标锁定。               |
| 左Shift  | 冲刺。                       |
| E        | 与可交互物体互动。           |

| 控制台命令 | 操作           |
| ---------- | -------------- |
| `kill`     | 杀死本地玩家。 |

英雄角色有魔法值（mana），但目前没有任何能力使用它。这个项目的初衷始于 **新 BioShock** 的发布，目的是实现类似 BioShock 的可升级能力系统。由于范围过大，最终放弃了，但将来可能会重新考虑。

副武器弹药未使用。它可以用于类似于步枪榴弹的功能。

## 涉及的概念

- [能力批处理](https://github.com/tranek/GASDocumentation#concepts-ga-batching)
- 可装备武器，授予能力
- 预测武器切换
- [武器弹药](https://github.com/tranek/GASDocumentation#concepts-as-design-itemattributes)
- 简单的武器库存
- 额外的爆头伤害
- [可重用的自定义 TargetActors](https://github.com/tranek/GASDocumentation#concepts-targeting-actors)
- [GameplayAbilityWorldReticles](https://github.com/tranek/GASDocumentation#concepts-targeting-reticles)
- 在多个属于 AvatarActor 的骨架网格组件上播放复制的动画蒙太奇
- [子类化 `FGameplayEffectContext`](https://github.com/tranek/GASDocumentation#concepts-ge-context) 以将附加信息发送到 GameplayCues
- 角色护盾，在健康值被伤害移除之前先消耗护盾
- 物品拾取
- 单按钮交互系统。按下或按住 `E` 键与可交互物体互动，包括玩家复活、武器箱和滑动门。

该项目未展示预测抛射物。对于如何使用假抛射物在拥有客户端上进行预测，可以参考 Unreal Tournament 的源代码。

| 武器       | 主能力（左键）                     | 次要能力（右键）                                             | 替代能力（中键）               |
| ---------- | ---------------------------------- | ------------------------------------------------------------ | ------------------------------ |
| 步枪       | 根据当前射击模式发射命中射击子弹。 | 瞄准下视，减少射击散布。                                     | 切换全自动、半自动和点射模式。 |
| 火箭发射器 | 发射火箭。                         | 瞄准下视，启动锁定目标，发射导弹。按左键发射锁定目标的导弹。 | 无                             |
| 霰弹枪     | 根据当前射击模式发射命中散弹。     | 瞄准下视，减少霰弹散布。                                     | 切换半自动和全自动模式。       |

## 致谢

[KaosSpectrum](https://github.com/KaosSpectrum) 在理解能力批处理系统如何工作以及提供一般性反馈方面做出了重要贡献。请查看他的游戏开发 [博客](https://www.thegames.dev/)。