# Local Setup

This documentation will help you setup tools and software needed to run Salesforce DX locally and to create Scratch Orgs.

## Windows

Open PowerShell and run:

```powershell
winget install -e --id OpenJS.NodeJS -v 18.11.0
winget install -e --id GitHub.GitHubDesktop
winget install -e --id Microsoft.VisualStudioCode
winget install -e --id EclipseAdoptium.Temurin.17.JDK
```

## macOS

1. Open terminal and run `xcode-select --install` first (Xcode install will open, install this before continuing):
1. Run the code below:

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
echo "export PATH=/opt/homebrew/bin:$PATH" >> ~/.bash_profile && source ~/.bash_profile

brew install node@18
brew install --cask github
brew install --cask visual-studio-code
brew tap homebrew/cask-versions
brew install --cask temurin17
```
