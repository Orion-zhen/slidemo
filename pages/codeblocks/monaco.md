# Monaco 编辑器

如果想在演示时实时对演示代码进行修改, 只需要在代码块的代码语言标识后面加上 `{monaco}` 即可. 注意, 这个功能与代码高亮**冲突**.

```ts {monaco}
console.log('HelloWorld')
```

Monaco 还可以生成两个代码块之间的差异. 使用 `{monaco-diff}` 来启用这个功能, 并使用 `~~~` 来分隔需要对比的两个代码块:

```json {monaco-diff}
{
    "dependencies": {
        "@slidev/cli": "^52.1.0",
        "@slidev/theme-apple-basic": "^0.25.1",
        "@slidev/theme-default": "latest",
        "@slidev/theme-seriph": "latest",
        "vue": "^3.5.18"
    }
}
~~~
{
    "dependencies": {
        "@slidev/cli": "^52.1.0",
        "@slidev/theme-default": "latest",
        "@slidev/theme-seriph": "latest",
        "vue": "^3.5.18"
    }
}
```

---

# Monaco 代码运行器

Monaco 还可以扩展编辑器的功能, 直接运行 JavaScript 或 TypeScript 代码. 使用 `{monaco-run}` 来启用这个功能. 注意, 这个功能与代码高亮**冲突**.

```ts {monaco-run}
function distance(x: number, y: number) {
  return Math.sqrt(x ** 2 + y ** 2)
}
console.log(distance(3, 4))
```

默认情况下, 代码将自动运行. 可以在后面加上 `{autorun: false}` 来禁用自动运行.

```ts {monaco-run} {autorun: false}
console.log('请点击右上角的运行按钮')
```

或者通过设置 `{showOutputAt: '+x'}` 来在 x 步动画后展示输出. 语法通 `v-click`:

```ts {monaco-run} {showOutputAt:'+1'}
console.log('一步动画后后显示该结果')
```

---

# 滚动代码块

如果代码确实很长, 但确实想要使用 Monaco, 就可以使用 HTML 标签中的 `overflow` 属性来滚动代码块:

<div class="overflow-auto mx-auto h-100">
```yaml {monaco}
name: OUR Publish

on:
  schedule:
    - cron: "0 0 * * 1"
  workflow_dispatch:
  push:
    branches:
      - main
    paths:
      - ".github/workflows/our.yml"
      - ".github/workflows/reusable-build.yml"
      - "scripts/**"
      - "configs/**"

jobs:
  standalone:
    strategy:
      fail-fast: false
      matrix:
        # LTO-enabled packages
        package:
          - nodejs-gitmoji-cli
          - pmount
          # - mihomo-party
          - fcitx5-skin-fluentdark-git
          - fcitx5-skin-fluentlight-git
          - hfd-git
          - wsl-open
          - wsl2-ssh-agent
          - ascii-image-converter
          - toolong
          - nali-nt-git
          - envfetch
          - hyprls-git
          - hyprshot-gui
          - matugen-git
          - clipse-git
          - linux-wallpaperengine-git
          - llama-swap
          - slidev-cli
    uses: ./.github/workflows/reusable-build.yml
    permissions:
      contents: write
    with:
      package: ${{ matrix.package }}
      lto: true
      download-artifacts: false
    secrets: inherit

  standalone-no-lto:
    strategy:
      fail-fast: false
      matrix:
        package:
          - wezterm-git
    uses: ./.github/workflows/reusable-build.yml
    permissions:
      contents: write
    with:
      package: ${{ matrix.package }}
      lto: false
      download-artifacts: false
    secrets: inherit

  stage-1:
    strategy:
      fail-fast: false
      matrix:
        # LTO-enabled packages
        package:
          - ckbcomp # depby: calamares-git
          - google-breakpad # depby: quickshell-git
          - python-safetensors # depby: python-transformers
          - python-msgspec # depby: python-vllm-bin
          - python-blake3 # depby: python-vllm-bin
          ### libastal series for hyprpanel ###
          - libastal-io-git
          - libastal-apps-git
          - libastal-auth-git
          - libastal-battery-git
          - libastal-bluetooth-git
          - libastal-greetd-git
          - libastal-hyprland-git
          - libastal-mpris-git
          - libastal-network-git
          - libastal-notifd-git
          - appmenu-glib-translator-git
          - libastal-powerprofiles-git
          - libastal-river-git
          - libastal-wireplumber-git
          ### End libastal ###
    uses: ./.github/workflows/reusable-build.yml
    permissions:
      contents: write
    with:
      package: ${{ matrix.package }}
      lto: true
      download-artifacts: false
    secrets: inherit

  stage-1-no-lto:
    strategy:
      fail-fast: false
      matrix:
        package:
          - libcava # depby: libastal-cava-git
    uses: ./.github/workflows/reusable-build.yml
    permissions:
      contents: write
    with:
      package: ${{ matrix.package }}
      lto: false
      download-artifacts: false
    secrets: inherit

  stage-2:
    needs: 
      - stage-1
      - stage-1-no-lto # Depend on both LTO and no-LTO groups
    strategy:
      fail-fast: false
      matrix:
        package:
          - calamares-git # depon: ckbcomp
          - quickshell-git # depon: google-breakpad
          ### libastal series for hyprpanel ###
          - libastal-git
          - libastal-4-git
          - libastal-cava-git
          - libastal-tray-git
          ### End libastal ###
    uses: ./.github/workflows/reusable-build.yml
    permissions:
      contents: write
    with:
      package: ${{ matrix.package }}
      lto: true
      download-artifacts: true
    secrets: inherit

  stage-3:
    needs: stage-2
    strategy:
      fail-fast: false
      matrix:
        package:
          ### libastal series for hyprpanel ###
          - libastal-meta # depby: aylurs-gtk-shell-git
          - libastal-gjs-git # depon: libastal-git | depby: aylurs-gtk-shell-git
          ### End libastal ###
    uses: ./.github/workflows/reusable-build.yml
    permissions: { contents: write }
    with:
      package: ${{ matrix.package }}
      lto: true
      download-artifacts: true
    secrets: inherit

  stage-4:
    needs: stage-3
    strategy:
      fail-fast: false
      matrix:
        package:
          - aylurs-gtk-shell-git # depon: libastal-gjs-git, libastal-meta | depby: ags-hyprpanel-git
    uses: ./.github/workflows/reusable-build.yml
    permissions: { contents: write }
    with:
      package: ${{ matrix.package }}
      lto: true
      download-artifacts: true
    secrets: inherit

  stage-5:
    needs: stage-4
    strategy:
      fail-fast: false
      matrix:
        package:
          - ags-hyprpanel-git # depon: aylurs-gtk-shell-git
    uses: ./.github/workflows/reusable-build.yml
    permissions: { contents: write }
    with:
      package: ${{ matrix.package }}
      lto: true
      download-artifacts: true
    secrets: inherit

  #####################################################################
  # FINAL STAGE: Aggregate all packages, build repo, and publish.
  #####################################################################
  publish:
    name: Publish to Pages
    needs: # This transitively depends on all previous stages
      - standalone
      - standalone-no-lto
      - stage-5
    runs-on: ubuntu-latest
    container: "archlinux:latest"
    permissions:
      contents: write
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Import GPG key
        uses: crazy-max/ghaction-import-gpg@v6
        with:
          gpg_private_key: ${{ secrets.GPG_SEC_KEY }}
          passphrase: ${{ secrets.GPG_PASSPHRASE }}
      
      - name: Download all built packages
        uses: actions/download-artifact@v4
        with:
          path: x86_64
          merge-multiple: true

      - name: Display downloaded files
        run: |
          echo "--- All built packages ---"
          ls -R x86_64

      - name: Generate repository database
        env:
          GPG_SIG_KEY: ${{ secrets.GPG_SIG_KEY }}
        run: bash scripts/repo-add.sh our

      - name: Generate package index page
        run: |
          pacman -Syu python python-pip --noconfirm --overwrite '*'
          pip install zstandard --break-system-packages
          python scripts/packages.py

      - name: Setup GitHub Pages
        uses: actions/configure-pages@v5

      - name: Upload pages artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: "."

      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```
</div>
