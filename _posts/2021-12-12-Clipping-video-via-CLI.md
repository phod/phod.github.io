---
layout: post
title: Clipping video via CLI.
---

## Introduction

Here's a quick low-effort little guide on how to cut out clips of video from a larger one. Mainly for my own reference,
but surely it'll be of use to someone out on the internet.

This is honestly just a glorified copy + paste of a [StackExchange answer](https://superuser.com/questions/458761/accurately-cut-video-files-from-command-line). Go read that.

It's also worth noting that the contents of this blog lead to an imperfect and slower solution than what is probably possible.
I found some [promising information on seeking](https://trac.ffmpeg.org/wiki/Seeking) that seems like it would speed this
process up significantly. But I couldn't get things working as needed. Given that I was trying to actually get something done,
I stuck with the imperfect solution and ate dinner whilst waiting for my bulk script to complete.

You'll need to have `ffmpeg` installed, and possibly some other dependencies for encoding. Installation is left
as an execise for the reader (sorry!).

## Guide

1. Get your source video. For this guide, we will call it `big-video.mp4`.
2. Identify the timestamps you want your video to be cut between. For this example, we want the clip to be
   between 1 minute and 15 seconds and 2 minutes and 5 seconds of the original `big-video.mp4` file. 
   Or 00:01:15.00 to 00.02.05.00. And the new video will be called `small-video.mp4`
3. Open a CLI, and run `ffmpeg -i big-video.mp4 -ss 00:01:15.00 -to 00:02:05.00 -c:v libx264 -c:a copy small-video.mp4`.

## Want more than one clip?

Lucky you, so did I. So I hacked out a bash script to do just that. (Nothing pretty)

Bash script, named `clippy.sh`:
```
#!/bin/bash
set -e

while read -a line
do
    SOURCE=$1
    DESTINATION=${line[0]}
    START_TIME=${line[1]}
    END_TIME=${line[2]}

    if [ -z "${SOURCE}" ] || [ -z "${DESTINATION}" ] || [ -z "${START_TIME}" ] || [ -z "${END_TIME}" ]; then
        echo "Missing input!"
        echo "Provided input was:"
        echo "Source: $SOURCE"
        echo "Destination: $DESTINATION"
        echo "Start time: $START_TIME"
        echo "End time: $END_TIME"
        echo "Exiting"
        exit 1
    fi
    ffmpeg -i $SOURCE -ss $START_TIME -to $END_TIME -c:v libx264 -c:a copy $DESTINATION </dev/null
    echo "Completed creating $DESTINATION"
done < /dev/stdin
```

You'll also need to create a `timestamps.txt` file. e.g.
```
clip1.mp4 00:01:05 00:01:55
clip2.mp4 00:03:30 00:04:30
clip3.mp4 00:02:08 00:02:56
```
The format essentially being
```
<destination file> <start timestamp> <end timestamp>
<destination file> <start timestamp> <end timestamp>
<destination file> <start timestamp> <end timestamp>
```

Then you can just run:
`cat timestamps.txt | ./clippy.sh big-video.mp4`

## Troubleshooting

### Could not find tag for codec pcm_s16le in stream #1, codec not currently supported in container

Full error:
```
Could not find tag for codec pcm_s16le in stream #1, codec not currently supported in container
Could not write header for output file #0 (incorrect codec parameters ?): Invalid argument
Error initializing output stream 0:0 -- 
Conversion failed!
```

I got this when trying to convert a `.mov` into an `.mp4`. i.e. `big-video.mov` and `small-video.mp4`. Fix was to make `small-video` also
of `.mov` format. I can convert to `.mp4` later should I desire.
