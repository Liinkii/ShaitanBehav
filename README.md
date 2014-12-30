using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using wServer.realm;
using wServer.logic.attack;
using wServer.logic.movement;
using wServer.logic.loot;
using wServer.logic.taunt;
using wServer.logic.cond;

namespace wServer.logic
{
    partial class BehaviorDb
    {
        static _ Shaitan = Behav()
    	        .Init(0x741b, Behaves("md1 Head of Shaitan",
            new RunBehaviors(
                Cooldown.Instance(3000, RingAttack.Instance(8, 0, 0, 0)),
                HpLesserPercent.Instance(0.2f, new SetKey(-1, 4)),
                Once.Instance(new SetKey(-1, 1)),
 IfEqual.Instance(-1, 1,
            new RunBehaviors(
                Cooldown.Instance(15000, (new SimpleTaunt("Let loose the fists of war!"))),
            new QueuedBehavior(
                Cooldown.Instance(100, MultiAttack.Instance(10, 5 * (float)Math.PI / 100, 3, 0, projectileIndex: 0)),
                Cooldown.Instance(110, MultiAttack.Instance(10, 5 * (float)Math.PI / 100, 3, 0, projectileIndex: 1)),
                Cooldown.Instance(120, MultiAttack.Instance(10, 5 * (float)Math.PI / 100, 3, 0, projectileIndex: 1)),
                Cooldown.Instance(130, MultiAttack.Instance(10, 5 * (float)Math.PI / 100, 3, 0, projectileIndex: 1)),
                Cooldown.Instance(140, MultiAttack.Instance(10, 5 * (float)Math.PI / 100, 3, 0, projectileIndex: 1)),
                Cooldown.Instance(600)
                ),


            new QueuedBehavior(
                Cooldown.Instance(3000, (SetConditionEffect.Instance(ConditionEffectIndex.Invulnerable))),
                Cooldown.Instance(5000, (UnsetConditionEffect.Instance(ConditionEffectIndex.Invulnerable)))
                ),


            new QueuedBehavior(
                Cooldown.Instance(15000),
                new SetKey(-1, 2))


                )
            ),
 IfEqual.Instance(-1, 2,
            new RunBehaviors(
            new QueuedBehavior(
                SetConditionEffect.Instance(ConditionEffectIndex.Invulnerable),
                SetAltTexture.Instance(1),
                TossEnemy.Instance(180, 3, 0x741c),
                TossEnemy.Instance(270, 3, 0x741d),
                new SetKey(-1, 3)),
                Cooldown.Instance(10000)


            ))),
            IfEqual.Instance(-1, 3,
            new RunBehaviors(
                If.Instance(
                EntityLesserThan.Instance(20, 1, 0x741d),
                new SetKey(-1, 4))
                )),
 IfEqual.Instance(-1, 4,
            new RunBehaviors(
                Cooldown.Instance(15000, new SimpleTaunt("YOUR ARE BEGINNING TO UPSET ME. ENJOY A FAST DEATH!")),
            new QueuedBehavior(


                SetAltTexture.Instance(0),
                Cooldown.Instance(100, MultiAttack.Instance(10, 5 * (float)Math.PI / 100, 5, 0, projectileIndex: 1)),
                Cooldown.Instance(120, MultiAttack.Instance(10, 5 * (float)Math.PI / 100, 5, 0, projectileIndex: 1)),
                Cooldown.Instance(600)
                ),
            new QueuedBehavior(
                Cooldown.Instance(3000, (SetConditionEffect.Instance(ConditionEffectIndex.Invulnerable))),
                Cooldown.Instance(5000, (UnsetConditionEffect.Instance(ConditionEffectIndex.Invulnerable)))
                ),
            new QueuedBehavior(
                Cooldown.Instance(15000),
                new SetKey(-1, 1)
                    )
                )
                    ),
                condBehaviors: new ConditionalBehavior[] {
                    new OnDeath(
                        new QueuedBehavior(
                    Once.Instance(SpawnMinionImmediate.Instance(0x7431, 1, 1, 1)),
                    Once.Instance(new SimpleTaunt("NOOOOOOOOOOOOOOOOOOOOO!!!"))))
                }
        	                     ))
    	    	                    .Init(0x7431, Behaves("Shaitan Loot",
                    new RunBehaviors(
                        Once.Instance(SetConditionEffect.Instance(ConditionEffectIndex.Invulnerable)),
                        Once.Instance(new SetKey(-1,0)),

                    IfEqual.Instance(-1,0,
                     new QueuedBehavior(
                         CooldownExact.Instance(2500),
                         UnsetConditionEffect.Instance(ConditionEffectIndex.Invulnerable),
                         new SetKey(-1,1)
                        ))
                         ),
                        loot: new LootBehavior(LootDef.Empty,
Tuple.Create(100, new LootDef(0, 3, 1, 4,
                        Tuple.Create(0.01, (ILoot)new ItemLoot("Skull of Endless Torment")),
                        Tuple.Create(0.05, (ILoot)new TierLoot(11, ItemType.Weapon)),
                        Tuple.Create(0.10, (ILoot)new ItemLoot("Large Flame Cloth")),
                        Tuple.Create(0.10, (ILoot)new ItemLoot("Small Flame Cloth")),
                        Tuple.Create(0.10, (ILoot)new ItemLoot("Large Heavy Chainmail Cloth")),
                        Tuple.Create(0.10, (ILoot)new ItemLoot("Small Heavy Chainmail Cloth")),
                        Tuple.Create(0.15, (ILoot)new TierLoot(10, ItemType.Armor)),
                        Tuple.Create(0.15, (ILoot)new TierLoot(5, ItemType.Ability)),
                        Tuple.Create(0.15, (ILoot)new TierLoot(10, ItemType.Weapon)),
                        Tuple.Create(0.20, (ILoot)new ItemLoot("Effusion of Defense")),
                        Tuple.Create(0.20, (ILoot)new ItemLoot("Tincture of Dexterity")),
                        Tuple.Create(0.99, (ILoot)new ItemLoot("Potion of Attack"))
                            ))
                        )
                    )



                              


                   )
          .Init(0x741c, Behaves("Shaitan Hand",
             new RunBehaviors(
               Chasing.Instance(3, 40, 2, null),
               Cooldown.Instance(900, MultiAttack.Instance(20, 20 * (float)Math.PI / 360, 3, 0, projectileIndex: 0))
             )
        	                     ))
          .Init(0x741d, Behaves("Shaitan Hand 2",
             new RunBehaviors(
               Chasing.Instance(3, 40, 2, null),
               Cooldown.Instance(900, MultiAttack.Instance(20, 20 * (float)Math.PI / 360, 3, 0, projectileIndex: 0))
             )
        	                     ));
        	
    }}
        	                      	
        	                      

                                 	
