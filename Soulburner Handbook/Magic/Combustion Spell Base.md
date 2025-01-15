Commonly used as a fire starter spell the spell creates a small explosion of fire. in its widespread form it creates a spark of fire within 5ft of the caster incapable of dealing direct damage no bigger than a match flame often used to light mundane objects like kindling or candle wicks. cost of 1 mp

spell variables:
damage die:
	0 = 0 mp
	d4 = 5 mp
	d6 = 7 mp
	d8 = 10 mp
	d10 = 12 mp
	d12 = 15 mp
Number of dice:
	(damage die cost+2) * # of dice
Range:
	range/5
Radius:
	(radius/5)^2
	If radius is <5 assume spell targets single square and add no extra cost
Difficulty of save:
	base is 10+soul of caster reflex save
	For every +1 above base increase cost by (range/5)+(radius/5)
	If radius is <5 ignore it
	If spell has no damage die save cannot be increased
Number of targets:
	Spell cost times * # of targets
	targets referring to point of casting not affected entities
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
examples:
	base fire starter: 
		((0+2)0+(5/5)+0(5/5))1 = 1
	dnd fireball:
		(((7+2)8+(150/5)+(20/5)^2)+Y((20/5)+(150/5)))1 = 118 + Y(46)
		w/reduced range 72+5+16+Y(4+5) = 93 + Y(9)
	dnd Firebolt:
		(((12+2)1+(120/5)+0)+Y(0+(120/5)))1 = 38 + Y(24)
		w/reduced range 14+9+0+Y(9 + 0) = 23 + Y(9)
	dnd scorching ray:
		(((7+2)2+(120/5)+0)+Y((120/5)+0))3 =126+Y(72)
		w/reduced range (18+9+0+Y(9))3 = 81+Y(27)
Mana burn effects
	Tier 1 gain a burn
	Tier 2 roll on the fire wound table and start burning
	Tier 3 spontaneously combust and gain every wound from the fire table
