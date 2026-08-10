# pachman
pachman
name: Generate Pacman Graph

on:
  schedule:
    # Berjalan otomatis setiap 12 jam
    - cron: "0 */12 * * *" 
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v4

      # Menggunakan Action dari DuyetBKU untuk membuat grafis Pac-Man
      - name: Generate pacman graph (light & dark)
        uses: DuyetBKU/viz-pacman-github-profile@main
        with:
          github_user_name: ${{ github.repository_owner }}
          # Anda bisa mengganti tema ke: github-light, gitlab-dark, dracula, dll.
          theme: react-dark 

      - name: Push SVG to output branch
        uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
