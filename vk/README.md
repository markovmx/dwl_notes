
# vk.com

Here you find methods grabbing and handle data.

### Install ffmpeg *

1. **Windows:**
Download ffmpeg from [ffmpeg.org](https://ffmpeg.org/download.html) and follow the installation instructions.

2. **macOS:**
Install ffmpeg via Homebrew by running:
     ```
     brew install ffmpeg
     ```

3. **Linux (Ubuntu/Debian):**
Install ffmpeg via apt by running:
     ```
     sudo apt update
     sudo apt install ffmpeg
     ```

### Install yt-dlp *

**Windows/macOS/Linux:**

Install yt-dlp via pip by running:
     ```
     pip install yt-dlp
     ```

## Community Videos
### Video Download

Download all videos from community:
   ```
   yt-dlp -f 'bestvideo[height<=720][ext=mp4]+bestaudio[ext=m4a]/best[height<=720][ext=mp4]/best' -o "${output_dir}/%(title)s.%(ext)s" "$community_url"
   ```

### Fixing Video File Extensions

Sometimes yt-dlp save vk.com video with extension .unknown_video, for fix run next command in folder with videos:
```
for file in *.unknown_video; do
    ffmpeg -i "$file" -c:v copy -c:a copy "${file%.unknown_video}.mp4"
    rm "$file"
done
```

### All in one bash script
```
#!/bin/bash

# Check if the number of arguments is correct
if [ "$#" -ne 2 ]; then
    echo "Usage: $0 <output-dir> <source-url>"
    exit 1
fi

# Assign arguments to variables
output_dir="$1"
source_url="$2"

# Run yt-dlp command to download the video
yt-dlp -f 'bestvideo[height<=720][ext=mp4]+bestaudio[ext=m4a]/best[height<=720][ext=mp4]/best' -o "${output_dir}/%(title)s.%(ext)s" "$community_url"

# Change directory to output directory
cd "$output_dir" || exit

# Run FFmpeg command to convert .unknown_video files to MP4
for file in *.unknown_video; do
    ffmpeg -i "$file" -c:v copy -c:a copy "${file%.unknown_video}.mp4"
    rm "$file"
done
```
