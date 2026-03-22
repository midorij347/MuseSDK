# MuseSDK

Muse 2 / Muse S 系の脳波デバイスを Android アプリから扱うための実験用・学習用プロジェクトです。

現時点では、Android Studio / Kotlin プロジェクトとして土台を作り、`libmuse_android.jar` を組み込んだ状態から開発を進めるためのリポジトリです。将来的には、Muse デバイスとの接続、脳波ストリーム取得、可視化、保存、解析までを扱える SDK / サンプルアプリに発展させることを想定しています。

## このリポジトリの位置づけ

このプロジェクトは、完成済みの製品版 SDK ではなく、**Muse Android ライブラリを Android アプリに統合するための出発点**です。

公開状態から確認できる範囲では、以下の状態です。

- Android アプリの Gradle プロジェクトが作成済み
- `app/libs/libmuse_android.jar` を依存として追加済み
- `minSdk = 34`, `compileSdk = 35`, `targetSdk = 35`
- Kotlin ベースの Android アプリ構成
- 主要実装はこれから拡張していく段階

そのため、README も「現時点でできること」と「今後目指すこと」を分けて説明しています。

## 想定ユースケース

- Muse デバイスと Android を接続したい
- 生の EEG / 加速度 / ジャイロなどのデータ取得を試したい
- 集中度・リラックス度の可視化アプリを作りたい
- 脳波データを保存して後で解析したい
- 将来的に EEG × 学習ログ × UI 可視化のような研究・開発につなげたい

## 現在の構成

```text
MuseSDK/
├── app/
│   ├── libs/
│   │   └── libmuse_android.jar
│   ├── src/
│   └── build.gradle.kts
├── gradle/
├── build.gradle.kts
├── settings.gradle.kts
└── gradlew
```

## 使用技術

- Kotlin
- Android SDK
- Gradle (Kotlin DSL)
- Muse Android Library (`libmuse_android.jar`)

## セットアップ

### 1. クローン

```bash
git clone https://github.com/midorij347/MuseSDK.git
cd MuseSDK
```

### 2. Android Studio で開く

Android Studio でこのフォルダをそのまま開いてください。

### 3. 同期

Gradle Sync を実行してください。

### 4. 実機での確認

Muse 系デバイスを扱う場合、最終的には Bluetooth 周りの実機確認が必要になります。エミュレータだけでは十分な検証にならない可能性があります。

## 現時点で分かっていること

このリポジトリでは、`app/build.gradle.kts` に `libmuse_android.jar` の組み込み設定があり、`jniLibs` 用ディレクトリも参照する構成になっています。

```kotlin
dependencies {
    implementation(files("libs/libmuse_android.jar"))
}

sourceSets["main"].jniLibs.srcDirs("src/main/jniLibs")
```

これは、Muse の Android 向け配布物をローカルライブラリとして取り込む前提の構成です。

## これから実装したい内容

今後は、たとえば次のような機能を追加していくとプロジェクトの価値が大きくなります。

- Bluetooth 接続処理
- Muse デバイス検索
- 接続状態の表示
- EEG データ購読
- データのリアルタイム表示
- CSV / JSON 保存
- セッション記録
- 集中度推定や簡易可視化
- サンプル画面の整備
- README / API ドキュメントの充実

## このリポジトリが向いている人

- Muse SDK の Android 組み込みを試したい人
- EEG アプリ開発の最初の土台を探している人
- Kotlin で脳波デバイス連携を始めたい人
- 学習・研究目的で Muse を扱いたい人

## 注意

- 現時点では、すぐにそのまま完成アプリとして使える状態ではありません。
- 実際の脳波取得には、Muse デバイス本体と Android 実機での検証が必要です。
- SDK の利用条件や再配布条件は、Muse 側の公式ライセンスを別途確認してください。

## 今後の目標

このプロジェクトの短期目標は、**Muse デバイスと接続し、EEG を Android 上で取得して表示できる最小実装を完成させること**です。

その後、以下を目指します。

1. 接続の安定化
2. データ取得の実装
3. UI 可視化
4. ログ保存
5. 再利用しやすい SDK / モジュール化

## ライセンス

このリポジトリ自体のライセンスは、必要に応じて追記してください。

なお、同梱または依存する Muse 関連ライブラリについては、元の配布元の利用条件に従ってください。
