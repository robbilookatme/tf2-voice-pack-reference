# Criteria Reference

This file is a reference document for all the different types of criteria that a rule may have in Team Fortress 2. When certain actions are performed, the game checks the list of dialogue rules to see if any apply to the current game state. If so, that rule fires a response, causing characters to comment on the situation.

There are (informally) three types of criteria: concepts, game state criteria, and context criteria.

Concepts are criteria that are the events that cause dialogue. For example, when firing a weapon, the game will trigger rules with the ConceptFireWeapon criteria. The first criteria of every rule will be a concept, and there can only be one concept per rule.

Game state criteria keep track of information such as what is the player's current class, is the player currently being healed, and how many kills the player has achieved in the past 30 seconds. Note that in engine code, it is not only required that every rule has a concept, but also every rule has to have a criteria that checks for which class is being played.

Contexts are information states that are only relevant to the dialogue system, and are the only parts of the game state that can be affected by the dialogue system. In Team Fortress 2, contexts are primarily used to prevent repetitive dialogue. Contexts can be set from within rules, and context criteria are criteria that check the state of contexts. For example, it would get repetitive if every time the player fired a gun as Scout, the Scout said "take this, bozos!". Instead, the rule for firing could set the context "ScoutCalledEnemiesBozos" to 1 for 30 seconds, and then the rule could have an additional criteria "HasScoutNotCalledEnemiesBozos", which checks for if the context ScoutCalledEnemiesBozos is set to 0. This way, the Scout will only say such a scathing insult every thirty seconds.

Criteria can theoretically be marked as not required, but every criteria used in TF2 is marked required, meaning rules must meet every criteria in order to play their corresponding response.

Last note about criteria is about weight. Every criteria has a weight, defaulting to 1. When rules are checked, they are given a weight equal to the sum of the weights of their matched criteria. When multiple rules are found to match a circumstance, the rule with the most weight is chosen. If multiple rules tie for the most weight, one is chosen at random. Context criteria are usually given a weight of 0.

In the following list, I explain every criteria and when they are resolved as matched. If a criteria is labeled "unused", it means the criteria works correctly but no rules use it and as such no voice lines will play when that criteria fires (unless the server is running custom rule-response files). If a criteria is labeled "never called", it means that the criteria will never match due to not being set in code. This means that it is not possible to write new rules using this criteria without running a modified game executable.

## Concepts

### Voice Command Concepts

<dl>
  <dt>ConceptPlayerMedic</dt>
  <dd>Fires when player uses "Medic!" voice command</dd>
  <dt>ConceptPlayerThanks</dt>
  <dd>Fires when player uses "Thanks!" voice command</dd>
  <dt>ConceptPlayerGo</dt>
  <dd>Fires when player uses "Go Go Go!" voice command</dd>
  <dt>ConceptPlayerMoveUp</dt>
  <dd>Fires when player uses "Move Up!" voice command</dd>
  <dt>ConceptPlayerLeft</dt>
  <dd>Fires when player uses "Go Left!" voice command</dd>
  <dt>ConceptPlayerRight</dt>
  <dd>Fires when player uses "Go Right!" voice command</dd>
  <dt>ConceptPlayerYes</dt>
  <dd>Fires when player uses "Yes" voice command</dd>
  <dt>ConceptPlayerNo</dt>
  <dd>Fires when player uses "No" voice command</dd>
  <dt>ConceptPlayerIncoming</dt>
  <dd>Fires when player uses "Incoming" voice command</dd>
  <dt>ConceptPlayerCloakedSpy</dt>
  <dd>Fires when player uses "Spy!" voice command</dd>
  <dt>ConceptPlayerSentryAhead</dt>
  <dd>Fires when player uses "Sentry Ahead!" voice command</dd>
  <dt>ConceptPlayerTeleporterHere</dt>
  <dd>Fires when player uses "Teleporter Here" voice command</dd>
  <dt>ConceptPlayerDispenserHere</dt>
  <dd>Fires when player uses "Dispenser Here" voice command</dd>
  <dt>ConceptPlayerSentryHere</dt>
  <dd>Fires when player uses "Sentry Here" voice command</dd>
  <dt>ConceptPlayerActivateCharge</dt>
  <dd>Fires when player uses "Activate UberCharge!" voice command</dd>
  <dt>ConceptPlayerChargeReady</dt>
  <dd>Fires when player uses "MEDIC: UberCharge Ready!" voice command</dd>
  <dt>ConceptPlayerHelp</dt>
  <dd>Fires when player uses "Help!" voice command</dd>
  <dt>ConceptPlayerBattleCry</dt>
  <dd>Fires when player uses "Battle Cry" voice command</dd>
  <dt>ConceptPlayerCheers</dt>
  <dd>Fires when player uses "Cheers" voice command</dd>
  <dt>ConceptPlayerJeers</dt>
  <dd>Fires when player uses "Jeers" voice command</dd>
  <dt>ConceptPlayerPositive</dt>
  <dd>Fires when player uses "Positive" voice command</dd>
  <dt>ConceptPlayerNegative</dt>
  <dd>Fires when player uses "Negative" voice command</dd>
  <dt>ConceptPlayerNiceShot</dt>
  <dd>Fires when player uses "Nice Shot" voice command</dd>
  <dt>ConceptPlayerGoodJob</dt>
  <dd>Fires when player uses "Good Job" voice command</dd>
  <dt>ConceptPlayerAskForBall</dt>
  <dd>Fires when player uses "Pass to me!" voice command</dd>
</dl>

### Game State Concepts

<dl>
  <dt>ConceptPlayerRoundStart</dt>
  <dd>Fires at round start</dd>
  <dt>ConceptPlayerGrabbedIntelligence</dt>
  <dd>Fires when player picks up briefcase (intelligence, australium briefcase)</dd>
  <dt>ConceptPlayerCapturedIntelligence</dt>
  <dd>Fires when player captures a briefcase</dd>
  <dt>ConceptPlayerCapturedPoint</dt>
  <dd>Fires when player captures a point</dd>
  <dt>ConceptPlayerLostPoint</dt>
  <dd>Unused-ish, fires when enemy captures a point owned by player's team, doesn't trigger responses due to a typo in response_rules.txt</dd>
  <dt>ConceptCapBlocked</dt>
  <dd>Fires when player kills an enemy capturing a player-owned point, or stops the payload cart when on defense</dd>
  <dt>ConceptCartMovingForward</dt>
  <dd>Fires when payload cart starts moving</dd>
  <dt>ConceptCartMovingStopped</dt>
  <dd>Fires when payload cart stops moving</dd>
  <dt>ConceptCartMovingBackward</dt>
  <dd>Fires when payload cart starts rolling back</dd>
  <dt>ConceptPlayerStalemate</dt>
  <dd>Fires when game ends in a stalemate</dd>
  <dt>ConceptPlayerSuddenDeathStart</dt>
  <dd>Fires when sudden death starts</dd>
</dl>

### Competitive Mode Concepts

<dl>
  <dt>ConceptPlayerRoundStartComp</dt>
  <dd>Fires at round start in competitive mode</dd>
  <dt>ConceptPlayerGameOverComp</dt>
  <dd>Fires when game ends in competitive mode</dd>
  <dt>ConceptPlayerMatchOverComp</dt>
  <dd>Fires when match ends in competitive mode</dd>
</dl>

### Player Concepts

<dl>
  <dt>ConceptAchievementAward</dt>
  <dd>Fires when player gets an achievement</dd>
  <dt>ConceptFireWeapon</dt>
  <dd>Fires when player fires a weapon</dd>
  <dt>ConceptKilledPlayer</dt>
  <dd>Fires when player has killed another player</dd>
  <dt>ConceptPain</dt>
  <dd>Fires when player takes damage</dd>
  <dt>ConceptAttackerPain</dt>
  <dd>Fires when player takes damage, but only to the attacker; is used to play different, louder pain sounds to attacker</dd>
  <dt>ConceptFire</dt>
  <dd>Fires when player is on fire</dd>
  <dt>ConceptJarateHit</dt>
  <dd>Fires when player is hit by a jar weapon (Jarate, Mad Milk, Gas Passer)</dd>
  <dt>ConceptTeleported</dt>
  <dd>Fires when a player uses a teleporter</dd>
  <dt>ConceptKilledObject</dt>
  <dd>Fires when a player destroys an enemy building</dd>
  <dt>ConceptPlayerExpression</dt>
  <dd>Fires every time the player's expression updates, usually used with contexts to play lines every few seconds in certain circumstances</dd>
  <dt>ConceptComboKilled</dt>
  <dd>Never called, attached to non-functional code related to breaking a combo (killing the same class several times in a row)</dd>
  <dt>ConceptPlayerDead</dt>
  <dd>Never called</dd>
  <dt>ConceptPlayerBuildingObject</dt>
  <dd>Fires when player begins constructing a building</dd>
  <dt>ConceptPlayerDetonatedObject</dt>
  <dd>Unused in rules, fires when player detonates own building</dd>
  <dt>ConceptEngineerPickupBuilding</dt>
  <dd>Fires when player picks up a building</dd>
  <dt>ConceptEngineerCarryingBuilding</dt>
  <dd>Fires between 6 and 12 seconds after player picks up a building</dd>
  <dt>ConceptEngineerDeployBuilding</dt>
  <dd>Fires when player deploys a carried building</dd>
  <dt>ConceptSpySapping</dt>
  <dd>Fires when a player-built building is sapped</dd>
  <dt>ConceptLostObject</dt>
  <dd>Fires when a player-built building is destroyed</dd>
  <dt>ConceptAteFood</dt>
  <dd>Fires after eating one of Heavy's lunchbox items</dd>
  <dt>ConceptRocketDestroyed</dt>
  <dd>Fires when destroying a projectile with the Destroy Projectiles MvM upgrade</dd>
</dl>

### Medic-Specific Concepts

<dl>
  <dt>ConceptMedicChargeReady</dt>
  <dd>Fires when player's medigun charge meter is filled</dd>
  <dt>ConceptMedicChargeDeployed</dt>
  <dd>Fires when player activates a medigun charge</dd>
  <dt>ConceptMedicChargeStopped</dt>
  <dd>Fires when friendly medic stops healing player</dd>
</dl>

### Pyro-Specific Concepts

<dl>
  <dt>ConceptDeflected</dt>
  <dd>Unused in rules, fires when a player or their projectile is airblasted, OR when a player airblasts another player or projectile</dd>
</dl>

### Scout-Specific Concepts

<dl>
  <dt>ConceptDoubleJump</dt>
  <dd>Fires when player double jumps</dd>
  <dt>ConceptDodging</dt>
  <dd>Fires when player's Bonk invulnerability starts or ends</dd>
  <dt>ConceptDodgeShot</dt>
  <dd>Fires when player is shot while under effects of Bonk</dd>
  <dt>ConceptTired</dt>
  <dd>Fires when player's drink effect wears off (Bonk or Crit-a-Cola)</dd>
  <dt>ConceptGrabBall</dt>
  <dd>Fires when player picks up Sandman ball</dd>
  <dt>ConceptScoutBallGrab</dt>
  <dd>Alias of ConceptGrabBall</dd>
  <dt>ConceptStunnedTarget</dt>
  <dd>Fires when player stuns an enemy</dd>
  <dt>ConceptRegenBall</dt>
  <dd>Never called</dd>
  <dt>ConceptBatBall</dt>
  <dd>Unused in rules, fires when player launches a ball from a bat weapon</dd>
  <dt>ConceptBallMissed</dt>
  <dd>Unused in rules, fires when The Sandman's ball hits objects or world geometry instead of a player</dd>
  <dt>ConceptStunned</dt>
  <dd>Unused in rules, fires when player is stunned or partially stunned</dd>
</dl>

### Sniper-Specific Concepts

<dl>
  <dt>ConceptJarateLaunch</dt>
  <dd>Fires when player throws a jar weapon</dd>
  <dt>ConceptRequestDuel</dt>
  <dd>Fires when a player sends a duel to another player</dd>
  <dt>ConceptDuelAccepted</dt>
  <dd>Unused in rules, fires when a player's duel is accepted by the other player</dd>
  <dt>ConceptDuelRejected</dt>
  <dd>Fires when a player's duel is rejected by the other player</dd>
  <dt>ConceptIAcceptDuel</dt>
  <dd>Fires when a player accepts another player's duel</dd>
  <dt>ConceptFireMinigun</dt>
  <dd>Fires when player fires a minigun</dd>
  <dt>ConceptFireMinigunTalk</dt>
  <dd>Fires every 5 seconds while firing a minigun</dd>
  <dt>ConceptWindMinigun</dt>
  <dd>Fires when player starts winding up minigun</dd>
</dl>

### Mann vs. Machine Concepts

<dl>
  <dt>ConceptMvMFirstBombPickup</dt>
  <dd>Fires when a normal robot picks up the bomb from its home in MvM</dd>
  <dt>ConceptMvMBombPickup</dt>
  <dd>Fires when a normal robot picks up the bomb from dropped state in MvM</dd>
  <dt>ConceptMvMBombCarrierUpgrade1</dt>
  <dd>Fires when the MvM bomb carrier is upgraded for the first time</dd>
  <dt>ConceptMvMBombCarrierUpgrade2</dt>
  <dd>Fires when the MvM bomb carrier is upgraded for the second time</dd>
  <dt>ConceptMvMBombCarrierUpgrade3</dt>
  <dd>Fires when the MvM bomb carrier is upgraded for the third time</dd>
  <dt>ConceptMvMBombDropped</dt>
  <dd>Fires when the MvM bomb is dropped</dd>
  <dt>ConceptMvMSniperCallout</dt>
  <dd>Fires when the first Sniper bot is spawned in a wave in MvM</dd>
  <dt>ConceptMvMGiantCallout</dt>
  <dd>Fires when a giant robot is spawned in MvM</dd>
  <dt>ConceptMvMGiantHasBomb</dt>
  <dd>Fires when a giant robot picks up the bomb in MvM</dd>
  <dt>ConceptMvMGiantKilledTeammate</dt>
  <dd>Fires when a giant robot kills a teammate in MvM</dd>
  <dt>ConceptMvMGiantKilled</dt>
  <dd>Fires when a giant robot is killed in MvM</dd>
  <dt>ConceptMvMSentryBuster</dt>
  <dd>Fires when a Sentry Buster is spawned in MvM</dd>
  <dt>ConceptMvMSentryBusterDown</dt>
  <dd>Fires when a Sentry Buster dies or explodes without destroying a sentry in MvM</dd>
  <dt>ConceptMvMTankCallout</dt>
  <dd>Fires when a Tank spawns in MvM</dd>
  <dt>ConceptMvMTankDeploying</dt>
  <dd>Fires when a Tank begins deploying a bomb in MvM</dd>
  <dt>ConceptMvMTankDead</dt>
  <dd>Fires when a Tank is killed in MvM</dd>
  <dt>ConceptMannhattanGateAttack</dt>
  <dd>Fires when a bot starts opening the gate in Mannhattan in MvM</dd>
  <dt>ConceptMannhattanGateTake</dt>
  <dd>Fires when the bots have opened the gate in Mannhattan in MvM</dd>
  <dt>ConceptMvMMedicShield</dt>
  <dd>Fires when player activates the Projectile Shield as Medic in MvM</dd>
  <dt>ConceptMvMResurrected</dt>
  <dd>Fires when player is resurrected by a Medic in MvM</dd>
  <dt>ConceptMvMDefenderDied</dt>
  <dd>Fires when another player dies in MvM</dd>
  <dt>ConceptMvMLastManStanding</dt>
  <dd>Fires when player is the last player alive in MvM</dd>
  <dt>ConceptMvMMoneyPickup</dt>
  <dd>Fires when player picks up money in MvM</dd>
  <dt>ConceptMvMUpgradeComplete</dt>
  <dd>Fires after closing the upgrade menu after buying an upgrade in MvM</dd>
  <dt>ConceptMvMLootCommon</dt>
  <dd>Fires after player receives common loot in MvM</dd>
  <dt>ConceptMvMLootRare</dt>
  <dd>Fires after player receives rare loot in MvM</dd>
  <dt>ConceptMvMLootUltraRare</dt>
  <dd>Fires after player receives ultra-rare lot in MvM</dd>
  <dt>ConceptMvMTaunt</dt>
  <dd>Never called</dd>
  <dt>ConceptMvMWaveStart</dt>
  <dd>Never called</dd>
  <dt>ConceptMvMWaveWin</dt>
  <dd>Never called</dd>
  <dt>ConceptMvMWaveLose</dt>
  <dd>Never called</dd>
  <dt>ConceptMvMEncourageUpgrade</dt>
  <dd>Never called</dd>
  <dt>ConceptMvMEncourageMoney</dt>
  <dd>Never called</dd>
  <dt>ConceptMvMCloseCall</dt>
  <dd>Never called</dd>
  <dt>ConceptMvMSappedRobot</dt>
  <dd>Never called</dd>
  <dt>ConceptMvMDeployRage</dt>
  <dd>Never called</dd>
  <dt>ConceptMvMAttackTheTank</dt>
  <dd>Never called</dd>
</dl>

### Taunt Concepts

<dl>
  <dt>ConceptPlayerTaunt</dt>
  <dd>Fires when player taunts</dd>
  <dt>ConceptTauntEurekaTeleport</dt>
  <dd>Fires when player taunts with the Eureka Effect</dd>
  <dt>ConceptTauntLaugh</dt>
  <dd>Fires when player is hit by a weapon that causes laughter (Holiday Punch)</dd>
  <dt>ConceptPlayerShowItemTaunt</dt>
  <dd>Unused in rules, triggers unused "tada" taunt when game is built in debug mode</dd>
  <dt>ConceptPlayerTaunt2</dt>
  <dd>Never called</dd>
  <dt>ConceptPlayerTaunts</dt>
  <dd>Unused in rules, fires when ball is intercepted in PASS Time</dd>
  <dt>ConceptTauntGuitarRiff</dt>
  <dd>Never called, this and the next four taunt concepts possibly were used before Love & War Update, which added the taunt menu</dd>
  <dt>ConceptTauntHeroicPose</dt>
  <dd>Never called</dd>
  <dt>ConceptTauntPyroArmageddon</dt>
  <dd>Never called</dd>
  <dt>ConceptTauntReplay</dt>
  <dd>Never called</dd>
  <dt>ConceptPlayerHoldTaunt</dt>
  <dd>Never called</dd>
</dl>

### Halloween Map Concepts

<dl>
  <dt>ConceptHalloweenPlayerPitFall</dt>
  <dd>Unused in code, triggered by maps (used in long fall pits)</dd>
  <dt>ConceptMagicGood</dt>
  <dd>Fires when player receives the Critical Hits fortune in Ghost Fort</dd>
  <dt>ConceptMagicBigHead</dt>
  <dd>Fires when player receives the Big Head fortune in Ghost Fort</dd>
  <dt>ConceptMagicSmallHead</dt>
  <dd>Fires when player receives the Small Head fortune in Ghost Fort</dd>
  <dt>ConceptMagicDance</dt>
  <dd>Fires when player receives the Dance Off fortune in Ghost Fort</dd>
  <dt>ConceptMagicGravity</dt>
  <dd>Fires when player receives the Zero Gravity fortune in Ghost Fort</dd>
  <dt>ConceptPlayerHelltowerMidnight</dt>
  <dd>Fires when the clock tower hits midnight in Helltower</dd>
  <dt>ConceptPlayerSkeletonKingAppear</dt>
  <dd>Fires when the Skeleton King appears in Helltower</dd>
  <dt>ConceptPlayerSpellPickupCommon</dt>
  <dd>Fires when picking up a common spell on Halloween maps</dd>
  <dt>ConceptPlayerSpellPickupRare</dt>
  <dd>Fires when picking up a rare spell on Halloween maps</dd>
</dl>

### Halloween Spell Concepts - Casting

<dl>
  <dt>ConceptPlayerCastBombHeadCurse</dt>
  <dd>Fires when casting a Fireball spell on Halloween maps</dd>
  <dt>ConceptPlayerCastBlastJump</dt>
  <dd>Fires when casting a Blast Jump or Bumper Car B.A.S.E. Jump spell on Halloween maps</dd>
  <dt>ConceptPlayerCastSelfHeal</dt>
  <dd>Fires when casting a Overheal or Bumper Car Uber Heal spell on Halloween maps</dd>
  <dt>ConceptPlayerCastMerasmusZap</dt>
  <dd>Fires when casting a Swarm of Bats or Bumper Car Boxing Rocket on Halloween maps</dd>
  <dt>ConceptPlayerCastMirv</dt>
  <dd>Fires when casting a Pumpkin MIRV spell on Halloween maps</dd>
  <dt>ConceptPlayerCastStealth</dt>
  <dd>Fires when casting a Stealth spell on Halloween maps</dd>
  <dt>ConceptPlayerCastTeleport</dt>
  <dd>Fires when casting a Shadow Leap spell on Halloween maps</dd>
  <dt>ConceptPlayerCastMonoculous</dt>
  <dd>Fires when casting a MONOCULUS spell on Halloween maps</dd>
  <dt>ConceptPlayerCastSkeletonHorde</dt>
  <dd>Fires when casting a Skeleton Horde spell on Halloween maps</dd>
  <dt>ConceptPlayerCastLightningBall</dt>
  <dd>Fires when casting a Ball O' Lightning spell on Halloween maps</dd>
  <dt>ConceptPlayerCastMeteorSwarm</dt>
  <dd>Fires when casting a Meteor Shower spell on Halloween maps</dd>
  <dt>ConceptPlayerCastMovementBuff</dt>
  <dd>Fires when casting a Power Up spell on Halloween maps</dd>
  <dt>ConceptPlayerCastFireball</dt>
  <dd>Fires when casting a Bumper Car Bombonomicon Head spell on Halloween maps</dd>
</dl>

### Halloween Spell Concepts - Witnessing

<dl>
  <dt>ConceptPlayerSpellBlastJump</dt>
  <dd>Unused in rules, fires when seeing an enemy Blast Jump or Bumper Car B.A.S.E. Jump spell on Halloween maps</dd>
  <dt>ConceptPlayerSpellSelfHeal</dt>
  <dd>Unused in rules, fires when seeing an enemy Overheal or Bumper Car Uber Heal spell on Halloween maps</dd>
  <dt>ConceptPlayerSpellMerasmusZap</dt>
  <dd>Unused in rules, fires when seeing an enemy Swarm of Bats on Halloween maps (due to spell objects reusing code, also fires for Pumpkin MIRV, Shadow Leap, MONOCULUS, and Skeleton Horde spells)</dd>
  <dt>ConceptPlayerSpellMirv</dt>
  <dd>Unused in rules, fires when seeing a Pumpkin MIRV spell on Halloween maps (and also fires for every pumpkin created by the spell)</dd>
  <dt>ConceptPlayerSpellStealth</dt>
  <dd>Unused in rules, fires when seeing an enemy Stealth spell on Halloween maps</dd>
  <dt>ConceptPlayerSpellTeleport</dt>
  <dd>Unused in rules, fires when seeing an enemy Shadow Leap spell on Halloween maps</dd>
  <dt>ConceptPlayerSpellMonoculous</dt>
  <dd>Unused in rules, fires when seeing an enemy MONOCULUS spell on Halloween maps</dd>
  <dt>ConceptPlayerSpellSkeletonHorde</dt>
  <dd>Fires when seeing an enemy Skeleton Horde spell on Halloween maps</dd>
  <dt>ConceptPlayerSpellLightningBall</dt>
  <dd>Unused in rules, fires when an enemy Ball O' Lightning spell deals damage to anyone on Halloween maps</dd>
  <dt>ConceptPlayerSpellMeteorSwarm</dt>
  <dd>Never called, bugged (supposed to fire when seeing an enemy Meteor Shower spell on Halloween maps)</dd>
  <dt>ConceptPlayerSpellMovementBuff</dt>
  <dd>Fires when seeing an enemy Power Up spell on Halloween maps</dd>
  <dt>ConceptPlayerSpellFireball</dt>
  <dd>Unused in rules, fires when seeing an enemy Fireball or Bumper Car Bombonomicon Head spell on Halloween maps (due to spell objects reusing code, also fires for every meteor created by Meteor Swarm spell)</dd>
</dl>

The only spell not accounted for is the Bumper Car Boxing Rocket spell, which is tied in game data to ConceptPlayerSpellMerasmusZap, but no concept is ever called in the spell's code.

## Criteria

### Random Chance Criteria

Note that the engine rolls 0 to 100 inclusive, meaning there are 101 possibilities. Also, the 2 and 5 percent chance rules use a different comparator to the others, meaning they have different odds than the names suggest.

<dl>
  <dt>2PercentChance</dt>
  <dd>3 out of 101 chance of passing, approx 3%</dd>
  <dt>5PercentChance</dt>
  <dd>6 out of 101 chance of passing, approx 5.9% chance</dd>
  <dt>10PercentChance</dt>
  <dd>10 out of 101 chance of passing, approx 9.9% chance</dd>
  <dt>20PercentChance</dt>
  <dd>20 out of 101 chance of passing, approx 19.8% chance</dd>
  <dt>30PercentChance</dt>
  <dd>30 out of 101 chance of passing, approx 29.7% chance</dd>
  <dt>40PercentChance</dt>
  <dd>40 out of 101 chance of passing, approx 39.6% chance</dd>
  <dt>50PercentChance</dt>
  <dd>50 out of 101 chance of passing, approx 49.5% chance</dd>
  <dt>75PercentChance</dt>
  <dd>75 out of 101 chance of passing, approx 74.3% chance</dd>
  <dt>100PercentChance</dt>
  <dd>100 out of 101 chance of passing, approx 99% chance, has extra weight so rules with this criteria will fire above other rules</dd>
</dl>

### Game State Criteria

<dl>
  <dt>IsRedTeam</dt>
  <dd>Unused in rules, passes if player is on RED</dd>
  <dt>IsBlueTeam</dt>
  <dd>Unused in rules, passes if player is on BLU</dd>
  <dt>IsOnOffense</dt>
  <dd>Passes if player is on offense</dd>
  <dt>IsOnDefense</dt>
  <dd>Passes if player is on defense</dd>
  <dt>GameRulesInWinState</dt>
  <dd>Passes if one of the teams has won the game</dd>
</dl>

### Player Class Criteria

<dl>
  <dt>IsDemoman</dt>
  <dd>Passes if player is a Demoman</dd>
  <dt>IsEngineer</dt>
  <dd>Passes if player is an Engineer</dd>
  <dt>IsHeavy</dt>
  <dd>Passes if player is a Heavy</dd>
  <dt>IsMedic</dt>
  <dd>Passes if player is a Medic</dd>
  <dt>IsPyro</dt>
  <dd>Passes if player is a Pyro</dd>
  <dt>IsScout</dt>
  <dd>Passes if player is a Scout</dd>
  <dt>IsSniper</dt>
  <dd>Passes if player is a Sniper</dd>
  <dt>IsSoldier</dt>
  <dd>Passes if player is a Soldier</dd>
  <dt>IsSpy</dt>
  <dd>Passes if player is a Spy</dd>
  <dt>IsNotDemoman</dt>
  <dd>Unused in rules, passes if player is not a Demoman</dd>
  <dt>IsNotHeavy</dt>
  <dd>Unused in rules, passes if player is not a Heavy</dd>
  <dt>IsNotMedic</dt>
  <dd>Unused in rules, passes if player is not a Medic</dd>
  <dt>IsNotPyro</dt>
  <dd>Unused in rules, passes if player is not a Pyro</dd>
  <dt>IsNotScout</dt>
  <dd>Unused in rules, passes if player is not a Scout</dd>
  <dt>IsNotSniper</dt>
  <dd>Unused in rules, passes if player is not a Sniper</dd>
  <dt>IsNotSoldier</dt>
  <dd>Unused in rules, passes if player is not a Soldier</dd>
  <dt>IsNotSpy</dt>
  <dd>Unused in rules, passes if player is not a Spy</dd>
  <dt>IsNotEngineer</dt>
  <dd>Passes if player is not an Engineer</dd>
</dl>

### Class Kill Criteria

<dl>
  <dt>IsVictimDemoman</dt>
  <dd>Passes if player has just killed a Demoman</dd>
  <dt>IsVictimEngineer</dt>
  <dd>Passes if player has just killed an Engineer</dd>
  <dt>IsVictimHeavy</dt>
  <dd>Passes if player has just killed a Heavy</dd>
  <dt>IsVictimMedic</dt>
  <dd>Passes if player has just killed a Medic</dd>
  <dt>IsVictimPyro</dt>
  <dd>Passes if player has just killed a Pyro</dd>
  <dt>IsVictimScout</dt>
  <dd>Passes if player has just killed a Scout</dd>
  <dt>IsVictimSniper</dt>
  <dd>Passes if player has just killed a Sniper</dd>
  <dt>IsVictimSoldier</dt>
  <dd>Passes if player has just killed a Soldier</dd>
  <dt>IsVictimSpy</dt>
  <dd>Passes if player has just killed a Spy</dd>
  <dt>IsNotVictimDemoman</dt>
  <dd>Passes if player just killed someone who is not a Demoman</dd>
  <dt>IsNotVictimEngineer</dt>
  <dd>Unused in rules, passes if player just killed someone who is not an Engineer</dd>
  <dt>IsNotVictimHeavy</dt>
  <dd>Unused in rules, passes if player just killed someone who is not a Heavy</dd>
  <dt>IsNotVictimMedic</dt>
  <dd>Unused in rules, passes if player just killed someone who is not a Medic</dd>
  <dt>IsNotVictimPyro</dt>
  <dd>Unused in rules, passes if player just killed someone who is not a Pyro</dd>
  <dt>IsNotVictimScout</dt>
  <dd>Unused in rules, passes if player just killed someone who is not a Scout</dd>
  <dt>IsNotVictimSniper</dt>
  <dd>Unused in rules, passes if player just killed someone who is not a Sniper</dd>
  <dt>IsNotVictimSoldier</dt>
  <dd>Unused in rules, passes if player just killed someone who is not a Soldier</dd>
  <dt>IsNotVictimSpy</dt>
  <dd>Unused in rules, passes if player just killed someone who is not a Spy</dd>
</dl>

### Duel Target Criteria

<dl>
  <dt>DuelTargetIsDemoman</dt>
  <dd>Unused in rules, passes if player requested a duel with a Demoman</dd>
  <dt>DuelTargetIsEngineer</dt>
  <dd>Unused in rules, passes if player requested a duel with an Engineer</dd>
  <dt>DuelTargetIsHeavy</dt>
  <dd>Unused in rules, passes if player requested a duel with a Heavy</dd>
  <dt>DuelTargetIsMedic</dt>
  <dd>Unused in rules, passes if player requested a duel with a Medic</dd>
  <dt>DuelTargetIsPyro</dt>
  <dd>Unused in rules, passes if player requested a duel with a Pyro</dd>
  <dt>DuelTargetIsScout</dt>
  <dd>Unused in rules, passes if player requested a duel with a Scout</dd>
  <dt>DuelTargetIsSniper</dt>
  <dd>Unused in rules, passes if player requested a duel with a Sniper</dd>
  <dt>DuelTargetIsSoldier</dt>
  <dd>Unused in rules, passes if player requested a duel with a Soldier</dd>
  <dt>DuelTargetIsSpy</dt>
  <dd>Unused in rules, passes if player requested a duel with a Spy</dd>
</dl>

### Under Crosshair Criteria

<dl>
  <dt>IsCrossHairEnemy</dt>
  <dd>Passes if player's crosshair is over an enemy player</dd>
  <dt>IsNotCrossHairEnemy</dt>
  <dd>Passes if player's crosshair is not over an enemy player</dd>
  <dt>IsOnDemoman</dt>
  <dd>Passes if player's crosshair is over a Demoman</dd>
  <dt>IsOnEngineer</dt>
  <dd>Passes if player's crosshair is over an Engineer</dd>
  <dt>IsOnHeavy</dt>
  <dd>Passes if player's crosshair is over a Heavy</dd>
  <dt>IsNotOnHeavy</dt>
  <dd>Passes if player's crosshair is over a Non-heavy</dd>
  <dt>IsOnMedic</dt>
  <dd>Passes if player's crosshair is over a Medic</dd>
  <dt>IsOnPyro</dt>
  <dd>Passes if player's crosshair is over a Pyro</dd>
  <dt>IsOnScout</dt>
  <dd>Passes if player's crosshair is over a Scout</dd>
  <dt>IsOnSniper</dt>
  <dd>Passes if player's crosshair is over a Sniper</dd>
  <dt>IsOnSoldier</dt>
  <dd>Passes if player's crosshair is over a Soldier</dd>
  <dt>IsOnSpy</dt>
  <dd>Passes if player's crosshair is over a Spy</dd>
</dl>

### Competitive Mode Criteria

<dl>
  <dt>IsComp6v6</dt>
  <dd>Passes if match is a competitive 6v6 match</dd>
  <dt>IsNotComp6v6</dt>
  <dd>Passes if match is not a competitive 6v6 match</dd>
  <dt>IsCompWinner</dt>
  <dd>Passes if match is a competitive 6v6 match and player is on the winning team</dd>
  <dt>IsFirstRound</dt>
  <dd>Passes if game is currently in its first round</dd>
  <dt>IsNotFirstRound</dt>
  <dd>Passes if game is past its first round</dd>
  <dt>PlayerWonPreviousRound</dt>
  <dd>Passes if player was on the team that won the previous round</dd>
  <dt>PlayerLostPreviousRound</dt>
  <dd>Passes if player was on the team that lost the previous round</dd>
  <dt>PlayerOnWinningTeam</dt>
  <dd>Passes if player is on the team that won this round</dd>
  <dt>PlayerOnLosingTeam</dt>
  <dd>Passes if player is on the team that lost this round</dd>
  <dt>PreviousRoundWasNotTie</dt>
  <dd>Passes if previous round was not a tie</dd>
  <dt>PreviousRoundWasTie</dt>
  <dd>Passes if previous round was a tie</dd>
</dl>

### Recent Kill Criteria

<dl>
  <dt>IsARecentKill</dt>
  <dd>Passes if player had a kill in the past 30 seconds</dd>
  <dt>IsManyRecentKills</dt>
  <dd>Passes if player had more than one kill in the past 30 seconds</dd>
  <dt>IsVeryManyRecentKills</dt>
  <dd>Passes if player had more than three kills in the past 30 seconds</dd>
  <dt>IsDominated</dt>
  <dd>Passes if kill that triggered concept earned player a domination</dd>
  <dt>IsRevenge</dt>
  <dd>Passes if kill that triggered concept was a revenge kill</dd>
</dl>

### Health Criteria

<dl>
  <dt>IsBeingHealed</dt>
  <dd>True when player is being continuously healed (any medi gun, Dispenser, Payload cart)</dd>
  <dt>IsNotBeingHealed</dt>
  <dd>True when player is not being continuously healed</dd>
  <dt>SuperHighHealthContext</dt>
  <dd>True when player has more than 1.4x of their base health</dd>
  <dt>LowHealthContext</dt>
  <dd>Passes if player has less than 25% health left</dd>
  <dt>NotLowHealth</dt>
  <dd>Passes if player has more than 50% health remaining</dd>
  <dt>IsInvulnerable</dt>
  <dd>Passes if player is UberCharged</dd>
</dl>

### Control Point Criteria

<dl>
  <dt>IsOnFriendlyControlPoint</dt>
  <dd>Passes if player is on a team-owned control point</dd>
  <dt>IsOnCappableControlPoint</dt>
  <dd>Passes if player is on a non-team-owned control point</dd>
</dl>

### Building Criteria

<dl>
  <dt>IsSentryGun</dt>
  <dd>Passes if Sentry Gun was object just sapped, destroyed, picked up, or detonated</dd>
  <dt>IsDispenser</dt>
  <dd>Passes if Dispenser was object just sapped, destroyed, picked up, or detonated</dd>
  <dt>IsTeleporter</dt>
  <dd>Passes if Teleporter was object just sapped, destroyed, picked up, or detonated</dd>
  <dt>IsSapper</dt>
  <dd>Passes if Sapper was object just destroyed</dd>
</dl>

### Mann vs. Machine Criteria

<dl>
  <dt>IsMvMDefender</dt>
  <dd>Passes if player is on the defending team in MvM mode</dd>
</dl>

### Demoman-Specific Criteria

<dl>
  <dt>CaberHealthContext</dt>
  <dd>Passes if player has more than 43% health remaining</dd>
  <dt>IsCritical</dt>
  <dd>Despite the name, set to pass for every call of ConceptPain or ConceptAttackerPain, only used by Ullapool Caber rule where it will always pass</dd>
</dl>

### Heavy-Specific Criteria

<dl>
  <dt>IsFiringMinigun</dt>
  <dd>Passes if player is firing minigun</dd>
  <dt>TimeFiringMinigunShort</dt>
  <dd>Passes if player has been firing minigun for between 4 and 8 seconds</dd>
  <dt>TimeFiringMinigunLong</dt>
  <dd>Passes if player has been firing minigun for between 8 and 15 seconds</dd>
  <dt>TimeFiringMinigunReallyLong</dt>
  <dd>Passes if player has been firing minigun for more than 15 seconds</dd>
</dl>

### Scout-Specific Criteria

<dl>
  <dt>BonkHealthContext</dt>
  <dd>Passes if player has less than 64% health remaining</dd>
  <dt>IsNotDoubleJumping</dt>
  <dd>Passes if player is not double jumping</dd>
  <dt>IsDoubleJumping</dt>
  <dd>Passes if player is double jumping</dd>
</dl>

### Sniper-Specific Criteria

<dl>
  <dt>IsHeadShot</dt>
  <dd>Passes if kill that triggered concept was a headshot</dd>
  <dt>DeployedContext</dt>
  <dd>Passes if player is zoomed in with a sniper rifle</dd>
  <dt>Unzoomed</dt>
  <dd>Passes if player is not zoomed in with a sniper rifle</dd>
</dl>

### Spy-Specific Criteria

<dl>
  <dt>IsCloaked</dt>
  <dd>Passes if player is cloaked</dd>
  <dt>IsNotCloaked</dt>
  <dd>Passes if player is not cloaked</dd>
  <dt>IsDisguised</dt>
  <dd>Passes if player is disguised</dd>
  <dt>IsNotDisguised</dt>
  <dd>Passes if player is not disguised</dd>
</dl>

### Holiday Taunts and Items Criteria

<dl>
  <dt>IsAprilFoolsTaunt</dt>
  <dd>Passes if taunt has been changed to laughter due to April Fools' Day</dd>
  <dt>IsHalloweenTaunt</dt>
  <dd>Passes if taunt has been changed to Thriller due to Halloween</dd>
  <dt>IsUnicornHead</dt>
  <dd>Passes if player has The Magical Mercenary equipped</dd>
  <dt>IsHauntedHat</dt>
  <dd>Passes if player has The Haunted Hat equipped</dd>
  <dt>IsSoldierBirdHead</dt>
  <dd>Passes if player has The Freedom Feathers equipped</dd>
  <dt>IsSoldierMaggotHat</dt>
  <dd>Passes if player has The Larval Lid equipped</dd>
  <dt>IsSoldierWizardHat</dt>
  <dd>Passes if player has The Spellbinder's Bonnet equipped</dd>
  <dt>IsHeavyBirdHead</dt>
  <dd>Passes if player has The Chicken Kiev equipped</dd>
  <dt>IsFairyHeavy</dt>
  <dd>Passes if player has the Grand Duchess item set equipped</dd>
  <dt>IsMedicDoubleFace</dt>
  <dd>Passes if player has The Second Opinion equipped</dd>
  <dt>IsMedicBirdHead</dt>
  <dd>Passes if player has Medimedes equipped</dd>
  <dt>IsMedicZombieBird</dt>
  <dd>Passes if player has Archimedes the Undying equipped</dd>
  <dt>IsSniperBirdHead</dt>
  <dd>Passes if player has Sir Shootsalot equipped</dd>
  <dt>IsZombieCostume</dt>
  <dd>Passes if player has a Voodoo-Cursed Soul equipped</dd>
  <dt>IsRobotCostume</dt>
  <dd>Passes if player has the Tin Soldier item set equipped</dd>
  <dt>IsFrankenHeavy</dt>
  <dd>Passes if player has the FrankenHeavy item set equipped</dd>
  <dt>IsDemowolf</dt>
  <dd>Passes if player has the Highland Hound item set equipped</dd>
</dl>

### Halloween Map Criteria

<dl>
  <dt>IsMapHelltower</dt>
  <dd>Passes if current map is plr_hightower_event</dd>
  <dt>IsInHell</dt>
  <dd>Unused in rules, passes if players are in the Hell section of Helltower</dd>
  <dt>IsNotInHell</dt>
  <dd>Passes if players are not in the Hell section of Helltower</dd>
  <dt>IsMerasmusHiding</dt>
  <dd>Passes if Merasmus is subjecting players to hide and seek</dd>
</dl>

### Weapon Slot Criteria

<dl>
  <dt>IsWeaponPrimary</dt>
  <dd>True when player's selected weapon is a primary weapon</dd>
  <dt>WeaponIsNotVanillaPrimary</dt>
  <dd>Passes if the primary weapon slot does not contain a stock weapon or a variant (e.g. Australium weapons will cause this criterion to not match)</dd>
  <dt>IsWeaponSecondary</dt>
  <dd>True when player's selected weapon is a secondary weapon</dd>
  <dt>WeaponIsNotVanillaSecondary</dt>
  <dd>Passes if the secondary weapon slot does not contain a stock weapon or a variant</dd>
  <dt>IsWeaponMelee</dt>
  <dd>True when player's selected weapon is a melee weapon</dd>
  <dt>WeaponIsNotVanillaMelee</dt>
  <dd>Passes if the melee weapon slot does not contain a stock weapon with no skin or variant</dd>
  <dt>IsNotWeaponMelee</dt>
  <dd>True when player's selected weapon is NOT a melee weapon</dd>
  <dt>IsWeaponPda</dt>
  <dd>True when player's selected weapon is a PDA</dd>
  <dt>IsWeaponBuilding</dt>
  <dd>True when player's selected weapon is a building</dd>
</dl>

### Demoman Weapon Criteria

<dl>
  <dt>WeaponIsBottle</dt>
  <dd>Passes if selected weapon is Bottle or The Scottish Handshake</dd>
  <dt>WeaponIsDefender</dt>
  <dd>Passes if selected weapon is The Scottish Resistance</dd>
  <dt>WeaponIsCaber</dt>
  <dd>Passes if selected weapon is The Ullapool Caber</dd>
  <dt>WeaponIsSword</dt>
  <dd>Passes if selected weapon is of weapon class tf_weapon_sword (The Eyelander, The Persian Persuader, The Claidheamh Mor, or The Scotsman's Skullcutter)</dd>
  <dt>WeaponClassIsNotAxe</dt>
  <dd>Passes if selected weapon is not of weapon class tf_weapon_sword (The Eyelander, The Persian Persuader, The Claidheamh Mor, or The Scotsman's Skullcutter)</dd>
  <dt>WeaponIsScotsmansSkullcutter</dt>
  <dd>Passes if selected weapon is The Scotsman's Skullcutter</dd>
  <dt>WeaponIsNotAxe</dt>
  <dd>Passes if selected weapon is not The Scotsman's Skullcutter</dd>
  <dt>WeaponIsPipebomb</dt>
  <dd>Passes if selected weapon is any sticky launcher</dd>
  <dt>WeaponIsGrenade</dt>
  <dd>Passes if selected weapon is Grenade Launcher, The Loch-n-Load, The Iron Bomber</dd>
  <dt>WeaponIsLooseCannon</dt>
  <dd>Passes if selected weapon is The Loose Cannon</dd>
</dl>

### Engineer Weapon Criteria

<dl>
  <dt>WeaponIsShotgunPrimary</dt>
  <dd>Passes if selected weapon is Shotgun (Engineer)</dd>
  <dt>WeaponIsFrontierJustice</dt>
  <dd>Passes if selected weapon is The Frontier Justice</dd>
  <dt>WeaponIsFestiveFrontierJustice</dt>
  <dd>Passes if selected weapon is Festive Frontier Justice</dd>
  <dt>WeaponIsPomson</dt>
  <dd>Passes if selected weapon is The Pomson 6000</dd>
  <dt>WeaponIsRescueRanger</dt>
  <dd>Passes if selected weapon is The Rescue Ranger</dd>
  <dt>WeaponIsPistol</dt>
  <dd>Passes if selected weapon is Pistol (Engineer)</dd>
  <dt>WeaponIsLaserPointer</dt>
  <dd>Passes if selected weapon is The Wrangler</dd>
  <dt>WeaponIsShortCircuit</dt>
  <dd>Passes if selected weapon is The Short Circuit</dd>
  <dt>WeaponIsWrench</dt>
  <dd>Passes if selected weapon is any Engineer melee</dd>
  <dt>WeaponIsRobotArm</dt>
  <dd>Passes if selected weapon is The Gunslinger</dd>
  <dt>WeaponIsNotRobotArm</dt>
  <dd>Passes if selected weapon is not The Gunslinger</dd>
  <dt>LoadoutIsNotRobotArm</dt>
  <dd>Passes if loadout does not contain The Gunslinger</dd>
  <dt>WeaponIsGoldenWrench</dt>
  <dd>Passes if selected weapon is The Golden Wrench</dd>
  <dt>WeaponIsEurekaEffect</dt>
  <dd>Passes if selected weapon is The Eureka Effect</dd>
  <dt>WeaponIsSentrygun</dt>
  <dd>Passes if kill that triggered concept was a Sentry Gun kill</dd>
  <dt>WeaponIsNotSentry</dt>
  <dd>Passes if kill that triggered concept was not a Sentry Gun kill</dd>
  <dt>WeaponIsMiniSentrygun</dt>
  <dd>Passes if kill that triggered concept was a Mini-Sentry kill</dd>
  <dt>WeaponIsNotMiniSentrygun</dt>
  <dd>Passes if kill that triggered concept was not a Mini-Sentry kill</dd>
  <dt>WeaponIsNotSentrygun</dt>
  <dd>Unused in rules, will never pass, compares to invalid "customdeath" value</dd>
</dl>

### Heavy Weapon Criteria

<dl>
  <dt>WeaponIsMinigun</dt>
  <dd>Passes if selected weapon is any minigun</dd>
  <dt>WeaponIsNotTaggedMinigun</dt>
  <dd>Passes if selected weapon is not Minigun or a variant (Australium or Festivized)</dd>
  <dt>WeaponIsNotTomislav</dt>
  <dd>Passes if selected weapon is not Tomislav</dd>
  <dt>WeaponIsShotgunHwg</dt>
  <dd>Passes if selected weapon is Shotgun (Heavy)</dd>
  <dt>WeaponIsLunchbox</dt>
  <dd>Passes if selected weapon is any lunchbox item</dd>
  <dt>WeaponIsSandvich</dt>
  <dd>Passes if selected weapon is The Sandvich</dd>
  <dt>WeaponIsFestiveSandvich</dt>
  <dd>Passes if selected weapon is Festive Sandvich</dd>
  <dt>WeaponIsRobotSandvich</dt>
  <dd>Passes if selected weapon is The Robo-Sandvich</dd>
  <dt>WeaponIsFishcake</dt>
  <dd>Passes if selected weapon is Fishcake</dd>
  <dt>WeaponIsSteak</dt>
  <dd>Passes if selected weapon is The Buffalo Steak Sandvich</dd>
  <dt>WeaponIsBenja</dt>
  <dd>Passes if selected weapon is The Dalokohs Bar</dd>
  <dt>WeaponIsFists</dt>
  <dd>Passes if selected weapon is any Heavy melee</dd>
  <dt>WeaponIsGloves</dt>
  <dd>Passes if selected weapon is The Killing Gloves of Boxing</dd>
  <dt>WeaponIsMetalFists</dt>
  <dd>Passes if selected weapon is The Fists of Steel</dd>
</dl>

### Medic Weapon Criteria

<dl>
  <dt>WeaponIsSyringe</dt>
  <dd>Passes if selected weapon is Syringe Gun, The Overdose, or The Blutsauger</dd>
  <dt>WeaponIsHealArrow</dt>
  <dd>Passes if selected weapon is The Crusader's Crossbow</dd>
  <dt>WeaponIsHeal</dt>
  <dd>Passes if selected weapon is any medigun</dd>
  <dt>WeaponIsNotMediGun</dt>
  <dd>Passes if selected weapon is not any medigun</dd>
  <dt>WeaponIsNotTaggedMedigun</dt>
  <dd>Passes if selected weapon is not Medi Gun or a variant (Australium or Festivized)</dd>
  <dt>WeaponIsKritzkrieg</dt>
  <dd>Passes if selected weapon is The Kritzkrieg</dd>
  <dt>WeaponIsBonesaw</dt>
  <dd>Passes if selected weapon is any Medic melee</dd>
  <dt>WeaponIsUbersaw</dt>
  <dd>Passes if selected weapon is The Ubersaw</dd>
  <dt>WeaponIsFestiveUbersaw</dt>
  <dd>Passes if selected weapon is Festive Ubersaw</dd>
  <dt>WeaponIsHippocrates</dt>
  <dd>Passes if selected weapon is The Solemn Vow</dd>
</dl>

### Pyro Weapon Criteria

<dl>
  <dt>WeaponIsFlamethrower</dt>
  <dd>Passes if selected weapon is Flamethrower</dd>
  <dt>WeaponIsRainblower</dt>
  <dd>Passes if selected weapon is The Rainblower</dd>
  <dt>WeaponIsDragonsFury</dt>
  <dd>Passes if selected weapon is The Dragon's Fury</dd>
  <dt>WeaponIsShotgunPyro</dt>
  <dd>Passes if selected weapon is Shotgun (Pyro)</dd>
  <dt>WeaponIsFlaregun</dt>
  <dd>Passes if selected weapon is Flare Gun or The Detonator</dd>
  <dt>WeaponIsScorchShot</dt>
  <dd>Passes if selected weapon is The Scorch Shot</dd>
  <dt>WeaponIsManmelter</dt>
  <dd>Passes if selected weapon is The Manmelter</dd>
  <dt>WeaponIsGasCan</dt>
  <dd>Passes if selected weapon is The Gas Passer</dd>
  <dt>WeaponIsAxe</dt>
  <dd>Passes if selected weapon is Fire Axe</dd>
  <dt>WeaponIsLollichop</dt>
  <dd>Passes if selected weapon is The Lollichop</dd>
  <dt>WeaponIsPromoAnnihilator</dt>
  <dd>Passes if selected weapon is Promo Neon Annihilator</dd>
  <dt>WeaponIsAnnihilator</dt>
  <dd>Passes if selected weapon is The Neon Annihilator</dd>
  <dt>WeaponIsThirdDegree</dt>
  <dd>Passes if selected weapon is The Third Degree</dd>
  <dt>WeaponIsSlap</dt>
  <dd>Passes if selected weapon is The Hot Hand</dd>
</dl>

### Scout Weapon Criteria

<dl>
  <dt>WeaponIsScattergun</dt>
  <dd>Passes if selected weapon is Scattergun</dd>
  <dt>WeaponIsScattergunDouble</dt>
  <dd>Passes if selected weapon is The Force-a-Nature</dd>
  <dt>WeaponIsNotScattergunDouble</dt>
  <dd>Passes if selected weapon is not The Force-a-Nature</dd>
  <dt>WeaponIsScattergunDoubleFestive</dt>
  <dd>Passes if selected weapon is Festive Force-a-Nature</dd>
  <dt>WeaponIsShortstop</dt>
  <dd>Passes if selected weapon is The Shortstop</dd>
  <dt>WeaponIsPEPBrawlerBlaster</dt>
  <dd>Passes if selected weapon is Baby Face's Blaster</dd>
  <dt>WeaponIsPistolScout</dt>
  <dd>Passes if selected weapon is Pistol (Scout)</dd>
  <dt>WeaponIsHandgunScoutSecondary</dt>
  <dd>Passes if selected weapon is The Winger or Pretty Boy's Pocket Pistol</dd>
  <dt>WeaponIsSDCleaver</dt>
  <dd>Passes if selected weapon is The Flying Guillotine</dd>
  <dt>WeaponIsMadMilk</dt>
  <dd>Passes if selected weapon is The Mad Milk</dd>
  <dt>WeaponIsMutatedMilk</dt>
  <dd>Passes if selected weapon is Mutated Milk</dd>
  <dt>LoadoutIsCritDrink</dt>
  <dd>Passes if loadout contains Crit-a-Cola</dd>
  <dt>LoadoutIsDrink</dt>
  <dd>Passes if loadout does not contain Crit-a-Cola</dd>
  <dt>WeaponIsBat</dt>
  <dd>Passes if selected weapon is any bat</dd>
  <dt>WeaponIsWoodBat</dt>
  <dd>Passes if selected weapon is The Sandman</dd>
  <dt>WeaponIsAtomizer</dt>
  <dd>Passes if selected weapon is The Atomizer</dd>
  <dt>WeaponIsMace</dt>
  <dd>Passes if selected weapon is Sun-on-a-Stick</dd>
  <dt>WeaponIsNotMace</dt>
  <dd>Passes if selected weapon is not Sun-on-a-Stick</dd>
  <dt>WeaponIsGunbai</dt>
  <dd>Passes if selected weapon is The Fan O'War</dd>
  <dt>WeaponIsNotGunbai</dt>
  <dd>Passes if selected weapon is not The Fan O'War</dd>
  <dt>WeaponIsBasher</dt>
  <dd>Passes if selected weapon is The Boston Basher</dd>
  <dt>WeaponIsNotBasher</dt>
  <dd>Passes if selected weapon is not The Boston Basher</dd>
  <dt>WeaponIsCandy</dt>
  <dd>Passes if selected weapon is The Candy Cane</dd>
  <dt>WeaponIsNotCandy</dt>
  <dd>Passes if selected weapon is not The Candy Cane</dd>
  <dt>WeaponIsHolyMackerel</dt>
  <dd>Passes if selected weapon is The Holy Mackerel</dd>
  <dt>WeaponIsNotFish</dt>
  <dd>Passes if selected weapon is not The Holy Mackerel</dd>
  <dt>WeaponIsFestiveHolyMackerel</dt>
  <dd>Passes if selected weapon is Festive Holy Mackerel</dd>
  <dt>WeaponIsLunchboxDrink</dt>
  <dd>Passes if selected weapon is Bonk! Atomic Punch or Crit-a-Cola</dd>
  <dt>WeaponIsSodaPopper</dt>
  <dd>Passes if selected weapon is The Soda Popper</dd>
  <dt>WeaponIsTRBlade</dt>
  <dd>Passes if selected weapon is Three-Rune Blade</dd>
  <dt>WeaponIsNotTRBlade</dt>
  <dd>Passes if selected weapon is not Three-Rune Blade</dd>
  <dt>WeaponIsUnarmedCombat</dt>
  <dd>Passes if selected weapon is Unarmed Combat</dd>
  <dt>WeaponIsWrapAssassin</dt>
  <dd>Passes if selected weapon is The Wrap Assassin</dd>
</dl>

### Sniper Weapon Criteria

<dl>
  <dt>WeaponIsSniperrifle</dt>
  <dd>Passes if selected weapon is any sniper rifle except The Bazaar Bargain or The Classic</dd>
  <dt>WeaponIsNotTaggedRifle</dt>
  <dd>Passes if selected weapon is not Sniper Rifle or a variant (Australium or Festivized)</dd>
  <dt>WeaponIsBow</dt>
  <dd>Passes if selected weapon is The Huntsman or The Fortified Compound</dd>
  <dt>WeaponIsBazaarBargain</dt>
  <dd>Passes if selected weapon is The Bazaar Bargain</dd>
  <dt>WeaponIsClassicSniperrifle</dt>
  <dd>Passes if selected weapon is The Classic</dd>
  <dt>WeaponIsSMG</dt>
  <dd>Passes if selected weapon is SMG</dd>
  <dt>WeaponIsJarate</dt>
  <dd>Passes if selected weapon is The Jarate (not any reskin)</dd>
  <dt>WeaponIsNotTaggedSMG</dt>
  <dd>Passes if selected weapon is not SMG or a variant (Australium or Festivized)</dd>
  <dt>WeaponIsChargedSMG</dt>
  <dd>Passes if selected weapon is The Cleaner's Carbine</dd>
  <dt>WeaponIsClub</dt>
  <dd>Passes if selected weapon is any Sniper melee</dd>
  <dt>WeaponIsNotTaggedKukri</dt>
  <dd>Passes if selected weapon is not Kukri or a variant (Festivized)</dd>
  <dt>WeaponIsShiv</dt>
  <dd>Passes if selected weapon is The Tribalman's Shiv</dd>
</dl>

### Soldier Weapon Criteria

<dl>
  <dt>WeaponIsRocket</dt>
  <dd>Passes if selected weapon is Rocket Launcher</dd>
  <dt>WeaponIsDirectHit</dt>
  <dd>Passes if selected weapon is The Direct Hit</dd>
  <dt>WeaponIsCowMangler</dt>
  <dd>Passes if selected weapon is The Cow Mangler 5000</dd>
  <dt>WeaponIsBeggarsBazooka</dt>
  <dd>Passes if selected weapon is The Beggar's Bazooka</dd>
  <dt>WeaponIsRocketLauncherAirStrike</dt>
  <dd>Passes if selected weapon is The Air Strike</dd>
  <dt>WeaponIsBanner</dt>
  <dd>Passes if selected weapon is The Buff Banner</dd>
  <dt>WeaponIsFestiveBanner</dt>
  <dd>Passes if selected weapon is Festive Buff banner</dd>
  <dt>WeaponIsBackup</dt>
  <dd>Passes if selected weapon is The Battalion's Backup</dd>
  <dt>WeaponIsSashimono</dt>
  <dd>Passes if selected weapon is The Concheror</dd>
  <dt>WeaponIsRayGun</dt>
  <dd>Passes if selected weapon is The Righteous Bison</dd>
  <dt>WeaponIsShotgunSoldier</dt>
  <dd>Passes if selected weapon is Shotgun (Soldier)</dd>
  <dt>WeaponIsShovel</dt>
  <dd>Passes if selected weapon is Shovel</dd>
  <dt>WeaponIsEqualizer</dt>
  <dd>Passes if selected weapon is The Equalizer</dd>
  <dt>WeaponIsEscapePlan</dt>
  <dd>Passes if selected weapon is The Escape Plan</dd>
</dl>

### Spy Weapon Criteria

<dl>
  <dt>WeaponIsRevolver</dt>
  <dd>Passes if selected weapon is any Spy primary</dd>
  <dt>WeaponIsKnife</dt>
  <dd>Passes if selected weapon is any Spy melee</dd>
  <dt>WeaponIsSharpDresser</dt>
  <dd>Unused in rules, passes if selected weapon is The Sharp Dresser</dd>
  <dt>WeaponIsSpycicle</dt>
  <dd>Passes if selected weapon is The Spy-cicle</dd>
  <dt>WeaponIsSpyPDA</dt>
  <dd>Passes if selected weapon is Disguise Kit</dd>
  <dt>WeaponIsBuild</dt>
  <dd>Passes if selected weapon is of class tf_weapon_builder (Engineer's PDA or Spy's Sapper)</dd>
  <dt>WeaponIsPainTrain</dt>
  <dd>Passes if selected weapon is The Pain Train</dd>
  <dt>WeaponIsNotPainTrain</dt>
  <dd>Passes if selected weapon is not The Pain Train</dd>
  <dt>WeaponIsKatana</dt>
  <dd>Passes if selected weapon is The Half-Zatoichi</dd>
  <dt>WeaponIsSaxxy</dt>
  <dd>Passes if selected weapon is The Saxxy</dd>
  <dt>WeaponIsNotSaxxy</dt>
  <dd>Passes if selected weapon is not The Saxxy</dd>
  <dt>WeaponIsFryingPan</dt>
  <dd>Passes if selected weapon is The Frying Pan</dd>
  <dt>WeaponIsNotFryingPan</dt>
  <dd>Passes if selected weapon is not The Frying Pan</dd>
  <dt>WeaponIsGoldenFryingPan</dt>
  <dd>Passes if selected weapon is The Gold Frying Pan</dd>
</dl>

### Unused Criteria

<dl>
  <dt>HasTaunt2Item_TauntEnablerTest</dt>
  <dd>Unused in rules, checks action slot for debug item "Taunt Enabler Test"</dd>
  <dt>SF13IsTheWitchingHour</dt>
  <dd>Unused in rules, passes if world context "worldIsTheWitchingHour" is active</dd>
  <dt>SF13IsNotTheWitchingHour</dt>
  <dd>Unused in rules, passes if world context "worldIsTheWitchingHour" is not active</dd>
  <dt>WeaponIsShotgun</dt>
  <dd>Unused in rules (compares to unused class "tf_weapon_shotgun_secondary")</dd>
  <dt>WeaponIsSMGScout</dt>
  <dd>Unused in rules (compares to unused class "tf_weapon_smg_scout")</dd>
</dl>

## Context Criteria

### Generic Context Criteria

<dl>
  <dt>NotDefendOnThePointSpeech</dt>
  <dd>Passes if any player has not said a "defend on the point" line in the past several seconds (duration depends on rule)</dd>
  <dt>NotMerasmusHideCooldown</dt>
  <dd>Passes if no player has said a "come out, Merasmus!" type line in the past 30 seconds</dd>
  <dt>NotMannhattanGateAttackCooldown</dt>
  <dd>Passes if no player has said a "robots are attacking the gate!" type line in the past 30 seconds</dd>
  <dt>KilledPlayerDelay</dt>
  <dd>Passes if world context "worldDontKilledPlayer" is not active (not set in any maps as far as I can tell)</dd>
  <dt>IsNotDominating</dt>
  <dd>Passes if player has not said a domination line in the past 10 seconds</dd>
</dl>

### Demoman-Specific Context Criteria

<dl>
  <dt>DemomanIsNotStillonFire</dt>
  <dd>Passes if player as Demoman has not said a line related to being on fire in the past 7 seconds</dd>
  <dt>DemomanIsStillonFire</dt>
  <dd>Passes if player as Demoman has said a line related to being on fire in the past 7 seconds</dd>
  <dt>DemomanNotAssistSpeech</dt>
  <dd>Passes if player as Demoman has not said a line thanking for a kill assist in the past 20 seconds</dd>
  <dt>DemomanNotAwardSpeech</dt>
  <dd>Passes if player as Demoman has not said a line related to getting an achievement in the past 10 seconds</dd>
  <dt>DemomanNotInvulnerableSpeech</dt>
  <dd>Passes if player as Demoman has not said a line related to firing while invulnerable in the past 30 seconds</dd>
  <dt>DemomanNotKillSpeech</dt>
  <dd>Passes if player as Demoman has not said a line related to getting a kill in the past 10 seconds</dd>
  <dt>DemomanNotKillSpeechMelee</dt>
  <dd>Passes if player as Demoman has not said a line related to getting a melee kill in the past 10 seconds</dd>
  <dt>DemomanNotSaidCartMovingBackwardD</dt>
  <dd>Passes if player as Demoman on defense has not said a line related to the cart moving back in the past 20 seconds</dd>
  <dt>DemomanNotSaidCartMovingBackwardO</dt>
  <dd>Passes if player as Demoman on offense has not said a line related to the cart moving back in the past 20 seconds</dd>
  <dt>DemomanNotSaidCartMovingForwardD</dt>
  <dd>Passes if player as Demoman on defense has not said a line related to the cart being pushed in the past 20 seconds</dd>
  <dt>DemomanNotSaidCartMovingForwardO</dt>
  <dd>Passes if player as Demoman on offense has not said a line related to the cart being pushed in the past 20 seconds</dd>
  <dt>DemomanNotSaidCartMovingStoppedD</dt>
  <dd>Passes if player as Demoman on defense has not said a line related to the cart stopping moving in the past 20 seconds</dd>
  <dt>DemomanNotSaidCartMovingStoppedO</dt>
  <dd>Passes if player as Demoman on offense has not said a line related to the cart stopping moving in the past 20 seconds</dd>
  <dt>DemomanNotSaidHealThanks</dt>
  <dd>Passes if player as Demoman has not said a line thanking for healing in the past 20 seconds</dd>
  <dt>IsDrunk</dt>
  <dd>Passes if player as Demoman has taunted with a bottle melee in the past 10 seconds</dd>
  <dt>DemomanIsKillSpeechObject</dt>
  <dd>Unused in rules, passes if player as Demoman has said a line related to destroying a building after getting a kill in the past 30 seconds</dd>
</dl>

### Engineer-Specific Context Criteria

<dl>
  <dt>IsSentryKill</dt>
  <dd>Passes if player-built Sentry Gun had a kill in the past 15 seconds</dd>
  <dt>IsMiniSentryKill</dt>
  <dd>Passes if player-built Mini Sentry had a kill in the past 15 seconds</dd>
  <dt>IsEngyFistSwung</dt>
  <dd>Passes if player has swung with the Gunslinger in the past 20 seconds</dd>
  <dt>IsNotEngyFistSwung</dt>
  <dd>Passes if player has not swung with the Gunslinger in the past 20 seconds</dd>
  <dt>EngineerIsNotStillonFire</dt>
  <dd>Passes if player as Engineer has not said a line related to being on fire in the past 7 seconds</dd>
  <dt>EngineerIsStillonFire</dt>
  <dd>Passes if player as Engineer has said a line related to being on fire in the past 7 seconds</dd>
  <dt>EngineerNotAssistSpeech</dt>
  <dd>Passes if player as Engineer has not said a line thanking for a kill assist in the past 20 seconds</dd>
  <dt>EngineerNotInvulnerableSpeech</dt>
  <dd>Passes if player as Engineer has not said a line related to firing while invulnerable in the past 30 seconds</dd>
  <dt>EngineerNotKillSpeech</dt>
  <dd>Passes if player as Engineer has not said a line related to getting a kill in the past 10 seconds</dd>
  <dt>EngineerNotKillSpeechMelee</dt>
  <dd>Passes if player as Engineer has not said a line related to getting a melee kill in the past 10 seconds</dd>
  <dt>EngineerNotSaidHealThanks</dt>
  <dd>Passes if player as Engineer has not said a line thanking for healing in the past 20 seconds</dd>
</dl>

### Heavy-Specific Context Criteria

<dl>

<dl>
  <dt>HeavyIsNotStillonFire</dt>
  <dd>Passes if player as Heavy has not said a line related to being on fire in the past 7 seconds</dd>
  <dt>HeavyIsStillonFire</dt>
  <dd>Passes if player as Heavy has said a line related to being on fire in the past 7 seconds</dd>
  <dt>HeavyNotAssistSpeech</dt>
  <dd>Passes if player as Heavy has not said a line thanking for a kill assist in the past 20 seconds</dd>
  <dt>HeavyNotAwardSpeech</dt>
  <dd>Passes if player as Heavy has not said a line related to getting an achievement in the past 10 seconds</dd>
  <dt>HeavyNotInvulnerableSpeech</dt>
  <dd>Passes if player as Heavy has not said a line related to firing while invulnerable in the past 30 seconds</dd>
  <dt>HeavyNotKillSpeech</dt>
  <dd>Passes if player as Heavy has not said a line related to getting a kill in the past 10 seconds</dd>
  <dt>HeavyNotKillSpeechMelee</dt>
  <dd>Passes if player as Heavy has not said a line related to getting a melee kill in the past 10 seconds</dd>
  <dt>HeavyNotKillSpeechObject</dt>
  <dd>Passes if player as Heavy has not said a line related to destroying a building in the past 30 seconds</dd>
  <dt>HeavyNotMedicSpeech</dt>
  <dd>Passes if player as Heavy has not said a line about killing an enemy Medic while being healed in the past 20 seconds</dd>
  <dt>HeavyNotSaidCartMovingBackwardD</dt>
  <dd>Passes if player as Heavy on defense has not said a line related to the cart moving back in the past 20 seconds</dd>
  <dt>HeavyNotSaidCartMovingBackwardO</dt>
  <dd>Passes if player as Heavy on offense has not said a line related to the cart moving back in the past 20 seconds</dd>
  <dt>HeavyNotSaidCartMovingForwardD</dt>
  <dd>Passes if player as Heavy on defense has not said a line related to the cart being pushed in the past 20 seconds</dd>
  <dt>HeavyNotSaidCartMovingForwardO</dt>
  <dd>Passes if player as Heavy on offense has not said a line related to the cart being pushed in the past 20 seconds</dd>
  <dt>HeavyNotSaidCartMovingStoppedD</dt>
  <dd>Passes if player as Heavy on defense has not said a line related to the cart stopping moving in the past 20 seconds</dd>
  <dt>HeavyNotSaidCartMovingStoppedO</dt>
  <dd>Passes if player as Heavy on offense has not said a line related to the cart stopping moving in the past 20 seconds</dd>
  <dt>HeavyNotSaidHealThanks</dt>
  <dd>Passes if player as Heavy has not said a line thanking for healing in the past 20 seconds</dd>
  <dt>HeavyNotShinySpeech</dt>
  <dd>Passes if player as Heavy has not said a line when winding up a non-stock, non-Tomislav minigun in the past 5 minutes</dd>
  <dt>IsNotDaring</dt>
  <dd>Passes if player has not performed a melee dare in the past 5 seconds</dd>
  <dt>IsHeavyFistsSwung</dt>
  <dd>Passes if player has performed the first melee swing line as Heavy ("Take that!") in the past 10 seconds</dd>
  <dt>IsNotHeavyFistsSwung</dt>
  <dd>Passes if player has not performed the first melee swing line as Heavy ("Take that!") in the past 10 seconds</dd>
  <dt>IsHeavyFistsSwinging</dt>
  <dd>Unused in rules, will never pass due to comparing "HeavyFistsSwinging" to "1", when it is only ever set to "0" or "2"</dd>
  <dt>IsNotHeavyFistsSwinging</dt>
  <dd>Passes if player has not performed any followup melee swing line as Heavy in the past 10 seconds</dd>
</dl>
  <dt>NotGunTauntHeavy</dt>
  <dd>Passes if player as Heavy has not insulted another non-Heavy player in the past 10 seconds</dd>
  <dt>HeavyIsKillSpeechObject</dt>
  <dd>Unused in rules, passes if player as Heavy has said a line related to destroying a building in the past 30 seconds </dd>
</dl>

### Medic-Specific Context Criteria

<dl>
  <dt>MedicIsNotStillonFire</dt>
  <dd>Passes if player as Medic has not said a line related to being on fire in the past 7 seconds</dd>
  <dt>MedicIsStillonFire</dt>
  <dd>Passes if player as Medic has said a line related to being on fire in the past 7 seconds</dd>
  <dt>MedicNotAssistSpeech</dt>
  <dd>Passes if player as Medic has not said a line thanking for a kill assist in the past 20 seconds</dd>
  <dt>MedicNotInvulnerableSpeech</dt>
  <dd>Passes if player as Medic has not said a line related to firing while invulnerable in the past 30 seconds</dd>
  <dt>MedicNotKillSpeech</dt>
  <dd>Passes if player as Medic has not said a line related to getting a kill in the past 10 seconds</dd>
  <dt>MedicNotKillSpeechMelee</dt>
  <dd>Passes if player as Medic has not said a line related to getting a melee kill in the past 10 seconds</dd>
  <dt>MedicNotSaidCartMovingBackwardD</dt>
  <dd>Passes if player as Medic on defense has not said a line related to the cart moving back in the past 20 seconds</dd>
  <dt>MedicNotSaidCartMovingBackwardO</dt>
  <dd>Passes if player as Medic on offense has not said a line related to the cart moving back in the past 20 seconds</dd>
  <dt>MedicNotSaidCartMovingForwardD</dt>
  <dd>Passes if player as Medic on defense has not said a line related to the cart being pushed in the past 20 seconds</dd>
  <dt>MedicNotSaidCartMovingForwardO</dt>
  <dd>Passes if player as Medic on offense has not said a line related to the cart being pushed in the past 20 seconds</dd>
  <dt>MedicNotSaidCartMovingStoppedD</dt>
  <dd>Passes if player as Medic on defense has not said a line related to the cart stopping moving in the past 20 seconds</dd>
  <dt>MedicNotSaidCartMovingStoppedO</dt>
  <dd>Passes if player as Medic on offense has not said a line related to the cart stopping moving in the past 20 seconds</dd>
  <dt>MedicNotSaidHealThanks</dt>
  <dd>Passes if player as Medic has not said a line thanking for healing in the past 20 seconds</dd>
  <dt>MedicIsKillSpeechObject</dt>
  <dd>Unused in rules, passes if player as Medic has said a line related to destroying a building after getting a kill in the past 30 seconds</dd>
</dl>

### Pyro-Specific Context Criteria

<dl>
  <dt>PyroIsNotStillonFire</dt>
  <dd>Passes if player as Pyro has not said a line related to being on fire in the past 7 seconds</dd>
  <dt>PyroIsStillonFire</dt>
  <dd>Passes if player as Pyro has said a line related to being on fire in the past 7 seconds</dd>
  <dt>PyroNotAssistSpeech</dt>
  <dd>Passes if player as Pyro has not said a line thanking for a kill assist in the past 20 seconds</dd>
  <dt>PyroNotInvulnerableSpeech</dt>
  <dd>Passes if player as Pyro has not said a line related to firing while invulnerable in the past 30 seconds</dd>
  <dt>PyroNotKillSpeech</dt>
  <dd>Passes if player as Pyro has not said a line related to getting a kill in the past 10 seconds</dd>
  <dt>PyroNotKillSpeechMelee</dt>
  <dd>Passes if player as Pyro has not said a line related to getting a melee kill in the past 10 seconds</dd>
  <dt>PyroNotSaidHealThanks</dt>
  <dd>Passes if player as Pyro has not said a line thanking for healing in the past 20 seconds</dd>
  <dt>PyroNotKillSpeechSapper</dt>
  <dd>Unused, is never set</dd>
</dl>

### Scout-Specific Context Criteria

<dl>
  <dt>NotSaidScoutHitBallSpeech</dt>
  <dd>Passes if player as Scout has not said a line related to hitting The Sandman's ball in the past 10 seconds</dd>
  <dt>NotScoutGrabbedIntelligence</dt>
  <dd>Passes if player as Scout has not said a line related to grabbing the intelligence in the past 30 seconds</dd>
  <dt>ScoutHasFired</dt>
  <dd>Passes if player as Scout has fired a weapon in the past 7 seconds</dd>
  <dt>ScoutIsNotCrit</dt>
  <dd>Passes if player as Scout has used a lunchbox drink item in the past 3 seconds (counter to its name, ScoutIsNotCrit is passes if the ScoutIsCrit context is set to 1)</dd>
  <dt>ScoutIsNotInvuln</dt>
  <dd>Passes if player as Scout has not said a line related to Bonk invulnerability starting or ending in the past 20 seconds</dd>
  <dt>ScoutIsNotStillonFire</dt>
  <dd>Passes if player as Scout has not said a line related to being on fire in the past 7 seconds</dd>
  <dt>ScoutIsStillonFire</dt>
  <dd>Passes if player as Scout has said a line related to being on fire in the past 7 seconds</dd>
  <dt>ScoutNotAssistSpeech</dt>
  <dd>Passes if player as Scout has not said a line thanking for a kill assist in the past 20 seconds</dd>
  <dt>ScoutNotAwardSpeech</dt>
  <dd>Passes if player as Scout has not said a line related to getting an achievement in the past 10 seconds</dd>
  <dt>ScoutNotDoubleJumpSpeech</dt>
  <dd>Passes if player as Scout has not said a line related to double jumping in the past 90 seconds</dd>
  <dt>ScoutNotDrinkReadySpeech</dt>
  <dd>Passes if player as Scout has not said a line related to being shot at low health while holding Bonk in the past 5 seconds</dd>
  <dt>ScoutNotInvulnerableSpeech</dt>
  <dd>Passes if player as Scout has not said a line related to firing while invulnerable in the past 30 seconds</dd>
  <dt>ScoutNotKillSpeech</dt>
  <dd>Passes if player as Scout has not said a line related to getting a kill in the past 10 seconds</dd>
  <dt>ScoutNotKillSpeechMelee</dt>
  <dd>Passes if player as Scout has not said a line related to getting a melee kill in the past 10 seconds</dd>
  <dt>ScoutNotKillSpeechMeleeFat</dt>
  <dd>Passes if player as Scout has not insulted Heavy after a melee kill in the past 10 seconds</dd>
  <dt>ScoutNotSaidCartMovingBackwardD</dt>
  <dd>Passes if player as Scout on defense has not said a line related to the cart moving back in the past 20 seconds</dd>
  <dt>ScoutNotSaidCartMovingBackwardO</dt>
  <dd>Passes if player as Scout on offense has not said a line related to the cart moving back in the past 20 seconds</dd>
  <dt>ScoutNotSaidCartMovingForwardD</dt>
  <dd>Passes if player as Scout on defense has not said a line related to the cart being pushed in the past 20 seconds</dd>
  <dt>ScoutNotSaidCartMovingForwardO</dt>
  <dd>Passes if player as Scout on offense has not said a line related to the cart being pushed in the past 20 seconds</dd>
  <dt>ScoutNotSaidCartMovingStoppedD</dt>
  <dd>Passes if player as Scout on defense has not said a line related to the cart stopping moving in the past 20 seconds</dd>
  <dt>ScoutNotSaidCartMovingStoppedO</dt>
  <dd>Passes if player as Scout on offense has not said a line related to the cart stopping moving in the past 20 seconds</dd>
  <dt>ScoutNotSaidHealThanks</dt>
  <dd>Passes if player as Scout has not said a line thanking for healing in the past 20 seconds</dd>
  <dt>ScoutIsKillSpeechObject</dt>
  <dd>Unused in rules, passes if player as Scout has destroyed a building after getting a kill in the past 30 seconds</dd>
</dl>

### Sniper-Specific Context Criteria

<dl>
  <dt>SniperIsNotStillonFire</dt>
  <dd>Passes if player as Sniper has not said a line related to being on fire in the past 7 seconds</dd>
  <dt>SniperIsStillonFire</dt>
  <dd>Passes if player as Sniper has said a line related to being on fire in the past 7 seconds</dd>
  <dt>SniperNotAssistSpeech</dt>
  <dd>Passes if player as Sniper has not said a line thanking for a kill assist in the past 20 seconds</dd>
  <dt>SniperNotAwardSpeech</dt>
  <dd>Passes if player as Sniper has not said a line related to getting an achievement in the past 10 seconds</dd>
  <dt>SniperNotHoldStill</dt>
  <dd>Passes if player as Sniper has not muttered under his breath while looking at enemies in the past 10 seconds</dd>
  <dt>SniperNotInvulnerableSpeech</dt>
  <dd>Passes if player as Sniper has not said a line related to firing while invulnerable in the past 30 seconds</dd>
  <dt>SniperNotKillSpeech</dt>
  <dd>Passes if player as Sniper has not said a line related to getting a kill in the past 10 seconds</dd>
  <dt>SniperNotKillSpeechMelee</dt>
  <dd>Passes if player as Sniper has not said a line related to getting a melee kill in the past 10 seconds</dd>
  <dt>SniperNotSaidCartMovingBackwardD</dt>
  <dd>Passes if player as Sniper on defense has not said a line related to the cart moving back in the past 20 seconds</dd>
  <dt>SniperNotSaidCartMovingBackwardO</dt>
  <dd>Passes if player as Sniper on offense has not said a line related to the cart moving back in the past 20 seconds</dd>
  <dt>SniperNotSaidCartMovingForwardD</dt>
  <dd>Passes if player as Sniper on defense has not said a line related to the cart being pushed in the past 20 seconds</dd>
  <dt>SniperNotSaidCartMovingForwardO</dt>
  <dd>Passes if player as Sniper on offense has not said a line related to the cart being pushed in the past 20 seconds</dd>
  <dt>SniperNotSaidCartMovingStoppedD</dt>
  <dd>Passes if player as Sniper on defense has not said a line related to the cart stopping moving in the past 20 seconds</dd>
  <dt>SniperNotSaidCartMovingStoppedO</dt>
  <dd>Passes if player as Sniper on offense has not said a line related to the cart stopping moving in the past 20 seconds</dd>
  <dt>SniperNotSaidHealThanks</dt>
  <dd>Passes if player as Sniper has not said a line thanking for healing in the past 20 seconds</dd>
</dl>

### Soldier-Specific Context Criteria

<dl>
  <dt>SoldierIsNotStillonFire</dt>
  <dd>Passes if player as Soldier has not said a line related to being on fire in the past 7 seconds</dd>
  <dt>SoldierIsStillonFire</dt>
  <dd>Passes if player as Soldier has said a line related to being on fire in the past 7 seconds</dd>
  <dt>SoldierNotAssistSpeech</dt>
  <dd>Passes if player as Soldier has not said a line thanking for a kill assist in the past 20 seconds</dd>
  <dt>SoldierNotAwardSpeech</dt>
  <dd>Passes if player as Soldier has not said a line related to getting an achievement in the past 10 seconds</dd>
  <dt>SoldierNotInvulnerableSpeech</dt>
  <dd>Passes if player as Soldier has not said a line related to firing while invulnerable in the past 30 seconds</dd>
  <dt>SoldierNotKillSpeech</dt>
  <dd>Passes if player as Soldier has not said a line related to getting a kill in the past 10 seconds</dd>
  <dt>SoldierNotKillSpeechMelee</dt>
  <dd>Passes if player as Soldier has not said a line related to getting a melee kill in the past 10 seconds</dd>
  <dt>SoldierNotSaidCartMovingBackwardD</dt>
  <dd>Passes if player as Soldier on defense has not said a line related to the cart moving back in the past 20 seconds</dd>
  <dt>SoldierNotSaidCartMovingBackwardO</dt>
  <dd>Passes if player as Soldier on offense has not said a line related to the cart moving back in the past 20 seconds</dd>
  <dt>SoldierNotSaidCartMovingForwardD</dt>
  <dd>Passes if player as Soldier on defense has not said a line related to the cart being pushed in the past 20 seconds</dd>
  <dt>SoldierNotSaidCartMovingForwardO</dt>
  <dd>Passes if player as Soldier on offense has not said a line related to the cart being pushed in the past 20 seconds</dd>
  <dt>SoldierNotSaidCartMovingStoppedD</dt>
  <dd>Passes if player as Soldier on defense has not said a line related to the cart stopping moving in the past 20 seconds</dd>
  <dt>SoldierNotSaidCartMovingStoppedO</dt>
  <dd>Passes if player as Soldier on offense has not said a line related to the cart stopping moving in the past 20 seconds</dd>
  <dt>SoldierNotSaidHealThanks</dt>
  <dd>Passes if player as Soldier has not said a line thanking for healing in the past 20 seconds</dd>
  <dt>SoldierIsKillSpeechObject</dt>
  <dd>Unused in rules, passes if player as Soldier has destroyed a a building after getting a kill in the past 30 seconds</dd>
</dl>

### Spy-Specific Context Criteria

<dl>
  <dt>SpyIsNotStillonFire</dt>
  <dd>Passes if player as Spy has not said a line related to being on fire in the past 7 seconds</dd>
  <dt>SpyIsStillonFire</dt>
  <dd>Passes if player as Spy has said a line related to being on fire in the past 7 seconds</dd>
  <dt>SapperDestroyed</dt>
  <dd>Passes if player's Sapper was destroyed in the past 10 seconds</dd>
  <dt>ToysMurdered</dt>
  <dd>Passes if player as Spy destroyed a building in the past 5 seconds</dd>
  <dt>EngineerWasKilled</dt>
  <dd>Passes if player as Spy killed an Engineer in the past 5 seconds</dd>
  <dt>SpyNotKillSpeech</dt>
  <dd>Passes if player as Spy has not said a kill line in the past 10 seconds</dd>
  <dt>SpyNotKillSpeechMelee</dt>
  <dd>Passes if player as Spy has not said a line related to getting a melee kill in the past 10 seconds</dd>
  <dt>NotSapSpeech</dt>
  <dd>Passes if player as Spy has not said a line related to killing an Engineer after sapping a building in the past 10 seconds</dd>
  <dt>NotSapperLostSpeech</dt>
  <dd>Passes if player as Spy has not said a line related to killing an Engineer who removed the player's Sapper in the past 10 seconds</dd>
  <dt>SpyNotAssistSpeech</dt>
  <dd>Passes if player as Spy has not said a line thanking for a kill assist in the past 20 seconds</dd>
  <dt>SpyNotSaidHealThanks</dt>
  <dd>Passes if player as Spy has not said a line thanking for healing in the past 20 seconds</dd>
  <dt>SpyNotInvulnerableSpeech</dt>
  <dd>Passes if player as Spy has not said a line related to attacking while UberCharged in the past 30 seconds</dd>
  <dt>IsHelpCapSpy</dt>
  <dd>Passes if player as Spy has already asked for help capturing a point in the past 10 seconds</dd>
  <dt>SpyNotSaidCartMovingBackwardD</dt>
  <dd>Passes if player as Spy on defense has not said a line related to the cart moving back in the past 20 seconds</dd>
  <dt>SpyNotSaidCartMovingBackwardO</dt>
  <dd>Passes if player as Spy on offense has not said a line related to the cart moving back in the past 20 seconds</dd>
  <dt>SpyNotSaidCartMovingForwardD</dt>
  <dd>Passes if player as Spy on defense has not said a line related to the cart being pushed in the past 20 seconds</dd>
  <dt>SpyNotSaidCartMovingForwardO</dt>
  <dd>Passes if player as Spy on offense has not said a line related to the cart being pushed in the past 20 seconds</dd>
  <dt>SpyNotSaidCartMovingStoppedD</dt>
  <dd>Passes if player as Spy on defense has not said a line related to the cart stopping moving in the past 20 seconds</dd>
  <dt>SpyNotSaidCartMovingStoppedO</dt>
  <dd>Passes if player as Spy on offense has not said a line related to the cart stopping moving in the past 20 seconds</dd>
</dl>

### Capture Help Request Context Criteria

<dl>
  <dt>IsHelpCapDemoman</dt>
  <dd>Passes if player as Demoman has already asked for help capturing a point in the past 10 seconds</dd>
  <dt>IsHelpCapEngineer</dt>
  <dd>Passes if player as Engineer has already asked for help capturing a point in the past 10 seconds</dd>
  <dt>IsHelpCapHeavy</dt>
  <dd>Passes if player as Heavy has already asked for help capturing a point in the past 10 seconds</dd>
  <dt>IsHelpCapMedic</dt>
  <dd>Passes if player as Medic has already asked for help capturing a point in the past 10 seconds</dd>
  <dt>IsHelpCapPyro</dt>
  <dd>Passes if player as Pyro has already asked for help capturing a point in the past 10 seconds</dd>
  <dt>IsHelpCapScout</dt>
  <dd>Passes if player as Scout has already asked for help capturing a point in the past 10 seconds</dd>
  <dt>IsHelpCapSniper</dt>
  <dd>Passes if player as Sniper has already asked for help capturing a point in the past 10 seconds</dd>
  <dt>IsHelpCapSoldier</dt>
  <dd>Passes if player as Soldier has already asked for help capturing a point in the past 10 seconds</dd>
</dl>

### Halloween Context Criteria

<dl>
  <dt>SoldierNotIdleSpeech</dt>
  <dd>Passes if player has not said an idle Larval Lid line in the past 10 seconds</dd>
  <dt>HeavyNotFairyNoises</dt>
  <dd>Passes if player has not said a Grand Duchess line in some amount of time (depends on which line was said)</dd>
  <dt>SoldierNotRobotNoises</dt>
  <dd>Passes if player has not said an idle Tin Soldier line in the past 30 seconds</dd>
  <dt>MedicNotIdleSpeech</dt>
  <dd>Passes if player as Medic has not said an idle Second Opinion line in the past 10 seconds</dd>
  <dt>scoutNotZombieNoises</dt>
  <dd>Passes if player has not performed a zombie Scout line in the past 30 seconds</dd>
  <dt>soldierNotZombieNoises</dt>
  <dd>Passes if player has not performed a zombie Soldier line in the past 30 seconds</dd>
</dl>
