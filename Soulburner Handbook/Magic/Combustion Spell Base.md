Commonly used as a fire starter spell the spell creates a small explosion of fire. in its widespread form it creates a spark of fire within 5ft of the caster incapable of dealing direct damage no bigger than a match flame often used to light mundane objects like kindling or candle wicks. cost of 1 mp

spell variables:
damage die:
	0 = 0 mp
	d4 = 5 mp
	d6 = 7 mp
	d8 = 10 mp
	d10 = 12 mp
	d12 = 15 mp
```python
possibleDamageDie = [('0', 0), ('d4', 5), ('d6', 7), 
					 ('d8', 10), ('d10', 12), ('d12', 15)]
def dDieCost(dieSize='0'):  
    for dieCost in possibleDamageDie:  
        if dieSize in dieCost:  
            return dieCost[1]  
    return -999
```
Number of dice:
	(damage die cost+2) * # of dice
```python
	def costDieCount(dDieCost, dDieCount):  
    return (dDieCost + 2) * dDieCount
```
Range:
	range/5
```python
def costRange(castRange):  
    return castRange/5
```
Radius:
	(radius/5)^2
	If radius is <5 assume spell targets single square and add no extra cost
```python
def costRadius(radius):  
    if radius < 5:  
        return 0  
    else:  
        return radius / 5
```
Difficulty of save:
	base is 10+soul of caster reflex save
	For every +1 above base increase cost by (range/5)+(radius/5)
	If radius is <5 ignore it
	If spell has no damage die save cannot be increased
```python
def costSave(aboveBase, castRange, radius):  
    totalCost = 0  
    for i in range(aboveBase):  
        totalCost += costRange(castRange) + costRadius(radius)  
    return totalCost
```
Number of targets:
	Spell cost times * # of targets
	targets referring to point of casting not affected entities
```python
def costTarget(targetCount,spellCost):  
    return spellCost*targetCount
```
Save ranges:
	on crit success take no damage
	on success take half damage
	on fail take full damage
	on crit fail take full damage and be lit ablaze
final Calculation:
	(((die+2)X+(L/5)+(r/5)^2)+Y((r/5)+(L/5)))Z
	X = # of dice
	Y = # of +1 to difficulty save
	Z = number of targets
	L = range
	r = radius
```python
def spellCost(dDie,dDieCount,castRange,castRadius,incressDC,targetCount):  
  
    dieCost = dDieCost(dDie) # Cost of Dice Level  
    totalCost = costDieCount(dieCost, dDieCount) + dieCost # Cost for total Dice  
    spellRange = costRange(castRange) # Cost for spell Range  
    spellRadius = costRadius(castRadius) # Cost for Spell Radius  
    totalCost += (costSave(incressDC, spellRange, spellRadius)  
                  + spellRange + spellRadius) # Cost of DC Range and Radius added  
    totalCost += costTarget(targetCount, totalCost) # add cost per target  
    return totalCost 
     
    # It as a one liner  
    return costTarget(targetCount,(costSave(incressDC, costRange(castRange),                 costRadius(castRadius)) + costRadius(castRadius) + costRange(castRange) +              costDieCount(dDieCost(dDie), dDieCount) + dDieCost(dDie)))
```
examples:
	base fire starter: 
		((0+2)0+(5/5)+0(5/5))1 = 1
			==This result can only happen if Target count is only a multiplicative property of the end spell total however doing so makes a 0 target spell (Fire bolt is a range projectile not targeting space and has always been my low side not a lighter) result in a 0 cost spell so it must be a multiple that is added on making this result 2 and all others far higher==
		(((7+2)8+(150/5)+(20/5)^2)+Y((20/5)+(150/5)))1 = 118 + Y(46)
		w/reduced range 72+5+16+Y(4+5) = 93 + Y(9)
	dnd Firebolt:
		(((12+2)1+(120/5)+0)+Y(0+(120/5)))1 = 38 + Y(24)
		w/reduced range 14+9+0+Y(9 + 0) = 23 + Y(9)
			==Is a cost of 23 for baby's first combat fire not a problem?
			no space is being targeted a projectile is being formed so should have a target value of 0 also not a "small explosion"==
	dnd scorching ray:
		(((7+2)2+(120/5)+0)+Y((120/5)+0))3 =126+Y(72)
		w/reduced range (18+9+0+Y(9))3 = 81+Y(27)
			==The jump from a first to second level spell in dnd terms is 58 mana hot damn
			no space is being targeted a projectile is being formed so should have a target value of 0 also even further from being a "small explosion"==
Mana burn effects
	Tier 1 gain a burn
	Tier 2 roll on the fire wound table and start burning
		==aren't we already burning??==
	Tier 3 spontaneously combust and gain every wound from the fire table
		==The "Tier" System was not universal we ended on each spell having their own progression and systems for burn not just wound stacking. Epically with a spell base this intently broad of trying to do all fire (if you wanted just detonations as written why include firebolt and scorching ray and not a fireball or other flame blast effects) it makes it where if I wanted to use this base to light 100 candles in the theater as a commoner I fucking explode in some horrid ball of fire and die instantly==
