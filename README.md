# TuringFinale
Turing Final Project
% FinalProjectBV6.t
% The Final Project : Role Playing Game
% Game : The Journey to Oblivion
% Albert Quon & Kyler Lin
% Initialization Date : 5/18/2017
% Current Date : 6/6/2017
% Current Version : Beta 6 - Interaction Stages
% Use lunapic.com to use transparent pictures
% Laptop Screen Resoltion : 1366 x 768

% Screen Setting + Resolution + Centre Variables ------------------------------------------ Screen Setting
setscreen ("graphics:1366;768")
var CENTREX : int := maxx div 2
var CENTREY : int := maxy div 2
% Fonts ----------------------------------------------------------------------------------- FONTS
var font1, font2, font3 : int
font1 := Font.New ("Nueva Std:40")
font2 := Font.New ("Agency FB:30")
font3 := Font.New ("Nueva Std:20")
% Position Variables ---------------------------------------------------------------------- Position Variables
var x, y, buttonNumber, buttonupdown : int
% Arrays ---------------------------------------------------------------------------------- Arrays
var rareItems : array 1 .. 10 of string
var chars : array char of boolean
% Pictures -------------------------------------------------------------------------------- Pictures
var pic1, pic2, pic3 : int
var housePic, cavePic, mineShaftPic, bossCavePic, mons1Pic, mons2Pic, mons3Pic : int
var mineOre, mineOre2 : int
var bossPic : int

bossCavePic := Pic.FileNew ("bosscave.gif")
bossCavePic := Pic.Scale (bossCavePic, maxx, maxy)

mineOre := Pic.FileNew ("mineore.gif")
mineOre := Pic.Scale (mineOre, 200, 200)
mineOre2 := Pic.FileNew ("mineOre2.gif")
mineOre2 := Pic.Scale (mineOre2, 200, 200)

% Boolean -------------------------------------------------------------------------------------------------------------------------- Boolean
var timer, timer2, count : int := 0
var lastkeydown : array char of boolean
var ch : char

% Boolean Variables for loops ---------------------------------------------------------------------- Boolean Variables
var startMenuB : boolean := true % \\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\ TEMPORARY
var houseRoom, oceanRoom, caveRoom, bbossRoom, mainMapRoom, forestRoom, mineRoom : boolean := false
var characterRoom, leadboardB, exitMenuB, instructB, achieveB : boolean := false
% Achievements
var fishAchieve, fightAchieve, chopAchieve, bossAchieve, mineAchieve : boolean := false
% Character Pictures ------------------------------------------------------------------------- Character Pictures +  Mobs
var charcWar, charcMage, charcRang : int
% Sprites
var charcSpr, bossSpr, monsSpr, mons2Spr, mons3Spr : int

% Characters
% Warrior, Mage, Ranger + Default
charcWar := Pic.FileNew ("warrior.gif")
charcWar := Pic.Scale (charcWar, 300, 400)
charcMage := Pic.FileNew ("mage.gif")
charcMage := Pic.Scale (charcMage, 300, 300)
charcRang := Pic.FileNew ("ranger.gif")
charcRang := Pic.Scale (charcRang, 300, 400)
charcSpr := Sprite.New (charcWar)

% Boss
bossPic := Pic.FileNew ("dragon.gif")
bossPic := Pic.Scale (bossPic, 500, 500)
bossSpr := Sprite.New (bossPic)

% Monsters
mons1Pic := Pic.FileNew ("MonsterSprite.gif")
mons1Pic := Pic.Scale (mons1Pic, 300, 300)
monsSpr := Sprite.New (mons1Pic)
mons2Pic := Pic.Scale (mons1Pic, 200, 200)
mons2Spr := Sprite.New (mons2Pic)
mons3Pic := Pic.Scale (mons1Pic, 150, 150)
mons3Spr := Sprite.New (mons3Pic)
% Gameplay Variables -------------------------------------------------------------------------------------------Gameplay Variables

% Enemy Health
var mobHealth1, mobHealth2, mobHealth3, bossHealth : int
% Levels
var mineLevel, chopLevel, fishLevel, fightLevel, charc : int := 1
% Counts
var health, woodCount, fishCount, oreCount, itemCount : int := 0
% Total XP
var totalMine, totalChop, totalFish, totalFight : int := 0
% Achievement Score
var achieveScore : int := 0
% Mob Count
var mobCount : int := 0
% Boss Count
var bossCount : int := 0
% Random Variables
var mineXP, fishXP, chopXP, fightXP, playerDamage, mobDamage, randItem : int
% Health, Levels, and Interaction
bossHealth := 1000
mobHealth1 := 100
mobHealth2 := 300
mobHealth3 := 600
% Music

% Map + Background ------------------------------------------------------------------------------------------- PROCEDURES
% Functions/Subprograms
% User Menu -------------------------------------------------------------------------------------------------- User Menu

% Start Menu -------------------------------------------------------------------------------------------------- START
procedure startMenu

    cls
    pic1 := Pic.FileNew ("startmenupic.jpg")
    pic1 := Pic.Scale (pic1, maxx, maxy)
    Pic.Draw (pic1, 0, 0, picMerge)
    Font.Draw ("Journey of Oblivion", CENTREX - 170, 600, font1, black)
    Font.Draw ("Start Game", CENTREX - 80, 500, font2, 0)
    Font.Draw ("Instructions", CENTREX - 85, 400, font2, 0)
    Font.Draw ("Achievements", CENTREX - 94, 300, font2, 0)
    Font.Draw ("Highscores", CENTREX - 84, 200, font2, 0)
    Font.Draw ("Exit Game", CENTREX - 75, 100, font2, 0)

end startMenu
% Instructions ------------------------------------------------------------------------------------------------ INSTRUCTIONS
procedure instruct

    cls
    Font.Draw ("Instructions", CENTREX - 85, CENTREY + 250, font1, black)
    Font.Draw ("Movement", CENTREX - 570, CENTREY + 180, font3, black)
    Font.Draw ("- Press arrow keys to move your character around", CENTREX - 570, CENTREY + 120, font2, black)
    Font.Draw ("- Press the 'E' key to interact", CENTREX - 570, CENTREY + 80, font2, black)
    Font.Draw ("Choosing a character", CENTREX - 570, CENTREY + 20, font3, black)
    Font.Draw ("- Click on the character you want", CENTREX - 570, CENTREY - 40, font2, black)
    Font.Draw ("- Click the 'OK' button to confirm your choice", CENTREX - 570, CENTREY - 80, font2, black)
    Font.Draw ("Game", CENTREX - 570, CENTREY - 140, font3, black)
    Font.Draw ("- Complete as many achievements as possible", CENTREX - 570, CENTREY - 200, font2, black)
    Font.Draw ("- Collect rare items", CENTREX - 570, CENTREY - 240, font2, black)
    Font.Draw ("- Train your character", CENTREX - 570, CENTREY - 280, font2, black)
    Font.Draw ("- Have fun", CENTREX - 570, CENTREY - 320, font2, black)
    drawfillbox (CENTREX + 490, CENTREY - 350, CENTREX + 570, CENTREY - 270, green)

end instruct
% Leaderboard ------------------------------------------------------------------------------------------------ LEADERBOARD
procedure leadBoard
    cls
    Font.Draw ("Highscores", CENTREX - 85, CENTREY + 250, font1, black)
    Font.Draw ("1. Kyler......................................................................................................................19890", CENTREX - 400, CENTREY + 180, font2, black)
    Font.Draw ("2. Albert....................................................................................................................18203", CENTREX - 400, CENTREY, font2, black)
    Font.Draw ("3. Kelvin....................................................................................................................200", CENTREX - 400, CENTREY - 180, font2, black)
end leadBoard
% Achievements ------------------------------------------------------------------------------------------------ ACHIEVEMENTS
procedure achieve
    %Achievements

    cls
    Font.Draw ("Achievements", CENTREX - 85, CENTREY + 250, font1, black)
    if itemCount = 3 then
        Font.Draw ("Item Collector: Collect 3 rare items (10)", CENTREX - 570, CENTREY + 180, font2, brightgreen)
        achieveScore += 10
    else
        Font.Draw ("Item Collector: Collect 3 rare items (10)", CENTREX - 570, CENTREY + 180, font2, black)
    end if

    if chopLevel = 10 then
        Font.Draw ("Expert Woodcutter: Reach wood cutting level 10 (25)", CENTREX - 570, CENTREY + 130, font2, brightgreen)
        achieveScore += 25
    else
        Font.Draw ("Expert Woodcutter: Reach wood cutting level 10 (25)", CENTREX - 570, CENTREY + 130, font2, black)
    end if

    if fishLevel = 10 then
        Font.Draw ("Expert Fisher: Reach fishing level 10 (25)", CENTREX - 570, CENTREY + 80, font2, brightgreen)
        achieveScore += 25
    else
        Font.Draw ("Expert Fisher: Reach fishing level 10 (25)", CENTREX - 570, CENTREY + 80, font2, black)
    end if

    if mineLevel = 10 then
        Font.Draw ("Expert Miner: Reach mining level 10 (25)", CENTREX - 570, CENTREY + 30, font2, brightgreen)
        achieveScore += 25
    else
        Font.Draw ("Expert Miner: Reach mining level 10 (25)", CENTREX - 570, CENTREY + 30, font2, black)
    end if

    if chopAchieve = true then
        Font.Draw ("Getting wood: Chop your first tree (5)", CENTREX - 570, CENTREY - 20, font2, brightgreen)
        achieveScore += 5
    else
        Font.Draw ("Getting wood: Chop your first tree (5)", CENTREX - 570, CENTREY - 20, font2, black)
    end if

    if mineAchieve = true then
        Font.Draw ("Time to mine: Mine your first ore (5)", CENTREX - 570, CENTREY - 70, font2, brightgreen)
        achieveScore += 5
    else
        Font.Draw ("Time to mine: Mine your first ore (5)", CENTREX - 570, CENTREY - 70, font2, black)
    end if

    if fishAchieve = true then
        Font.Draw ("Delicious Fish: Catch your first fish (5)", CENTREX - 570, CENTREY - 120, font2, brightgreen)
        achieveScore += 5
    else
        Font.Draw ("Delicious Fish: Catch your first fish (5)", CENTREX - 570, CENTREY - 120, font2, black)
    end if

    if bossAchieve = true then
        Font.Draw ("Champion: Defeat the final boss (50)", CENTREX - 570, CENTREY - 170, font2, brightgreen)
        achieveScore += 50
    else
        Font.Draw ("Champion: Defeat the final boss (50)", CENTREX - 570, CENTREY - 170, font2, black)
    end if
    Font.Draw ("Your total achievement score is " + intstr (achieveScore), CENTREX - 570, CENTREY - 220, font2, black)


end achieve
% Exit + Credits ---------------------------------------------------------------------------------------- EXIT
procedure exitMenu
    % Exit Menu


    cls
    Font.Draw ("Thanks", CENTREX - 85, CENTREY + 250, font1, black)
    Font.Draw ("For Playing!", CENTREX - 115, CENTREY + 180, font1, black)
    Font.Draw ("Program Manager", CENTREX - 115, CENTREY + 40, font2, black)
    Font.Draw ("Albert Quon", CENTREX - 115, CENTREY, font3, black)
    Font.Draw ("Project Manager", CENTREX - 115, CENTREY - 100, font2, black)
    Font.Draw ("Kyler Lin", CENTREX - 115, CENTREY - 150, font3, black)

    % exit


end exitMenu
%  ------------------------------------------------------------------------------------------------ IN-GAME PROCEDURES ------------------------------------------------------------------------------
% Health
procedure hpBar

    drawfillbox (maxx - 230, 0, maxx, 80, brightgreen)
    Font.Draw ("HP: " + intstr (health), maxx - 200, 20, font1, white)
    % Note to change for HP changes, just add the procedure again
end hpBar

% House ---------------------------------------------------------------------------------------------- HOUSE
procedure house

    x := CENTREX - 100
    y := CENTREY
    Sprite.SetPosition (charcSpr, x, y, true)
    drawfillbox (CENTREX - 150, CENTREY - 100, CENTREX, CENTREY, 233)
    % Health Reset
    if totalFight >= 100 and totalFight < 200 then
        fightLevel := 2
        health := 200
    elsif totalFight >= 200 and totalFight < 350 then
        fightLevel := 3
        health := 300
    elsif totalFight >= 350 and totalFight < 500 then
        fightLevel := 4
        health := 400
    elsif totalFight >= 500 and totalFight < 750 then
        fightLevel := 5
        health := 500
    else
        health := 100
    end if


    % Environment
    housePic := Pic.FileNew ("houseInt.jpeg")
    housePic := Pic.Scale (housePic, maxx, maxy)
    Pic.Draw (housePic, 0, 0, picMerge)
    hpBar
    Font.Draw ("EXIT", CENTREX - 60, 100, font1, 120)
    % Back to Menu button
    drawfillbox (maxx - 200, maxy - 200, maxx, maxy, 230)
    Font.Draw ("MENU", maxx - 190, maxy - 150, font3, white)

end house
% Cave --------------------------------------------------------------------------- CAVE
procedure cave

    % Character Sprite Position
    cls
    x := maxx - 150
    y := maxy - 250
    Sprite.SetPosition (charcSpr, x, y, true)
    % Background + Entrance/Exit
    drawfillbox (0, 0, maxx, maxy, 23)
    drawfillbox (0, maxy - 200, maxx, maxy, 21)
    drawfillarc (maxx - 100, maxy - 210, 50, 200, 0, 180, 14)
    Sprite.Show (monsSpr)
    Sprite.Show (mons2Spr)
    Sprite.Show (mons3Spr)

    % Boss Room Entrance
    drawfillarc (100, maxy - 210, 50, 200, 0, 180, 18)

    % Monsters
    Sprite.SetPosition (monsSpr, 200, 200, true)
    Sprite.SetPosition (mons2Spr, CENTREX, CENTREY, true)
    Sprite.SetPosition (mons3Spr, maxx - 200, CENTREY - 100, true)
    % Fight Statements
    hpBar
end cave
% Boss Room ---------------------------------------------------------------------- B ROOM
procedure bossRoom

    % Character Sprite Position
    x := maxx - 200
    y := 100
    % Environment
    Sprite.Hide (monsSpr)
    Sprite.Hide (mons2Spr)
    Sprite.Hide (mons3Spr)
    cls
    Pic.Draw (bossCavePic, 0, 0, picMerge)
    Sprite.Show (bossSpr)
    Sprite.SetPosition (bossSpr, 250, 250, true)

    % Fight Statements
end bossRoom
% Mineshaft --------------------------------------------------------------------------- MINESHAFT
procedure mineshaft

    cls
    % Sprite Position
    x := maxx - 300
    y := maxy - 400
    Sprite.SetPosition (charcSpr, x, y, true)

    % Mineshaft
    % Background
    drawfillbox (0, 0, maxx, maxy, 23)
    drawfillbox (0, maxy - 350, maxx, maxy, 22)
    % Entrance/Exit
    drawfillbox (maxx - 260, maxy - 350, maxx - 150, maxy - 100, 92)
    drawfillbox (maxx - 300, maxy - 350, maxx - 260, maxy - 100, 233)
    drawfillbox (maxx - 150, maxy - 350, maxx - 110, maxy - 100, 233)
    drawfillbox (maxx - 330, maxy - 100, maxx - 80, maxy - 150, 233)
    Pic.Draw (mineOre, CENTREX, CENTREY, picMerge)
    Pic.Draw (mineOre2, CENTREX - 100, CENTREY - 200, picMerge)
    Pic.Draw (mineOre, 200, 200, picMerge)
    Pic.Draw (mineOre, 400, 400, picMerge)
    %Pic.Draw (mineOre2, maxx - 300, CENTREY - 300, picMerge)

    % Mining Statements

end mineshaft

% Fishing Ocean ------------------------------------------------------------------------- OCEAN
procedure ocean

    cls
    % Character Sprite Position
    x := 200
    y := CENTREY
    Sprite.SetPosition (charcSpr, x, y, true)
    % Sky
    drawfillbox (0, 0, maxx, maxy, 11)
    % Water
    drawfillbox (0, CENTREY - 200, CENTREX, CENTREY - 100, 138)
    % Dock
    drawfillbox (CENTREX - 100, CENTREY - 200, CENTREX - 150, 0, 138)
    drawfillbox (0, 0, maxx, 150, 55)
    drawfillbox (CENTREX - 300, CENTREY - 150, CENTREX - 250, 0, 138)
    % Sun
    drawfillarc (maxx, maxy, 200, 200, 180, 270, yellow)
    % Ripples to show fish
    drawoval (CENTREX + 100, 100, 50, 50, 53)
    drawoval (CENTREX + 100, 100, 20, 20, 53)
    drawoval (CENTREX + 100, 100, 5, 5, 53)
    drawoval (CENTREX + 100, 100, 30, 30, 53)

    % Fishing statements

end ocean

% Forest -------------------------------------------------------------------------------- FOREST
procedure forest

    cls
    % Sprite Position
    x := 100
    y := 100
    Sprite.SetPosition (charcSpr, x, y, true)
    % Sky
    drawfillbox (0, 0, maxx, maxy, 11)
    % Grass
    drawfillbox (0, 0, maxx, CENTREY, 47)
    % Sun
    drawfillarc (maxx, maxy, 200, 200, 180, 270, yellow)
    % Trees
    drawfillbox (maxx - 300, CENTREY, maxx - 280, CENTREY + 100, 186)
    drawfilloval (maxx - 290, CENTREY + 100, 50, 50, 120)
    drawfillbox (maxx - 200, CENTREY, maxx - 180, CENTREY + 120, 186)
    drawfilloval (maxx - 190, CENTREY + 120, 50, 50, 120)
    drawfillbox (maxx - 270, CENTREY, maxx - 250, CENTREY + 150, 186)
    drawfilloval (maxx - 260, CENTREY + 150, 50, 50, 119)
    drawfillbox (maxx - 340, CENTREY, maxx - 320, CENTREY + 80, 186)
    drawfilloval (maxx - 330, CENTREY + 80, 50, 50, 118)
    drawfillbox (maxx - 160, CENTREY, maxx - 140, CENTREY + 110, 186)
    drawfilloval (maxx - 150, CENTREY + 110, 50, 50, 118)
    drawfillbox (300, CENTREY, 280, CENTREY + 100, 186)
    drawfilloval (290, CENTREY + 100, 50, 50, 120)
    drawfillbox (200, CENTREY, 180, CENTREY + 120, 186)
    drawfilloval (190, CENTREY + 120, 50, 50, 120)
    drawfillbox (270, CENTREY, 250, CENTREY + 150, 186)
    drawfilloval (260, CENTREY + 150, 50, 50, 119)
    drawfillbox (340, CENTREY, 320, CENTREY + 80, 186)
    drawfilloval (330, CENTREY + 80, 50, 50, 118)
    drawfillbox (160, CENTREY, 140, CENTREY + 110, 186)
    drawfilloval (150, CENTREY + 110, 50, 50, 118)
    drawfillbox (CENTREX, 50, CENTREX + 100, CENTREY, 186)
    drawfilloval (CENTREX + 50, CENTREY + 100, 200, 200, 118)
    % Trees for chopping
    drawfillbox (CENTREX - 200, 50, CENTREX - 100, CENTREY - 100, 186)
    drawfilloval (CENTREX - 150, CENTREY - 100, 150, 150, 119)

    % Interaction Statements

end forest

% Main Map ---------------------------------------------------------------------------- MAIN MAP ------------------------------------------------------------
procedure mainMap

    cls
    % Character Sprite Position
    x := CENTREX
    y := CENTREY
    Sprite.SetPosition (charcSpr, x, y, true)

    % Ocean + Grass
    drawfillbox (0, 0, maxx, maxy - 100, 10)
    drawfillbox (0, maxy, maxx, maxy - 100, 102)
    Font.Draw ("Ocean", CENTREX - 50, maxy - 50, font1, white)
    Font.Draw ("Fishing", CENTREX - 40, maxy - 90, font3, white)
    % House
    drawfillbox (maxx - 400, CENTREY - 400, maxx - 100, CENTREY - 100, 115)
    drawfillbox (maxx - 300, CENTREY - 400, maxx - 200, CENTREY - 225, 114)
    drawfilloval (maxx - 225, CENTREY - 275, 8, 8, 44)
    Font.Draw ("House", maxx - 315, CENTREY - 175, font1, white)
    % Cave
    cavePic := Pic.FileNew ("cave.gif")
    cavePic := Pic.Scale (cavePic, 200, 150)
    Pic.Draw (cavePic, CENTREX - 500, CENTREY, picMerge)
    Font.Draw ("Cave", CENTREX - 480, CENTREY - 30, font1, white)
    Font.Draw ("Combat", CENTREX - 470, CENTREY - 60, font3, white)
    % Mineshaft
    mineShaftPic := Pic.FileNew ("mineshaft.gif")
    mineShaftPic := Pic.Scale (mineShaftPic, 200, 150)
    Pic.Draw (mineShaftPic, 0, 0, picMerge)
    Font.Draw ("Mineshaft", 40, CENTREY - 140, font1, white)
    Font.Draw ("Mining", 50, CENTREY - 170, font3, white)
    % Forest
    drawfillbox (maxx - 300, CENTREY, maxx - 280, CENTREY + 100, 186)
    drawfilloval (maxx - 290, CENTREY + 100, 50, 50, 120)
    drawfillbox (maxx - 200, CENTREY, maxx - 180, CENTREY + 120, 186)
    drawfilloval (maxx - 190, CENTREY + 120, 50, 50, 120)
    drawfillbox (maxx - 270, CENTREY, maxx - 250, CENTREY + 150, 186)
    drawfilloval (maxx - 260, CENTREY + 150, 50, 50, 119)
    drawfillbox (maxx - 340, CENTREY, maxx - 320, CENTREY + 80, 186)
    drawfilloval (maxx - 330, CENTREY + 80, 50, 50, 118)
    drawfillbox (maxx - 160, CENTREY, maxx - 140, CENTREY + 110, 186)
    drawfilloval (maxx - 150, CENTREY + 110, 50, 50, 118)
    Font.Draw ("Forest", maxx - 280, CENTREY - 40, font1, white)
    Font.Draw ("Woodcutting", maxx - 280, CENTREY - 70, font3, white)


end mainMap

% Character Design Background  ----------------------------------------------------------------------------  MENU ---------------------------------------
procedure characterCreate
    cls
    Font.Draw ("Choose Your Character", CENTREX - 150, CENTREY - 150, font2, blue)
    drawfillbox (100, CENTREY - 100, 500, CENTREY + 300, red)
    drawfillbox (CENTREX - 200, CENTREY - 100, CENTREX + 200, CENTREY + 300, blue)
    drawfillbox (maxx - 500, CENTREY - 100, maxx - 100, CENTREY + 300, green)
    Pic.Draw (charcWar, 120, CENTREY - 100, picMerge)
    Pic.Draw (charcMage, CENTREX - 150, CENTREY - 100, picMerge)
    Pic.Draw (charcRang, maxx - 420, CENTREY - 100, picMerge)
    drawfillbox (CENTREX - 100, 50, CENTREX + 100, 100, brightgreen)
    Font.Draw ("START", CENTREX - 50, 70, font3, 0)

end characterCreate

% Gameplay ----------------------------------------------------------------------------------------- GAMEPLAY



% Mining -------------------------------------------------------------------------- MINING
procedure mlevelUp

    if totalMine >= 100 and totalMine < 200 then
        mineLevel := 2
    elsif totalMine >= 200 and totalMine < 300 then
        mineLevel := 3
    elsif totalMine >= 300 and totalMine < 400 then
        mineLevel := 4
    elsif totalMine >= 400 and totalMine < 500 then
        mineLevel := 5
    end if

end mlevelUp

procedure mine
    if oreCount <= 15 then
        Font.Draw ("You have mined some coal!", CENTREX - 190, CENTREY + 270, font3, 92)
    elsif oreCount <= 30 then
        Font.Draw ("You have mined some copper!", CENTREX - 190, CENTREY + 270, font3, 92)
    elsif oreCount <= 45 then
        Font.Draw ("You have mined some iron!", CENTREX - 190, CENTREY + 270, font3, 92)
    else
        Font.Draw ("You have mined some gold!", CENTREX - 190, CENTREY + 270, font3, 92)
    end if
    totalMine := totalMine + mineXP
    mlevelUp
end mine
% Fishing -------------------------------------------------------------------------- FISHING

procedure fishlevelUp
    if totalFish >= 100 and totalFish < 200 then
        fishLevel := 2
    elsif totalFish >= 200 and totalFish < 300 then
        fishLevel := 3
    elsif totalFish >= 300 and totalFish < 400 then
        fishLevel := 4
    elsif totalFish >= 400 and totalFish < 500 then
        fishLevel := 5
    end if
end fishlevelUp

procedure fish

    if fishCount = 0 then
        Font.Draw ("You have caught nothing!", CENTREX - 190, CENTREY + 260, font3, 92)
    elsif fishCount <= 15 then
        Font.Draw ("You have caught trout!", CENTREX - 190, CENTREY + 260, font3, 92)
    elsif fishCount <= 30 then
        Font.Draw ("You have caught salmon!", CENTREX - 190, CENTREY + 260, font3, 92)
    elsif fishCount <= 40 then
        Font.Draw ("You have caught tuna!", CENTREX - 190, CENTREY + 260, font3, 92)
    else
        Font.Draw ("You have caught a lobster!", CENTREX - 190, CENTREY + 260, font3, 92)
    end if
    totalFish := totalFish + fishXP
    fishlevelUp
end fish

% Wood Cutting -------------------------------------------------------------------- WOOD CHOP

procedure chlevelUp
    if totalChop >= 100 and totalChop < 200 then
        chopLevel := 2
    elsif totalChop >= 200 and totalChop < 300 then
        chopLevel := 3
    elsif totalChop >= 300 and totalChop < 400 then
        chopLevel := 4
    elsif totalChop >= 400 and totalChop < 500 then
        chopLevel := 5
    end if
end chlevelUp

procedure chop
    if woodCount = 0 then
        Font.Draw ("You have cut down nothing!", CENTREX + 320, CENTREY + 260, font3, 92)
        chopXP := 0
    elsif woodCount <= 15 then
        Font.Draw ("You have cut down a branch!", CENTREX + 320, CENTREY + 260, font3, 92)
        randint (chopXP, 1, 3)
    elsif woodCount <= 30 then
        Font.Draw ("You have cut down half an oak log!", CENTREX + 320, CENTREY + 260, font3, 92)
        randint (chopXP, 6, 8)
    elsif woodCount <= 40 then
        Font.Draw ("You cut down an oak log!", CENTREX + 320, CENTREY + 260, font3, 92)
        chopXP := 9
    else
        Font.Draw ("You have cut down an ENTIRE oak tree!", CENTREX + 320, CENTREY + 260, font3, 92)
        chopXP := 10
    end if
    totalChop := totalChop + chopXP
    chlevelUp
end chop

% Combat --------------------------------------------------------------------------- COMBAT

procedure flevelUp

    if totalFight >= 100 and totalFight < 200 then
        fightLevel := 2
        health := 200
    elsif totalFight >= 200 and totalFight < 350 then
        fightLevel := 3
        health := 300
    elsif totalFight >= 350 and totalFight < 500 then
        fightLevel := 4
        health := 400
    elsif totalFight >= 500 and totalFight < 750 then
        fightLevel := 5
        health := 500
    else
        health := 100
    end if

end flevelUp

procedure fightMob1

    randint (fightXP, 10, 20)
    randint (playerDamage, 10, 20)
    randint (mobDamage, 20, 30)
    totalFight := totalFight + fightXP
    health := health - mobDamage
    mobHealth1 := mobHealth1 - playerDamage
    hpBar

end fightMob1

procedure fightMob2

    randint (fightXP, 20, 30)
    randint (playerDamage, 20, 30)
    randint (mobDamage, 30, 40)
    totalFight := totalFight + fightXP
    health := health - mobDamage
    mobHealth1 := mobHealth1 - playerDamage
    hpBar

end fightMob2

procedure fightMob3

    randint (fightXP, 40, 60)
    randint (playerDamage, 40, 60)
    randint (mobDamage, 50, 60)
    totalFight := totalFight + fightXP
    health := health - mobDamage
    mobHealth1 := mobHealth1 - playerDamage
    hpBar

end fightMob3
% Bosses ------------------------------------------------------------------------ BOSS

procedure bossFight

    randint (fightXP, 25, 50)
    randint (playerDamage, 50, 100)
    randint (mobDamage, 50, 100)
    totalFight := totalFight + fightXP
    health := health - mobDamage
    bossHealth := bossHealth - playerDamage
    hpBar

end bossFight

% Rare Items
procedure rItem
    randint (randItem, 1, 50)
end rItem








% MAIN ******************************************************************************************************* MAIN ************

% Start Menu
% startMenu
% instruct
% achieve
% leadboard
% exitmenu



% Interaction Statements


loop % outer game loop, loops through, checks which is true (one procedure only), other executions are false

    if startMenuB = true then
        startMenuB := false
        startMenu
        loop
            buttonwait ("down", x, y, buttonNumber, buttonupdown)
            if x > CENTREX - 100 and x < CENTREX + 80 and y > CENTREY + 120 and y < CENTREY + 200 then
                characterRoom := true
                exit
            end if
            if x > CENTREX - 100 and x < CENTREX + 80 and y > CENTREY + 20 and y < CENTREY + 100 then
                instructB := true
                exit
            end if
            if x > CENTREX - 100 and x < CENTREX + 80 and y > CENTREY - 80 and y < CENTREY then
                achieveB := true
                exit
            end if
            if x > CENTREX - 100 and x < CENTREX + 80 and y > CENTREY - 180 and y < CENTREY - 100 then
                leadboardB := true
                exit
            end if
            if x > CENTREX - 100 and x < CENTREX + 80 and y > CENTREY - 280 and y < CENTREY - 200 then
                exitMenuB := true
                exit
            end if
        end loop
    end if

    if instructB = true then
        instructB := false
        instruct
        % Back to start menu
        drawfillbox (maxx - 100, maxy - 75, maxx, maxy, green)
        Font.Draw ("Back", maxx - 75, maxy - 60, font3, black)
        loop
            buttonwait ("down", x, y, buttonNumber, buttonupdown)
            if x >= maxx - 100 and x <= maxx and y >= maxy - 75 and y <= maxy then
                startMenuB := true
                exit
            end if
        end loop
    end if

    if achieveB = true then
        achieveB := false
        achieve
        % Back to start menu
        drawfillbox (maxx - 100, maxy - 75, maxx, maxy, green)
        Font.Draw ("Back", maxx - 75, maxy - 60, font3, black)
        loop
            buttonwait ("down", x, y, buttonNumber, buttonupdown)
            if x >= maxx - 100 and x <= maxx and y >= maxy - 75 and y <= maxy then
                startMenuB := true
                exit
            end if
        end loop
    end if

    if leadboardB = true then
        leadboardB := false
        leadBoard
        % Back to start menu
        drawfillbox (maxx - 100, maxy - 75, maxx, maxy, green)
        Font.Draw ("Back", maxx - 75, maxy - 60, font3, black)
        loop
            buttonwait ("down", x, y, buttonNumber, buttonupdown)
            if x >= maxx - 100 and x <= maxx and y >= maxy - 75 and y <= maxy then
                startMenuB := true
                exit
            end if
        end loop
    end if

    if exitMenuB = true then
        exitMenu
        exit
    end if

    % ------------------------------------------------------------------- END OF START MENU------------------------------------
    if characterRoom = true then
        characterRoom := false
        characterCreate
        charcWar := Pic.Scale (charcWar, 300, 400)
        charcMage := Pic.Scale (charcMage, 300, 300)
        charcRang := Pic.Scale (charcRang, 300, 400)
        % Character Selection
        loop % If User clicks a character, it highlights the box and darkens the others
            buttonwait ("down", x, y, buttonNumber, buttonupdown)
            if charc = 0 then
                randint (charc, 1, 3)
            elsif x >= 100 and y >= CENTREY - 100 and x <= 500 and y <= CENTREY + 300 then
                charc := 1
                drawfillbox (100, CENTREY - 100, 500, CENTREY + 300, brightred)
                Pic.Draw (charcWar, 120, CENTREY - 100, picMerge)
                drawfillbox (CENTREX - 200, CENTREY - 100, CENTREX + 200, CENTREY + 300, blue)
                drawfillbox (maxx - 500, CENTREY - 100, maxx - 100, CENTREY + 300, green)
                Pic.Draw (charcMage, CENTREX - 150, CENTREY - 100, picMerge)
                Pic.Draw (charcRang, maxx - 420, CENTREY - 100, picMerge)
            elsif x >= CENTREX - 200 and y >= CENTREY - 100 and x <= CENTREX + 200 and y <= CENTREY + 300 then
                charc := 2
                drawfillbox (CENTREX - 200, CENTREY - 100, CENTREX + 200, CENTREY + 300, brightblue)
                Pic.Draw (charcMage, CENTREX - 150, CENTREY - 100, picMerge)
                drawfillbox (100, CENTREY - 100, 500, CENTREY + 300, red)
                Pic.Draw (charcWar, 120, CENTREY - 100, picMerge)
                drawfillbox (maxx - 500, CENTREY - 100, maxx - 100, CENTREY + 300, green)
                Pic.Draw (charcRang, maxx - 420, CENTREY - 100, picMerge)
            elsif x >= maxx - 500 and y >= CENTREY - 100 and x <= maxx - 100 and y <= CENTREY + 300 then
                charc := 3
                drawfillbox (maxx - 500, CENTREY - 100, maxx - 100, CENTREY + 300, brightgreen)
                Pic.Draw (charcRang, maxx - 420, CENTREY - 100, picMerge)
                drawfillbox (100, CENTREY - 100, 500, CENTREY + 300, red)
                Pic.Draw (charcWar, 120, CENTREY - 100, picMerge)
                drawfillbox (CENTREX - 200, CENTREY - 100, CENTREX + 200, CENTREY + 300, blue)
                Pic.Draw (charcMage, CENTREX - 150, CENTREY - 100, picMerge)
            elsif x >= CENTREX - 100 and y >= 50 and x <= CENTREX + 100 and y <= 100 then
                houseRoom := true
                % Characters
                if charc = 1 then
                    charcWar := Pic.Scale (charcWar, 150, 200)
                    charcSpr := Sprite.New (charcWar)
                elsif charc = 2 then
                    charcMage := Pic.Scale (charcMage, 150, 150)
                    charcSpr := Sprite.New (charcMage)
                elsif charc = 3 then
                    charcRang := Pic.Scale (charcRang, 150, 200)
                    charcSpr := Sprite.New (charcRang)
                end if

                exit
            end if
        end loop

    end if
    %------------------------------------------------------------------------------------------- END OF CHARACTER SELECT


    %--------------------------------------------------------------------HOUSE -----------------------
    if houseRoom = true then
        houseRoom := false
        house
        Sprite.Show (charcSpr)
        loop
            Input.KeyDown (chars)
            if chars (KEY_UP_ARROW) then
                y += 10
            end if
            if chars (KEY_RIGHT_ARROW) then
                x += 10
            end if
            if chars (KEY_LEFT_ARROW) then
                x -= 10
            end if
            if chars (KEY_DOWN_ARROW) then
                y -= 10
            end if
            delay (20)
            View.Update
            Sprite.SetPosition (charcSpr, x, y, true)

            if x >= CENTREX - 160 and y >= 0 and x <= CENTREX - 50 and y <= 200 then
                mainMapRoom := true
                exit
            end if
            if x >= maxx - 200 and y >= maxy - 200 then
                startMenuB := true
                Sprite.Free (charcSpr)
                exit
            end if
        end loop
    end if
    % end of house ---------------------------------------------------------------------------------------------


    % ------------------------------------------------------------------main Map -------------------------------
    if mainMapRoom = true then
        mainMapRoom := false
        mainMap
        loop         % main Map
            Input.KeyDown (chars)
            if chars (KEY_UP_ARROW) then
                y += 10
            end if
            if chars (KEY_RIGHT_ARROW) then
                x += 10
            end if
            if chars (KEY_LEFT_ARROW) then
                x -= 10
            end if
            if chars (KEY_DOWN_ARROW) then
                y -= 10
            end if
            delay (20)
            View.Update
            Sprite.SetPosition (charcSpr, x, y, true)
            if y > maxy - 100 then
                oceanRoom := true
                exit
            elsif x >= maxx - 340 and y >= CENTREY and x <= maxx - 150 and y <= CENTREY + 100 then
                forestRoom := true
                exit
            elsif x >= 0 and y >= 0 and x <= 200 and y <= 200 then
                mineRoom := true
                exit
            elsif x >= CENTREX - 500 and y >= CENTREY and x <= CENTREX - 300 and y <= CENTREY + 200 then
                caveRoom := true
                exit
            elsif x >= maxx - 300 and y >= 100 and x <= maxx - 100 and y <= 300 then
                houseRoom := true
                exit
            end if
        end loop
    end if
    % --------------------------------------------------------------------- END OF MAIN MAP --------------


    % -------------------------------------------------------------------------- OCEAN-------------
    if oceanRoom = true then
        oceanRoom := false
        ocean
        Sprite.Show (charcSpr)
        loop
            Input.KeyDown (chars)
            if chars (KEY_UP_ARROW) then
                y += 10
            end if
            if chars (KEY_RIGHT_ARROW) then
                x += 10
            end if
            if chars (KEY_LEFT_ARROW) then
                x -= 10
            end if
            if chars (KEY_DOWN_ARROW) then
                y -= 10
            end if
            delay (20)
            View.Update
            Sprite.SetPosition (charcSpr, x, y, true)
            if x <= 0 then
                x := CENTREX
                y := CENTREY
                mainMapRoom := true
                exit
            end if
            % Interaction, FISHING!! ----------------------------------------------------------------------------------- FISHING
            if x >= CENTREX - 150 and y <= maxy and x <= CENTREX + 100 then
                drawfillbox (CENTREX - 300, CENTREY + 150, CENTREX + 200, CENTREY + 300, 54)
                Font.Draw ("Press E to fish", CENTREX - 250, CENTREY + 225, font3, 93)
                fishAchieve := true
                Input.KeyDown (chars)
                if chars ('e') then

                    drawfillbox (CENTREX - 300, CENTREY + 150, CENTREX + 200, CENTREY + 300, 54)

                    Music.PlayFile ("Splash.mp3")
                    fish
                    Font.Draw ("You have gained " + intstr (fishXP) + " fishing XP", CENTREX - 190, CENTREY + 210, font3, 92)
                    Font.Draw ("Fishing Level : " + intstr (fishLevel), CENTREX - 190, CENTREY + 180, font3, 92)
                    delay (2000)
                    Input.Pause
                end if
            end if
        end loop
    end if
    % --------------------------------------------------------------------- END OF OCEAN --------


    % --------------------------------------------------------------------- FOREST --------------
    if forestRoom = true then
        forestRoom := false
        forest
        loop
            Input.KeyDown (chars)
            if chars (KEY_UP_ARROW) then
                y += 10
            end if
            if chars (KEY_RIGHT_ARROW) then
                x += 10
            end if
            if chars (KEY_LEFT_ARROW) then
                x -= 10
            end if
            if chars (KEY_DOWN_ARROW) then
                y -= 10
            end if
            delay (20)
            View.Update
            Sprite.SetPosition (charcSpr, x, y, true)
            if x >= 0 and y <= maxx and x <= 50 then
                mainMapRoom := true
                x := CENTREX
                y := CENTREY
                exit
            end if
            % Interaction, Wood Cutting!! --------------------------------------------------------------------------- WOOD CUTTING
            if x >= CENTREX - 300 and y <= maxy and x <= CENTREX + 300 then
                drawfillbox (CENTREX + 300, CENTREY + 150, CENTREX + 800, CENTREY + 300, green)
                Font.Draw ("Press E to chop the tree", CENTREX + 320, CENTREY + 225, font3, 93)
                chopAchieve := true
                Input.KeyDown (chars)
                if chars ('e') then
                    drawfillbox (CENTREX + 300, CENTREY + 150, CENTREX + 800, CENTREY + 300, green)
                    Font.Draw ("Spam E to chop the trees!", CENTREX + 320, CENTREY + 225, font3, 93)
                    timer2 := Time.Elapsed + 5000
                    woodCount := 0
                    for i : 1 .. maxint


                        timer := Time.Elapsed
                        lastkeydown := chars
                        Input.KeyDown (chars)
                        if chars ('e') and not lastkeydown ('e') then
                            woodCount += 1

                        end if

                        exit when timer > timer2

                        exit when woodCount = 50


                    end for

                    drawfillbox (CENTREX + 300, CENTREY + 150, CENTREX + 800, CENTREY + 300, green)
                    Font.Draw ("Timber!!!", CENTREX + 320, CENTREY + 225, font3, 93)
                    Music.PlayFile ("Chop.mp3")
                    chop
                    drawfillbox (CENTREX + 300, CENTREY + 150, CENTREX + 800, CENTREY + 300, green)
                    Font.Draw ("You have gained " + intstr (chopXP) + " chopping XP", CENTREX + 320, CENTREY + 210, font3, 92)
                    Font.Draw ("Woodcutting Level : " + intstr (chopLevel), CENTREX + 320, CENTREY + 180, font3, 92)

                    delay (2000)
                    Input.Pause
                end if

            end if
        end loop
    end if
    % --------------------------------------------------------------------- END OF FOREST --------------


    % --------------------------------------------------------------------- MINESHAFT --------------
    if mineRoom = true then
        mineRoom := false
        mineshaft
        loop
            Input.KeyDown (chars)
            if chars (KEY_UP_ARROW) then
                y += 10
            end if
            if chars (KEY_RIGHT_ARROW) then
                x += 10
            end if
            if chars (KEY_LEFT_ARROW) then
                x -= 10
            end if
            if chars (KEY_DOWN_ARROW) then
                y -= 10
            end if
            delay (20)
            View.Update
            Sprite.SetPosition (charcSpr, x, y, true)
            if x >= maxx - 300 and y >= maxy - 350 and x <= maxx - 150 and y <= maxy - 100 then
                mainMapRoom := true
                x := CENTREX
                y := CENTREY
                exit
            end if
            % Interaction, Mining!! -------------------------------------------------------------------------------------- MINING
            if y <= maxy and x <= CENTREX + 100 then
                drawfillbox (CENTREX - 300, CENTREY + 200, CENTREX + 200, maxy, 19)
                Font.Draw ("Press E to mine", CENTREX - 250, CENTREY + 250, font3, 93)
                mineAchieve := true
                Input.KeyDown (chars)
                if chars ('e') then
                    drawfillbox (CENTREX - 300, CENTREY + 200, CENTREX + 200, maxy, 19)
                    Font.Draw ("Press E to mine", CENTREX - 250, CENTREY + 250, font3, 93)
                    timer2 := Time.Elapsed + 5000
                    oreCount := 0
                    for i : 1 .. maxint


                        timer := Time.Elapsed
                        lastkeydown := chars
                        Input.KeyDown (chars)
                        if chars ('e') and not lastkeydown ('e') then
                            oreCount += 1

                        end if

                        exit when timer > timer2

                        exit when oreCount = 50


                    end for
                    mine
                    drawfillbox (CENTREX - 300, CENTREY + 200, CENTREX + 200, maxy, 19)
                    Music.PlayFile ("Mine.mp3")
                    Font.Draw ("You have gained " + intstr (mineXP) + " mining XP", CENTREX - 190, CENTREY + 240, font3, 92)
                    Font.Draw ("Mining Level : " + intstr (mineLevel), CENTREX - 190, CENTREY + 210, font3, 92)
                    Input.Pause
                end if
            end if
        end loop
    end if
    % --------------------------------------------------------------------- END OF MINESHAFT --------------


    % --------------------------------------------------------------------- CAVE --------------
    if caveRoom = true then
        cave
        caveRoom := false
        loop
            Input.KeyDown (chars)
            if chars (KEY_UP_ARROW) then
                y += 10
            end if
            if chars (KEY_RIGHT_ARROW) then
                x += 10
            end if
            if chars (KEY_LEFT_ARROW) then
                x -= 10
            end if
            if chars (KEY_DOWN_ARROW) then
                y -= 10
            end if
            delay (20)
            View.Update
            Sprite.SetPosition (charcSpr, x, y, true)
            if x >= 100 and y >= maxy - 210 and x <= 160 and y <= maxy then
                bbossRoom := true
                exit
            end if
            if x >= maxx - 300 and y >= maxy - 210 and x <= maxx and y <= maxy then
                mainMapRoom := true
                Sprite.Hide (monsSpr)
                Sprite.Hide (mons2Spr)
                Sprite.Hide (mons3Spr)
                x := CENTREX
                y := CENTREY
                exit
            end if
            % Interaction, Combat!! -------------------------------------------------------------------------------------- COMBAT


            % Monster 1 (Big) ------------------------------------------------------------------------------------- BIG MONSTER
            if x >= 50 and x <= 450 and y >= 50 and y <= 450 then
                drawfillbox (CENTREX - 300, CENTREY + 200, CENTREX + 200, maxy, 19)
                Font.Draw ("Press E to fight", CENTREX - 250, CENTREY + 250, font3, 93)
                Input.KeyDown (chars)
                if chars ('e') then
                    fightMob3
                    drawfillbox (CENTREX - 300, CENTREY + 200, CENTREX + 200, maxy, 19)
                    Music.PlayFile ("monsRoar.mp3")
                    if playerDamage <= 43 then
                        Font.Draw ("You have hit the arm!", CENTREX - 190, CENTREY + 270, font3, 92)
                    elsif playerDamage <= 46 then
                        Font.Draw ("You have hit the chest!", CENTREX - 190, CENTREY + 270, font3, 92)
                    elsif fightXP <= 49 then
                        Font.Draw ("You have hit the mouth!", CENTREX - 190, CENTREY + 270, font3, 92)
                    else
                        Font.Draw ("Critical Hit!", CENTREX - 190, CENTREY + 270, font3, 92)
                    end if
                    Font.Draw ("You have done " + intstr (playerDamage) + " damage", CENTREX - 190, CENTREY + 240, font3, 92)
                    Font.Draw ("Monster Health : " + intstr (mobHealth1), CENTREX - 190, CENTREY + 210, font3, brightred)
                    if mobHealth1 <= 0 then
                        flevelUp
                        Sprite.Hide (monsSpr)
                        mobHealth1 := 200
                        drawfillbox (CENTREX - 300, CENTREY + 200, CENTREX + 200, maxy, 19)
                        Font.Draw ("You have gained " + intstr (fightXP) + " experience", CENTREX - 190, CENTREY + 270, font3, 92)
                        Font.Draw ("Fighting Level : " + intstr (fightLevel), CENTREX - 190, CENTREY + 300, font3, 92)
                        mobCount += 1
                        hpBar
                    end if
                    if health <= 0 then
                        houseRoom := true
                        exit
                    end if
                    Input.Pause
                end if
            end if


            % Monster 2 (Med) ------------------------------------------------------------------------------------- MEDIUM MONSTER
            if x >= CENTREX - 100 and x <= CENTREX + 100 and y >= CENTREY - 100 and y <= CENTREY + 100 then
                drawfillbox (CENTREX - 300, CENTREY + 200, CENTREX + 200, maxy, 19)
                Font.Draw ("Press E to fight", CENTREX - 250, CENTREY + 250, font3, 93)
                Input.KeyDown (chars)
                if chars ('e') then
                    fightMob2
                    drawfillbox (CENTREX - 300, CENTREY + 200, CENTREX + 200, maxy, 19)
                    Music.PlayFile ("Fight.mp3")
                    if playerDamage <= 23 then
                        Font.Draw ("You have hit the arm!", CENTREX - 190, CENTREY + 270, font3, 92)
                    elsif playerDamage <= 25 then
                        Font.Draw ("You have hit the chest!", CENTREX - 190, CENTREY + 270, font3, 92)
                    elsif fightXP <= 28 then
                        Font.Draw ("You have hit the mouth!", CENTREX - 190, CENTREY + 270, font3, 92)
                    else
                        Font.Draw ("Critical Hit!", CENTREX - 190, CENTREY + 270, font3, 92)
                    end if
                    Font.Draw ("You have done " + intstr (playerDamage) + " damage", CENTREX - 190, CENTREY + 240, font3, 92)
                    Font.Draw ("Monster Health : " + intstr (mobHealth1), CENTREX - 190, CENTREY + 210, font3, 92)
                    if mobHealth1 <= 0 then
                        flevelUp
                        Sprite.Hide (mons2Spr)
                        mobHealth1 := 200
                        drawfillbox (CENTREX - 300, CENTREY + 200, CENTREX + 200, maxy, 19)
                        Font.Draw ("You have gained " + intstr (fightXP) + " experience", CENTREX - 190, CENTREY + 270, font3, 92)
                        Font.Draw ("Fighting Level : " + intstr (fightLevel), CENTREX - 190, CENTREY + 300, font3, red)
                        mobCount += 1
                        hpBar
                    end if
                    if health <= 0 then
                        houseRoom := true
                        exit
                    end if
                    Input.Pause
                end if
            end if


            % Monster 3 (Small) ------------------------------------------------------------------------------------- SMALL MONSTER
            if x >= maxx - 275 and x <= maxx - 125 and y >= CENTREY - 175 and y <= CENTREY - 25 then
                drawfillbox (CENTREX - 300, CENTREY + 200, CENTREX + 200, maxy, 19)
                Font.Draw ("Press E to fight", CENTREX - 250, CENTREY + 250, font3, 93)
                Input.KeyDown (chars)
                if chars ('e') then
                    fightMob3
                    drawfillbox (CENTREX - 300, CENTREY + 200, CENTREX + 200, maxy, 19)
                    Music.PlayFile ("Fight.mp3")
                    if playerDamage <= 13 then
                        Font.Draw ("You have hit the arm!", CENTREX - 190, CENTREY + 270, font3, 92)
                    elsif playerDamage <= 15 then
                        Font.Draw ("You have hit the chest!", CENTREX - 190, CENTREY + 270, font3, 92)
                    elsif fightXP <= 19 then
                        Font.Draw ("You have hit the mouth!", CENTREX - 190, CENTREY + 270, font3, 92)
                    else
                        Font.Draw ("Critical Hit!", CENTREX - 190, CENTREY + 270, font3, 92)
                    end if
                    Font.Draw ("You have done " + intstr (playerDamage) + " damage", CENTREX - 190, CENTREY + 240, font3, 92)
                    Font.Draw ("Monster Health : " + intstr (mobHealth1), CENTREX - 190, CENTREY + 210, font3, red)
                    if mobHealth1 <= 0 then
                        flevelUp
                        Sprite.Hide (mons3Spr)
                        mobHealth1 := 200
                        drawfillbox (CENTREX - 300, CENTREY + 200, CENTREX + 200, maxy, 19)
                        Font.Draw ("You have gained " + intstr (fightXP) + " experience", CENTREX - 190, CENTREY + 270, font3, 92)
                        Font.Draw ("Fighting Level : " + intstr (fightLevel), CENTREX - 190, CENTREY + 300, font3, 92)
                        mobCount += 1
                        hpBar
                    end if
                    if health <= 0 then
                        houseRoom := true
                        exit
                    end if
                    Input.Pause
                end if
            end if
        end loop
    end if
    % --------------------------------------------------------------------- END OF CAVE --------------


    % --------------------------------------------------------------------- BOSS ROOM --------------
    if bbossRoom = true then
        bbossRoom := false
        bossRoom
        hpBar
        loop
            Input.KeyDown (chars)
            if chars (KEY_UP_ARROW) then
                y += 10
            end if
            if chars (KEY_RIGHT_ARROW) then
                x += 10
            end if
            if chars (KEY_LEFT_ARROW) then
                x -= 10
            end if
            if chars (KEY_DOWN_ARROW) then
                y -= 10
            end if
            delay (20)
            View.Update
            Sprite.SetPosition (charcSpr, x, y, true)
            if y <= maxy and x <= CENTREX - 400 then
                drawfillbox (CENTREX - 300, maxy - 300, CENTREX + 200, maxy, 19)
                Font.Draw ("Press E to challenge the boss", CENTREX - 250, maxy - 250, font3, 93)
                Input.KeyDown (chars)
                if chars ('e') then
                    bossFight
                    drawfillbox (CENTREX - 300, maxy - 300, CENTREX + 200, maxy, 19)
                    Music.PlayFile ("monsRoar.mp3")
                    if playerDamage <= 15 then
                        Font.Draw ("You have struck the wing!", CENTREX - 190, maxy - 270, font3, 92)
                    elsif playerDamage <= 25 then
                        Font.Draw ("You have struck the horn!", CENTREX - 190, maxy - 270, font3, 92)
                    elsif playerDamage <= 45 then
                        Font.Draw ("You have struck the neck!", CENTREX - 190, maxy - 270, font3, 92)
                    else
                        Font.Draw ("You have hit the heart!", CENTREX - 190, maxy - 270, font3, 92)
                    end if
                    Font.Draw ("You have dealt " + intstr (playerDamage) + " damage", CENTREX - 190, maxy - 240, font3, 92)
                    Font.Draw ("Boss Health : " + intstr (bossHealth), CENTREX - 190, maxy - 210, font3, 92)
                    if bossHealth <= 0 then
                        flevelUp
                        Sprite.Hide (bossSpr)
                        Font.Draw ("Congratulations! You have earned " + intstr (fightXP), CENTREX - 190, maxy - 270, font3, 92)
                        bossAchieve := true
                    end if
                    if health <= 0 then
                        houseRoom := true
                        Sprite.Hide (bossSpr)
                        exit
                    end if
                    Input.Pause
                end if
            end if
        end loop
    end if
    % --------------------------------end of BOSS ROOM--------------------------
end loop         % outer game loop
% ************************************************************************************ END OF MAIN *******************************
