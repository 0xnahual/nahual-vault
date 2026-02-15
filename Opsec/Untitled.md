Remove video metadata.

ffmpeg -i input.mov -map_metadata -1 -codec copy output.mov