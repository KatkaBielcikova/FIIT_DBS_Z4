### Registracia
EMAIL
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

**USERS** = id, meno AS name, priezvisko AS last_name, email, overenie (1/0) AS verification, napojenie facebook as Facebook, napojenie google AS Google, odkaz na zahashovanu tabulku hesiel AS password

**CHARACTERS** = id, userID, exp, roleID, abilityID, level, lives, attack_number, defense_number, coordinates, areaID

**ROLES** = id, level_exp, max_level, level_lives_increase, level_attack_number_increase, level_defense_number_increase

**ROLE_ABILITIES** = id, roleID, level, prerequired_abilityID


### Priatelstva
 - ked raz ma zamietnutu pozvanku na priatelstvo uz nevie poslat dalsiu tomu pouzivatelovi

**FRIENDSHIPS** = id, userID_sender, userID_reciever, accepted (1/0),  rejected (1/0), ended (1/0), datetime as requested_at

### Timy
 - admin je aj v tabulke TEAMMATES a je automaticky accepted

**TEAMS** = id, adminID, name, icon

**TEAMMATES** = id, teamID, userID, created_at, accepted, rejected, ended

### Chat
 - ID reciever moze byt bud userID alebo teamID

**MESSAGES**: id, userID_sender, ID_reciever, text, created_at

### Ignore list
 - reciever je ten ktory je zablokovany a sender je ten co zablokoval

**IGNORE_LIST** = id, userID_sender, userID_reciever, created_at

### Monsters

**MONSTER_LIST** = id, start_level, end_level, prerequired_monster (references monsterID), taskID_prerequired_task, exp_reward

**MONSTERS** = id, monsterID, characterID, lives (0 means kileld), attack_number (0 if killed), defense_number (0 if killed), coordinates (null if killed), areaID, killed_by (references characterID)

### Tasks

**TASK_LIST** = id, areaID, killed_monsters_requirement, character_lvl, exp_reward

**TASKS** = id, taskID, ownerID (REFERENCES characterID), started_at, finished_at (null if not finished)

**AREA_LIST** = id, level, name, matrix

**ITEM_LIST** = id, areaID, prerequired_kill (references monsterID), prerequired_task (references taskID), lives_increase, attack_number_increase, defense_number_increase, time_span

**ITEMS** = id, ownerID (REFERENCES characterID), status (used = 1, unused=null), required_at, used_at

### Combat
 - ked character x monster tak player1 = caracter, player2 = null

**COMBAT_LOG** = id, character1 (references characterID), character2 (references characterID), monster (references monsterID), areaID, winner (references characterID)

**COMBAT_EVENTS** = id, combat_logID, characterID, exp_change, lives_change, created_at















