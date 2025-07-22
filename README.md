# Fixes & Hacks

A categorized collection of developer fixes, configurations, and tips across Drupal, Angular, Git, Node, Linux, and more.

> 🛠️ Collected from real-world debugging and experience.

## Local Setup Instructions

1. **Clone the repository:**
   ```sh
   git clone <REPO_URL>
   cd fixes-n-hacks
   ```

2. **Install Python 3 (if not already installed):**
   - On Ubuntu/Debian:
     ```sh
     sudo apt update && sudo apt install python3 python3-pip
     ```
   - On Mac (with Homebrew):
     ```sh
     brew install python3
     ```

3. **Install MkDocs and Material theme:**
   ```sh
   pip3 install mkdocs mkdocs-material
   ```

4. **(Optional) Add Python and MkDocs to your PATH in `.zshrc`:**
    - Add the path to rc file `export PATH="$HOME/Library/Python/3.x/bin:$PATH"`
  e.g
   ```sh
   echo 'export PATH="$HOME/Library/Python/3.9/bin:$PATH"' >> ~/.zshrc
   source ~/.zshrc
   ```

## Useful MkDocs Commands

- Start local server:
  ```sh
  mkdocs serve
  ```
- Build static site:
  ```sh
  mkdocs build
  ```
- Deploy to GitHub Pages:
  ```sh
  mkdocs gh-deploy --force
  ```

> For more, see [MkDocs documentation](https://www.mkdocs.org/).
