# terminal_styling_macos

Personal terminal styling for macOS.

### Setup Instructions
Run the following command to initialize your styling. This script is idempotent and will not corrupt your existing `~/.zshrc`.

```bash
bash -s << 'EOF'
# 1. Create the style file in /tmp
cat << 'STYLE_EOF' > /tmp/.terminal_style.zsh
# Custom Prompt
PROMPT=$'\n%F{198}%B%n %1~ >> %b%f '
STYLE_EOF

# 2. Ensure it is sourced in .zshrc exactly once (referencing the tmp path)
if ! grep -q "/tmp/.terminal_style.zsh" ~/.zshrc; then
    echo "source /tmp/.terminal_style.zsh" >> ~/.zshrc
fi

# 3. Apply macOS Terminal UI Settings
defaults write com.apple.Terminal "Window Settings" -dict-add "Clear Dark" '{ 
    "BackgroundColor" = <00000000 00000000 00000000 ffff0000>; 
    "Transparency" = 0.65; 
    "UseTransparency" = 1; 
    "TextSettings" = <ffffffff ffffffff ffffffff ffff0000>;
}'

echo ""
echo "Configuration applied. Please restart Terminal and ensure 'Clear Dark' is your Default profile."
EOF
```
