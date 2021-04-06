# DBS Zadanie 4

#### Meno hry napady 
(akoze je jedno ake meno to bude mat len nech to ma dobru skratku :D )  
Gods of the hunt (GOTH)  
Hunt of the year (HOTY)  


<br/>

## Registracia
##### EMAIL
 - email (overenie cez potvrdzovacie tlacidlo)
 - Pouzivatelske meno
 - real meno a priezvisko
 - Heslo (min 8znakov, 1 uppercase, 1cislo, 1specialny znak)
##### FACEBOOK
 - aplikacia si vytiahne z FB meno a email
 - pouzivatelske meno
 - heslo
##### GOOGLE
 - vytiahne si meno a email
 - pouzivatelske meno
 - heslo

_**USERS**_ = id, meno AS name, priezvisko AS last_name, email, overenie (1/0) AS verification, napojenie facebook as Facebook, napojenie google AS Google, odkaz na zahashovanu tabulku hesiel AS password

_**CHARACTERS**_ = id, userID, exp, roleID, abilityID, level, lives, attack_number, defense_number, coordinates, areaID

_**ROLES**_ = id, level_exp, max_level, level_lives_increase, level_attack_number_increase, level_defense_number_increase

_**ROLE_ABILITIES**_ = id, roleID, level, prerequired_abilityID

<br/><br/>
## Priatelstva
 - ked raz ma zamietnutu pozvanku na priatelstvo uz nevie poslat dalsiu tomu pouzivatelovi

_**FRIENDSHIPS**_ = id, userID_sender, userID_reciever, accepted (1/0),  rejected (1/0), ended (1/0), datetime as requested_at

<br/><br/>
## Timy
 - admin je aj v tabulke TEAMMATES a je automaticky accepted

_**TEAMS**_ = id, adminID, name, icon

_**TEAMMATES**_ = id, teamID, userID, created_at, accepted, rejected, ended

<br/><br/>
## Chat
 - ID reciever moze byt bud userID alebo teamID

_**MESSAGES**_: id, userID_sender, ID_reciever, text, created_at

<br/><br/>
## Ignore list
 - reciever je ten ktory je zablokovany a sender je ten co zablokoval

_**IGNORE_LIST**_ = id, userID_sender, userID_reciever, created_at

<br/><br/>
## Monsters

_**MONSTER_LIST**_ = id, start_level, end_level, prerequired_monster (references monsterID), taskID_prerequired_task, exp_reward

_**MONSTERS**_ = id, monsterID, characterID, lives (0 means kileld), attack_number (0 if killed), defense_number (0 if killed), coordinates (null if killed), areaID, killed_by (references characterID)

<br/><br/>
## Tasks

_**TASK_LIST**_ = id, areaID, killed_monsters_requirement, character_lvl, exp_reward

_**TASKS**_ = id, taskID, ownerID (REFERENCES characterID), started_at, finished_at (null if not finished)

_**AREA_LIST**_ = id, level, name, matrix

_**ITEM_LIST**_ = id, areaID, prerequired_kill (references monsterID), prerequired_task (references taskID), lives_increase, attack_number_increase, defense_number_increase, time_span

_**ITEMS**_ = id, ownerID (REFERENCES characterID), status (used = 1, unused=null), required_at, used_at

<br/><br/>
## Combat
 - ked character x monster tak player1 = caracter, player2 = null

_**COMBAT_LOG**_ = id, character1 (references characterID), character2 (references characterID), monster (references monsterID), areaID, winner (references characterID)

_**COMBAT_EVENTS**_ = id, combat_logID, characterID, exp_change, lives_change, created_at















