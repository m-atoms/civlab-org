# civlab-org
civlab.org website

## Image Optimization

Images are optimized using ImageMagick for better quality and faster loading:

```bash
# Install ImageMagick
sudo apt install imagemagick

# Optimize images for web display (2x resolution for retina screens)
convert original_image.png -resize 540x360^ -gravity center -extent 540x360 -quality 90 -strip optimized_image.png
```

**The Problem (CSS Scaling):**
- Browser downloads 1897×1032px image (7x larger than needed)
- Browser uses fast bilinear interpolation to scale down in real-time
- Bilinear scaling averages nearby pixels, creating blur and artifacts
- Information loss from discarding 6 out of every 7 pixels
- Different browsers/devices scale differently, causing inconsistency

**The Solution (ImageMagick Pre-scaling):**
- Lanczos resampling algorithm analyzes larger pixel neighborhoods
- Preserves edge detail and reduces aliasing artifacts
- Optimal pixel data for exact display size (540×360 for 270×180 retina)
- 75% smaller file size with better visual quality
- Consistent across all devices since scaling is pre-computed