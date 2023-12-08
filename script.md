# dnd_test_project_1
This is the beginning 'rough draft' of a D&amp;D style combat encounter that I'm building in Python.

import matplotlib.pyplot as plt
import numpy as np
# A simulation of total damage output between a single 'player' and an 'enemy'

HP = 120 # HP stands for Health Points
d20 = np.random.randint(1,20) #the d stands for dice, so a d20 is a 20 sided die
d12 = np.random.randint(1,12)
d10 = np.random.randint(1,10)
d8 = np.random.randint(1,8)
d6 = np.random.randint(1,6)
d4 = np.random.randint(1,4)
ability_mods = {'str':5, 'dex':3, 'con':3, 'int':-1, 'wis':0, 'cha':1} #the modifiers that are added to the appropriate roll
prof_bonus = 4 # the extra bonus added to an 'attack roll'
great_axe = (d6 + d6)
AC = 16 # AC stands for Armor Class, or the number that must be met or exceeded to 'hit'
crit = (great_axe * 2)

enemy_outcome = []
player_outcome = []
enemy_HP = 100

for x in range(30) :
    pl_dice_role = np.random.randint(1,20)
    attack_role = pl_dice_role + ability_mods['str'] + prof_bonus #the dice roll and bonuses added to the total score against an AC
    if attack_role >= 16 :
        enemy_outcome.append('hit')
    else :
        enemy_outcome.append('miss')
dmg_delt = enemy_outcome.count('hit') * great_axe
if enemy_outcome == 20 : #trying to build in the chance of a critical hit happening.
    crit.replace(great_axe)
else :
    great_axe
enemy_health = enemy_HP - dmg_delt
print('enemy suffers:' + ' ' + str(dmg_delt) + ' ' +'damage')

for y in range(30) :
    enemy_weapon = (np.random.randint(1,8) + np.random.randint(1,8))
    enemy_crit = enemy_weapon*2
    enemy_attack = np.random.randint(1,20) + 6
    if enemy_attack >= AC :
        player_outcome.append('hit')
    else :
        player_outcome.append('miss')
player_dmg = player_outcome.count('hit') * enemy_weapon
if player_outcome == 20 :
    enemy_crit.replace(enemy_weapon)
else :
    enemy_weapon
player_health = HP - player_dmg
print('player suffers:' + ' ' + str(player_dmg) + ' ' + 'damage')

if player_health > enemy_health and player_health != 0 and player_health > 0 and player_health < HP :
    print('player wins and needs healing')
elif player_health == 0 :
    print('player is dead')
elif enemy_health > player_health and enemy_health != 0 and enemy_health > 0 and enemy_health < enemy_HP :
    print('enemy wins, but is wounded')
elif enemy_health == 0 :
    print('enemy is dead')
# I thought it would be fun to visualize how many times the 'player' and 'enemy' hit and miss each other
plt.hist(player_outcome, bins = 3, alpha = .75, color = 'blue', label = 'enemy')
plt.hist(enemy_outcome, bins = 3, alpha = .75, color='orange', label = 'player')
plt.legend(loc='center')
plt.show()
#something also interesting is noting the times when each character will miss more than the other but still do more damage.
