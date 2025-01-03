# VS Code Settings Update

This commit updates the VS Code settings to improve the development experience.  The previous code was React component code for creating and joining chat rooms and is not directly related to this commit.

The following settings have been added or modified:


{
    "editor.mouseWheelZoom": true,
    "liveServer.settings.donotShowInfoMsg": true,
    "security.workspace.trust.untrustedFiles": "open",
    "liveServer.settings.donotVerifyTags": true,
    "code-runner.runInTerminal": true,
    "workbench.startupEditor": "none",
    "editor.accessibilitySupport": "off",
    "workbench.iconTheme": "material-icon-theme",
    "workbench.editorAssociations": {
        "*.db": "default",
        "{git,gitlens,git-graph}:/**/*.{md,csv,svg}": "default"
    },
    "[python]": {
        "editor.formatOnType": true
    },
    "git.autofetch": true,
    "git.enableSmartCommit": true,
    "git.confirmSync": false,
    "update.showReleaseNotes": false,
    "editor.wordWrap": "on",
    "redhat.telemetry.enabled": true,
    "extensions.ignoreRecommendations": true,
    "terminal.integrated.enableMultiLinePasteWarning": false,
    "git.openRepositoryInParentFolders": "never",
    "darkSynthwave84.brightness": 0.9,
    "workbench.colorTheme": "After Dark No Italics",
    "workbench.editor.enablePreview": false,
    "editor.fontSize": 15,
    "tabnine.experimentalAutoImports": true,
    "[javascriptreact]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[css]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[html]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "emojisense.languages": {
        "*": true,
        "markdown": true,
        "plaintext": {
            "markupCompletionsEnabled": false,
            "emojiDecoratorsEnabled": false
        },
        "scminput": true,
        "git-commit": true
    },
    "terminal.integrated.env.windows": {},
    "console-ninja.featureSet": "Community",
    "files.associations": {
        ".env*": "dotenv"
    },
    "editor.tokenColorCustomizations": {
        "textMateRules": [
            {
                "scope": "keyword.other.dotenv",
                "settings": {
                    "foreground": "#FF000000"
                }
            }
        ]
    },
    "[typescriptreact]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[typescript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "files.autoSave": "afterDelay"
}
```
These settings configure various aspects of the VS Code editor, including zoom, live server behavior, security, code runner settings, startup behavior, accessibility, icon theme, editor associations, Python formatting, Git settings, updates, word wrap, telemetry, extension recommendations, terminal behavior, Git repository handling, theme settings, editor preview, font size, TabNine auto imports, default formatters for various languages, emoji support, terminal environment variables, console enhancements, file associations, custom token colors, and auto-save behavior.