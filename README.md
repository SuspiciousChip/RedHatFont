# Red Hat Typeface Files

## Designers

### Jeremy Mickel

Jeremy Mickel runs [MCKL](https://www.mckltype.com), a Los Angeles-based type foundry and design studio publishing original fonts and creating custom designs for clients. Founded in 2012, MCKL has collaborated with leading design firms, companies, and organizations around the world to provide custom typeface and logo design services. Mickel's work has been recognized by the Type Directors Club and the AIGA, and he has taught at RISD and the Minneapolis College of Art and Design.

## About Red Hat Display and Red Hat Text

![Type specimen](type-specimen@2x.png)

Red Hat is an enterprise software company with an open source development model. We use collaboration and knowledge sharing to craft better, more reliable, and more adaptable technologies. How our words look is as important to our brand voice as the words we choose. That’s why we developed a type family that’s all our own.

The Red Hat Typeface is a superfamily of Display, Text, and Mono styles, each with a range of weights in roman and italic. The fonts were originally commissioned by Paula Scher / [Pentagram](https://www.pentagram.com/) and designed by Jeremy Mickel / [MCKL](https://www.mckltype.com) for the new Red Hat identity.

Red Hat is a fresh take on the geometric sans genre, taking inspiration from a range of American sans serifs including Tempo and Highway Gothic. The Display styles, made for headlines and big statements, are low contrast and spaced tightly, with a large x-height and open counters. The Text styles have a slightly smaller x-height and narrower width for better legibility, are spaced more generously, and have thinned joins for better performance at small sizes. In 2021 we added Light and Light Italic styles, and a Monospace family. The fonts can be used together seamlessly at a range of sizes.

As part of Red Hat’s commitment to open source software, the fonts are made available for use under the SIL Open Font License.

## Variable Fonts

 A demo for variable fonts is available at [https://redhatofficial.github.io/RedHatFont/](https://redhatofficial.github.io/RedHatFont/).

Variable fonts are available for each of the Red Hat Typeface families. The fonts include the `wght` axis, which allows for interpolation between light and black weights.

There are two versions of the variable fonts: with and without VF in the name. It is Red Hat's preference to name these differently than the OTF / TTF fonts, but Google requires the names to be the same. We recommend using ***either*** the VF or standard named variable fonts, but not both.

## Google Fonts Distribution

Red Hat fonts are available on [Google Fonts](https://fonts.google.com/), but please be aware of current status:

### Current Status (Updated 2026-09-24)

⚠️ **Known Issue:** Google Fonts is currently serving TTF format instead of woff2 for Red Hat fonts due to an infrastructure issue on their end. While fonts load correctly via the TTF fallback, woff2 files (which are smaller and more efficient) are temporarily unavailable.

- **Impact:** Fonts work normally, but with slightly larger file sizes
- **Details:** See [GOOGLE_FONTS_STATUS.md](GOOGLE_FONTS_STATUS.md) for technical details and timeline
- **Workaround:** Self-hosting (recommended) or continue using Google Fonts with TTF format

### Using Google Fonts

To use Red Hat fonts from Google Fonts, add to your HTML:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Red+Hat+Display:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
```

Then in your CSS:
```css
body {
  font-family: 'Red Hat Display', sans-serif;
}
```

**Available families:**
- [Red Hat Display](https://fonts.google.com/specimen/Red+Hat+Display) - For headlines and large text
- [Red Hat Text](https://fonts.google.com/specimen/Red+Hat+Text) - For body copy and paragraphs
- [Red Hat Mono](https://fonts.google.com/specimen/Red+Hat+Mono) - For code and monospaced text

## Building the Fonts

From terminal, run the build script at `sources/build-all.sh`. Fonts output to `fonts/`.

NOTE: The first time you build, you will need to set up a virtual environment and install dependencies:

<details>
<summary><b><!-------->Setting up the build environment<!--------></b> (Click to expand)</summary>

### Set up the environment

**The basics**

You will need to open a terminal to run the following commands.

Clone the repo & navigate into it:

```
git clone https://github.com/RedHatOfficial/RedHatFont.git
cd RedHatFont
```

Check that you have Python 3:

```
which python3
```

It should return a path ending with `python3`, such as `/Library/Frameworks/Python.framework/Versions/3.7/bin/python3`. If it returns an error like `python3 not found`, you will need to [download Python 3](https://www.python.org/downloads/).

**Setting up a virtual environment**

To build, set up the virtual environment:

```bash
cd ~
python3 -m venv venv
```

Then activate it:

```bash
source venv/bin/activate
```

Now, install requirements:

```bash
cd RedHatFont
pip install -U -r requirements.txt
```


**Making woff2 files**

Finally, you will also need to separately install [google/woff2](https://github.com/google/woff2) to enable the `woff2_compress` and `woff2_decompress` commands. Open a new terminal session, window, or tab to do this step.

```bash
# open a new terminal session first, then run
git clone --recursive https://github.com/google/woff2.git
cd woff2
make clean all
```

To make sure woff2_compress is installed properly, enter the following inyour terminal window:

```
woff2_compress
```

If terminal cannot find the command, you may need to ensure binaries are in $PATH, [a description of which you can find here.](https://github.com/google/woff2/issues/131)

Once woff2_compress is working in your terminal, you can now run the build!

</details>

### Build fonts

Once you have set up the environment (see above), you can build fonts & prep releases!

1.030 uses GFTOOLS builder to build the fonts. It should be as simple as running

```bash
gftools builder source/Mono/config.yaml
```
```bash
gftools builder source/Proportional/RedHatDisplay/config.yaml
```
```bash
gftools builder source/Proportional/RedHatText/config.yaml
```


## Installation

The OTF or TTF folders contain the font files used by most user operating systems.

If you are running Fedora, Red Hat Enterprise Linux 7, CentOS 7, or any similar derivatives, you can install the fonts with the following:
```
sudo yum install redhat-display-fonts redhat-text-fonts
```
Note that Red Hat Enterprise Linux/CentOS users will need to [enable Fedora EPEL first](https://fedoraproject.org/wiki/EPEL).


If you are running Homebrew, you can install the fonts with the following:

```text
brew cask install homebrew/cask-fonts/font-redhat
```

## Bug reports and improvement requests

If you find a problem with a font file or have a request for future development of a font project, please [create a new issue in this project's issue tracker](https://github.com/RedHatOfficial/RedHatFont/issues).

## Self-Host Fonts Available From Red Hat (Recommended)

Self-hosting gives you full control over font delivery, better performance, and immunity from third-party service issues.

### Option 1: Direct Download from Repository

1. **Download fonts from this repository:**
   - OTF files: `fonts/Proportional/RedHatDisplay/otf/`
   - TTF files: `fonts/Proportional/RedHatDisplay/ttf/`
   - WOFF2 files: `fonts/Proportional/RedHatDisplay/webfonts/`
   - Variable fonts: `fonts/Proportional/RedHatDisplay/variable/`

2. **Add fonts to your project:**
   ```
   your-project/
   ├── fonts/
   │   ├── RedHatDisplay-Regular.woff2
   │   ├── RedHatDisplay-Bold.woff2
   │   └── ...
   └── css/
       └── fonts.css
   ```

3. **Create CSS @font-face declarations:**
   ```css
   @font-face {
     font-family: 'Red Hat Display';
     src: url('../fonts/RedHatDisplay-Regular.woff2') format('woff2');
     font-weight: 400;
     font-style: normal;
     font-display: swap;
   }

   @font-face {
     font-family: 'Red Hat Display';
     src: url('../fonts/RedHatDisplay-Bold.woff2') format('woff2');
     font-weight: 700;
     font-style: normal;
     font-display: swap;
   }
   ```

### Option 2: CDN via jsDelivr (No build required)

Use jsDelivr to serve fonts directly from GitHub releases:

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/RedHatOfficial/RedHatFont@latest/fonts/proportional/RedHatDisplay/RedHatDisplay.css">
```

Or for specific font files:
```css
@font-face {
  font-family: 'Red Hat Display';
  src: url('https://cdn.jsdelivr.net/gh/RedHatOfficial/RedHatFont@latest/fonts/Proportional/RedHatDisplay/webfonts/RedHatDisplay-Regular.woff2') format('woff2');
  font-weight: 400;
  font-style: normal;
  font-display: swap;
}
```

**jsDelivr Benefits:**
- ✅ Automatic CDN distribution
- ✅ Versioned releases (use `@4.0.2` for specific version)
- ✅ Free and reliable
- ✅ No third-party account needed

### Option 3: npm Package

Install via npm for build-tool integration:

```bash
npm install @fontsource/red-hat-display
```

Then import in your JavaScript/CSS:
```javascript
import '@fontsource/red-hat-display'; // Defaults to 400 weight
import '@fontsource/red-hat-display/700.css'; // Bold
```

### Performance Tips for Self-Hosting

1. **Use woff2 format** - Best compression, supported by all modern browsers
2. **Subset fonts** - Include only characters you need
3. **Use font-display: swap** - Prevents invisible text during load
4. **Preload critical fonts:**
   ```html
   <link rel="preload" href="/fonts/RedHatDisplay-Regular.woff2" as="font" type="font/woff2" crossorigin>
   ```
5. **Consider variable fonts** - One file for all weights (see `/variable` directory)

## Version Information

### Repository Versions
This repository uses semantic versioning:
- **Current Release:** 4.0.2 (2021-04-28)
- **Latest Updates:** Weight adjustments (2026-04-28)

See [CHANGELOG.md](CHANGELOG.md) for detailed history.

### Google Fonts Versions
Google Fonts uses incremental versioning:
- Red Hat Display: v21
- Red Hat Text: v19
- Red Hat Mono: v16

**Note:** These version numbers are not directly comparable. Google Fonts versions increment with each update to their infrastructure, while repository versions follow semantic versioning based on font changes.

## Licensing

Copyright 2026 Red Hat, Inc.

Licensed under the SIL Open Font License, Version 1.1, with Reserved Font Name Red Hat.

The SIL OFL does not grant any rights under trademark law and all such rights are reserved. Modified versions must be renamed to avoid use of any Red Hat trademarks, including but not limited to "Red Hat".
