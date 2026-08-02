mkdir -p ~/.claude/skills && \
git clone https://github.com/tassiovale/claude-code-kit.git && \
cp -rv claude-code-kit/skills/* ~/.claude/skills/ && \
git clone https://github.com/secondsky/claude-skills.git && \
cp -rv claude-skills/security-skills/* ~/.claude/skills/ && \
git clone https://github.com/Kevinchamplin/claude-skills.git && \
cp -rv claude-skills/review ~/.claude/skills/ && \
rm -rf claude-code-kit claude-skills && \
echo "✅ Skills instaladas! Reinicie o Claude para carregar."
