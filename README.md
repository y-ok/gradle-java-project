# gradle-java-project

フォルダ構成

```bash
gradle-java-project
├── README.md
├── build.gradle
├── gradle
│   ├── environment
│   │   ├── development
│   │   │   └── env.gradle : 開発環境用のビルド設定
│   │   └── production
│   │       └── env.gradle : 本番環境用のビルド設定
│   ├── install-git-hooks.gradle : Git hook設定用gradleファイル
│   ├── settings
│   │   └── pre-commit : フォーマッター適用Git hook
│   └── wrapper
│       ├── gradle-5.6.3-bin.zip
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradle-java-project.code-workspace : VSCode用ワークスペース定義ファイル
├── gradle.properties
├── gradlew
├── gradlew.bat
├── settings.gradle
├── src
│   ├── main
│   │   ├── java
│   │   │   └── gradle
│   │   │       └── java
│   │   │           └── project
│   │   └── resources
│   │       ├── application.properties : 外部定義ファイル
│   │       ├── common.properties : 外部定義ファイル用パス定義ファイル
│   │       └── settings
│   │           ├── files
│   │           └── sql
│   └── test
│       ├── java
│       │   └── gradle
│       │       └── java
│       │           └── project
│       └── resources
└── styleguide
    └── eclipse-java-google-style.xml
```

## 開発環境

### Javaバージョン

- `1.8.0_101`

### IDE

- [VSCode](https://code.visualstudio.com/)

### ビルドツール

- [gradle](https://gradle.org/)

### フォーマッター

- [diffplug/spotless](https://github.com/diffplug/spotless)
- [google/styleguide](https://github.com/google/styleguide)

### 静的解析

- [SpotBugs](https://spotbugs.readthedocs.io/en/stable/index.html)

### ライブラリ

- [Lombok](https://projectlombok.org/)
- [Guava](https://github.com/google/guava)
- [JUnit5](https://oohira.github.io/junit5-doc-jp/user-guide/)
- [Shadow](https://imperceptiblethoughts.com/shadow/)

### TIPS

- [Gradleでpropertiesファイルの文字列を置換](https://blog.scheakur.com/post/41283944018/gradle-%E3%81%A7-ant-%E3%81%AE-replacetokens-%E3%82%92%E4%BD%BF%E3%81%A3%E3%81%A6-properties)
- [【Java】Lombokで冗長コードを削減しよう](https://www.casleyconsulting.co.jp/blog/engineer/107/)
- [VS Codeを持ち運ぶには（ポータブルモード）](https://www.atmarkit.co.jp/ait/articles/1807/20/news023.html)
- [Visual Studio CodeをオフラインPCで使用する](https://qiita.com/mekemeke421/items/98d5a3e2f2cc7517a6ab)

### VSCodeで利用しているプラグイン一覧

```bash
$code --list-extensions | xargs -L 1 echo code --install-extension
code --install-extension codezombiech.gitignore
code --install-extension DavidAnson.vscode-markdownlint
code --install-extension donjayamanne.githistory
code --install-extension DotJoshJohnson.xml
code --install-extension eamodio.gitlens
code --install-extension formulahendry.auto-close-tag
code --install-extension GabrielBB.vscode-lombok
code --install-extension GrapeCity.gc-excelviewer
code --install-extension jebbs.plantuml
code --install-extension joelday.docthis
code --install-extension mhutchie.git-graph
code --install-extension mkxml.vscode-filesize
code --install-extension ms-azuretools.vscode-docker
code --install-extension MS-CEINTL.vscode-language-pack-ja
code --install-extension ms-python.python
code --install-extension ms-vscode-remote.remote-containers
code --install-extension ms-vscode-remote.remote-ssh
code --install-extension ms-vscode-remote.remote-ssh-edit
code --install-extension ms-vscode-remote.remote-ssh-explorer
code --install-extension ms-vscode-remote.remote-wsl
code --install-extension ms-vscode-remote.vscode-remote-extensionpack
code --install-extension mtxr.sqltools
code --install-extension naco-siren.gradle-language
code --install-extension oleg-shilo.codemap
code --install-extension Pivotal.vscode-boot-dev-pack
code --install-extension Pivotal.vscode-concourse
code --install-extension Pivotal.vscode-manifest-yaml
code --install-extension PKief.material-icon-theme
code --install-extension redhat.java
code --install-extension redhat.vscode-xml
code --install-extension redhat.vscode-yaml
code --install-extension spmeesseman.vscode-taskexplorer
code --install-extension sysoev.language-stylus
code --install-extension uctakeoff.vscode-counter
code --install-extension VisualStudioExptTeam.vscodeintellicode
code --install-extension vscjava.vscode-java-debug
code --install-extension vscjava.vscode-java-dependency
code --install-extension vscjava.vscode-java-pack
code --install-extension vscjava.vscode-java-test
code --install-extension vscjava.vscode-maven
code --install-extension vscode-icons-team.vscode-icons
code --install-extension yzane.markdown-pdf
code --install-extension yzhang.markdown-all-in-one
```

### Gradleコマンド一覧

1. ソースコード、テストコードビルド

   ```bash
   gradle build
   ```

   `build`タスクの依存関係は以下の通り。

   ```bash
   $gradle build taskTree

   > Task :taskTree

    ------------------------------------------------------------
    Root project
    ------------------------------------------------------------

    :build
    +--- :assemble
    |    +--- :distTar
    |    |    +--- :jar
    |    |    |    \--- :classes
    |    |    |         +--- :compileJava
    |    |    |         \--- :processResources
    |    |    \--- :startScripts
    |    +--- :distZip
    |    |    +--- :jar
    |    |    |    \--- :classes
    |    |    |         +--- :compileJava
    |    |    |         \--- :processResources
    |    |    \--- :startScripts
    |    +--- :jar
    |    |    \--- :classes
    |    |         +--- :compileJava
    |    |         \--- :processResources
    |    +--- :shadowDistTar
    |    |    +--- :shadowJar
    |    |    |    \--- :classes
    |    |    |         +--- :compileJava
    |    |    |         \--- :processResources
    |    |    \--- :startShadowScripts
    |    |         \--- :shadowJar
    |    |              \--- :classes
    |    |                   +--- :compileJava
    |    |                   \--- :processResources
    |    \--- :shadowDistZip
    |         +--- :shadowJar
    |         |    \--- :classes
    |         |         +--- :compileJava
    |         |         \--- :processResources
    |         \--- :startShadowScripts
    |              \--- :shadowJar
    |                   \--- :classes
    |                        +--- :compileJava
    |                        \--- :processResources
    +--- :check
    |    +--- :spotbugsMain
    |    |    \--- :classes
    |    |         +--- :compileJava
    |    |         \--- :processResources
    |    +--- :spotbugsTest
    |    |    +--- :classes
    |    |    |    +--- :compileJava
    |    |    |    \--- :processResources
    |    |    \--- :testClasses
    |    |         +--- :compileTestJava
    |    |         |    \--- :classes
    |    |         |         +--- :compileJava
    |    |         |         \--- :processResources
    |    |         \--- :processTestResources
    |    +--- :spotlessCheck
    |    |    \--- :spotlessJavaCheck
    |    |         \--- :spotlessJava
    |    \--- :test
    |         +--- :classes
    |         |    +--- :compileJava
    |         |    \--- :processResources
    |         \--- :testClasses
    |              +--- :compileTestJava
    |              |    \--- :classes
    |              |         +--- :compileJava
    |              |         \--- :processResources
    |              \--- :processTestResources
    +--- :installGitHooks
    \--- :processResources
    ```

2. テスト実行

   ```bash
   gradle test
   ```

   テストレポートは、以下に出力される。

   ```bash
   build/reports/tests
   ```

3. カバレッジレポート生成

   ```bash
   gradle jacocoTestReport
   ```

4. フォーマッター適用

   フォーマッターは`styleguide/eclipse-java-google-style.xml`を適用する。

   ```bash
   gradle spotlessApply
   ```

5. 成果物削除

   ```bash
   gradle clean
   ```

   `build`フォルダが削除される。

6. 静的解析

   ソースコードのチェックは以下のコマンドを実行する。

   ```bash
   gradle spotbugsMain
   ```

   レポートは、`build/reports/spotbugs/main.html`に出力される。

   一方、テストコードのチェックは以下のコマンドを実行する。

   ```bash
   gradle spotbugsTest
   ```

   レポートは、`build/reports/spotbugs/test.html`に出力される。

7. Git hookの設定

   `git commit`時に自動でフォーマッターを適用するhookを設定する。

   ```bash
   gradle installGitHooks
   ```
