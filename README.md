
def is_valid_note(greet_dict, voice_note):
    for key, value in greet_dict.items():
        if value == voice_note.split(' ')[0]:
            return True
        else:
            return False
