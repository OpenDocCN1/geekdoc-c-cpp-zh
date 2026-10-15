# Listing 4.1 Combatant.cs (Showing Events)

```
using System;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Ink;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;

namespace WindowsPhoneApplication1
{
    public delegate void DidGetKilledDelegate(
        Combatant killer, Combatant target);

    public delegate void DidHitTargetDelegate(
        Combatant attacker, Combatant target, int hitPoints);

    public class Combatant
    {
        public event DidGetKilledDelegate OnGotKilled;
        public event DidHitTargetDelegate OnHitCombatant;
        public event DidHitTargetDelegate OnHitByCombatant;

        public int HitPoints { get; set; }
        public string Name { get; set; }

        public void Attack(Combatant target)
        {
            // obviously this would be algorithm-based in a real game
            bool didHit = true;
            int hitPoints = 42;

            if (didHit)
            {
                NotifyHitCombatant(target, hitPoints);
            }
        }

        public void TakeDamage(Combatant attacker, int hitPoints)
        {
            this.HitPoints -= hitPoints;
            NotifyHitByCombatant(attacker, hitPoints);
            if (this.HitPoints <= 0)
```