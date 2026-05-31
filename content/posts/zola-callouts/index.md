+++
title = "Inserting callouts into a Zola static site"
date = "2026-05-01"

[taxonomies]
tags = ["zola", "blog"]
+++

I really like [Zola](https://www.getzola.org) as a static site generator for my blog. It is free to install and because I run it through my GitHub account there are no hosting fees.  The only ongoing cost is my domain name, dajhub.co.uk.  

The Zola site has some great themes to choose from but the one I went for is a theme provided by **not-matthias** called [apollo](https://github.com/not-matthias/apollo).  Its simplicity appealed and it has been working well for me.  

The only change I have made is to add **callouts** to my site.  Callouts are useful for highlighting tips, warnings, or extra context without breaking the reading flow. The Apollo theme doesn’t include them by default, so I added my own lightweight implementation.

## 1. Add a Nerd Font

I wanted my callouts to use icons and so I needed to add an appropriate font.  I went for a [Nerd Font](https://www.nerdfonts.com/font-downloads) and downloaded the **JetBrainsMono Nerd Font**.  Once downloaded I placed just one font, **JetBrainsMonoNerdFontPropo-Regular.ttf**, into the already existing folder at /static/fonts/JetbrainsMono, i.e.

```
static/
  fonts/
    JetBrainsMono/
      JetBrainsMonoNerdFontPropo-Regular.ttf
```


## 2. Create _callouts.scss

Create a new file, **_callouts.scss**, in 
```
sass/
  parts/
    _callouts.scss
```

Add the content below to this new file. Each callout type uses the same base structure but with different colours and icons, so the SCSS repeats the same pattern with small variations.

```scss
@font-face {
  font-family: "JetBrainsMono Nerd";
  src: url("/fonts/JetbrainsMono/JetBrainsMonoNerdFontPropo-Regular.ttf")
    format("truetype");
  font-weight: normal;
  font-style: normal;
}

.callout {
  padding: 1rem 1.25rem;
  margin: 0rem 0rem;
  border-top: 2px solid;
  border-bottom: 2px solid;
  border-left: 2px solid;
  border-right: 2px solid;
  border-radius: 0;
  overflow: hidden;
}

// TIP
.callout-tip {
  @extend .callout;
  border-color: #b7d9d3;
  background: #b7d9d333;

  position: relative;
  padding-top: 3rem;

  &::before {
    content: "\f0eb";
    font-family: "JetBrainsMono Nerd";

    position: absolute;
    top: 0;
    left: 0;

    width: 100%;
    padding: 0.4rem 1.25rem;

    background: #b7d9d3;
    color: #233;
    font-weight: 600;
  }

  &::after {
    content: "Tip";

    position: absolute;
    top: 0.4rem;
    left: 3rem;

    font-family: inherit;
    font-weight: 600;
    color: #233;
  }
}

// IMPORTANT
.callout-important {
  @extend .callout;
  border-color: #f3c7b3;
  background: #f3c7b333;

  position: relative;
  padding-top: 3rem;

  &::before {
    content: "\f071";
    font-family: "JetBrainsMono Nerd";

    position: absolute;
    top: 0;
    left: 0;

    width: 100%;
    padding: 0.4rem 1.25rem;

    color: #232634;             
    background:  #f3c7b3;
    font-weight: 600;
  }
  &::after {
    content: "Important";

    position: absolute;
    top: 0.4rem;
    left: 3rem;

    font-family: inherit;
    font-weight: 600;
    color: #233;
  }
}

// NOTE
.callout-note {
  @extend .callout;
  border-color: #fff4b8;
  background: #fff4b833;

  position: relative;
  padding-top: 3rem;

  &::before {
    content: "\f040";
    font-family: "JetBrainsMono Nerd";

    position: absolute;
    top: 0;
    left: 0;

    width: 100%;
    padding: 0.4rem 1.25rem;

    color: #232634;             
    background:  #fff4b8;
    font-weight: 600;
  }

  &::after {
    content: "Note";

    position: absolute;
    top: 0.4rem;
    left: 3rem;

    font-family: inherit;
    font-weight: 600;
    color: #233;
  }
}

// INFORMATION
.callout-info {
  @extend .callout;
  border-color: #c9dff3;
  background: #c9dff333;

  position: relative;
  padding-top: 3rem;

  &::before {
    content: "\f449";
    font-family: "JetBrainsMono Nerd";

    position: absolute;
    top: 0;
    left: 0;

    width: 100%;
    padding: 0.4rem 1.25rem;

    color: #232634;             
    background:  #c9dff3;
    font-weight: 600;
  }

  &::after {
    content: "Information";

    position: absolute;
    top: 0.4rem;
    left: 3rem;

    font-family: inherit;
    font-weight: 600;
    color: #233;
  }

}
```
### Understanding the icon codes

<div class="callout-note">
The content values (\f0eb, \f071, etc.) come from the Font Awesome glyphs included in Nerd Fonts. You can swap these for any other Nerd Font icon.
</div>

The callouts now available are:
- Tip
- Important
- Note
- Information

Feel free to adjust colours, icons, or spacing to suit your theme.

## 3.  Add the callout HTML

To add each of the callouts, within your post you would need to add:

a) **Tip**

```html
<div class="callout-tip">
This is the callout tip.
</div>
```

<div class="callout-tip">
This is the callout tip.
</div>

b) **Important**

```html
<div class="callout-important">
This is where you can place important information.
</div>
```

<div class="callout-important">
This is where you can place important information.
</div>

c) **Note**

```html
<div class="callout-note">
Where you add a note.
</div>
```

<div class="callout-note">
Where you add a note.
</div>

d) **Information**

```html
<div class="callout-info">
This is additional information.
</div>
```

<div class="callout-info">
This is additional information.
</div>

---

That’s all you need to add callouts to the Apollo theme.