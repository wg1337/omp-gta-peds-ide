# What is it?

This is a simple include that parses the "peds.ide" file from GTA:SA into Pawn. This include can be useful for gamemodes that want to add immersion to the game. For example, by using this include you can provide a model ID of a ped and get answers to questions like:
- Is this ped a civilian, a gang mamber, a medic?
- What kind of a character does the ped have? is it agressive, is it geek, is it a criminal?
- What animations does this ped use?
- What is the ped's favorite radio station?

But more importantly this include also resolves the ped's voice lines. The voice line system is quite complex, check the include for more detailed explanation, but essentially a ped can be in a situation, for example, fighting, The ped can be a gang member. Combining those values you can ask the include to give which audio file should be played from the GTA:SA sounds. It is also possible to get PlayerPlaySound()'s sound ID, but there is a caveat.

# How to use it?

1) Place "peds.ide" in your "scriptfiles/" folder

2) Include it in your script:
```
#include <omp_gta_peds_ide>

public OnFilterScriptInit() {
    ....
    if(!LoadPedsIde()) {
        print("ERROR: Failed to load peds.ide");
        return false;
    }
    ....
    return true;
}
```

3) Use the provided functions, for example:
```
new E_GTA_PEDS_IDE_STAT:pedsStats = GetPedsIdeStatByModel(36);
//Returns GTA_PEDS_IDE_STAT_COWARD

new E_GTA_PEDS_IDE_RADIO:favoriteRadio = GTA_PEDS_IDE_RADIO:GetRandomPedIdeRadioByModel(9);
//Returns GTA_PEDS_IDE_RADIO_CLASSIC_HIP_HOP

new E_GTA_PEDS_IDE_SPEECH_TYPE:speechType = GetPedsIdeSpeechTypeByModel(127);
//Returns GTA_PEDS_IDE_SPEECH_TYPE_GANG, meaning that the ped talks like a gang member
```

# SA-MP limitation
Due to how SA-MP passes the sound IDs to GTA:SA and how GTA:SA interprets sound IDs larger than 45400, then it is very likely that you will encounter some sound IDs that are either silent or very quiet while most others work fine. A proper workaround is to extract all the sound archives and stream the audio files to the player. Check the include file to see how to get the proper file names.
