# Arreglar keyframes y índices

-v Indicates "verbose" mode, displaying more output within the console.
-inter Specifies the duration, in seconds, of the interleaved media data chunks.
-out Displays the output file name and path.
 
mp4box -v -inter 1000 [input-file] -out [output-file]


# KeyFrames y índices más pesados en fichero pero menos seeks en el disco

Alternatively, you can use the -tight option to perform sample-based interleaving of the media tracks. This results in a larger file size, but also reduces the number of disk seeks on the server side.

-tight Requires no value.
 
mp4box -v -tight [input-file] -out [output-file]

