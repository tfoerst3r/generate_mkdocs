
<a name="readme-top"></a>

<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->

<!-- PROJECT Title -->
<h3 align="center">generate_mkdocs</h3>

<p align="center">
This project builds a `mkdocs` base project for your next workshop/lecture or general 
documentation of any kind.
</p>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#about-the-project">About The Project</a></li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
  </ol>
</details>


<!-- ABOUT THE PROJECT -->
## About the Project

This project is based on `mkdocs-material` template using:
    
With this template build you can start either building your project documentation or workshop.
Besides initializing the git repo it enables you to to generate locally or directly on gitlab 
or github your template.


<!-- GETTING STARTED -->
## Getting Started

This is an example of how you may give instructions on setting up your project locally.
To get a local copy up and running follow these simple example steps.

### Prerequisites

You need the following command line tools installed

- python 3.9
- [poetry 1.2](https://python-poetry.org/)
  
### Installation

1. Clone the repo
   
   ``` sh
   $ git clone git@github.com:tfoerst3r/generate_mkdocs.git
   ```

2. Copy this script in a directory which is part of your PATH variable, 
   ex. `$USER/bin/` or `$USER/.local/bin/`. You can check your path variable beforhand,
   via `echo $PATH`

3. Run the script in an **empty** directory where you want to start your new project
   
    ``` sh
    $ mkdir myproject
    $ cd myproject
    $ generate_mkdocs [OPTIONS]
    ```

4. Change add/change your remote git url depending what you use (ssh/https)
    
    ~~~ sh
    $ git remote set-url origin <your gitlab or github ssh/https url>
    ~~~

5. Now you are ready to get started on your mkdocs project.



<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Usage

If you want to quickly set up a web site for your project or workshop you can use this script for a quick setup:

~~~
$generate_mkdocs [OPTIONS]
~~~

For more informations you can use the `--help` option.

-----

This script generates a poetry environment in the folder you generated your project. 
It installs `mkdocs`, `mkdocs-material` and `reuse` and downloads and generates several files 
in order to start your project right away.

The folder structure is the following

~~~
.
├── custom_theme
│   └── partials
│       └── copyright.html
├── LICENSE.md
├── LICENSES
│   ├── CC-BY-4.0.txt (default)
│   └── MIT.txt (default)
├── materials (default)
│   ├── about.md
│   ├── css
│   │   └── extra.css
│   ├── episodes
│   ├── fonts
│   │   ├── Font_Mono.woff2 (Noto Sans Mono)
│   │   └── Font_Text.woff2 (Noto Sans)
│   ├── images
│   ├── index.md
│   ├── legal
│   └── tasks
├── .git/
├── .venv/
├── .gitignore
├── .gitlab-ci.yml
├── mkdocs.yml
├── poetry.lock
├── poetry.toml
├── pyproject.toml
└── README.md
~~~


### Generated Copyright, License, Imprint and Privacy Policy Informations

Information regarding the copyright, license, imprint and privacy policy is placed 
in the footer of each page and can be found in `custom_theme/partials/copyright.html`.

~~~
├── custom_theme
│   └── partials
│       └── copyright.html
~~~

You may change the desired informations in the file `copyright.html`.


### Generated Repo Licenses

The default licenses which will be generated are 

- CC-BY-4.0 for Text
- MIT for code

This can be changed by using the options:

- `--codelicense ARG` for the code license file
- `--textlicense ARG` for the text license file
 
### Project Fonts

To prevent legal issues with google fonts which are not hosted on the page repo itself, fonts are downloaded from google directly and place in the folder `materials/fonts/`.

~~~
├── materials (default)
│   ├── fonts
│   │   ├── Font_Mono.woff2 (Noto Sans Mono)
│   │   └── Font_Text.woff2 (Noto Sans)
~~~

Alternative fonts can be declared by providing the font links. Recommended are `*.woff2` or `*.ttf` formats.
Be aware that the font is open source or you have a license for public use.

Options for change the fonts:

- `--font_text LINK` text font
- `--font_mono LINK` mono font for code

### Configuration file `mkdocs.yml`

The default configuration file includes several recommendations which can be changed generation.

- Extra logo in the header `logo:` and a link to the main project `homepage:`.
- own style sheet `extra.css` for your own modifications, like font colors
- ability to use admonitions (boxes) and emojis

~~~
site_name: Documentation
docs_dir: materials

theme:
  font: false
  name: 'material'
  sticky-navigation: true
  custom_dir: custom_theme
  logo: "https://hifis.net/assets/img/HIFIS_Logo_Inverted_cropped.svg"

extra:
  homepage: https://hifis.net  # sets the link of the logo on top
  generator: false             # disable notics 'Made with Material for MkDocs

extra_css:
  - css/extra.css

markdown_extensions:
  - smarty
  - toc: 
      baselevel: 1
      permalink: true
  - admonition
  - pymdownx.details
  - attr_list
  - md_in_html
  - pymdownx.emoji:
      emoji_index: !!python/name:materialx.emoji.twemoji
      emoji_generator: !!python/name:materialx.emoji.to_svg

nav:
  - index.md
  - about.md
~~~

The `nav:` is the your playground. It is recommended to just define the files and the main levels of your documentations, but not the titles of each file. The titles should be defined in the files itself via the file header:

~~~
$ cat materials/index.md
---
title: Introduction
---
# Getting started
Hallo world!
~~~

Example of 

~~~
nav:
  - Documentation:
        - ch1.md
        - ...
  - Exercises:
        - ex1.md
        - ...
~~~

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Deployment

- Local: `$ poetry run mkdocs serve`
- GitLab: `$ git push` after adding your remote GitLab url
- Github: `$ poetry run mkdocs gh-deploy` after adding your remote Github url

<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- LICENSE -->
## License

Distributed under the MIT and CC-BY-4.0 Licenses. See `LICENSE.md` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

