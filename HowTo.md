### How to

- Create a repository with the same name as your github username. E.g. my GitHub username is huabin, and the repository name must be huabin.

- Create a file in .github/workflows in repository and name it, E.g. snake.yml

- Put following code into the file

  
  # GitHub Action for generating a contribution graph with a snake eating your contributions.
  name: Generate Snake
  # Controls when the action will run. This action runs every 6 hours.
  on:
    schedule:
      # every 12 hours
      - cron: "0 */12 * * *"
  # This command allows us to run the Action automatically from the Actions tab.
    workflow_dispatch:
  # The sequence of runs in this workflow:
  jobs:
    # This workflow contains a single job called "build"
    build:
      # The type of runner that the job will run on
      runs-on: ubuntu-latest
      # Steps represent a sequence of tasks that will be executed as part of the job
      steps:
      # Checks repo under $GITHUB_WORKSHOP, so your job can access it
        - uses: actions/checkout@v2
      # Generates the snake  
        - uses: Platane/snk@master
          id: snake-gif
          with:
            # your GitHub username
            github_user_name: huabin
            # these next 2 lines generate the files on a branch called "output". This keeps the main branch from cluttering up.
            gif_out_path: dist/github-contribution-grid-snake.gif
            svg_out_path: dist/github-contribution-grid-snake.svg
       # show the status of the build. Makes it easier for debugging (if there's any issues).
        - run: git status
        # Push the changes
        - name: Push changes
          uses: ad-m/github-push-action@master
          with:
            github_token: ${{ secrets.GITHUB_TOKEN }}
            branch: master
            force: true
        - uses: crazy-max/ghaction-github-pages@v2.1.3
          with:
            # the output branch we mentioned above
            target_branch: output
            build_dir: dist
          env:
            GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
  
  
- Put following code into your README.md file. Only README.md can be displayed in your profile. E.g. I don't want it to show up in my profile, I renamed README.md to Example.md.

  
  ![snake gif](https://github.com/your_github_name/your_github_name/blob/output/github-contribution-grid-snake.svg)
  
