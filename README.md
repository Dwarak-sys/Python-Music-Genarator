from mido import MidiFile, MidiTrack, Message
from pydub import AudioSegment
from pydub.playback import play
from random import randint

rand_list=[]
for i in range(100):
    rand_list.append(randint(60,100))
melody_notes = rand_list

# Create MIDI file
midi = MidiFile()
track = MidiTrack()
midi.tracks.append(track)

# Add notes to the track
for note in melody_notes:
    track.append(Message('note_on', note=note, velocity=64, time=100))
    track.append(Message('note_off', note=note, velocity=64, time=100))

# Save MIDI file
midi.save('generated_melody.mid')

# Play generated melody
melody = AudioSegment.from_file('generated_melody.mid', format='midi')
play(melody)
