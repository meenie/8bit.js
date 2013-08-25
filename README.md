8Bit.js Audio Library
====
#### Write music using 8bit oscillation sounds.  Supports rhythms, multiple instruments, repeating sections, and complex time signatures.

#### Get Started

1. Include `8bit.min.js` in the head of your document.
2. Create an new instance: `var music = new EightBit();`
3. Give it a Time Signature: `music.setTimeSignature(4,4);`
4. Set the tempo: `music.setTempo(120);`
5. Create an instrument: `var piano = music.createInstrument();`
6. Start adding notes:

    ```javascript
    piano.note('C4', 'quarter');
    piano.note('D4', 'quarter');
    piano.note('E4', 'quarter');
    piano.note('F4', 'quarter');
    ```
    
7. Mark the `piano` instrument as finished: `piano.finish();`
8. Tell the `music` everything is done: `music.end();`
9. Start playing the music: `music.play()`

#### Examples

* [Super Mario Bros Theme](http://plnkr.co/edit/dv5iEPuMun0EIdmt9Y6n?p=preview) - Created by me
* [Tetris Theme](http://plnkr.co/edit/ev289bKEonSvqL3HVkDQ?p=preview) - Created by [rooktakesqueen](http://www.reddit.com/user/rooktakesqueen)
* [Zelda Main Theme](http://plnkr.co/edit/nVP3gnYrBWc7D7CMxpXv?p=preview) - Created by [legosjedi](http://www.reddit.com/r/javascript/comments/1kuskc/8bitjs_audio_library_write_music_using_8bit/cbthhwx)
* [Cities](http://plnkr.co/edit/KYHDjzVTYsCKw8ibm6Bt?p=preview) - Original Composition by GFM (If you want to use this in a project, please contact le9ato@yahoo.com)

#### API

##### EightBit Class
<table>
<tr>
<th width="20%">Method</th>
<th width="15%">Params</th>
<th width="65%">Description</th>
</tr>
<tr>
<td><code>setTimeSignature(top, bottom)</code></td>
<td><code>top: 4</code><br><code>bottom: 4</code></td>
<td>This will set the Time Signature for the music.  Any number of top numbers (how many beats per bar) can be set, but the bottom number (which note gets the beat) can only be 2, 4, or 8.</td>
</tr>
<tr>
<td><code>setTempo(tempo)</code></td>
<td><code>tempo: 120</code></td>
<td>Set the tempo (BPM) of the music</td>
</tr>
<tr>
<td><code>setMasterVolume(volume)</code></td>
<td><code>volume: 100</code></td>
<td>Set the master volume of the music. From 0 to 100</td>
</tr>
<tr>
<td><code>pause()</code></td>
<td>n/a</td>
<td>Pause the music.</td>
</tr>
<tr>
<td><code>stop(fadeOut)</code></td>
<td><code>fadeOut: true</code></td>
<td>Stop the music with a slight fade out.  If you don't want the fade, pass in false.</td>
</tr>
<tr>
<td><code>play()</code></td>
<td>n/a</td>
<td>Play the music.</td>
</tr>
<tr>
<td><code>end()</code></td>
<td>n/a</td>
<td>Collects all of the notes of each finished instrument and creates the oscillators in preperation to play.</td>
</tr>
<tr>
<td><code>mute(callback)</code></td>
<td>n/a</td>
<td>Mutes the music.  You can pass in a function as a callback when the music completely faded.</td>
</tr>
<tr>
<td><code>unmute(callback)</code></td>
<td>n/a</td>
<td>Unmute the music. You can pass in a function as a callback when the music is completely faded up.</td>
</tr>
<tr>
<td><code>onFinished(callback)</code></td>
<td>n/a</td>
<td>Pass in a function that will be called when the music has completed</td>
</tr>
<tr>
<td><code>loop(loop)</code></td>
<td><code>loop: false</code></td>
<td>Pass in true if you want the music to keep looping forever.</td>
</tr>
<tr>
<td><code>createInstrument(waveForm)</code></td>
<td><code>waveForm: sine</code></td>
<td>Creates an instrument that you can add notes/rests with.  The possible instrument types are: <code>sine</code>, <code>square</code>, <code>sawtooth</code>, and <code>triangle</code></td>
</tr>
<tr>
<td valign="top"><code>load(json)</code></td>
<td valign="top"><code>json: JSON</code></td>
<td>Load a song into 8bit.js using JSON. Format is:<br>
<pre>{
    timeSignature: [4, 4],
    tempo: 100,
    instruments: {
        rightHand: 'square',
        leftHand: 'sawtooth'
    },
    notes: {
        // Shorthand notation
        rightHand: [
            'E5, F#4|quarter|tie',
            'rest|quarter',
            'E5, F#4|quarter',
            'rest|quarter'
        ],
        // More verbose notation
        leftHand: [
            {
                type: 'note',
                pitch: 'D3',
                rhythm: 'quarter'
            }
        ]
    }
}</pre>
</td>
</tr>
</table>

##### Instrument Class - Created by using the `EightBit:createInstrument()` method.
<table>
<tr>
<th width="20%">Method</th>
<th width="15%">Params</th>
<th width="65%">Description</th>
</tr>
<tr>
<td valign="top"><code>note(pitch, note, tie)</code></td>
<td valign="top"><code>pitch</code> Must be set<br><code>note</code> Must be set<br><code>tie: false</code></td>
<td>Adds a note to the stack of notes for the particular instrument.<br>
    <code>pitch</code> can be any note between <code>C0</code> and <code>C8</code> (e.x. Bb3 or G#7)<br>
    <code>note</code> can be any from the list below
    <ul>
        <li>whole</li>
        <li>dottedHalf</li>
        <li>half</li>
        <li>dottedQuarter</li>
        <li>tripletHalf</li>
        <li>quarter</li>
        <li>dottedEighth</li>
        <li>tripletQuarter</li>
        <li>eighth</li>
        <li>dottedSixteenth</li>
        <li>tripletEighth</li>
        <li>sixteenth</li>
        <li>tripletSixteenth</li>
        <li>thirtySecond</li>
    </ul>
    <code>tie</code> can tie two notes together without any gap.  By default the library puts in an articulation gap of about a tenth of the length of the note.
</td>
</tr>
<tr>
<td><code>rest(note)</code></td>
<td><code>note</code> Must be set</td>
<td>Adds a rest to the list of notes.  Use the note list above for the type of rest you can use.</td>
</tr>
<tr>
<td><code>setVolume(volume)</code></td>
<td><code>volume: 25</code></td>
<td>Sets the volume for this particular instrument. From 0 to 100. You can call this multiple times before notes to change their volume at that point of the music.</td>
</tr>
<tr>
<td><code>repeatStart()</code></td>
<td>n/a</td>
<td>Puts in a marker where a section of music should be repeated from.</td>
</tr>
<tr>
<td><code>repeat(times)</code></td>
<td><code>times: 1</code></td>
<td>Used in conjunction with <code>repeatStart()</code>. Pass in how many times the section should be repeated.  If no <code>repeatStart()</code> is set, it goes from the beginning.</td>
</tr>
<tr>
<td><code>finish()</code></td>
<td>n/a</td>
<td>This will mark the instrument as complete and add it's notes to the master list.  If this is missing, the instrument will not be played.</td>
</tr>
</table>

### Copyright and License

Copyright 2013 Cody Lundquist under the [MIT License (MIT)](LICENSE).
