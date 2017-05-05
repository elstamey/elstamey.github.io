# Welcome to my Slides
[serve the site](http://elstamey.github.io)

# Notes to Self

### Build a new slide deck with Cleaver
`> cleaver watch index.md`

### Build and Serve the Slide Decks
> npm install 
> npm serve

## My default slide deck notes

### Screen resolutions:

    Reveal.initialize({
    
        ...
    
        // The "normal" size of the presentation, aspect ratio will be preserved
        // when the presentation is scaled to fit different resolutions. Can be
        // specified using percentage units.
        width: 960,
        height: 700,
    
        // Factor of the display size that should remain empty around the content
        margin: 0.1,
    
        // Bounds for smallest/largest possible scale to apply to content
        minScale: 0.2,
        maxScale: 1.5
    
    });

#### Resolutions to use for screen ratio:

    4:3 - 1024x768
    16:9 - 1280 x 720
