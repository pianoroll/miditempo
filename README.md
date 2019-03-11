miditempo script
================

This PERL script changes or lists the tempo on piano-roll MIDI files.

The tempo is handled differently than in a typical MIDI files.
Ticks in the MIDI files are equivalent to pixel rows in the original
image (starting at the first note/expression hole on the roll).
The tempo is not controlled directly by tempo meta messages, but
rather the ticks per quarter note value in the MIDI file header.
For a 300 DPI scan, the tpq value is six times the tempo.

Tempo meta-messages are used to emulate the roll acceleration.
These tempo meta-messages do not change when changing the tempo
using this script.  The accelleration is set to 0.4%/foot
(0.4%/3600 ticks).

The binasc program needs to be installed before using this script. It
can be found in https://github.com/craigsapp/midifile .

Installation
------------

To install the script in `/usr/local/bin` type the command:

```bash
git clone https://github.com/pianoroll/miditempo
cd miditempo
make install
```

The binasc program is required by this script.  To install from github, type these commands in the terminal:

```bash
git clone https://github.com/craigsapp/binasc
cd binasc
make
make install
```

The last step will copy the executable program to `/usr/local/bin`.  Type the command:

```bash
which binasc
```

to verify that the shell can see it; if so, then you should be ready to use the miditempo script to change tempos of pianoroll MIDI files.



Options
-------

|Option | Description
|:-----:|:-----------
| -s #  | Set the tempo to # (such as "-s 100" to set the tempo to 100).
| -l    | List the current tempo of the MIDI file(s). 
| -o    | Overwrite original MIDI file with new tempo version.
| -r    | Use red welte tempo (98.4251968504 -> 98.5).


Examples
--------

* To change the tempo of a MIDI file to the default Red-Welte tempo:

```bash
miditempo -ro file.mid
```

* To change all tempos in multipl files to default Red-Welte tempo:

```bash
miditempo -ro *.mid
```

* To set the tempo of a MIDI file to 100:

```bash
miditempo -s 100 file.mid
```

* To list tempo in a file:

```bash
miditempo -l file.mid
```

* To list tempos in multiple files:

```bash
miditempo -l *.mid
```


Caveats
--------

This script will need to be updated for MIDI files that are derived from scans of DEA rolls (or any roll scanned at the higher camera position).


