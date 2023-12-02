import kivy
kivy.require('2.0.0') # replace with your current kivy version !

from kivy.app import App
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.label import Label
from kivy.uix.button import Button
from kivy.uix.slider import Slider
from kivy.core.audio import SoundLoader

class RadioApp(App):

    def build(self):
        # Load the sound file
        self.sound = SoundLoader.load('http://icecast.omroep.nl/radio1-bb-mp3')
        # Create the main layout
        self.layout = BoxLayout(orientation='vertical')
        # Create a label to display the station name
        self.label = Label(text='Radio 1', font_size=50)
        # Create a button to play or pause the sound
        self.button = Button(text='Play', size_hint=(1, 0.2))
        self.button.bind(on_press=self.play_pause)
        # Create a slider to adjust the volume
        self.slider = Slider(min=0, max=1, value=1, size_hint=(1, 0.1))
        self.slider.bind(value=self.change_volume)
        # Add the widgets to the layout
        self.layout.add_widget(self.label)
        self.layout.add_widget(self.button)
        self.layout.add_widget(self.slider)
        # Return the layout
        return self.layout

    def play_pause(self, instance):
        # Play or pause the sound
        if self.sound.state == 'play':
            self.sound.stop()
            self.button.text = 'Play'
