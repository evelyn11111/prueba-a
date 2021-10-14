# prueba-a
prueba 1
#@title Gif magic
%cd "/content/dreamtime/src/cli"


path='gifs'
import os
if not os.path.exists(path):
    os.makedirs(path)

path='gif_results'
if not os.path.exists(path):
    os.makedirs(path)

from IPython.display import display
from ipywidgets import widgets
from os import listdir
from os.path import isfile, join

mypath = '/content/dreamtime/src/cli/gifs'
onlyfiles = [f for f in listdir(mypath) if isfile(join(mypath, f))]

if len(onlyfiles)>0:
  filename_ch = widgets.Dropdown(
      options=onlyfiles,
      description='Choose gif:',
  )
  butt = widgets.Button(description='Start')
  def on_butt_clicked(b):
      print(filename_ch.value)
      %cd '/content/dreamtime/src/cli/'
      !python main.py -i "gifs/$filename_ch.value" -o "gif_results/$filename_ch.value" --gpu 0 --gif
  

  butt.on_click(on_butt_clicked)
  # display
  display(widgets.VBox([filename_ch,butt]))
else:
  print('Upload gif at first')


