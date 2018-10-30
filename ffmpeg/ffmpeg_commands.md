# Copiar codecs de vídeo y audio

ffmpeg -i input.mp4 -vcodec copy -acodec copy output.mp4

# Componer cuatro entradas, un cuarto para cada una, creando mosaico

ffmpeg
	-i 1.avi -i 2.avi -i 3.avi -i 4.avi
	-filter_complex "
		nullsrc=size=640x480 [base];
		[0:v] setpts=PTS-STARTPTS, scale=320x240 [upperleft];
		[1:v] setpts=PTS-STARTPTS, scale=320x240 [upperright];
		[2:v] setpts=PTS-STARTPTS, scale=320x240 [lowerleft];
		[3:v] setpts=PTS-STARTPTS, scale=320x240 [lowerright];
		[base][upperleft] overlay=shortest=1 [tmp1];
		[tmp1][upperright] overlay=shortest=1:x=320 [tmp2];
		[tmp2][lowerleft] overlay=shortest=1:y=240 [tmp3];
		[tmp3][lowerright] overlay=shortest=1:x=320:y=240
	"
	-c:v libx264 output.mkv

### Convert sequence of JPEG images to MP4 video

`ffmpeg  -r 24 -pattern_type glob -i '*.JPG' -i DSC_%04d.JPG -s hd1080 -vcodec libx264 timelapse.mp4`

- `-r 24` - output frame rate
- `-pattern_type glob -i '*.JPG'` - all JPG files in the current directory
- `-i DSC_%04d.JPG` - e.g. DSC_0397.JPG
- `-s hd1080` - 1920x1080 resolution

#### Slower, better quality

Add the following after `-vcodec libx264` to achieve better quality output

`-crf 18 -preset slow`

