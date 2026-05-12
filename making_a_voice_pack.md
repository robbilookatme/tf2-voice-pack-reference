# So, You Wanna Make A Voice Pack

Bad choice. But, if I can't stop you, there's some things you should know.

### Voice Line Count

This doesn't 100% correspond to how much work you would be doing, but here's how many lines each class has (according to my own research):

1. Pyro - 189
2. Medic - 534
3. Demoman - 584
4. Engineer - 666
5. Spy - 690
6. Heavy - 765
7. Sniper - 834
8. Soldier - 847
9. Scout - 949

Of course, you have to choose the scale of your voice pack. Many of these lines are only played when using a special taunt, wearing a Halloween item, playing on a Halloween map, playing in competitive mode, playing in Mann vs Machine, completing contracts, and other specific scenarios. What lines of dialogue are of importance to you is up to you.

### Writing

If you are writing all new dialogue, you will want to know what you're getting into. Here is a list of lines that are common to all or most classes, along with examples of what a character might say:

* Voice Commands
  * "Medic!"
    * If looking at a Medic, "Follow me, doc!"
  * "Thanks!"
    * If just got a kill, "Thanks for your help!"
  * "Go go go!"
  * "Move up!"
  * "Go Left!"
  * "Go Right!"
  * "Yes"
  * "No"
  * "Incoming!"
  * "Spy!"
    * If looking at another player, "that X is a Spy!" for each class
  * "Sentry Ahead!"
  * "Need a Teleporter here"
  * "Need a Dispenser here"
  * "Need a Sentry here"
  * "Activate UberCharge!"
  * "Help!"
    * If on a cappable point, "Help me capture!"
    * If on an owned point, "Help me defend!"
  * Battle Cry - "Let's do it!" type line
    * If holding a non-stock weapon, shiny cry line - "I'm gonna get you with this new weapon!"
    * If looking at an enemy with melee out, melee dare line - "I'm gonna beat you with this!"
  * Cheers - "We are doing great!"
  * Jeers - "We are doing bad!"
  * Positive - "This is great!"
  * Negative - "This is bad!"
  * "Nice Shot!"
  * "Good Job!"
* Domination
  * Generic domination - "I just dominated you!"
  * Class specific domination - "I just dominated you, X!"
* Revenge - "I won't let you dominate me again!"
* Pain
  * Sharp pain - "Ow!" - normal pain sounds
  * Severe pain - "Owww!" - slightly louder pain sounds played to the causer of damage
  * Death scream - "Aaaaagh!" - long screams played for death by melee or critical hit
  * Fire - "I am on fire!"
* Hit by Jarate, Mad Milk, or Gas Passer - "This is terrible!"
* Thanks for Teleporter - "Thanks for the teleporter!"
* Healed by Medic - "Thanks, doctor!"
* Ubered - "I'm going to kill you now that I am Ubered!"
* Achievement - "I earned that!"
* Captured Intelligence - "I took your intelligence!"
* Control Point
  * Captured a Point - "This point is ours now!"
  * Firing on unowned Control Point - "Stand on the point and help me capture!"
  * Firing on owned Control Point - "Stand on the point and help me defend!"
  * Blocking a capture - "Get off my point!"
* Payload
  * Offense
    * Cart goes forward - "Let's push the cart!"
    * Cart stops - "Why did the cart stop?!"
    * Cart rolls back - "Get to the cart!"
  * Defense
    * Cart goes forward - "We gotta stop the cart!"
    * Cart stops - "It's great that the cart stopped!"
    * Cart rolls back - "It's great that the cart is going back!"
* Stalemate - "I am ashamed of this outcome!"

Note that not every class has these lines, classes that do have these lines usually have three or more variants of each, every class reuses some lines across categories, and every class has lines that no other class has. This is just an overview of the more common ones, and to give you an idea of the scale of a voice pack.

Some examples (not comprehensive at all) of class-specific lines are:
* Scout has lines for double jumping
* Demoman has lines for decapitating players with swords
* Heavy has lines for winding up his minigun
* Medic has access to the voice command for "UberCharge Ready!"
* Engineer has lines for getting a kill with the Wrangler
* Sniper has lines for getting headshots

If not using the associated spreadsheets, be sure to compare against the TF2 Wiki to make sure you aren't missing any lines. As well, remember that there are voiceline sets for Special Taunts, Halloween items, Contracts, Competitive Mode, and Mann vs. Machine. It's not required to replace every voice line in your voice pack, but it's good to remember in case there are any extra lines you want to replace.

Something I might as well mention early on is how to avoid lines getting cut off. Best I can tell, most lines in TF2 will not be cut off at any length, assuming you don't interrupt the line yourself by using a voice command. However, there are a two circumstances where lines getting cut short CAN happen:
1. Lines that are played in a timed sequence, like the Administrator's timer countdown, or taunts that play multiple dialogue lines
2. Lines that are played by a rule with the criteria ConceptPlayerExpression, which include only Halloween taunts with idle lines and Sniper scoped-in muttering-under-breath lines
These two categories of lines are guaranteed to get cut off or interrupted if they are longer than the original lines of dialogue. In the case of Sniper's "hold still" type lines, it is recommended you time out your custom lines to be the same length or shorter than the originals to avoid getting cut off. As for taunt lines, since these lines of dialogue are often used elsewhere (and since the taunts are often timed specifically to match the original lines), it is up to you how important the timing is. Many workshop taunts were created with one or two lines in mind and are timed to match them exactly. Writing new dialogue that fits your voice pack's goal, suits every circumstance the line is played in, AND avoids getting cut off in every taunt that uses the line is no simple task, and it's understandable if you choose to focus only on the first two.

### Recording

This section is only relevant for creators who are doing voice acting themselves. If your voice pack is the type that uses someone else's voice, you don't have to worry about this part. This section also varies depending on what software you are comfortable using or have access to.

I recommend recording as many lines as possible in one session, as much of the later audio processing work can be done in bulk. To do this, you can use audio markers (or whatever similar feature is available in your audio editor of choice) between voice lines. There should be a shortcut for adding a marker while recording, making this process even easier. If you have to do multiple takes, I recommend leaving all the takes together between audio markers, as it's easier to pick the best take or combine pieces of different takes when they are still together. Once you have recorded all your dialogue, your audio software should allow you to export a single file for each audio marker. At this stage, you should be saving audio in WAV format so as to not lose audio information to file compression.

Note that the output files will probably be exported as 1.wav, 2.wav, etc. Of course, the filenames used by the game are usually in the format "classname_action01", so you will need to rename these files at some point. I recommend doing it now, as it's easier to replace or edit specific files that way. You also could put the output file names as the names of the audio markers, though that can't easily be done while recording. (I am hoping to create a script that will batch rename the audio files for you.)

How to voice act or what kind of voice to do is left as an exercise for the reader.

### Editing

Like the last section, this section depends on which audio software you are using, but I will still try to keep it in general terms. I try to keep a separate folder for every step of this process so that mistakes can easily be undone, but this isn't strictly necessary. At the very least, you should keep a copy of the original recordings before any editing.

Once you have a set of audio files, you need to get them ready for Team Fortress 2. You can just replace an MP3, but it probably won't sound very good in-game for a few reasons. I will explain the steps I go through for audio editing, and what this does for the audio. For reference, I use Tenacity (a fork of Audacity) for recording and editing audio.

First, you need to go through each audio file and edit it down. Remove any pauses before or after the dialogue, cut out any noises from mouse and keyboard, and take out those weird noises that mouths make. This is the only part of the editing process that can really only be done by hand, as I've found that automated solutions like silence-based trimming do not give good results. You may also want to run noise removal, depending on your audio setup. For emphasis: if you think you might need to do noise removal, do it now; doing it later gives worse results.

Thankfully, the rest of the steps can be done in bulk to every file at once.

Next, you need to run a compressor on the audio to balance out the audio levels. This can be done in many different ways, and the exact specifications aren't set in stone. My process is running normalization to 0dB, then running a compressor/limiter to boost low level audio. The goal here is to reduce the difference in volume between the loud and quiet parts of the sound. This is necessary to make the whole voiceline audible in-game, even in loud situations.

Finally, it's a good idea to run equalization on the audio. I borrowed the settings from the Vocal Presence present in FL Studio: cut off frequencies below 100Hz, slight dip in volume around 330Hz, and slight boost at around 12.5kHz. This makes the audio less "muddy", and easier to hear in a noisy firefight. The exact settings you use will depend on the original audio and what frequencies it favors. Don't go overboard on the dips or boosts, as that can result in the voice sounding artifical or tinny.

Now that the audio has been processed, it can be saved in a format that TF2 will load. TF2 prefers audio files in MP3 format, at 44.1kHz. Once your files are in this format, they can be loaded into the game.

### File/Folder Composition.

The Source Engine loads modded files from a subfolder in the user's "custom" folder, expecting the same file path as that of the game's data. As an example, say you want to replace the file "engineer_revenge01.mp3". This is in the "vo" folder in the "sound" folder of the game's data. (Actually, it's in a .vpk file, which contains these same folders.) This means you should place your modified file in the following place:

"(TF2 Installation Folder)/tf/custom/(Your Mod Name)/sound/vo/engineer_revenge01.mp3"

If you're using the provided spreadsheets, they should inform you of the folders and subfolders that each file should be placed in. Remember that every file needs to be in the "sound" folder.

### Testing

I highly recommend testing a voice pack thoroughly, not just to find errors in editing but to see if any lines are annoying, out of place, or otherwise should be replaced or re-recorded. There's no hard and fast rules for testing a voice pack, but I go about it in two ways. The first is what I call "lab testing". There are a variety of multi-purpose test maps (I use Supertest by Horiuchi), but any map that allows you to test items and spawn bots easily will do. The second is "field testing", meaning playing actual games of TF2 with the voice pack. This doesn't have to be online necessarily; playing offline bot-filled games with godmode enabled allows you to hear objective-related voicelines without fear of respawn times or letting teammates down when focusing on dialogue.

### Release

If your voice pack is ready for primetime, you'll want to package it into a .zip file (how to do this is left as an exercise for the reader) and upload it somewhere. Your zip file should contain the mod folder created earlier, and a readme that says something like:

"Place (Mod Name) folder in your Team Fortress 2/tf/custom folder."

If you use the above line in your readme, you owe me royalties. (This is a joke, feel free to steal that.)

If your target demographic is friends, a Discord server, etc, you can get away with uploading to MEGA, Dropbox, Google Drive, or even a temporary service like Litterbox. For mass consumption, the biggest Team Fortress 2 mod site is Gamebanana. How to upload to any of these services is beyond the scope of this guide.

Congratulations! If you followed all the above steps, you should have a beautiful (maybe), entertaining (maybe), worthwhile (maybe) voice pack to share with the world!
