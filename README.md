<div align="center">
  <img src="https://github-readme-stats.vercel.app/api?hide_title=false&hide_rank=true&show_icons=true&include_all_commits=true&count_private=true&disable_animations=true&theme=dracula&locale=en&hide_border=false&username=ali" height="150" alt="stats graph"  />
  <img src="https://github-readme-stats.vercel.app/api/top-langs?locale=en&hide_title=false&layout=compact&card_width=320&langs_count=6&theme=dracula&hide_border=false&username=ali" height="150" alt="languages graph"  />
</div>

###

<div align="left">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg" height="30" width="42" alt="python logo"  />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg" height="30" width="42" alt="javascript logo"  />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/typescript/typescript-plain.svg" height="30" width="42" alt="typescript logo"  />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg" height="30" width="42" alt="html5 logo"  />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/css3/css3-original.svg" height="30" width="42" alt="css3 logo"  />
</div>

###

<div align="left">
  <a href="a.mzaffari2000@gmail.com" target="_blank">
    <img src="https://img.shields.io/static/v1?message=Gmail&logo=gmail&label=&color=D14836&logoColor=white&labelColor=&style=for-the-badge" height="35" alt="gmail logo"  />
  </a>
  <a href="www.linkedin.com/in/ali-mozaffari22" target="_blank">
    <img src="https://img.shields.io/static/v1?message=LinkedIn&logo=linkedin&label=&color=0077B5&logoColor=white&labelColor=&style=for-the-badge" height="35" alt="linkedin logo"  />
  </a>
  <a href="https://t.me/parllax" target="_blank">
    <img src="https://img.shields.io/static/v1?message=Telegram&logo=telegram&label=&color=2CA5E0&logoColor=white&labelColor=&style=for-the-badge" height="35" alt="telegram logo"  />
  </a>
</div>

###

<br clear="both">

<img src="https://raw.githubusercontent.com/ali/ali/blob/output/snake.svg" alt="Snake animation" />
![GitHub Snake Light](github-snake.svg#gh-light-mode-only)
![GitHub Snake dark](github-snake-dark.svg#gh-dark-mode-only)
- uses: Platane/snk@v2
  with:
    # github user name to read the contribution graph from (**required**)
    # using action context var `github.repository_owner` or specified user
    github_user_name: ${{ AliMozaffri }}

    # list of files to generate.
    # one file per line. Each output can be customized with options as query string.
    #
    #  supported options:
    #  - palette:     A preset of color, one of [github, github-dark, github-light]
    #  - color_snake: Color of the snake
    #  - color_dots:  Coma separated list of dots color.
    #                 The first one is 0 contribution, then it goes from the low contribution to the highest.
    #                 Exactly 5 colors are expected.
    outputs: |
      dist/github-snake.svg
      dist/github-snake-dark.svg?palette=github-dark
      dist/ocean.gif?color_snake=orange&color_dots=#bfd6f6,#8dbdff,#64a1f4,#4b91f1,#3c7dd9
      #
      
      name: generate animation

on:
  # run automatically every 12 hours
  schedule:
    - cron: "0 */12 * * *" 
  
  # allows to manually run the job at any time
  workflow_dispatch:
  
  # run on every push on the master branch
  push:
    branches:
    - master
    
  

jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10
    
    steps:
      # generates a snake game from a github user (<github_user_name>) contributions graph, output a svg animation at <svg_out_path>
      - name: generate github-contribution-grid-snake.svg
        uses: Platane/snk/svg-only@v2
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark

      # push the content of <build_dir> to a branch
      # the content will be available at https://raw.githubusercontent.com/<github_user>/<repository>/<target_branch>/<file> , or as github page
      - name: push github-contribution-grid-snake.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v2.6.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
