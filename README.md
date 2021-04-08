# DBS Zadanie 4

Tutorial na WorkBench:
https://www.youtube.com/watch?v=7Pwj7nV-oRM

#### Meno hry napady 
(akoze je jedno ake meno to bude mat meno len ma napadli nejake blbosti tak treba vybrat jedno :D )  
Gods of the hunt (GOTH)  
Hunt of the year (HOTY)  
Queens of the century (QOTC)  
Hunters and prey (HAP)


Veci co treba dorobit
==========
 - Neviem ako sa ukladaju hesla do databazy zatial som tam dala iba ze password



<br/>

## Registracia
##### EMAIL
 - email (overenie cez potvrdzovacie tlacidlo)
 - Pouzivatelske meno
 - realne meno a priezvisko
 - Heslo (min 8znakov, 1 uppercase, 1cislo, 1specialny znak)
##### FACEBOOK
 - aplikacia si vytiahne z FB meno a email
 - pouzivatelske meno
 - heslo
 - https://developers.facebook.com/docs/games/gaming-services/login/
 - https://developers.facebook.com/docs/games/gaming-services/enroll
##### GOOGLE
 - vytiahne si meno a email
 - pouzivatelske meno
 - heslo  
 - https://www.itsolutionstuff.com/post/php-and-mysql-login-with-google-account-exampleexample.html

 <br/>

Každý používateľ môže mať jeden alebo viac charakterov
 > _**USERS**_ = id, meno AS name, priezvisko AS last_name, email, overenie (1/0) AS verification, napojenie facebook as Facebook, napojenie google AS Google, odkaz na zahashovanu tabulku hesiel AS password  

### Characters

Pri vytváraní charakterov si používateľ musí vybrať rolu z listu. Každá rola má dostupné iné úlohy a iné objekty. V tabulke characters sa ukladajú súradnice o polohe pouzívateľa na základe čoho sa určuje blízkosť ostatných používateľov a príšer. 
 > _**CHARACTERS**_ = id, userID, exp, roleID, level, lives, attack_number, defense_number, coordinates_x, coordinates_y, areaID

### Roles 

Používateľ si môže vybrať zo zoznamu rolí. Každá rola má iný počet levelov potrebných na dosiahnutie levela s bossom. Medzi role patria:
 - Collector = na posun v leveloch a získanie exp musí postava pozbierať špecifické objekty
 - Warrior = na posun v leveloch musí poraziť čo najviac spoluhráčov
 - Monster Slayer = na posun v leveloch musí zabiť čo najviac príšer
 - Explorer = na posun v leveloch musí zabiť príšeru z každého druhu a pozbierať objekty z každého druhu
 - Adventurer = musi splnit najviac uloh co ho dostane do ciela  

 - . Treba doplniť a upravit tie role alebo upravit  


 > _**ROLES_LIST**_ = id, level_exp, max_level, level_lives_increase, level_attack_number_increase, level_defense_number_increase

### Abilities  

Podľa výberu role si používateľ vyberie schopnosť.
 - Collector = 2 * lives, 1/2 * attack_number, 2 * defense_number, 5/3 * rýchlosť pohybu, mapa blízkeho okolia na ktorej vidí objekty blízko neho
 - Warrior = 3 * lives, 4/3 * attack_number, viac možností objektov zbraní
 - Monster Slayer = 4/3 * attack_number, 5/3 * rýchlosť pohybu, viac možností objektov zbraní
 - Explorer = 2 * lives, 5/3 * rýchlosť pohybu, mapa blízkeho okolia na ktorej vidí objekty blízko neho
 - Adventurer = 
 > _**ABILITY_LIST**_ = id, roleID, level, prerequired_abilityID


 > _**ABILITIES**_ = id, abilityID, characterID

<br/><br/>
## Priatelstva
Používatelia môžu nadväzovať priateľstvá. Keďže usernames sú unikátne tak si vedia vuhľadať podľa pouívateľského mena svojho spoluhráča a poslať mu žiadosť o priateľstvo a následne spolupracovať a  vytvárať tímy. Pokiaľ má používateľ raz zamiestnutú pozvnánku na priateľstvo, už nevie poslať ďalšiu danému používateľovi.

 > _**FRIENDSHIPS**_ = id, userID_sender, userID_reciever, accepted (1/0),  rejected (1/0), ended (1/0), datetime as requested_at

<br/><br/>
## Timy
Používateľ sa môže rozhodnúť vytvoríť tím a pozvať do neho svojich priateľov. Týmto sa stane adminom tímu a je automaticky priradený to tabuľky teammates s parametrom accepted. Ak používateľ ktorý dostane pozvánku ju príjme tak je v tabuľke "teammates" vytvorený záznam z jeho ID. 

 > _**TEAMS**_ = id, adminID, name, icon

 > _**TEAMMATES**_ = id, teamID, userID, created_at, accepted, rejected, ended

<br/><br/>
## Chat
Pocas hrania hry mozu pouzivatelia pouzivat chat. Pouzivatelia mozu chatovat iba so svojimi priatelmi alebo so svojim timom.

 > _**MESSAGES**_: id, userID_sender, userID_reciever, teamID_reciever, text, created_at

<br/><br/>
## Ignore list
Používateľ má možnosť zablokovať druhého používateľa ktorý mu už nebude schopný posielať žiadosti alebo správy.  
Reciever je ten ktory je zablokovany a sender je ten co zablokoval recievera.

 > _**IGNORE_LIST**_ = id, userID_sender, userID_reciever, created_at

<br/><br/>
## Monsters
V hre sa nachádzajú príšery rôznych druhov. Každá príšera má svoje meno a rozsah levelov na ktorých sa zobrazuje používateľovi. Medzi príšery patria napríklad:

 - Anger Minion - These exploding minions are made of scorched rock with only magma holding the brittle pieces together
 - Behemoth - a giant elephant that could drink an entire river, and its strength was significant
 - Apep - giant snakel with venoumos skin/claws 
 - Ophanim - angels of devil, they could see through every object infront of them and can only be destroyed from behind
 - Gluttony Minions - they attacked in groups, Upon being destroyed, it would explode and leave behind a puddle of filth which could damage 
 - Gorger Worm -  If an unwary victim moves close to its burrow, they instantly rise up and attempt to devour it. They rise from the ground when you lures them out from the dusty area, trying to snap you.
 - Glutton -  attack by either vomiting on their foes, obese with jaws for hands, sagging mouths on their necks just below their ears and minds reduced to that of apes and eating anything that they came across
 - Hoarder/Waster - this pair of souls, one who hoarded in life and one who wasted are now melded into a singular creature, they swing around in a circle, tossing coins when they became threatened 
 - Greed Minion -  extremely swift and evasive and appeared to shimmer like gold. They jump back and forth before attempting a leap attack
 - Throne Demon -  gilded armor and are armed with a shield in one hand and a massive axe in the other
 - Fire guardian - So long as these foes are in their smoke form, they are completely invincible to any kind of attack. Only when they are briefly in their fire forms, can they be extinguished by a strong blast from the Cross
 - Leviathan - double-thick armor running down its back and muscular body, its skin tough as stone, giantic water lizard 
 -  Heretic - warlocks in hell, their only power is energy shields that they can also use on other minions and blocked all magic and attacks, they are imune to cross, they can be destroyed by a special weapon 
 -  Pagan - priests who carried a staff that could attack from a distance by firing balls of magical energy, easier to kill than herectic, no special weapon neeeded
 -  Fiend - large flying blue haired bat like creature covered in fish scales and a lizards tail with the power to blast unblockable, icy projectiles, appear in large groups
 - Arch Demon -  winged and armed with a pair of swords, 
 - Damned Crusader - Their shields and armor are fragmented and their blades long since became rusted.
 - Damned Captain - Leaders of crusaders,  They could engulf their shields in flames which would make them immune to attacks by a special weapon
 - Malacoda -  wingless creature with shield of flames that surrounded them with a fiery protection, that can be reduced by cross 
 - Ice giants - massive and humanoid creatures, confined to the icy gates surrounding Hell and they are unable to move though they are capable of seeing and  blowing their icy breath

 > _**MONSTER_LIST**_ = id, name, start_level, end_level, prerequired_monster (references monsterID), taskID_prerequired_task, exp_reward

 > _**MONSTERS**_ = id, monsterID, lives (0 means kileld), attack_number (0 if killed), defense_number (0 if killed), coordinates (null if killed), areaID, killed_by (references characterID)

<br/><br/>
## Tasks
V hre sa nachadzaju ulohy ktore je splnaju postavy na postup v leveloch a ziskanie exp. Kazda rola postavy ma ine ulohy. Najviac ich ma rola typu adventurer. Medzi zakladne ulohy patria naprikad:

 - [ ] **TODO** Vymysliet nejake ulohy

 > _**TASK_LIST**_ = id, areaID, preprequired_monster_kill, prerequired_task, character_lvl, exp_reward

 > _**TASKS**_ = id, taskID, ownerID (REFERENCES characterID), started_at, finished_at (null if not finished)

<br/><br/>
## Mapa
Hra sa odohrava na mape. Pouzivatelia vidia iba ostatnych pouzivatelov ktori sa nachadzaju v danej oblasti podla levelu. Kazda oblast sa teda viaze iba na prislusny level. V danej oblasti sa nachádzajú iba príšery a objekty prislúchajúce danému levelu. Medzi základné oblasti patria napríklad:

![alt text](Obrazky/limbo_small.jpg)  
#### lvl.1: Limbo
  - Anger Minion 
  - Behemoth  

![alt text](Obrazky/lust_small.jpg)   
####  lvl.2: Lust
  - Apep 
  - Ophanim    

![alt text](Obrazky/glutony_small.jpg)  
####  lvl.3: Gluttony
  - Gluttony Minions
  - Gorger Worm 
  - Glutton  

![alt text](Obrazky/greed_small.jpg)  
####  lvl.4: Greed
  - Hoarder/Waster
  - Greed Minion 
  - Throne Demon  

![alt text](Obrazky/anger_small.jpg)  
####  lvl.5: Anger
  - Fire guardian
  - Leviathan  

![alt text](Obrazky/hoax_small.jpg)  
####  lvl.6: Heresy
  -  Heretic 
  -  Pagan 
  -  Fiend  

![alt text](Obrazky/violence_small.jpg)  
####  lvl.7: Violence
  - Arch Demon
  - Damned Crusader 
  - Damned Captain   

![alt text](Obrazky/fraud_small.jpg)  
####  lvl.8: Fraud
  - Malacoda   

![alt text](Obrazky/betrayal_small.jpg)  
####  lvl.9: Treachery
  - Ice giants   

 > _**AREA_LIST**_ = id, level, name, matrix

<br/><br/>
## Objekty
Na mape sa nachadzaju objekty ktore sluzia bud na zberatelske ucely (bud na splnenie ulohy alebo naplnenie svojej role) alebo zbrane a brnenie alebo potions a amulety ktoré poskytujú používateľovi dočasné schopnosti. Medzi základné objekty patria napríklad:
Zberateľské účely:
 - Map of treasures (používateľ vidí okolo seba objekty ktoré by bez mapy nenašiel)
 - Mermaids scale (nemá špeciálnu silu) 

Zbrane a brnenie:
 - Smaugs tooth (slúži ako ochrana hlavy, 9/10 * defense_number)
 - Excalibur (2 * attack_number)

Potions and amulets:
 - Potion of immortality (po vypití 1minúta)
 - Potion of enemy vision (po vypití vidí použivateľ po dobu 1nej minúty okolo seba všetkých používateľov a príšery nachádzajúce sa aj za objektami v jeho blízkosti)

 > _**ITEM_LIST**_ = id, areaID, prerequired_kill (references monsterID), prerequired_task (references taskID), lives_increase, attack_number_increase, defense_number_increase, time_span (ako dlho to mozes mat u seba)

 > _**ITEMS**_ = id, ownerID (REFERENCES characterID), status (used = 1, unused=null), required_at, used_at, time_span

<br/><br/>
## Combat
Počas hry sa zaznamenávajú všetky udalosti na vytváranie štatistík. Vrámci zaznamenávania udalostí je relevantný údaj či sa v boji nachádza používateľ vs. pouívateľ alebo používateľ vs. príšera.   

 > _**COMBAT_LOG**_ = id, character1 (references characterID), character2 (references characterID), monster (references monsterID), areaID, winner (references characterID), started_at, finished_at

 Monster môže byť null alebo character môže byť null podľa toho komu patrí event.
 > _**COMBAT_EVENTS**_ = id, combat_logID, characterID, monster, exp_change, lives_change, created_at
