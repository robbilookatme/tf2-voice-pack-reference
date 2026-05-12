# TF2 Voice Pack Reference

This is a collection of spreadsheets in .csv format detailing each audio file used in the game Team Fortress 2, sorted by class along with other categories. This information is formatted in such a way to make it as easy as possible to create voice packs replacing character dialogue. Also included is this same information stored in .json format, if you want to investigate it yourself programatically.

### Dialogue System Summary

When a game event happens, like getting a kill or capturing a point, the game checks a set of predefined rules to see if the game state matches any rule's criteria. If so, the rule triggers a response, which plays a choreography scene, which plays a soundscript event, which plays an audio file. You can look at it like this:

(game action) -> (rule) -> (response) -> (scene) -> (soundscript event) -> (audio file)

For example:

(Player uses Help voice command as Scout) ->
(Rule with criteria "did use Help voice command" and "is playing as Scout" plays response) ->
(Response plays a choreography scene) ->
(Scene plays a soundscript event) ->
(Event plays an mp3 file) ->
Scout (ingame): "Help!"

### Spreadsheet Format

The spreadsheet (.csv) files will contain the following data:

|   |       A        |                        B                        |         C          |              D               |
|---|----------------|-------------------------------------------------|--------------------|------------------------------|
| 1 | Filename:      | (filename)                                      | Events:            | (list of soundscript events) |
| 2 | Full Path:     | (full filename with extension)                  | Scenes:            | (list of scenes)             |
| 3 | Transcription: | (line transcription)                            | Responses:         | (list of responses)          |
| 4 | Your Line:     | (empty space to type your dialogue, if desired) | Rules:             | (list of rules)              |
| 5 | (line usage)   | Criteria:                                       | (list of criteria) |                              |

For writing new dialogue, what matters most is the sets of criteria, which tell you the situations in which a line is used.

To save space, the Responses list also contains the names of taunts which use the voiceline in question.

The (line usage) cell will contain "Unused?" if the line is in the TF2 files, but is not called by any soundscript, and will contain "Missing?" if the file is called by a soundscript but does not exist in the TF2 files.

Note that a file that is marked unused, it may still be called by engine code or maps.

### JSON Format
```
{
    "path/to/audio/file.mp3": {
        "base_name" : "(filename with no containing folders or file extension)",
        "criteria" : [
            [
                "Criteria1",
                "Criteria2",
                etc
            ],
            etc
        ],
        "events" : [
            "EventName1",
            etc
        ],
        "scenes" : [
            "path/to/scene/file.vcd",
            etc
        ],
        "responses" : [
            "ResponseNameOne",
            etc
        ],
        "rules" : [
            "RuleNameOne",
            etc
        ],
        "state": ("used" if file is used,
                  "unused" if sound file exists in TF2 data but is not called by any soundscript event
                  "missing" if sound file is called by a soundscript event but doesn't exist in TF2 data),
        "transcription": "(transcription of dialogue line, if such a transcription exists on the TF2 wiki)"
    },
    etc
}
```

### Sorting

For each class's .csv file, the lines are sorted in the following way:

1. Regular gameplay lines
2. MvM lines
3. Contract-related lines
4. Taunt Item lines
5. Scream Fortress lines
6. Halloween-limited item lines
7. Competitive mode lines

Within groups, lines are sorted alphabetically by filename.

### How Dialogue Works

There are four steps to the dialogue process: rules, responses, choreography scenes, and soundscripts. Rules are sets of criteria based on game state. Rules trigger responses, which play choreography scenes, which play soundscript events. Soundscripts define events that play a sound file. When a game event happens (getting a kill, building a sentry, taking damage, etc.), the game chooses a rule based on which one has the most matching criteria. Note that in TF2, a rule is discarded at this step if ANY of its criteria do not match. The chosen rule has an attached response, and that response has a list of choreography scenes it can play. One scene is chosen either randomly or sequentially, depending on how the response is configured (all TF2 responses are set to random). A choreography scene can play one or more soundscript events. These events are defined in soundscripts, and can play an audio file from disk or can choose one randomly from a list of audio files.

A brief summary of one dialogue event is as follows:
* Imagine you are a Spy. You kill a Scout, and this kill results in you getting a Domination.
* The game triggers rule checks for certain events. In this case, getting a kill causes the game to look for matching rules. The rule "PlayerKilledDominatingScoutSpy" has the following criteria:
  * ConceptKilledPlayer - you just killed a player
  * IsSpy - you are playing as Spy
  * IsVictimScout - the person you killed was a Scout
  * IsDominated - this kill earned a domination
* This rule is selected because all its criteria match, and no other rules have more matching criteria.
* This rule triggers its attached response, also named "PlayerKilledDominatingScoutSpy". Most rules have the same name as their paired response, but this is not necessarily required.
* The response "PlayerKilledDominatingScoutSpy" chooses one of the following scenes at random:
  * scenes/Player/Spy/low/3011.vcd
  * scenes/Player/Spy/low/3043.vcd
  * scenes/Player/Spy/low/3044.vcd
  * scenes/Player/Spy/low/3045.vcd
  * scenes/Player/Spy/low/3046.vcd
  * scenes/Player/Spy/low/3047.vcd
  * scenes/Player/Spy/low/3048.vcd
  * scenes/Player/Spy/low/3049.vcd
* Let's say the first scene is chosen. The scene "scenes/Player/Spy/low/3011.vcd" performs two actions: making the Spy have an amused expression, and playing the soundscript event "Spy.DominationScout01".
* "Spy.DominationScout01" is a soundscript event defined in game_sounds_vo.txt. This event only has one sound file it can play, "vo/spy_DominationScout01.mp3".
* The file "vo/spy_DominationScout01.mp3" is played from the game files, which contains Spy saying "well, off to visit your mother!"

As you can see, while there are many steps in the process, dialogue can typically be paired to a set of criteria that trigger it. Since this line isn't used anywhere else, we can confidently say that the only way to hear the line "well, off to visit your mother!" is to get a dominating kill against a Scout as Spy. Conversely, if you were to get a dominating kill against a Scout as Spy, we know one of the possible outcomes is this line. By automating the process of teasing out the chain of rules to responses to scenes to events, we can construct a list of every voice line in the game and the exact circumstances in which they are spoken.

You might ask, why is this system so complicated? Why are there so many steps involved in playing a simple sound file? The answer is different for each step. Response-rule files exist to permit dialogue writers to have a hand in the dialogue system without having to learn how it's programmed. Choreography files are very complex, allowing for full scripted sequences with precise timing. They are used in TF2 for dialogue as lines spoken by characters ingame have lip-syncing, and some also trigger gestures, like a thumbs up for the "Thanks!" voice command. Sound files are wrapped in soundscripts for several reasons. The first is that soundscripts allow custom options for sound files, like volume. Another is that soundscript events can be configured to play one of several lines, like having "Weapon_Knife.HitFlesh" play one of three different sounds when a knife hits a player. All of this information is in files on disk rather than in the compiled executable, meaning data can be reloaded with a restart or even a reload command rather than needing a recompile.

### Motivation

I was creating my own voice pack by hand, using the TF2 wiki to determine where lines were used. However, the wiki groups dialogue information by when the lines are spoken, not by each line itself, because that's what the average player is interested in. I found that many dialogue lines were reused for different game events, and that some of what I had written did not make sense in every circumstance in which the line appeared.
Someone turned me onto soundscripts, saying they gave more control than just replacing sound files. This is true, with one big asterisk: player-edited soundscripts work ONLY for sounds played client-side and not in the game world, such as hit sounds, user interface sounds, the administrator, etc. This meant they could not be used for my purposes. This gave me the idea, though: if I knew how the dialogue system worked, I would understand where soundscript events were called, and would be able to write dialogue that actually fit most of the places they're used. This led me to learn not just how the entire dialogue system works, but also find several issues with the choreography files, the rule-response files, soundscript files, the TF2 wiki, and with the game's code itself. At this point, I figure I have some kind of responsibility to share this information, if for no other reason than to prevent someone from going down the same rabbit holes I did.

### Notes

Many scenes are not called by the rule-response system, but are instead played directly by taunts. This information can be found in the item schema file, "scripts/items/items_game.txt". Look for any line with ".vcd" to find where scene information is stored.

The rule-response system loads "scripts/talker/response_rules.txt". This file contains #include lines that pull in other files in the "scripts/" folder.

The choreography system does not actually load scene (.vcd) files, and scene files are not distributed with the game. Rather, there is a file called "scenes.image", which is a compressed form of the scene files the game uses, intended for optimization on optical format media. The game essentially uses the scene filename as a key into this file to find the corresponding scene data. This file can be decompressed using VSIF2VCD, though I was unable to test if that works on TF2 due to being on Linux. Instead, I used vsif2vcd.py by drobotk. (Actually, my first attempt involved editing the SDK myself to export all the scene files, which worked for scenes called by responses but did not cover scenes called by taunts). You can read about scenes.image on the Valve Developer Community Wiki.

Soundscripts are called from "scripts/game_sounds_manifest.txt", which loads other soundscript files. Note that there are four files that are loaded not from this file, but whose filenames are hardcoded into the game and loaded when joining an MvM map:
* scripts/mvm_level_sounds.txt
* scripts/mvm_level_sound_tweaks.txt
* scripts/game_sounds_vo_mvm.txt
* scripts/game_sounds_vo_mvm_mighty.txt

As mentioned above, custom soundscripts do not work when connected to servers, save for client-side sounds like user interface noises and hit sounds. To be more accurate, aside from the aforementioned client-side sounds, soundscript events are determined by the server and not the client. This means that if you host a game from the "Create Server" dialog on the main menu, your custom soundscripts WILL work, as well as custom rule-response files! This also applies to hosting dedicated servers, meaning your server can change, add, or remove the game's rules, responses, and soundscript events! Note that you CANNOT add new audio this way, at least not audio that other players can hear. Sound files in the tf/custom folder on the server are not automatically synced, so you have to add them through some other method. Custom sounds are a staple of many TF2 servers, but how to activate them through soundscripts is left as an exercise for the reader.

The ConceptPlayerExpression criteria fires every time a player model's facial expression updates. This is used in two circumstances. The first is for Halloween items like the Larval Lid, any Voodoo-Cursed Soul, or The Second Opinion, where it is used to randomly play lines while the player isn't doing anything in particular. The second is when the Sniper is aiming at a player, which causes him to mutter under his breath about something Australian probably. This criteria is unique in that it fires as soon as any choreography scene ends, including one triggered by a rule with this very critiera. In practice, that means that TF2's base dialogue lines which are triggered by the ConceptPlayerExpression criteria are timed out exactly in the choreography scenes, and any custom lines which are longer than the originals will be cut off.

Please keep in mind that this information is collected from the game files, and in-game results may not reflect the data collected here exactly. I have done my best to confirm information collected here through code inspection and actual testing, but I encourage you to test this information yourself in-game.

### Thanks

Thank you to Valve and the TF team, especially the voice actors (whose extremely funny performances made this project bearable) and whichever freaks at Valve originally wrote the dialogue system. You gave me something to do for weeks.

Thank you to drobotk for making vsif2vcd.py, not just for scene extraction but without which I would never have even thought to look in the item schema.

Thank you to the maintainers of the Valve Developer Community Wiki and the TF2 Wiki. This would not have been possible without you.

Thank you to Remi. Without you I would not even have started this project.

Thank you to my partner, cuz I like you.
