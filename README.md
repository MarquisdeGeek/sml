# SML
Steev's Javascript MIDI Library

Steven Goodwin (StevenGoodwin@gmail.com)
Copyright 1998-2016, Steven Goodwin

Released under the GPL 2


# About

Steev's MIDI Library is Javascript library to generate standards-compliant MIDI files. This 
provides code functionality for developers wishing to write music apps that auto-compose music.

It is a port of https://github.com/MarquisdeGeek/midilib

# Examples

The most basic is

```
var mf = new SML.Midi();
var track = mf.createTrack();
var scale = [60,62,64,65,67,69,71,72];

	track.addTempo(120);
	for(var i=0;i<scale.length;++i) {
		track.addNoteOn(0, scale[i], 100, SML.MidiNote.crochet);	
	}

	SML.MidiFile.save(mf, "example.mid");
```
By using a duration parameter with addNoteOn, the playback pointer will automatically increment so
the next note starts after it.

Therefore, to create chords you omit this parameter and manually turn the note off, like so...

```
var mf = new SML.Midi();
var track = mf.createTrack();
var playChord = function(root, off1, off2) {

	track.addNoteOn(0, root, 100);
	track.addNoteOn(0, root+off1, 100);
	track.addNoteOn(0, root+off2, 100);

	track.addRest(SML.MidiNote.minim);

	track.addNoteOff(0, root, 100);
	track.addNoteOff(0, root+off1, 100);
	track.addNoteOff(0, root+off2, 100);
};

playChord(60, 4, 7);
playChord(65, 4, 7);
playChord(67, 4, 7);
playChord(60, 4, 7);

SML.MidiFile.save(mf, "chords.mid");
```

